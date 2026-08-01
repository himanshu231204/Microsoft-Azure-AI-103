# Unit 3 — Options for agent development

> **Module:** [Get started with AI agent development on Azure](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/) · **Unit:** [Options for agent development](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/3-agent-development) · **Time:** ~6 min · **Status:** ✅ Completed

## Traditional AI frameworks vs AI agent frameworks

**Traditional AI frameworks** — integrate *intelligent capabilities* into apps (enhance, not autonomous):

| Capability | Example |
|------------|---------|
| Personalization | Netflix recommends shows based on viewing history |
| Automation & efficiency | Customer-service chatbots handle common inquiries |
| Enhanced UX | Siri / Google Assistant voice commands, predictive text |

**AI Agent Frameworks** — enable *autonomous, goal-oriented* agents that **reason, act, learn**:

| Capability | What it enables |
|------------|-----------------|
| Agent collaboration & coordination | Multiple agents communicate, share info, solve problems together |
| Task automation & management | Multi-step workflows + dynamic task delegation across agents |
| Contextual understanding & adaptation | Perceive context, decide on real-time data, adapt to change |

> 💡 Agents don't just process data — they pursue **objectives** (see `Agents.md` §1–2).

## The agent development solutions (know the full landscape)

| Solution | What it is | Best for |
|----------|-----------|----------|
| **Foundry Agent Service** | Managed Azure service; based on OpenAI Assistants API with more model choice, data integration, enterprise security | Professional devs building Azure-based AI solutions |
| **OpenAI Assistants API** | Subset of Foundry Agent Service; OpenAI models only | Simple agent work; in Azure, Foundry gives more flexibility |
| **Microsoft Agent Framework** | Lightweight dev kit; optimized for agents + multi-agent orchestration | Standalone / multi-agent systems (production path) |
| **AutoGen** | Open-source rapid agent development framework | Research & ideation; concepts folded into Agent Framework |
| **Microsoft 365 Agents SDK** | Self-hosted agents delivered through many channels (Slack, Messenger, etc.) | Professional devs extending Microsoft 365 Copilot |
| **Copilot Studio** | Low-code visual environment ("citizen developers") | Business users w/ low-code skills; Microsoft 365 ecosystem |
| **Agent Builder (M365 Copilot)** | Declarative natural-language agent creation, no coding | Business users with no dev experience |

> 💡 **AutoGen → Agent Framework migration** is the recommended production path (see [migration guide](https://learn.microsoft.com/agent-framework/migration-guide/from-autogen/)).

## Choosing the right solution (memorize this mapping table)

| User type / scenario | Recommended solution | Key capabilities |
|----------------------|---------------------|------------------|
| Business users, no dev experience | **Agent Builder (M365 Copilot)** | Declarative creation, no coding |
| Business users, low-code (Power Platform) | **Copilot Studio** | Low-code + business domain knowledge; Teams/Slack/Messenger |
| Professional devs extending M365 Copilot | **Microsoft 365 Agents SDK** | Full flexibility, complex extensions |
| Professional devs building Azure solutions | **Foundry Agent Service** | Azure AI integration, multiple models/storage/search |
| Devs building standalone/multi-agent systems | **Microsoft Agent Framework** | Single or multi-agent, orchestration patterns |

> ⚠️ **Exam insight:** There's overlap between solutions — familiarity, language preference, and ecosystem fit also drive the choice. Expect "match the user type to the right tool" questions.

## Key takeaways

- Agent frameworks go beyond traditional AI: agents **reason, act, and learn** toward goals
- Microsoft's spectrum spans **no-code → low-code → full SDK** (Agent Builder → Copilot Studio → 365 Agents SDK / Foundry Agent Service / Agent Framework)
- **Foundry Agent Service** = managed, Azure-native, Assistants-API-based
- **Microsoft Agent Framework** = recommended production path (AutoGen's successor)

## Related resources

- Deep dive: [`Agents.md`](../../../Agents.md) §5 (development options spectrum), §10 (frameworks comparison)
- Next: [Unit 4 — Azure AI Foundry Agent Service](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/4-azure-ai-agent-service)
