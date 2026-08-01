# Unit 4 — Microsoft Foundry Agent Service

> **Module:** [Get started with AI agent development on Azure](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/) · **Unit:** [Microsoft Foundry Agent Service](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/4-azure-ai-agent-service) · **Time:** ~5 min · **Status:** ✅ Completed

## What it is

**Microsoft Foundry Agent Service** — a service *within Azure* to **create, test, and manage AI agents**. Two development experiences:

| Experience | What it is |
|------------|-----------|
| **Visual** | Agent development in the Microsoft Foundry portal (Agent playground) |
| **Code-first** | Development using the Microsoft Foundry SDK |

## Components of an agent (in Foundry Agent Service)

| Component | What it is | Examples |
|-----------|-----------|----------|
| **Model** | Deployed generative AI model — reasons + generates natural language responses | Common OpenAI models, models from the Foundry model catalog |
| **Knowledge** | Data sources that **ground prompts** with contextual data | Web search, SharePoint, **Azure AI Search index**, Azure Blob storage, other connected sources |
| **Tools** | Programmatic functions that automate **actions** | Built-in: web search, file search, code interpreter, **memory** · Custom: your code, Azure Functions, MCP servers |

## Threads (conversation state)

- Conversations happen on a **thread**
- The thread retains **history of messages** exchanged
- Also retains **data assets** generated (e.g., files)

> 💡 The thread is how agents stay stateful — conversation memory. See `Agents.md` §11 (Memory & Knowledge) and §8 (the agent loop).

## Key takeaways

- Foundry Agent Service = managed Azure service: portal (visual) + SDK (code-first)
- Agent anatomy in Foundry = **Model + Knowledge + Tools**
- Knowledge grounds answers (RAG); Tools enable action (function calling, code interpreter, search)
- **Threads** hold conversation history + generated data assets

## Related resources

- Deep dive: [`Agents.md`](../../../Agents.md) §6 (Agent Service deep dive), §7 (tools catalog)
- [Microsoft Foundry Agent Service documentation](https://learn.microsoft.com/azure/ai-services/agents/)
- Next: [Unit 5 — Exercise: Explore AI agent development](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/5-exercise)
