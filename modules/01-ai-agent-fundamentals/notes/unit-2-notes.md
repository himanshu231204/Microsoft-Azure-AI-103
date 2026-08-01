# Unit 2 — What are AI agents?

> **Module:** [Get started with AI agent development on Azure](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/) · **Unit:** [What are AI agents?](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/2-what-are-agents) · **Time:** ~3 min · **Status:** ✅ Completed

## Core definition

> AI agents are smart applications that use **language models** to understand what you need and then **take action** to help you.

**What makes an agent special (vs a chatbot):**
- **Remembers** your conversation
- **Actually does things** — answers, decides, completes tasks automatically

**Architecture:** a language model + **instructions** + **tools** (per the agent component diagram).

## Three essential agent capabilities (expense agent example)

| Capability | What it does | Expense agent example |
|------------|--------------|-----------------------|
| **Knowledge integration & reasoning** | Generative model + documents → accurate answers | Answers policy questions from expense policy docs |
| **Task automation through functions** | Executes programmatic functions | Automatically submits expense claims |
| **Intelligent decision-making** | Applies business rules | Routes claims to the right approver by amount |

**Agent flow (grounded RAG pattern — memorize this):**
1. User asks a question
2. Agent accepts it as a **prompt**
3. Agent uses a **knowledge store** (policy docs) to **ground the prompt**
4. Grounded prompt → **language model** → response
5. Agent **generates an expense claim** and submits it for processing → check payment

> 💡 This is the **retrieval + action** loop — the foundation of RAG in agents. See `Agents.md` §3 (Agent vs RAG) and §8 (function calling).

## Multi-agent coordination (travel agent)

| Capability | What it does |
|------------|--------------|
| **Service integration** | Books flights/hotels via external travel service APIs |
| **Cross-agent communication** | Initiates expense claims through the expense agent (with receipts) |
| **End-to-end automation** | Completes booking + expense workflow with no manual intervention |

**Multi-agent flow:**
1. User provides trip details to the travel booking agent
2. Travel agent automates booking (flights + hotel)
3. Travel agent initiates an expense claim through the **expense agent**
4. Expense agent submits the claim for processing

## ⚠️ Security risks of AI agents

As agents become autonomous + integrated into enterprise systems, they introduce **new security risks beyond traditional apps**.

| Risk area | What's happening | Example symptom |
|-----------|------------------|-----------------|
| **Data leakage & privacy exposure** | Agent accessed sensitive data w/o controls to prevent external exposure | Shared confidential salary data in a customer chat |
| **Prompt injection & manipulation** | Malicious input overrode the agent's intended behavior | Tricked into revealing a database password |
| **Unauthorized access & privilege escalation** | Weak access controls let agent act beyond scope | Support agent deleting customer records it shouldn't touch |
| **Data poisoning** | Corrupted training/contextual data → unsafe outputs | Recommending fraudulent products after data update |
| **Supply chain vulnerabilities** | Third-party dependency introduced a vulnerability | Plugin sending data to an unknown server |
| **Over-reliance on autonomous actions** | Agent acted without validation or human oversight | Auto-processed a refund without verification |
| **Inadequate auditability & logging** | Missing logs → can't trace actions or detect misuse | Can't figure out who accessed what, when |
| **Model inversion & output leakage** | Attacker exploited outputs to infer sensitive data | Extracting customer info via repeated queries |

### Security-by-design best practices (memorize — maps to `Agents.md` §15)

| Practice | What to do |
|----------|------------|
| **Control access tightly** | RBAC + **least privilege** — agents only get what they need |
| **Validate all inputs** | Prompt filtering/validation to block injection before it reaches the agent |
| **Human oversight for critical actions** | Sandbox or gate sensitive ops behind **human-in-the-loop approvals** |
| **Track everything** | Comprehensive logging + traceability — who did what, when, why |
| **Monitor supply chain** | Audit third-party dependencies & integrations regularly |
| **Keep models healthy** | Retrain/validate continuously to detect **drift** or **poisoning** |

## Key takeaways

- Agent = language model + instructions + tools; it **acts**, doesn't just chat
- Agent loop: prompt → ground with knowledge → generate → take action
- Multi-agent = agents coordinate across processes (delegation between specialized agents)
- Security-by-design from day one: least privilege, input validation, human-in-the-loop, logging, supply-chain audits, model monitoring

## Related resources

- Deep dive: [`Agents.md`](../../../Agents.md) §2 (agent capabilities), §15 (Responsible AI & guardrails)
- Next: [Unit 3 — Options for agent development](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/3-agent-development)
