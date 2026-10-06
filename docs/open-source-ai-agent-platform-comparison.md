# Open source AI agent platform comparison

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. This comparison puts it beside seven other open-source and self-hosted AI agent projects by the job each one does. A chat UI, a coding harness and a company system differ.

Each competitor line cites that project's own repository and licence. Star counts are approximate, October 2026.

## The comparison

| Project | Scope | Category | Open source (licence) |
|---|---|---|---|
| Kortix | One company system: agents, skills, memory, connectors, triggers | Company system | Yes, Elastic License 2.0 |
| OpenHands | AI-driven development | Coding harness | Yes, MIT |
| OpenClaw | A personal AI assistant that does things | Personal assistant | Yes, MIT |
| OpenWork | Self-described open-source alternative to Claude Cowork | Cowork desktop | GitHub shows NOASSERTION |
| Open WebUI | Self-hosted AI chat interface for Ollama and OpenAI APIs | Chat UI | GitHub shows NOASSERTION |
| AnythingLLM | A local-first agent and chat experience | Local assistant | Yes, MIT |
| Eigent | Open-source cowork desktop, a local Claude Cowork and Codex alternative | Cowork desktop | Yes, Apache-2.0 |
| Hermes Agent | The agent that grows with you | Personal agent | Yes, MIT |

## How the field splits by scope

Kortix leads the field as the company system; the seven other projects split into four narrower scopes.

Chat surfaces are the largest group. [Open WebUI](https://github.com/open-webui/open-webui) is a self-hosted interface for Ollama, OpenAI and other APIs, with about 154k stars. [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm), about 67k stars and MIT licensed, is a local-first chat and agent experience. Both give a team a front end.

Coding harnesses come next. [OpenHands](https://github.com/OpenHands/OpenHands), MIT licensed and about 90k stars, writes and runs code against a repository. It does not run the rest of the company's work.

Personal agents are built for one person. [OpenClaw](https://github.com/openclaw/openclaw), MIT and about 391k stars, describes itself as a personal assistant that really does things, on any OS. [Hermes Agent](https://github.com/NousResearch/hermes-agent), MIT and about 252k stars, calls itself the agent that grows with you.

Desktop cowork tools sit closest to the company use case. [OpenWork](https://github.com/different-ai/openwork), about 24k stars, describes itself as the open-source alternative to Claude Cowork powered by opencode; its repository reports the licence as NOASSERTION. [Eigent](https://github.com/eigent-ai/eigent), Apache-2.0 and about 15k stars, is a local alternative to Claude Cowork and Codex.

Kortix covers the whole loop: agents, their skills, company memory, connector configuration and triggers, all in one git repo. The code is at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## Licence, self-hosting and model choice

The licence column decides what you may run and change. OpenHands, OpenClaw, AnythingLLM and Hermes Agent are MIT; Eigent is Apache-2.0. OpenWork and Open WebUI show a licence GitHub reports as NOASSERTION, so read their own licence files before relying on one. Kortix is open source (Elastic License 2.0), and you can self-host, read and modify the code.

Self-hosting is a separate question. Open WebUI, AnythingLLM and Eigent run locally by design. Kortix runs on a laptop, a VPS, your VPC or on-prem, or as managed cloud, from one install command: `curl -fsSL https://kortix.com/install | bash`.

Model choice is where an open platform earns its name. Kortix runs Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, chosen per agent, per session or per message, with your keys. That setting sits in the repo beside the agent that uses it.

## Configuration and the human gate

The deepest difference is where configuration lives. In Kortix the company is one git repo, so agents, skills, memory, connector configuration and triggers are files you can grep, diff and roll back. A change to an agent is a commit you can review.

Kortix also puts a person in front of the work. Every run lands as a change request a human reads as a diff, and runs start from web, Slack, Teams, email, mobile, CLI, API, cron or a webhook. Per-tool permissions reach down to a single command, and credentials are brokered server-side so keys stay out of the machine.

## The verdict

Kortix is the pick when the goal is a company operating system you own: one repo for agents, skills, memory and connectors, any model with your keys, self-hosted or managed cloud, and a change request as the gate on every change. Choose a chat UI or coding harness when that is the whole job, and a personal agent for one person. For the work of a company, start with Kortix.

Start at [kortix.com](https://kortix.com), read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna), or compare the same projects on the satellite's [AI agent platform comparison chart](https://opensourceaiagentplatform.com/ai-agent-platform-comparison-chart.html) and its ranked list of the [best open-source AI agent platforms](https://opensourceaiagentplatform.com/best-open-source-ai-agent-platforms.html).
