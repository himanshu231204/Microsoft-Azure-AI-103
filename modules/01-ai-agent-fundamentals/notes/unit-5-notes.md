# Unit 5 — Exercise: Explore AI agent development

> **Module:** [Get started with AI agent development on Azure](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/) · **Unit:** [Exercise](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/5-exercise) · **Time:** ~30 min · **Status:** ⬜ Pending

## Setup requirements (do this BEFORE the exercise)

| Requirement | Details |
|-------------|---------|
| **Azure subscription** | Needed to access the Foundry portal · Sign up: [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account) (30-day credits) |
| **Foundry project** | Create a project in the Microsoft Foundry portal ([ai.azure.com](https://ai.azure.com)) |
| **Model deployment** | Deploy a model (e.g., GPT-4o-mini) from Build → Deployments in Foundry |

## Exercise steps (what you'll do)

1. **Sign into Microsoft Foundry** portal ([ai.azure.com](https://ai.azure.com))
2. **Create or select a project** in your Foundry resource
3. **Deploy a model** (e.g., GPT-4o-mini)
4. **Open the Agent playground** (Build → Agents → New Agent)
5. **Configure the agent** — name, instructions, model selection
6. **Add tools** — e.g., web search grounding, file search
7. **Test the agent** — ask questions, verify behavior
8. **Observe the responses** — notice grounded answers vs hallucination-free output

## Key things to notice during the exercise

| What you're testing | What to observe |
|---------------------|-----------------|
| Agent instructions | How different instructions change agent behavior |
| Web search grounding | Real-time info with inline citations (Bing) |
| File search | Agent uses uploaded docs to answer policy-type questions |
| Thread/conversation | Agent remembers previous messages in the same thread |
| Model playground | Direct model testing vs agent — difference in tool use |

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "No access to Foundry" | Ensure you have Contributor/Owner role on the Azure subscription |
| "Model not deployed" | Go to Build → Deployments → deploy GPT-4o or GPT-4o-mini |
| "Agent tool not working" | Check tool permissions — some require specific Azure services enabled |
| "Can't find the exercise" | Exercise opens in a new browser window; ensure popup blocker is off |

## Tips

- **Follow along in your own Foundry project** if you have one set up — this builds muscle memory
- **Try different instructions** — the playground lets you iterate quickly on agent behavior
- **Check token usage** — Foundry portal shows token consumption per agent run (useful for cost awareness later)
- **This is a repeatable exercise** — you'll revisit this pattern in Units 6 (Module assessment) and when building agents in Modules 2–7

## Related resources

- Deep dive: [`Agents.md`](../../../Agents.md) §6 (Agent Service), §9 (Python SDK essentials)
- [Foundry Agent Service documentation](https://learn.microsoft.com/azure/ai-services/agents/)
- Next: [Unit 6 — Module assessment](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/6-knowledge-check)
