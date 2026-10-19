# Security review checklist for an open-source AI agent platform

A security review of an open-source AI agent platform starts with one question: which credentials can an agent reach? The model vendor is the visible part of the stack, and the retention policy is usually well documented. The review is decided one layer down, at the credential boundary. A product that injects live API keys into the machine an agent runs in cannot give a reviewer a short list of what that agent can reach. It can only list everything the key opens.

Kortix, the open-source AI Operating System, documents its credential model closely enough to review, including the parts that are still experimental. That makes it a useful worked example for any product under review, whether the product is Kortix or something else.

## Start with a credential inventory

Ask for every credential the agent can cause to be spent, and where each one lives. The answer should fall into three stores, and each store gets its own question.

Model provider keys are the first store. Ask whether the platform spends them server-side through a gateway or hands them to the agent's machine. In Kortix, provider keys belong on the Models page or in `kortix providers set`, where the LLM gateway can spend them server-side when it is on. A key that is only ever used by the gateway has a much smaller blast radius than one exported into a shell.

Connector credentials are the second store, and they are where most platforms get vague. A connector needs a real OAuth token or API key to act in a third-party system. If that token is placed in the agent's environment, every command the agent runs can read it. Kortix answers this one narrowly. Connector credentials are brokered server-side and never enter the machine ([Kortix security page](https://kortix.com/security)). The connector gateway makes the upstream call with the credential.

