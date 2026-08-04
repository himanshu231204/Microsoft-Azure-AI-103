# Module 2.2 — Practice Questions

**Module**: Integrate custom tools into your agent
**Source**: [Microsoft Learn](https://learn.microsoft.com/training/modules/build-agent-with-custom-tools/)

50 practice questions covering the benefits of custom tools, custom tool options (function calling, Azure Functions, OpenAPI, Logic Apps), and how to integrate them with the Microsoft Foundry Agent Service.

---

## Section 1: Why Use Custom Tools (Q1–10)

**Q1.** What are the three core benefits of using custom tools with an agent?
- A) Lower cost, faster training, larger models
- B) Enhanced productivity, improved accuracy, tailored solutions
- C) More storage, better graphics, higher uptime
- D) Simpler code, fewer dependencies, no cloud

<details><summary>Answer</summary>**B** — Custom tools enhance productivity, improve accuracy, and provide tailored solutions for specific business needs.</details>

**Q2.** Which statement best describes how an agent uses a custom tool?
- A) The developer writes code that explicitly calls the tool on every prompt
- B) The agent decides when to call the tool based on the user prompt
- C) The tool is called automatically before any prompt is processed
- D) The agent only uses tools when the model is fine-tuned

<details><summary>Answer</summary>**B** — The agent determines when to call a tool based on the user prompt and its instructions.</details>

**Q3.** In the weather example, what triggers the agent to call the meteorological tool?
- A) A scheduled timer
- B) The user asking about weather conditions
- C) A manual API call from the developer
- D) The tool calling the agent first

<details><summary>Answer</summary>**B** — The user asks about weather; the agent determines it has a tool that can retrieve the info and calls it.</details>

**Q4.** Which benefit of custom tools refers to "reducing the likelihood of human error"?
- A) Enhanced productivity
- B) Improved accuracy
- C) Tailored solutions
- D) Scalability

<details><summary>Answer</summary>**B** — Improved accuracy provides precise, consistent outputs and reduces human error.</details>

**Q5.** A retail company connects its agent to a CRM to retrieve order histories and process refunds. This is an example of which scenario?
- A) Inventory management
- B) Customer support automation
- C) Healthcare scheduling
- D) IT helpdesk support

<details><summary>Answer</summary>**B** — Customer support automation connects the agent to a CRM for order history, refunds, and shipping status.</details>

**Q6.** A manufacturing company links its agent to an inventory system to check stock and place supplier orders. This is an example of which scenario?
- A) Customer support automation
- B) E-learning and training
- C) Inventory management
- D) IT helpdesk support

<details><summary>Answer</summary>**C** — Inventory management lets the agent check stock, predict restocking, and place orders.</details>

**Q7.** Which scenario involves connecting an agent to a learning management system (LMS)?
- A) Healthcare appointment scheduling
- B) E-learning and training
- C) Inventory management
- D) Customer support automation

<details><summary>Answer</summary>**B** — E-learning connects the agent to an LMS to recommend courses, track progress, and answer content questions.</details>

**Q8.** An IT department connects its agent to ticketing and knowledge base systems. This is an example of which scenario?
- A) IT helpdesk support
- B) Healthcare scheduling
- C) Inventory management
- D) E-learning

<details><summary>Answer</summary>**A** — IT helpdesk support lets the agent troubleshoot, escalate, and track ticket statuses.</details>

**Q9.** Which scenario connects an agent to patient records and appointment slots?
- A) Customer support automation
- B) Healthcare appointment scheduling
- C) Inventory management
- D) E-learning and training

<details><summary>Answer</summary>**B** — Healthcare scheduling lets the agent access patient records, suggest slots, and send reminders.</details>

**Q10.** Why might built-in tools not meet all of an agent's needs?
- A) Built-in tools are always slower
- B) Built-in tools may not cover a specific business scenario
- C) Built-in tools cannot be enabled
- D) Built-in tools require custom code to run

<details><summary>Answer</summary>**B** — Built-in tools are useful but may not cover every specific business need, which is why custom tools exist.</details>

---

## Section 2: Options for Implementing Custom Tools (Q11–22)

**Q11.** Which custom tool option lets the agent return the functions that need to be called along with their arguments?
- A) Azure Functions
- B) OpenAPI specification
- C) Function calling
- D) Azure Logic Apps

