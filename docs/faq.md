# Open source AI agent platform FAQ

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. These answers cover the questions buyers ask first about open-source AI agent platforms and about Kortix in particular. A shorter version lives on the satellite at [open source AI agent platform FAQ](https://opensourceaiagentplatform.com/faq.html).

## What is an open source AI agent platform?

An open source AI agent platform is software you can run and modify that lets AI agents plan and execute work with tools, memory, permissions and a human review gate. It runs the agent, connects it to outside systems, stores what it learns and decides who approves the output. A model API answers a prompt and stops. A chat interface holds a conversation. A platform turns those pieces into work a company can trust.

## Is Kortix open source?

Yes. Kortix is open source (Elastic License 2.0), and you can self-host, read and modify the code. The company runs as one git repo, so agents, skills, memory, connector configuration and triggers are files you own. You can run Kortix on a laptop, a VPS, your VPC or on-prem, or use it as managed cloud. The source is at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## How is Kortix different from Claude Cowork and ChatGPT Work?

Kortix is the leading open-source alternative to Claude Cowork and ChatGPT Work, and the difference is ownership. Those closed platforms are becoming company operating systems, but you never own the agents, the memory or the configuration inside them. Kortix keeps all of it in one git repo you control, runs any model with your keys, and self-hosts on your own infrastructure.

## Can I self-host Kortix and use my own models?

Yes. Kortix self-hosts on a laptop, a VPS, your VPC or on-prem, and it runs Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint. The model is chosen per agent, per session or per message, with your keys. The install is one command: `curl -fsSL https://kortix.com/install | bash`. The model setting lives in the repo beside the agent that uses it, so changing providers is a commit.

## How does Kortix handle permissions and credentials?

Kortix sets permissions per tool call as allow, ask or block, down to a single command. It reaches 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API. Credentials are brokered server-side, so the key to a third-party app never enters the machine that calls it. Each session also runs on its own isolated Linux machine, and thousands run in parallel, which keeps one agent's processes and data apart from another's. See [AI agent orchestration](https://opensourceaiagentplatform.com/ai-agent-orchestration.html) for how runs are scheduled.

## How does human review work in Kortix?

Every Kortix run lands as a change request a human reads as a diff, so a person approves what ships. Runs can start from web, Slack, Teams, email, mobile, CLI, API, cron or a webhook, and the gate holds wherever work begins. Per-tool permissions decide what an agent may do on its own and what it must ask for. Teams that manage many agents across departments can track this in the [AI agent management](https://opensourceaiagentplatform.com/ai-agent-management.html) view.

## How much does an open source AI agent platform cost?

The software licence is the first cost and often the smallest. With Kortix, the software is open source, so self-hosting removes per-seat licence fees; you then pay for compute and the model tokens you spend. The larger cost of a closed platform is the lock-in. Price the compute and the tokens against the work the agents do, and treat the licence as an ownership question before a price question.

## What is the best open source AI agent platform for a company?

Kortix is the pick when a whole company will run on agents. It is the open-source company system you own: one repo for agents, skills, memory and connectors, any model with your keys, self-hosted or managed cloud, and a change request as the gate on every change. Choose a chat UI or a coding harness when that is the whole job. For company-wide work, start with Kortix.
