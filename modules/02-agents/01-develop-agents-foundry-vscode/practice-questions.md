# Module 2.1 — Practice Questions

**Module**: Develop AI agents with Microsoft Foundry and Visual Studio Code
**Source**: [Microsoft Learn](https://learn.microsoft.com/training/modules/develop-ai-agents-azure-vs-code/)

50 practice questions covering AI agent fundamentals, Foundry Agent Service, VS Code development, tools, testing, and deployment.

---

## Section 1: AI Agent Fundamentals (Q1–10)

**Q1.** What three core elements combine to form an AI agent?
- A) Model, dataset, and training pipeline
- B) LLM, instructions, and tools
- C) Endpoint, key, and container
- D) Thread, message, and run

<details><summary>Answer</summary>**B** — An AI agent combines an LLM (reasoning engine), instructions (role/scope), and tools (APIs, code, data).</details>

**Q2.** Which statement best distinguishes an AI agent from a plain LLM call?
- A) An agent always uses a larger model
- B) An agent can call tools and iterate toward a goal, while a plain call is one-shot
- C) A plain call maintains conversation state
- D) There is no difference

<details><summary>Answer</summary>**B** — Agents are goal-directed, can call tools, and iterate; a plain LLM call is a single prompt→response.</details>

**Q3.** In the classic function-calling loop, who actually executes the custom function?
- A) The LLM
- B) The Foundry Agent Service
- C) Your application code
- D) The model deployment

<details><summary>Answer</summary>**C** — The agent *requests* a function call, but **your app** executes the function and submits the output back.</details>

**Q4.** What is the correct order of the 5-step function-calling pattern?
- A) Create agent → define tools → send prompt → execute → final response
- B) Define tools → create agent → send prompt → execute and return → final response
- C) Send prompt → define tools → create agent → execute → final response
- D) Define tools → send prompt → create agent → final response → execute

<details><summary>Answer</summary>**B** — Define function tools → create agent → send prompt → execute and return → get final response.</details>

**Q5.** Which of the following is NOT one of the three core ingredients of an AI agent?
- A) LLM
- B) Instructions
- C) Tools
- D) A dedicated GPU

<details><summary>Answer</summary>**D** — Agents are defined by LLM + instructions + tools; compute is managed by the platform.</details>

**Q6.** What is a "thread" in agent terminology?
- A) A single model inference
- B) A conversation session between an agent and a user
- C) A container instance
- D) A tool definition

<details><summary>Answer</summary>**B** — A thread is a conversation session; it stores messages and auto-truncates to fit the model's context.</details>

**Q7.** What is a "run" in agent terminology?
- A) A single execution of an agent that can span multiple threads and messages
- B) A single message in a conversation
- C) The deployment of an agent
- D) A tool call

<details><summary>Answer</summary>**A** — A run is a single execution of an agent that can span multiple threads and messages.</details>

**Q8.** Which element of an agent defines its role, scope, and behavioral rules?
- A) The model
- B) The instructions (system prompt)
- C) The tools
- D) The endpoint

<details><summary>Answer</summary>**B** — Instructions define the agent's role, scope, and behavioral rules.</details>

**Q9.** What is the primary purpose of tools in an agent?
- A) To increase model size
- B) To let the agent access external capabilities like APIs, data, and code execution
- C) To replace the LLM
- D) To store conversation history

<details><summary>Answer</summary>**B** — Tools extend the agent's capabilities to access APIs, data, search, and run code.</details>

**Q10.** Which statement about agent state is correct?
- A) Agents are always stateless
- B) Agents maintain conversation state through threads
- C) State is stored only in the model weights
- D) Agents cannot remember prior messages

<details><summary>Answer</summary>**B** — Agents maintain conversation state through threads, which store messages across turns.</details>

---

## Section 2: Foundry Agent Service (Q11–20)

**Q11.** What does Microsoft Foundry Agent Service provide for the agents you define?
- A) Only model hosting
- B) Hosting, scaling, identity, state, and monitoring
- C) Only tool definitions
- D) Only authentication

<details><summary>Answer</summary>**B** — Agent Service handles hosting, scaling, identity, state, and monitoring.</details>

**Q12.** Which agent type is defined entirely through configuration with no runtime code to maintain?
- A) Hosted agent
- B) Prompt agent
- C) Container agent
- D) Function agent