<details><summary>Answer</summary>**C** — Function calling describes custom functions to the agent and returns which functions to call with their arguments.</details>

**Q12.** Which option provides serverless, event-driven computing with triggers and bindings?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tools
- D) Azure Logic Apps

<details><summary>Answer</summary>**B** — Azure Functions enables intelligent, event-driven applications with triggers and bindings.</details>

**Q13.** Which option connects an agent to an external HTTP API using a standardized specification?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tools
- D) Custom code execution

<details><summary>Answer</summary>**C** — OpenAPI specification tools connect the agent to external APIs using an OpenAPI 3.0 spec.</details>

**Q14.** Which option provides low-code/no-code workflows connecting apps, data, and services?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tools
- D) Azure Logic Apps

<details><summary>Answer</summary>**D** — Azure Logic Apps provides low-code/no-code solutions to add workflows and connect apps, data, and services.</details>

**Q15.** In Azure Functions, what determines *when* a function executes?
- A) Bindings
- B) Triggers
- C) The agent's instructions
- D) The OpenAPI spec

<details><summary>Answer</summary>**B** — Triggers determine when a function executes; bindings connect to input/output data sources.</details>

**Q16.** In Azure Functions, what facilitates streamlined connections to input or output data sources?
- A) Triggers
- B) Bindings
- C) Storage queues
- D) HTTP endpoints

<details><summary>Answer</summary>**B** — Bindings facilitate streamlined connections to input or output data sources.</details>

**Q17.** Which custom tool option is described as integrating "custom logic and workflows, in a selection of programming languages"?
- A) Function calling
- B) Azure Logic Apps
- C) OpenAPI specification tools
- D) Azure Functions

<details><summary>Answer</summary>**A** — Function calling lets agents integrate custom logic and workflows in a selection of programming languages.</details>

**Q18.** Which version of the OpenAPI specification does the Foundry Agent Service use for OpenAPI tools?
- A) OpenAPI 2.0
- B) OpenAPI 3.0
- C) OpenAPI 4.0
- D) Swagger 1.2

<details><summary>Answer</summary>**B** — Foundry Agent Service uses OpenAPI 3.0 specified tools.</details>

**Q19.** Which of the following is NOT one of the custom tool options listed in the module?
- A) Function calling
- B) Azure Functions
- C) Power Automate flows
- D) OpenAPI specification tools

<details><summary>Answer</summary>**C** — The module lists function calling, Azure Functions, OpenAPI specification tools, and Azure Logic Apps (not Power Automate).</details>

**Q20.** Which option is best suited for an event-driven workflow that responds to queue messages?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tools
- D) Azure Logic Apps only

<details><summary>Answer</summary>**B** — Azure Functions is ideal for event-driven workflows, responding to triggers such as HTTP requests or queue messages.</details>

**Q21.** What do OpenAPI specifications describe that helps people understand how an API works?
- A) The database schema
- B) HTTP APIs
- C) The agent's instructions
- D) Cloud resource costs

<details><summary>Answer</summary>**B** — OpenAPI specifications describe HTTP APIs, enabling understanding, client code generation, tests, and design standards.</details>

**Q22.** Which statement correctly distinguishes function calling from Azure Functions?
- A) They are the same thing with different names
- B) Function calling is declarative in code; Azure Functions is a serverless service
- C) Azure Functions runs inside the LLM
- D) Function calling requires an OpenAPI spec

<details><summary>Answer</summary>**B** — Function calling describes functions your app executes; Azure Functions is serverless compute that executes them.</details>

---

## Section 3: How to Integrate Custom Tools (Q23–38)

**Q23.** In the function calling example, what does the `FunctionTool` define?
- A) The model deployment name
- B) The function's name, parameters, and description
- C) The storage queue endpoint
- D) The API server URL

<details><summary>Answer</summary>**B** — `FunctionTool` defines the function's name, parameter schema, and description so the model knows when/how to call it.</details>

**Q24.** In the function calling example, what does the `recent_snowfall` function return?
- A) A Python dict object
- B) A JSON string with snowfall details
- C) An OpenAPI spec
- D) A storage queue message

<details><summary>Answer</summary>**B** — It returns a JSON string like `{"location": ..., "snowfall": ...}` via `json.dumps`.</details>

**Q25.** How is the function tool attached to the agent in the example?
- A) Via the `tools` list in `PromptAgentDefinition`
- B) Via an environment variable
- C) Via a separate REST call
- D) Via the model deployment name

