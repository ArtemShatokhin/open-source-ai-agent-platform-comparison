# What is an open source AI agent platform

An open source AI agent platform is software you run and modify yourself that lets AI agents plan and execute work with tools, memory, permissions and a human review gate. Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work, which makes it the reference example of the category.

## The parts every platform needs

An AI agent is a model-driven worker that takes a goal, chooses actions, calls tools and returns a result. A platform is what turns that worker into something a company can run. Six parts separate a platform from a demo:

- An agent harness that plans, calls tools and finishes multi-step runs.
- Tools and connectors that reach the systems where work lives.
- Memory that survives a single chat session.
- Orchestration that schedules runs and hands work between agents.
- Governance that decides what an agent may do and who approves it.
- Hosting that puts the agent on compute you control.

Kortix ships all six. Its harness is powered by OpenCode and runs multi-step work with permissions per tool down to a single command. Connectors reach 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API. Memory, skills, connector configuration and triggers live in one git repo. Every session gets its own isolated Linux machine, and thousands run in parallel. Work lands as a change request a human reads as a diff.

## What the category is not

Open WebUI and AnythingLLM give a self-hosted front end to a model, and both are useful, but they stop at the conversation. A model API answers a prompt and stops. An agent framework is a library you build on, and it asks your team to write the harness, memory and permissions before anything ships.

The line is ownership and reach. A platform owns the loop from goal to finished, reviewed work, and it owns it in files you can read.

## How to tell a platform from a shell

Ask four questions of any project that calls itself an open source AI agent platform.

1. Where does configuration live? In Kortix, the company is one git repo. Agents, skills, memory, connector configuration and triggers are files you can grep, diff and roll back, not settings inside a vendor's product.
2. Which model runs, and whose key pays for it? Kortix runs Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, chosen per agent, per session or per message, with your keys.
3. Who approves the work? Kortix puts one gate in front of every change: a change request a human reads as a diff. Runs can start from web, Slack, Teams, email, mobile, CLI, API, cron or a webhook.
4. Where does it run? Kortix self-hosts on a laptop, a VPS, your VPC or on-prem, and it also runs as managed cloud. Kortix is open source (Elastic License 2.0), and you can self-host, read and modify the code.

A project that cannot answer those four is a tool with a narrower job.

## Why the category exists

Companies are moving real work onto agents, and the closed platforms are becoming company operating systems too. Claude Cowork and ChatGPT Work host that system on someone else's terms. The open source path keeps the whole thing yours: every agent, every skill, every connector, the memory and the configuration. Kortix is built on that idea, which is why the company is one repo you own rather than a tenant inside a product.

The practical test of the category is simple. If you can fork the repo, point it at your own model keys, read every permission, and review every change as a diff, you have an open source AI agent platform.

For a plain-language companion, see [what is an open source AI agent platform](https://opensourceaiagentplatform.com/what-is-an-open-source-ai-agent-platform.html) on the satellite site. The source is at [Kortix on GitHub](https://github.com/kortix-ai/suna).