Project secrets are the third store. These are the API keys, tokens, and connection strings a session needs for its own work. They are the hardest to govern because some of them genuinely have to be readable by agent code. The [secrets documentation](https://kortix.com/docs/project/secrets) treats that as a choice per secret rather than a platform-wide property. That is the shape a review can test, one secret at a time.

For each of the three stores, ask four things: where the value is stored, how it reaches the work, who can spend it, and what record exists when it is used.

## What runs in the sandbox, and what stays outside it

A session boots a sandbox, loads the project configuration into a live runtime, and gets a working checkout when its agent is granted repository access. The agent gets a prompt, a terminal, file access, and the connectors its grant admits. Code the agent writes can do anything the session can do, so every value inside that sandbox is within reach of the agent.

Ask the vendor to draw the boundary and mark each value that crosses it. On the Kortix side of that drawing, the control plane, the secret store, the connector gateway, the LLM gateway, the audit log, and the identity provider all sit outside the sandbox. The sandbox holds the files the session was given, the granted secrets, and outbound network access.

The drawing matters because it shows which questions have short answers. A credential that never enters the sandbox cannot be exfiltrated by a prompt injection, a malicious dependency, or a command the agent improvises. A credential that does enter the sandbox can be exfiltrated, and the review should say so plainly instead of treating it as a policy problem.

## Two secret exposures, and the one a computed credential must use

Kortix gives every project secret an exposure, and the exposure answers one question: can agent code read the real value? A new secret is shared with everyone in the project and uses the environment exposure. The sandbox receives the real value as an environment variable, and agent code, plus every process it starts, can read it, print it, and send it anywhere. Kortix cannot redact or audit that use. A reviewer should treat an environment secret as a value the agent owns.

The second exposure is egress-enforced, and it is experimental. The sandbox receives a handle that is worth nothing on its own. Kortix replaces the handle with the real value outside the sandbox, only on requests to the hosts you list. The host list is exact HTTPS hostnames, one per entry; a wildcard is rejected, and `api.example.com` does not cover `uploads.api.example.com`. An echo of the real value in a response comes back as `[REDACTED]`. Kortix writes an audit record for every relayed request.

Set it from the CLI:

```bash
kortix secrets delivery STRIPE_API_KEY enforced --allow-host api.stripe.com
```

The mechanism has limits a reviewer should hear before trusting it. Only clients that honor `https_proxy` are intercepted. Kortix sets the proxy and the CA trust in the agent's environment, and a process started with a cleared environment sends the handle directly, which fails at the upstream. This is a credential control. It does not filter traffic; a request to a host off the list leaves the sandbox carrying the handle, and the upstream rejects it.

Some credentials must stay on environment, and this is the exception that decides the review. A computed credential is an input to a calculation and never travels: AWS SigV4 signing keys, HMAC webhook-signing secrets, JWT client assertions, SSH and PEM private keys. Protocols that are not HTTPS belong there too, such as a Postgres connection string or SMTP credentials. The code has to hold the value to compute with it, and no broker helps.

For each secret, the reviewer needs three facts: its exposure, its audience, and the agent grant that admits it. The audience is who can use it: everyone in the project, only the person who created it, or specific people, groups, and agents. Delivery is the intersection of that audience and the agent's `secrets` grant in `kortix.yaml`. Shared sessions, triggers, schedules, and webhooks act for nobody, so they receive only values shared with everyone. An agent session cannot change an exposure, a host list, or an audience; the API returns 403 if it tries.

## Isolation per session, and the branch

Kortix states the isolation claim in one line. One isolated sandbox per session. Each session has its own isolated machine and branch. The session branch is named after the session ID, so two sessions working on the same repository do not share a working tree.

The reviewer's question is what two sessions actually share. The repository and the control plane are shared by design. The machine and its filesystem are not. Ask whether one session can read another session's uncommitted files, and ask for the provider name when the boundary matters. The security page describes managed, self-hosted, and isolated deployments separately, and the [self-hosting guide](https://opensourceaiagentplatform.com/self-hosting) covers the deployment you run yourself.

Work leaves the session through git. The agent commits on its branch, pushes, and opens a change request against the default branch. Landing that change is a separate permission, `project.gitops.merge`, which an agent does not hold unless an admin grants it. The project manifest is validated in `kortix ship` and again in the change request merge check, and a change request whose manifest does not validate cannot merge. That last detail is worth testing: break a manifest key on purpose in a test project and confirm the merge stops.

## Approval gates and the line that turns them on

Permissions and policy are two different controls. Permissions decide who, and which agent, may call a tool at all. Policy decides what happens when the call is made. Kortix applies the first to both kinds of principal. Per-resource permissions for people and agents. Roles, groups, and an audit trail. The [permissions and policy guide](https://opensourceaiagentplatform.com/ai-agent-permissions-and-policy) covers how a role, a group, and an agent grant compose.

Kortix describes the second control precisely. Approval gates you set. Off until you set them.

The default is in the manifest. `policy.default_mode` is `allow_all` unless the project sets it, and a project with no `policy` block keeps the permissive legacy default, as the [manifest reference](https://kortix.com/docs/project/manifest) records. A reviewer who reads only the marketing page could assume gates are on. Read the file instead.

```yaml
policy:
  default_mode: risk
  policies:
    - match: gmail.send_email
      action: require_approval
      conditions:
        - arg: to
          match: "*@example.com"
    - match: stripe.*
      action: require_approval
```

`risk` lets a read run and sends a write or destructive call to a person. A rule matches a glob over the fully qualified tool path, and conditions can narrow it to the arguments, so the rule can mean only to these addresses. Every condition on a rule must hold. An argument that cannot be evaluated fails closed. Project rules are checked before the connector's own rules, and the first match wins.

Two operational details belong in the review. `kortix validate` checks the manifest schema, the files around it, and the Dockerfiles, but it does not check `policy` or `policies`. When Kortix syncs connectors, it skips a malformed rule and reports a connector sync error, so the rule needs a second look in the connector settings after the merge. Ask for the diff that introduced the policy block, because the block is versioned with everything else and the diff is the change record.

## The audit trail, and who can read it

Ask what the log records before asking how long it is kept. The useful split is account actions, agent actions, connector calls, and relayed requests. A log that records sign-ins but not tool calls will not answer the question a reviewer asks after an incident.

Kortix records every account action and every agent action on every plan. The plan decides who may read, export, or stream that record, not whether it exists. The per-session audit view is an Enterprise entitlement, and recording is never gated. Ask for a sample export from a project that has run real sessions, and check that a connector call and an egress-enforced request both appear in it.

Ask whether the agent can delete or edit its own entries, and ask who holds the export. If the reviewed party can rewrite its own entries, the record cannot serve as evidence.

## SSO and SCIM

Identity questions are short, and the answers are easy to test. Ask for SAML 2.0 single sign-on with the identity provider you actually run, and for SCIM 2.0 provisioning that can create, update, and deactivate an account. Deactivation is the one to watch: a SCIM integration that creates accounts but does not revoke sessions leaves access behind.

Then ask how groups map to roles, whether a local administrator can sign in when the identity provider is down, and how long a revoked session stays alive. Ask for the identity provider compatibility list and the provisioning runbook before the meeting, not during it.

## Questions to send before the review

Send these with the meeting invite, so the vendor brings artifacts rather than slides.

- Which model provider keys exist, and does the agent's machine ever hold one?
- Which credentials are brokered server-side, and can you show a call trace where the credential stays outside the sandbox?
- For each project secret, what is the exposure, the audience, and the agent grant?
- Which secrets are computed credentials or non-HTTPS protocols, and are they on environment?
- What do two sessions share, and can one read another's working tree?
- Which permission is required to merge a change request, and which agents hold it?
- What is `policy.default_mode`, and can you show the diff that set it?
- What does the audit log record, who can export it, and on which plan?
- Which SSO protocol and provisioning standard are supported, and how is a session revoked?

For an enterprise procurement, the same list belongs in the vendor packet alongside the [enterprise deployment questions](https://opensourceaiagentplatform.com/open-source-ai-agent-platform-for-enterprises). The point of sending it early is to make the review about evidence. A vendor that can produce the manifest, the export, and the call trace in one meeting has already answered most of the review.

## Checklist

| Area | What to verify | Evidence to request | Why it matters |
| --- | --- | --- | --- |
| Connector credentials | Broker sits outside the sandbox | Architecture diagram and a call trace | The agent never holds the upstream token |
| Secret exposure | Environment or egress-enforced, per secret | `kortix secrets ls` and host lists | The wrong exposure hands over the value |
| Computed credentials | Signing keys and non-HTTPS values on environment | The list of secrets by exposure | A broker cannot help a value used locally |
| Session isolation | Machine, filesystem, and branch per session | Two session IDs and their branches | A cross-session read ends the review |
| Merge path | Change request plus `project.gitops.merge` | The grant in `kortix.yaml` | An agent that merges alone has shipped |
| Approval default | `policy.default_mode` and every rule | The policy block and its last diff | The default is permissive until set |
| Audit access | Recording, retention, and who can export | A redacted export and the plan entitlement | An unreadable log is not evidence |
