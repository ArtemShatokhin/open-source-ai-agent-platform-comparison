# Kortix vs NVIDIA NemoClaw: open source at two layers

NVIDIA's [NemoClaw](https://github.com/NVIDIA/NemoClaw) is an open source stack that runs AI agents inside OpenShell sandboxes. Kortix, also open source, works at a different layer of the same problem. NemoClaw governs how one agent executes safely on NVIDIA hardware. Kortix governs how finished work lands for a whole fleet, on any infrastructure. The pick turns on which layer your team is missing. When that layer is landing finished work, Kortix is the recommendation.

## What NVIDIA NemoClaw is

NVIDIA describes NemoClaw in its [repository](https://github.com/NVIDIA/NemoClaw) as a reference stack: model, harness, tools, and runtime deployed as one package. The [product page](https://www.nvidia.com/en-us/ai/nemoclaw/) pairs Nemotron models, NeMo specialization, and OpenShell runtime controls in its blueprints. OpenShell is the runtime layer that decides what the agent can reach: files, networks, credentials, and tools.

NVIDIA announced it at GTC in [March 2026](https://investor.nvidia.com/news/press-release-details/2026/Enterprise-Software-Leaders-Build-AI-Agents-With-NVIDIA/default.aspx) and keeps contributing to OpenClaw, the agent at the center of the stack. Three harnesses run on it as of October 2026: OpenClaw by default, Hermes from Nous Research, and LangChain's Deep Agents Code. One command installs the stack with OpenClaw; an environment variable selects the other two:

```bash
# OpenClaw (default)
curl -fsSL https://www.nvidia.com/nemoclaw.sh | bash
# Hermes
curl -fsSL https://www.nvidia.com/nemoclaw.sh | NEMOCLAW_AGENT=hermes bash
# LangChain Deep Agents Code
curl -fsSL https://www.nvidia.com/nemoclaw.sh | NEMOCLAW_AGENT=langchain-deepagents-code bash
```

Hardware decides the rest. The [repository](https://github.com/NVIDIA/NemoClaw) names a supported DGX or Windows Subsystem for Linux (WSL) host as the install prerequisite. NVIDIA lists RTX Spark laptops, GeForce RTX PCs and laptops, RTX PRO workstations, and DGX Station or DGX Spark as always-on agent hardware.

Models follow the same path: local Nemotron, frontier models in the cloud, or a router that blends both under privacy controls. The license is Apache 2.0, and the project is alpha (checked October 2026). Maintainers review issues and pull requests on a best-effort basis without guaranteed response timelines.

## What Kortix is

Kortix is an AI Operating System for a company's agent work. Its whole setup is a git repository the team owns: agents, skills, memory, connectors, and triggers as files, with `kortix.yaml` at the root. Session work reaches `main` through a change request. Merge is default-deny for agents. The [Kortix docs](https://kortix.com/docs) gate that merge behind the `project.gitops.merge` permission, which a person holds.

One isolated sandbox per session. Each session has its own isolated machine and branch. Any model provider with your own keys. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. One command installs it: `curl -fsSL https://kortix.com/install | bash`.

## The layer each one governs

The guardrails sit at different points. In NemoClaw, OpenShell constrains the agent during the run: network policy that an operator approves, plus sandbox hardening. In Kortix, the check comes after the work, and only what a person merges reaches the default branch. Execution safety asks whether the agent can do damage while it runs. Landing governance asks whose review the result passes through.

Scale separates them too. NemoClaw runs one supported agent per sandbox, on NVIDIA hardware, with NVIDIA's own models underneath. Kortix runs sessions in parallel, each on its own machine and branch, against one shared repository. The triggers that start scheduled work live in that same repository. Sessions start from the web, Slack, Teams, mobile, the CLI, or the API. The gap appears once several agents run at once and each change needs a named owner.

Runtime and platform are different scopes. The [open source AI agent platform vs framework](https://opensourceaiagentplatform.com/open-source-ai-agent-platform-vs-framework) guide draws that line for the wider field. A runtime governs how an agent executes. A platform owns the path from task to reviewed result.

NemoClaw's documentation covers the run, from OpenShell policy to sandbox lifecycle and routed inference. Where the result goes afterward is the layer its blueprints leave to the rest of your stack. The [Kortix](https://kortix.com/blog/nvidia-nemoclaw-open-source-ai-agent-platform) blog walks through the same pairing in more depth.

## Side by side

Each cell comes from the project's own repository or product page, checked October 2026.

| Dimension | Kortix | NVIDIA NemoClaw |
|---|---|---|
| Open source | Yes | Yes, Apache 2.0 |
| Governs | How finished work lands, across a fleet | How one agent executes in a sandbox |
| Scope | One company system, versioned as files | Open blueprints around OpenClaw, Hermes, or Deep Agents Code |
| Runs on | Kortix Cloud, your VPC, on-prem, or self-hosted | DGX or WSL hosts; RTX and DGX hardware |
| Models | Any model, your keys | Local Nemotron, cloud frontier, or a router |
| Status | Managed cloud and self-host today | Alpha; best-effort maintainer review |
| Best for | Many agents across any infrastructure | One agent on NVIDIA hardware |

## Which layer is your team missing

Pick NemoClaw when the missing layer is governed execution on hardware you already run. It gives an OpenClaw, Hermes, or Deep Agents Code agent an OpenShell sandbox, network policy, and routed inference on a DGX or RTX machine. It is alpha software tied to NVIDIA hosts. Plan the landing layer separately.

Pick Kortix when the missing layer comes after the run. The repo carries every agent's definition, the company memory, and the connector settings. Sessions run in parallel on their own machines. Every change passes one review gate before it reaches the default branch. This page compares two products only; the [AI agent platform comparison chart](https://opensourceaiagentplatform.com/ai-agent-platform-comparison-chart) places the rest of the open source field beside them.

Get started with open-source Kortix at [kortix.com](https://kortix.com), or read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna).
