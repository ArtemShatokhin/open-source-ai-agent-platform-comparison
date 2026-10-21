# Before the second person: open source agents for a five-person team

A five-person company gets useful work out of open source agents long before it needs a platform: a laptop, a model key and one good prompt file will carry it, and the bill stays near zero. The decision arrives the day a second person needs the first person's agent, when the question stops being whether the agent works and becomes who can read, change and keep it after the builder is gone.

## When does a five-person team actually need a platform?

Count the people who touch the agent, not the work it produces. One person writing prompts on a laptop, running them when they remember to, has a script with a personality. That is the right tool at that size, and buying software for it is premature.

The second user changes the shape of the problem. They want the same agent, at the same time, with the same context, and they want to adjust it without asking the first person to sit beside them. Two people editing one prompt in a notes app is where the laptop stops working. The moment is smaller than most teams expect: one colleague asking for the pipeline thing this week, and the honest answer being "not from your account".

It depends, though, and the exception is large. If the output is chat-shaped, belongs to one person, and nobody on the team will ever read a diff, Claude Cowork or ChatGPT Work is the better pick. You get a working assistant in an afternoon, no repository to learn, and support that answers. Pay for it happily while that description holds. It stops holding at the second user. Kortix is the open-source AI Operating System, and its assumption is that the second person eventually arrives.

## What the laptop gets you, and where it stops

Before the threshold, the honest setup is a folder, a key and a markdown file. The prompt sits in a draft, the key sits in a shell profile, and whatever the agent learned about the business sits in a chat history nobody else opens.

The cracks are all in the same place: state that lives with a person rather than with the company. A second person cannot see what the agent was told. They cannot tell whether its output changed because the data changed or because someone edited the prompt, and they cannot schedule it without borrowing an account. Each gap is survivable once. Together they keep the work at the first person's desk.

## The Tuesday the analyst leaves: what changes hands

Take the ordinary version. The analyst built the weekly revenue agent, and she hands in her notice. On her last Friday four things have to move: the instructions, the permissions, the know-how and the memory. In Kortix those are files in the project repository. Its layout is stated at the top of the manifest:

```text
#   agents/<name>.md          one file per agent (`agents.<name>.file`)
#   skills/<name>/SKILL.md    skills, loaded by every harness
#   memory/                   the project brain (the `kortix-memory` skill)
#   tools/<name>.ts           project tools, loaded by every harness
```

The manifest itself opens with two lines that say which agent a session boots when nobody names one, then declares each agent and how far it may reach:

```yaml
kortix_version: 2
default_agent: kortix

agents:
  kortix:
    file: agents/kortix.md
    connectors: all
    secrets: all
```

The split matters for a handover. Behavior lives in the markdown file the `file:` key points at; the manifest holds governance only, meaning which connectors, secrets and skills that agent may use. Her replacement opens `agents/kortix.md` and reads the instructions as prose. The top of the file is short:

```markdown
mode: primary
permission: allow
```

Under it the starter writes the working rules in plain language. What she wrote is what the next person reads.

Then the rest of the inheritance. `skills/close-pipeline/SKILL.md` holds the procedure the team agreed on, steps and exceptions. `memory/MEMORY.md` indexes what the company has taught its agents, one line per file behind it: which customer pays late, which report the board reads, why the old query was wrong. `tools/` holds any module the team wrote itself. The change request history holds the argument: why the prompt changed in March, what broke in June, who merged the fix.

A new analyst gets all of it with a clone:

```bash
git clone git@github.com:acme/company.git
cd company
ls agents skills memory tools
cat kortix.yaml
```

Nothing in that list was in her head, and nothing needed exporting from a vendor account. The starter is public at [Kortix on GitHub](https://github.com/kortix-ai/suna) if you want to read it before cloning.

Credentials are where small teams usually get hurt. Connector credentials are brokered server-side and never enter the machine, so the new analyst inherits a grant in `kortix.yaml` and a person with permission to change it, not a spreadsheet of API keys.

## Why a settings screen costs more after that Tuesday

Ownership is cheap while one person holds the setup and expensive the moment they leave. In a hosted builder, the agents, their instructions and their memory live in the vendor's workspace. The company keeps the output and loses the reasoning, and the next hire learns the vendor's screens. That trade is fine for one person and poor for five, because five eventually include someone who wants to know why the number changed.

Kortix keeps that reasoning in git, and work lands the way code does. The [docs](https://kortix.com/docs) describe the loop: the sandbox clones the repo and works on a new branch, then "The agent commits, pushes the session branch, and opens a change request against the project's default branch", and a person with the `project.gitops.merge` permission reviews the diff and merges it. Session work reaches `main` through a change request. Merge is default-deny for agents.

That gate is the point of the upgrade. The second user does not need a dashboard with more switches. They need to see, in a diff, what the agent's instructions were and what someone wants them to become, and to say yes or no. A settings screen shows the current value and forgets the history. A repository shows both.

## What five people pay

The pricing suits a team that has not decided how much it will use. The free plan is $0 with 500 credits a month and one project, enough for a handful of jobs a week while the second person works out whether the agent is worth sharing.

Paid credits start at $50 a month, and the $200 tier buys 20,000 credits, which the [pricing page](https://kortix.com/pricing) puts at roughly 1,830 agent-computer hours. A credit is a cent, and 11 credits buy an hour of the default 2 vCPU, 4 GB machine. A stopped computer costs nothing, so an agent that runs three times a day does not pay for the other twenty-one hours. People are not billed per seat and share one credit pool: the fifth colleague adds no line to the invoice.

Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. Self-hosting moves the record rather than the compute, so the cost of ownership is a machine you already have plus the attention of whoever patches it, and the [self-hosting guide](https://opensourceaiagentplatform.com/self-hosting) works through that trade. For the buyer's side, [open source AI agent platforms for small business](https://opensourceaiagentplatform.com/open-source-ai-agent-platform-for-small-business) covers the deployment shape end to end.

## Where the threshold sits in the wider field

Nothing here argues for buying early. The threshold decides which tool, because a closed one charges for the handover at the moment the choice is already made.

If you are still at one person, keep the laptop and the prompt. If you have just become two, start with Kortix. The [full comparison](open-source-ai-agent-platform-comparison.md) puts it beside seven other open source and self-hosted projects on scope, configuration ownership, model choice and the review boundary, and [how to choose an open source AI agent platform](how-to-choose-an-open-source-ai-agent-platform.md) turns those into six questions for any candidate.