<details><summary>Answer</summary>**A** — The `tools: list[Tool] = [function_tool]` list is passed to `PromptAgentDefinition(tools=tools)`.</details>

**Q26.** What SDK method creates an agent in the module's code examples?
- A) `project_client.agents.create(...)`
- B) `project_client.agents.create_version(...)`
- C) `project_client.agents.deploy(...)`
- D) `project_client.agents.register(...)`

<details><summary>Answer</summary>**B** — `project_client.agents.create_version(...)` creates the agent with a `PromptAgentDefinition`.</details>

**Q27.** In the Azure Functions example, how does the agent communicate with the function?
- A) Direct HTTP call
- B) Via a storage queue (input/output bindings)
- C) Via email
- D) Via a shared database

<details><summary>Answer</summary>**B** — The agent sends requests to the Azure Function via a storage queue and processes results via output binding.</details>

**Q28.** What class wraps an Azure Function as an agent tool?
- A) `FunctionTool`
- B) `AzureFunctionTool`
- C) `OpenApiTool`
- D) `PromptAgentDefinition`

<details><summary>Answer</summary>**B** — `AzureFunctionTool` wraps an `AzureFunctionDefinition` with input/output bindings.</details>

**Q29.** In the OpenAPI example, what three authentication types are supported?
- A) Anonymous, API key, managed identity
- B) Basic, Bearer, OAuth
- C) Anonymous, SAS, certificate
- D) Client secret, password, API key

<details><summary>Answer</summary>**A** — OpenAPI 3.0 tools support anonymous, API key, and managed identity authentication.</details>

**Q30.** Which class registers an OpenAPI-defined tool with the agent?
- A) `FunctionTool`
- B) `AzureFunctionTool`
- C) `OpenApiTool`
- D) `OpenApiAnonymousAuthDetails` alone

<details><summary>Answer</summary>**C** — `OpenApiTool` wraps an `OpenApiFunctionDefinition` containing the spec and auth details.</details>

**Q31.** Why is the OpenAPI JSON loaded with `jsonref.loads()` in the example?
- A) To compress the file
- B) To resolve JSON references ($ref) in the spec
- C) To encrypt the spec
- D) To validate the server URL

<details><summary>Answer</summary>**B** — `jsonref.loads` resolves JSON references so the spec is fully expanded for the tool definition.</details>

**Q32.** What does the `auth` field set to `[]` in the OpenAPI JSON example indicate?
- A) No authentication is required
- B) API key authentication
- C) Managed identity authentication
- D) An error in the spec

<details><summary>Answer</summary>**A** — An empty `auth` array with `OpenApiAnonymousAuthDetails` means anonymous (no auth) access.</details>

**Q33.** What is the declarative nature of custom tools?
- A) You must write code that explicitly calls each tool
- B) You provide function definitions and the agent decides when to call them
- C) Tools require a YAML manifest to run
- D) Tools run only at scheduled times

<details><summary>Answer</summary>**B** — You don't write code that explicitly calls tools; the agent decides based on prompt messages.</details>

**Q34.** Why is it important to give functions meaningful names and well-documented parameters?
- A) For code style only
- B) So the agent can "figure out" when and how to call them
- C) To reduce Azure costs
- D) To pass linters

<details><summary>Answer</summary>**B** — Meaningful names and documented parameters help the agent determine when and how to call a function.</details>

**Q35.** In the function calling example, what does `strict=True` on the `FunctionTool` indicate?
- A) The function is only available to admins
- B) The model must conform to the parameter schema
- C) The function runs in a sandbox
- D) The tool cannot be removed

<details><summary>Answer</summary>**B** — `strict=True` enforces strict schema conformance for the model's tool calls.</details>

**Q36.** Which model deployment is used in the module's code examples?
- A) gpt-4o
- B) gpt-4.1
- C) o3-mini
- D) text-embedding-3

<details><summary>Answer</summary>**B** — The examples use `gpt-4.1` in `PromptAgentDefinition(model="gpt-4.1", ...)`.</details>

**Q37.** What is the purpose of the agent's `instructions` in the tool examples?
- A) They define the OpenAPI spec
- B) They tell the agent how to behave and when to use the provided tools
- C) They set the model temperature
- D) They configure storage bindings

<details><summary>Answer</summary>**B** — Instructions define agent behavior, e.g., "Use the provided functions to answer questions."</details>

