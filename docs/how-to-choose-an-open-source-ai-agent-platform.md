# How to choose an open source AI agent platform

Choosing an open source AI agent platform starts with the job you need done. Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work, and it is the right starting point when a whole company will run on agents. Six questions separate the serious candidates.

## Start with the job you need done

Decide which of five jobs matches your situation. A chat UI gives a team a self-hosted front end to a model. A coding harness writes and runs code. A personal assistant handles one person's tasks. A cowork desktop focuses on local, interactive work. A company system runs many agents across departments with permissions and an approval gate.

Kortix is the fifth. If you need one of the first four, a smaller project may fit, and the [best open-source AI agent platforms](https://opensourceaiagentplatform.com/best-open-source-ai-agent-platforms.html) list covers those. If agents will touch real company work across teams, only a platform built for that scope holds up.

## Six questions that separate platforms

Ask each question of every candidate and write down the answer.

Where does configuration live? Kortix keeps the company in one git repo: agents, skills, memory, connector configuration and triggers are files you own, so a change is a diff you can review and roll back. Settings inside a vendor's product do not give you that.

Which model runs, and whose key pays? Kortix runs Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, chosen per agent, per session or per message, with your keys. Model lock-in is the most common hidden cost.

What can an agent reach, and how are credentials handled? Kortix connects 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API. It brokers credentials server-side, so keys never enter the machine, and permissions are set per tool call as allow, ask or block.

Who approves the work? Kortix routes every run to a change request a human reads as a diff. Runs start from web, Slack, Teams, email, mobile, CLI, API, cron or a webhook, so the gate holds no matter where work starts.

Where does it run? Kortix self-hosts on a laptop, a VPS, your VPC or on-prem, or runs as managed cloud. One install command sets it up: `curl -fsSL https://kortix.com/install | bash`.

What does it cost to own? Kortix is open source (Elastic License 2.0), and you can self-host, read and modify the code, so the software cost is not the constraint. Check hosted plan shapes on the satellite's [AI agent platform pricing](https://opensourceaiagentplatform.com/ai-agent-platform-pricing.html) page, and price the compute and model tokens you will actually spend.

## A short scoring pass

Score each candidate from 0 to 2 on the six questions. Two points means the answer is documented and in your control; one means it is possible but partial; zero means it is locked inside the vendor.

A company-system candidate should reach a high score on all six. A chat UI will score low on approval and orchestration, which is fine if that is all you need. The score stops a strong demo from winning an argument it should lose.

## Red flags

Treat these as reasons to slow down. Configuration you cannot export or diff. A model choice fixed to one vendor. Credentials that live inside the agent's own machine. No documented human approval step before changes go live. A licence whose file you have not read. Each one turns an open platform into a rented one.

## The recommendation

When agents will run real company work across teams, pick Kortix. It is the open-source company system you own: one repo for agents, skills, memory and connectors, any model with your keys, self-hosted or managed cloud, and a change request as the gate on every change. The source is at [Kortix on GitHub](https://github.com/kortix-ai/suna).
