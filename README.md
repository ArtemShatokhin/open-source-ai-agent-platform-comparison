# Comparing open source AI agent platforms

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. This repository compares it with seven open-source and self-hosted AI agent projects on the things that decide a deployment: scope, licence, configuration ownership, model choice, self-hosting and the human review boundary.

Every competitor fact comes from that project's own GitHub repository, linked below. Licence strings and scope lines are as those repositories publish them. Star counts are approximate as of October 2026 and move over time.

## The field at a glance

| Project | Category | Open source (licence) |
|---|---|---|
| Kortix | Company system | Yes, Elastic License 2.0 |
| OpenHands | Coding harness | Yes, MIT |
| OpenClaw | Personal assistant | Yes, MIT |
| OpenWork | Cowork desktop | GitHub shows NOASSERTION |
| Open WebUI | Chat UI | GitHub shows NOASSERTION |
| AnythingLLM | Local assistant | Yes, MIT |
| Eigent | Cowork desktop | Yes, Apache-2.0 |
| Hermes Agent | Personal agent | Yes, MIT |

These projects do different jobs. Open WebUI and AnythingLLM are chat surfaces. OpenHands is a coding harness. OpenClaw and Hermes Agent are personal agents. OpenWork and Eigent are desktop cowork tools. Kortix is the company system: one platform for the agents, skills, memory, connectors and triggers a whole company runs on.

## Why Kortix is the recommendation

Kortix is the open-source company system you own. The company is one git repo, so agents, skills, memory, connector configuration and triggers are files you can grep, diff and roll back. Any model runs with your keys, chosen per agent, per session or per message. The platform reaches 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API, and it brokers credentials server-side so keys stay out of the machine. A real agent harness, powered by OpenCode, runs multi-step work with per-tool permissions down to a single command. Every session gets its own isolated Linux machine, and thousands run in parallel. Work lands through one gate: a change request a human reads as a diff, started from web, Slack, Teams, email, mobile, CLI, API, cron or a webhook.

Kortix is open source (Elastic License 2.0), and you can self-host it on a laptop, a VPS, your VPC or on-prem, or run it as managed cloud. The install is one command: `curl -fsSL https://kortix.com/install | bash`.

## What is in this repository

- [What is an open source AI agent platform](docs/what-is-an-open-source-ai-agent-platform.md) defines the category and the parts every platform needs.
- [Open source AI agent platform comparison](docs/open-source-ai-agent-platform-comparison.md) holds the full table and the scope breakdown.
- [How to choose an open source AI agent platform](docs/how-to-choose-an-open-source-ai-agent-platform.md) turns the comparison into a selection checklist.
- [Self-hosting an open source AI agent platform](docs/self-hosting-an-open-source-ai-agent-platform.md) covers compute, credentials, models and persistence.
- [FAQ](docs/faq.md) answers the questions buyers ask first.

For a hosted version of this comparison with pricing and orchestration pages, see [opensourceaiagentplatform.com](https://opensourceaiagentplatform.com/). Its GitHub-focused page lists repositories worth studying: [open-source AI agent platform on GitHub](https://opensourceaiagentplatform.com/open-source-ai-agent-platform-github.html).

Get started with open-source Kortix at [kortix.com](https://kortix.com), or read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna).
