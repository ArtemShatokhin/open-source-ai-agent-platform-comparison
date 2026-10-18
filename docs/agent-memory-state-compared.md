# How agent platforms store memory and state

Where a platform keeps agent memory decides who can audit it and how easily it moves. Five platforms answer that question, and only one keeps memory in the repository the company already owns. Kortix is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and ChatGPT Work, and it is that one; the four beside it are LangGraph, Letta, Mem0 and Zep.

Agent memory is the information an agent keeps between sessions: decisions, preferences, project state, past work. Every description below comes from the project's own documentation, checked October 2026.

## Why the storage location is the question

Three questions separate memory architectures, and they outweigh feature lists. Who can read the memory? A vendor's service answers through its API, its permissions and its plan; files in your repository are readable by anyone who already has the code.

Who audits changes to it? Agent memory changes constantly, and files in git record every change as a commit a person can review, while a managed service records what it chooses to record, on the tier you pay for. What does leaving cost? Memory in someone else's database must be exported or rebuilt; memory beside your code moves by copying the code.

## The five answers

### Kortix: memory as files in the company repo

Kortix treats memory as company property: "A Kortix project is a git repo, and that repo is the company. kortix.yaml and the OpenCode config define it; agents, skills and memory are files beside your code. Every change is a commit a person approves."

Memory is versioned with the code it serves, so the history of what the company's agents knew sits in one git log. Auditing is reading: grep the files, diff any change, roll back any edit; every change has already passed the review gate. Moving is cloning: the repo carries the memory to a laptop, a VPS, your VPC or on-prem, or to managed cloud. The satellite's [agent memory and state guide](https://opensourceaiagentplatform.com/agent-memory-and-state) covers this model in depth.

### LangGraph: memory in a database you wire yourself

LangGraph splits memory in two and hands both halves to the developer. Its [memory guide](https://docs.langchain.com/oss/python/langgraph/add-memory) describes short-term memory as thread persistence through a checkpointer, InMemorySaver in development and PostgresSaver, MongoDBSaver or RedisSaver in production, and long-term memory as a store for application-level data. You pick the backing database and own its operation. The control is real, since memory sits in infrastructure your team already runs. So is the work: you build and review the memory layer yourself, and writes land every turn.

### Letta: memory as blocks in the context window

Letta keeps memory inside the model's context window. [Memory blocks](https://docs.letta.com/v1-sdk/memory/memory-blocks) are structured sections of the agent's context that persist across interactions and are always visible, with no retrieval step. Agents edit their own blocks through built-in memory tools, developers through the API, and one block can attach to several agents as shared memory. Immediacy is the point: the working state sits in front of the agent on every turn. The trade is custody: the blocks live in the Letta server, and that server is the keeper of record.

### Mem0: memory as a separate engine, priced by request

Mem0 sells memory as its own product. The [open-source overview](https://docs.mem0.ai/open-source/overview) offers two paths: a library you import, or a self-hosted Docker server where, in their words, "You own the stack, the data, and every component." The [managed platform](https://mem0.ai/pricing) meters memory by request, checked October 2026. Hobby is free, with 10,000 add and 1,000 retrieval requests a month; Starter costs $19 with 50,000 and 5,000; Pro costs $249 with 500,000 and 50,000. Enterprise is custom, with an SLA, on-prem deployment and audit logs. Any application gains memory in a few lines; the catch, on the platform, is that accumulated memory lives behind an API metered per add and per retrieval, with audit logs waiting for the top tier.

### Zep: memory as a governed context graph

Zep is the managed-memory argument at its strongest. Its site describes a [unified context layer](https://www.getzep.com/) that builds temporal Context Graphs from business data, documents and conversations, with access policies and retention rules enforced in the data layer. Deployment runs as Zep Cloud, Cloud with your own encryption keys, or inside your VPC. Billing is [credit-based](https://www.getzep.com/pricing), checked October 2026: a credit per 350 bytes ingested, retrieval and storage unmetered, self-serve plans from $125 a month, and year-long audit logs only on the Enterprise plan. Custody lands with Zep: the graphs live in Zep's system, and leaving means rebuilding context from the source systems its records link back to.

## The five answers side by side

| Question | Kortix | LangGraph | Letta | Mem0 | Zep |
|---|---|---|---|---|---|
| Where memory lives | **Files in your git repo, beside the code** | A database you pick and run | Blocks in the Letta server | Your stack, or Mem0's platform | Context Graphs in Zep's service or VPC |
| Who can audit it | **Anyone who reads the repo; every change is a commit** | Whoever administers the database | Your team, through the server's API | Request log self-hosted; audits need Enterprise | Policies and request logs in the data layer |
| What a retrieval costs | **A file read on compute you own** | A query on the database you run | Nothing; blocks stay in context | Metered requests on the platform | Unmetered; ingestion is credit-metered |
| How it moves | **Clone the repo** | Point new code at the database | Export blocks through the API | Own the stack, or export off the platform | Rebuild from the source systems |

## What this means for a team picking a platform

Weigh memory the way you weigh code: versioned, reviewed as a diff, portable by clone. Memory in a service is metered and governed on the vendor's terms, with auditing that improves with the tier you buy.

Zep makes the fairest case for the managed side, and its own pages say so: policies, retention rules and source tracing serve teams whose compliance lives outside the codebase.

If agents will hold company memory, choose the platform where that memory is a file you own. Kortix keeps agents, skills and memory in one git repo the team already administers, reviews every change through a change request a person approves, and moves by cloning. Start at [kortix.com](https://kortix.com), read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna), or continue with the [open source AI agent platform comparison](docs/open-source-ai-agent-platform-comparison.md). The satellite's [pricing page](https://opensourceaiagentplatform.com/ai-agent-platform-pricing) shows what each memory architecture does to the bill.