<details><summary>Answer</summary>**B** — Prompt agents are config-only (instructions, model, tools); no app code or compute to manage.</details>

**Q13.** Which agent type ships as a container image or zip of source code and runs on Azure Container Apps?
- A) Prompt agent
- B) Hosted agent
- C) Portal agent
- D) Playground agent

<details><summary>Answer</summary>**B** — Hosted agents are code-based, shipped as a container image or source zip, and run on Azure Container Apps.</details>

**Q14.** Which agent type is best suited for agents that call custom code or require custom orchestration?
- A) Prompt agent
- B) Hosted agent
- C) Both equally
- D) Neither

<details><summary>Answer</summary>**B** — Hosted agents are best for custom code, multi-agent, and custom protocols.</details>

**Q15.** What is the Responses API?
- A) A separate model deployment type
- B) The single model-and-tools endpoint behind every agent type
- C) A tool for web search
- D) A monitoring service

<details><summary>Answer</summary>**B** — The Responses API is the single model-and-tools endpoint behind every agent type.</details>

**Q16.** Which agent type has automatic, dedicated Microsoft Entra identity per agent?
- A) Prompt agents only
- B) Hosted agents only
- C) Both prompt and hosted agents
- D) Neither

<details><summary>Answer</summary>**C** — Both agent types have agent identity; hosted agents get an automatic dedicated Entra identity per agent.</details>

**Q17.** What is the cost model difference for hosted agents compared to prompt agents?
- A) Hosted agents are always free
- B) Hosted agents add container compute costs on top of inference and tool usage
- C) Prompt agents cost more
- D) There is no difference

<details><summary>Answer</summary>**B** — Hosted agents cost per-call inference + tool usage **+ container compute**.</details>

**Q18.** Which agent type is best for a fast start with no custom orchestration?
- A) Hosted agent
- B) Prompt agent
- C) Container agent
- D) Multi-agent

<details><summary>Answer</summary>**B** — Prompt agents are best for fast start and agents without custom orchestration.</details>

**Q19.** What does the additive pattern of the Responses API allow?
- A) Adding more models to an agent
- B) Calling Foundry models + platform tools directly, then later packaging the same code as a hosted agent
- C) Adding more tools to the catalog
- D) Combining multiple subscriptions

<details><summary>Answer</summary>**B** — You can call the Responses API directly, then package the same code as a hosted agent later.</details>

**Q20.** Which of the following is a key feature of Foundry Agent Service?
- A) Manual scaling only
- B) Automatic scaling
- C) No identity management
- D) No monitoring

<details><summary>Answer</summary>**B** — Agent Service provides automatic scaling (request volume for prompt agents, container instances for hosted agents).</details>

---

## Section 3: Development Approaches & Portal (Q21–30)

**Q21.** Which of the following is NOT a development approach for building agents?
- A) Foundry portal
- B) VS Code extension (designer)
- C) SDK / REST
- D) Azure DevOps pipelines only

<details><summary>Answer</summary>**D** — Agents can be built via portal, VS Code, and SDK/REST; DevOps is for CI/CD, not the primary authoring surface.</details>

**Q22.** What is the recommended platform for AI development on Azure?
- A) Azure Cognitive Services
- B) Microsoft Foundry
- C) Azure Machine Learning only
- D) Azure Functions

<details><summary>Answer</summary>**B** — Microsoft Foundry is the recommended platform for AI development on Azure.</details>

**Q23.** When configuring an agent, what model reference do you use?
- A) The model family name (e.g., GPT-4o)
- B) The model deployment name
- C) The model's training date
- D) The model's parameter count

<details><summary>Answer</summary>**B** — You reference the **model deployment name** (what you chose when deploying the model).</details>

**Q24.** What is the first prerequisite for building an agent in the Foundry portal?
- A) A deployed model in a Foundry project
- B) A GitHub Copilot subscription
- C) A container registry
- D) A custom function

<details><summary>Answer</summary>**A** — You need a Foundry project with a deployed model.</details>

**Q25.** Which approach is best for CI/CD-friendly, programmatic agent creation?
- A) Foundry portal
- B) VS Code designer
- C) SDK / REST
- D) Playground

