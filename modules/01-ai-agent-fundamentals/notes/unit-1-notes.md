# Unit 1 — Introduction

> **Module:** [Get started with AI agent development on Azure](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/) · **Unit:** [Introduction](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/1-introduction) · **Time:** ~1 min · **Status:** ✅ Completed

## Key point

Generative AI is moving beyond simple chat apps → **agents** that operate **autonomously** to automate tasks, orchestrate business processes, and coordinate workloads.

## Single-agent scenario (expense agent)

An agent helping employees manage expense claims:

| Capability | How it works |
|------------|--------------|
| **Answer questions** | Generative model + corporate expense policy docs → "what can I claim, what limits apply?" |
| **Automate tasks** | Programmatic functions → auto-submit recurring claims (e.g., monthly cellphone bill) |
| **Route work** | Intelligently send claims to the right approver based on claim amount |

## Multi-agent scenario (travel agent → expense agent)

Multiple agents coordinating work between them:

1. **Travel booking agent** — books flights and hotels for employees
2. **Expense agent** — receives claims + receipts automatically from the travel agent
3. Result: an **integrated workflow spanning multiple business processes**

> 💡 **Pattern to remember:** agents can delegate to each other (this becomes *connected agents / multi-agent orchestration* in later modules — see `Agents.md` §12).

## Module learning objectives (the "why" for the whole module)

By the end of this module you'll be able to:

- [x] Describe core concepts related to AI agents
- [ ] Describe options for agent development
- [ ] Create and test an agent in the Azure AI Foundry portal

## Key takeaways

- Agents combine **generative models** (reasoning) with **programmatic functions** (action)
- Single-agent → one business process; multi-agent → cross-process workflows
- Agents don't just answer — they **act** (submit, route, book, coordinate)

## Related resources

- Module home: [ai-agent-fundamentals](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/)
- Next: [Unit 2 — What are AI agents?](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/2-what-are-agents)
