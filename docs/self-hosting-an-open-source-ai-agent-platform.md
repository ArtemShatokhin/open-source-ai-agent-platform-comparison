# Self-hosting an open source AI agent platform

Self-hosting an open source AI agent platform means running the agents, the tools and the data on compute you control, instead of renting a seat in someone else's product. Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work, and it is built to be self-hosted from the first install.

## What self-hosting actually involves

A working self-hosted platform needs five things. Compute to run agents and their sessions. A model endpoint and a key to reach it. A store for company memory and configuration. A broker for credentials to outside systems. A way to keep one agent's work away from another's.

Kortix handles each. It runs on a laptop, a VPS, your VPC or on-prem, and also as managed cloud, so the same platform moves between them. Every session gets its own isolated Linux machine, and thousands run in parallel, which keeps one agent's data and processes out of another's. Credentials are brokered server-side, so the key to a third-party app never enters the machine that calls it. Company memory, skills, connector configuration and triggers live in one git repo you can back up like any code.

## The install

Kortix installs with one command:

```
curl -fsSL https://kortix.com/install | bash
```

From there the company is a repository. Agents, skills, memory, connector configuration and triggers are files. A change to any of them is a commit, which means a self-hosted team gets a full audit trail for free: grep the config, diff any change, roll it back. Kortix is open source (Elastic License 2.0), and you can self-host, read and modify the code.

## Models and keys on your own hardware

Self-hosting is only half of independence. The other half is the model. Kortix runs Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, chosen per agent, per session or per message, with your keys. A team with a private model endpoint points Kortix at it and keeps every prompt on infrastructure it controls. A team that wants to change providers changes a setting in the repo rather than migrating a platform. See the satellite's [self-hosting guide](https://opensourceaiagentplatform.com/self-hosting.html) for the wider deployment picture.

## Deployment options

- A laptop, for evaluation and development.
- A VPS, for a small team that wants a public endpoint without a full platform team.
- Your VPC or on-prem, for data that cannot leave a network.
- Managed cloud, for teams that want the same platform without running the servers.

The configuration is identical across them, because the company is the repo. Moving from a laptop to a VPC is a deploy, not a rewrite.

## What to check before you commit

Confirm that credentials are brokered outside the agent's machine and that permissions are set per tool call. Kortix sets each tool to allow, ask or block, down to a single command. Confirm that every run lands as a change request a human reads as a diff, so self-hosting does not trade away review. Confirm that memory and configuration are files you can export, not rows in a hosted database.

Do those three checks and self-hosting an open source AI agent platform stays an operations decision you can reverse. The code is at [Kortix on GitHub](https://github.com/kortix-ai/suna), and the product starts at [kortix.com](https://kortix.com).