<details><summary>Answer</summary>**C** — SDK/REST is CI/CD-friendly and enables programmatic control and automation.</details>

**Q26.** Where do you create and test agents visually without writing code?
- A) In the model catalog
- B) In the Foundry portal and VS Code designer
- C) In Azure DevOps
- D) In the container registry

<details><summary>Answer</summary>**B** — The Foundry portal and VS Code designer provide visual agent authoring.</details>

**Q27.** What is the purpose of the agent playground?
- A) To deploy agents
- B) To send messages to a deployed agent and verify its behavior
- C) To create models
- D) To manage subscriptions

<details><summary>Answer</summary>**B** — The playground lets you test a deployed agent by sending prompts and viewing outputs.</details>

**Q28.** Which of the following is required to deploy an agent to Agent Service?
- A) A custom container
- B) A deployed model in the project
- C) A GitHub Copilot subscription
- D) A custom function

<details><summary>Answer</summary>**B** — You need a deployed model in your Foundry project to build and deploy an agent.</details>

**Q29.** What does the "Open in VS Code for the Web" capability in the playground do?
- A) Deploys the agent to production
- B) Imports your code sample, API endpoint, and key into a VS Code workspace
- C) Deletes the model
- D) Creates a new subscription

<details><summary>Answer</summary>**B** — It imports the code sample, endpoint, and key into a VS Code for the Web workspace.</details>

**Q30.** Which statement about agent authoring is correct?
- A) Agents can only be authored in the portal
- B) Agents are declarative and can be authored in the portal, VS Code, or SDK/REST
- C) Agents require custom code in all cases
- D) Agents cannot be edited after deployment

<details><summary>Answer</summary>**B** — Agents are declarative (YAML) and authorable across portal, VS Code, and SDK/REST.</details>

---

## Section 4: VS Code Extension & Configuration (Q31–40)

**Q31.** What is the name of the VS Code extension for Foundry agent development?
- A) Azure Tools
- B) Microsoft Foundry Toolkit for Visual Studio Code
- C) GitHub Copilot
- D) C# Dev Kit

<details><summary>Answer</summary>**B** — The **Microsoft Foundry Toolkit for Visual Studio Code** extension (aka.ms/foundrytk).</details>

**Q32.** What format is used to define an agent's configuration in VS Code?
- A) JSON
- B) YAML
- C) XML
- D) TOML

<details><summary>Answer</summary>**B** — Agents are defined declaratively in **YAML**.</details>

**Q33.** In the agent YAML, which field specifies the model deployment?
- A) `name`
- B) `model.id`
- C) `instructions`
- D) `version`

<details><summary>Answer</summary>**B** — `model.id` specifies the model deployment (e.g., `gpt-4o-1`).</details>

**Q34.** Which field in the agent YAML defines the agent's behavioral rules?
- A) `model`
- B) `instructions`
- C) `tools`
- D) `metadata`

<details><summary>Answer</summary>**B** — The `instructions` field defines the agent's system instructions/behavior.</details>

**Q35.** How do you deploy an agent created in the VS Code designer?
- A) Select **Create Agent on Microsoft Foundry**
- B) Run `az deploy`
- C) Push to GitHub
- D) Select **Open Playground**

<details><summary>Answer</summary>**A** — Select **Create Agent on Microsoft Foundry** in the designer to deploy.</details>

**Q36.** How do you update a deployed agent's configuration?
- A) Delete and recreate it
- B) **AGENT PREFERENCES** → **Edit Agent** → edit → **Update Agent on Microsoft Foundry**
- C) Edit the model directly
- D) It cannot be updated

<details><summary>Answer</summary>**B** — Edit the agent, then select **Update Agent on Microsoft Foundry**; changes take effect immediately.</details>

**Q37.** What does the **View Code** option in the AGENT PREFERENCES pane do?
- A) Deploys the agent
- B) Generates a sample code file to interact with the agent programmatically
- C) Deletes the agent
- D) Opens the model catalog

<details><summary>Answer</summary>**B** — **View Code** generates boilerplate code for interacting with the deployed agent.</details>

**Q38.** When generating sample code, which selections can you make?
- A) SDK, language, and authentication method
- B) Model and region only
- C) Subscription and resource group only
- D) Container and image only