**Q38.** Which statement about combining custom tool options is true?
- A) Only one tool option can be used per agent
- B) You can use one option or any combination of them
- C) Function calling and Azure Functions cannot be combined
- D) OpenAPI tools exclude all other tools

<details><summary>Answer</summary>**B** — You can use one of the available custom tool options or any combination of them.</details>

---

## Section 4: Exercise and Application (Q39–50)

**Q39.** What does the module's exercise have you build?
- A) A prompt flow in the Foundry portal
- B) An agent in code with a custom tool function
- C) A Power Automate workflow
- D) A fine-tuned model

<details><summary>Answer</summary>**B** — The exercise has you create an agent in code and connect the tool definition to a custom tool function.</details>

**Q40.** Roughly how long does the exercise take?
- A) 5 minutes
- B) 30 minutes
- C) 2 hours
- D) 1 day

<details><summary>Answer</summary>**B** — The exercise is approximately 30 minutes.</details>

**Q41.** What should you do with Azure resources after completing the exercise?
- A) Keep them for future modules
- B) Delete them to avoid unnecessary costs
- C) Scale them up
- D) Nothing

<details><summary>Answer</summary>**B** — The module recommends deleting the Azure resources you created during the exercise.</details>

**Q42.** Which prerequisite is highly recommended before taking this module?
- A) Experience with the Microsoft Foundry Agent Service
- B) Experience with Azure Logic Apps
- C) Experience with the Azure CLI only
- D) Experience with Docker containers

<details><summary>Answer</summary>**A** — Experience with the Microsoft Foundry Agent Service is highly recommended.</details>

**Q43.** A company needs its agent to call an existing public REST API with an OpenAPI spec available. Which option is the best fit?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tool
- D) Azure Logic Apps

<details><summary>Answer</summary>**C** — An OpenAPI specification tool connects the agent to external HTTP APIs using a standardized spec.</details>

**Q44.** A company needs the agent to run a small piece of custom Python logic defined directly in the agent's code. Which option is the best fit?
- A) Function calling
- B) OpenAPI specification tool
- C) Azure Logic Apps
- D) Web search

<details><summary>Answer</summary>**A** — Function calling lets you define custom functions in code that the agent calls dynamically.</details>

**Q45.** A team wants to integrate the agent with a serverless function that runs when a queue message arrives. Which option fits best?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tool
- D) Azure Logic Apps

<details><summary>Answer</summary>**B** — Azure Functions is ideal for event-driven workflows responding to triggers such as queue messages.</details>

**Q46.** A non-developer wants to build an integration using visual workflows. Which option fits best?
- A) Function calling
- B) Azure Functions
- C) OpenAPI specification tool
- D) Azure Logic Apps

<details><summary>Answer</summary>**D** — Azure Logic Apps provides low-code/no-code solutions to add workflows and connect apps, data, and services.</details>

**Q47.** In the Azure Functions example, what is the name of the deployed function referenced by the tool?
- A) recent_snowfall
- B) queue_trigger
- C) get_weather
- D) process_results

<details><summary>Answer</summary>**B** — The `AzureFunctionDefinitionFunction` has `name="queue_trigger"`.</details>

**Q48.** What does the input binding in the Azure Functions example use?
- A) An HTTP trigger
- B) A storage queue (`STORAGE_INPUT_QUEUE_NAME`)
- C) A timer trigger
- D) A blob trigger

<details><summary>Answer</summary>**B** — The input binding uses `storage_queue` with `queue_name="STORAGE_INPUT_QUEUE_NAME"`.</details>

**Q49.** Which concept do developers often have difficulty with regarding custom tools?
- A) Writing the function code
- B) The declarative nature — the agent decides when to call tools
- C) Choosing a model
- D) Setting up Azure credentials

<details><summary>Answer</summary>**B** — Developers often struggle with the declarative nature: no code explicitly calls the tool; the agent decides.</details>

**Q50.** What is the overall goal of integrating custom tools into an agent?
- A) To replace the LLM
- B) To extend agent capabilities and enable seamless interaction with external systems, real-time processing, and scalable workflows
- C) To reduce the number of tools used
- D) To remove the need for instructions

<details><summary>Answer</summary>**B** — Custom tools create powerful, flexible agents with seamless external integration, real-time processing, and scalable workflows.</details>

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module via MCP*