<details><summary>Answer</summary>**A** — You choose the preferred SDK, language, and authentication method.</details>

**Q39.** Where do you view conversation threads created during agent runs in VS Code?
- A) **Resources** → **Classic** → **Threads**
- B) The model catalog
- C) The container registry
- D) Azure DevOps

<details><summary>Answer</summary>**A** — Threads appear under **Resources** → **Classic** → **Threads**.</details>

**Q40.** What does **View run info** on the THREAD DETAILS pane open?
- A) A YAML file
- B) A `.json` file with agent configuration, messages, and tool calls
- C) The playground
- D) The model catalog

<details><summary>Answer</summary>**B** — It opens a `.json` file with run details including config, messages, and tool calls.</details>

---

## Section 5: Tools, Testing, Deployment & Integration (Q41–50)

**Q41.** Which tool grounds an agent with real-time web information and inline citations?
- A) File Search
- B) Grounding with Bing search
- C) Code Interpreter
- D) OpenAPI tool

<details><summary>Answer</summary>**B** — Grounding with Bing search provides real-time web info with inline citations.</details>

**Q42.** Which tool lets an agent write and run Python code in a sandboxed environment?
- A) File Search
- B) Code Interpreter
- C) Bing Grounding
- D) MCP tool

<details><summary>Answer</summary>**B** — Code Interpreter lets the agent write and run Python code in a sandbox.</details>

**Q43.** Which tool connects an agent to an external API via an OpenAPI spec?
- A) File Search
- B) OpenAPI 3.0 tool
- C) Code Interpreter
- D) Bing Grounding

<details><summary>Answer</summary>**B** — The OpenAPI 3.0 tool connects to external APIs via an OpenAPI spec.</details>

**Q44.** Which tool augments an agent with knowledge from uploaded files?
- A) File Search
- B) Bing Grounding
- C) Code Interpreter
- D) Function calling

<details><summary>Answer</summary>**A** — File Search augments agents with knowledge from uploaded files/proprietary documents.</details>

**Q45.** Which tool connects an agent to tools hosted on an existing MCP endpoint?
- A) OpenAPI tool
- B) MCP tool
- C) Code Interpreter
- D) File Search

<details><summary>Answer</summary>**B** — The MCP tool connects to tools hosted on an existing MCP endpoint.</details>

**Q46.** To ground an agent with data from an existing Azure AI Search index, which tool do you use?
- A) File Search
- B) Azure AI Search
- C) Bing Grounding
- D) Code Interpreter

<details><summary>Answer</summary>**B** — Azure AI Search grounds agents with data from an existing index (chat with your data).</details>

**Q47.** What is the standard Python SDK pattern for consuming a Foundry agent?
- A) `OpenAIClient` with an API key
- B) `AIProjectClient` + `DefaultAzureCredential`
- C) `BlobServiceClient` + connection string
- D) `ComputeClient` + SAS token

<details><summary>Answer</summary>**B** — Use `AIProjectClient` with `DefaultAzureCredential` for keyless auth.</details>

**Q48.** Which authentication approach should you use in production code?
- A) Hardcoded API keys
- B) Keyless auth via `DefaultAzureCredential` (managed identity)
- C) Shared access signatures
- D) Anonymous access

<details><summary>Answer</summary>**B** — Use keyless auth via `DefaultAzureCredential`; never hardcode keys in code.</details>

**Q49.** What does `DefaultAzureCredential` try in order?
- A) Env → CLI → managed identity
- B) CLI → managed identity → env (and other sources)
- C) Managed identity → CLI → env
- D) Keys → tokens → certificates

<details><summary>Answer</summary>**B** — `DefaultAzureCredential` tries CLI, managed identity, env, and other sources in order.</details>

**Q50.** Which SDK packages are the primary ones for agent development in Python?
- A) `azure-ai-projects` and `azure-identity`
- B) `azure-storage-blob` and `azure-keyvault`
- C) `azure-mgmt-compute` and `azure-mgmt-network`
- D) `azure-cognitiveservices` and `azure-mgmt-resource`

<details><summary>Answer</summary>**A** — `azure-ai-projects` (Foundry Projects SDK) and `azure-identity` are the primary agent SDK packages.</details>

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module via MCP*