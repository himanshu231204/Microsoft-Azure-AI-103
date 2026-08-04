<div align="center">

# Module 1.4: Get Started with Prompt Flow
## Practice Questions (50)

</div>

---

### Section 1: Prompt Flow Fundamentals (10 questions)

**1. What is the primary purpose of Prompt Flow in Azure AI Foundry?**

A) To deploy machine learning models
B) To streamline the development cycle of LLM-based AI applications
C) To manage Azure subscriptions
D) To create virtual machines

<details>
<summary>Answer</summary>

**B) To streamline the development cycle of LLM-based AI applications**

Prompt Flow is a development tool designed to simplify prototyping, experimenting, iterating, and deploying AI applications powered by Large Language Models.
</details>

---

**2. Which of the following is NOT a key capability of Prompt Flow?**

A) Orchestrate executable flows with LLMs and Python tools
B) Create prompt variants and compare performance
C) Manage Azure billing and costs
D) Test, debug, and iterate flows easily

<details>
<summary>Answer</summary>

**C) Manage Azure billing and costs**

Prompt Flow focuses on development capabilities (orchestration, testing, variants) but does not manage billing or costs directly.
</details>

---

**3. What does DAG stand for in the context of Prompt Flow visualization?**

A) Data Access Gateway
B) Directed Acyclic Graph
C) Dynamic Application Generator
D) Distributed Application Grid

<details>
<summary>Answer</summary>

**B) Directed Acyclic Graph**

A DAG (Directed Acyclic Graph) is the visual representation of the flow structure, showing connectivity and dependencies between nodes.
</details>

---

**4. In Prompt Flow, what is a "node"?**

A) A virtual machine in Azure
B) A specific tool with unique capabilities in the flow
C) A user account
D) A database table

<details>
<summary>Answer</summary>

**B) A specific tool with unique capabilities in the flow**

Nodes represent individual tools (LLM, Python, Prompt, etc.) that handle data processing, task execution, and algorithmic operations.
</details>

---

**5. What templating language do LLM and Prompt tools use for dynamic prompt generation?**

A) Jinja
B) Mustache
C) Handlebars
D) EJS

<details>
<summary>Answer</summary>

**A) Jinja**

LLM and Prompt tools use Jinja templating with `{{variable}}` syntax to dynamically generate prompts based on inputs.
</details>

---

**6. What is the file that defines the flow structure in Prompt Flow?**

A) `config.json`
B) `flow.dag.yaml`
C) `prompt_flow.py`
D) `settings.yml`

<details>
<summary>Answer</summary>

**B) `flow.dag.yaml`**

The `flow.dag.yaml` file defines the flow structure, including inputs, outputs, nodes, and connections.
</details>

---

**7. Which built-in tool is used to execute custom Python code in a flow?**

A) LLM tool
B) Prompt tool
C) Python tool
D) Serp API tool

<details>
<summary>Answer</summary>

**C) Python tool**

The Python tool allows you to execute custom Python code for data processing and custom logic.
</details>

---

**8. What is the purpose of the Serp API tool in Prompt Flow?**

A) To execute Python code
B) To integrate web search capabilities
C) To manage database connections
D) To handle authentication

<details>
<summary>Answer</summary>

**B) To integrate web search capabilities**

The Serp API tool enables web search integration within your flow for retrieving information from the internet.
</details>

---

**9. How do you reference a flow input within a node?**

A) `$input.<name>`
B) `${input.<name>}`
C) `@input.<name>`
D) `#input.<name>`

<details>
<summary>Answer</summary>

**B) `${input.<name>}`**

Flow inputs are referenced using the `${input.<name>}` syntax, such as `${input.question}`.
</details>

---

**10. What is the purpose of the Content Safety tool in Prompt Flow?**

A) To generate content
B) To filter and ensure content safety
C) To store content in databases
D) To encrypt content

<details>
<summary>Answer</summary>

**B) To filter and ensure content safety**

The Content Safety tool provides content filtering and safety checks to ensure generated content meets safety guidelines.
</details>

---

### Section 2: Flow Types (10 questions)

**11. How many flow types does Prompt Flow offer?**

A) 2
B) 3
C) 4
D) 5

<details>
<summary>Answer</summary>

**B) 3**

Prompt Flow offers three flow types: Standard, Chat, and Evaluation.
</details>

---

**12. Which flow type is designed for general application development?**

A) Chat flow
B) Evaluation flow
C) Standard flow
D) Deployment flow

<details>
<summary>Answer</summary>

**C) Standard flow**

The Standard flow is designed for general application development with flexibility across different domains.
</details>

---

**13. Which flow type is specifically tailored for conversational applications?**

A) Standard flow
B) Chat flow
C) Evaluation flow
D) Batch flow

<details>
<summary>Answer</summary>

**B) Chat flow**

Chat flow is specifically designed for conversational application development with enhanced support for chat inputs/outputs.
</details>

---

**14. What are the three required components in a Chat flow?**

A) Input, Processing, Output
B) Chat input, Chat history, Chat output
C) User message, Bot response, Database
D) Question, Answer, Context

<details>
<summary>Answer</summary>

**B) Chat input, Chat history, Chat output**

Chat flow requires: Chat input (user messages), Chat history (auto-managed record), and Chat output (AI responses).
</details>

---

**15. What is the special characteristic of `chat_history` in Chat flow?**

A) It must be manually configured
B) It is automatically managed by Prompt Flow
C) It is optional
D) It stores only user messages

<details>
<summary>Answer</summary>

**B) It is automatically managed by Prompt Flow**

`chat_history` is automatically stored and managed - you cannot manually set its value.
</details>

---

**16. Which flow type is used to evaluate the performance of previous flow runs?**

A) Standard flow
B) Chat flow
C) Evaluation flow
D) Test flow

<details>
<summary>Answer</summary>

**C) Evaluation flow**

Evaluation flow takes outputs from previous flow runs as inputs to evaluate performance and output metrics.
</details>

---

**17. In a Chat flow, how do you designate an input as the chat input?**

A) By setting a special flag in the YAML
B) By marking it in the Inputs section
C) By naming it "chat_input"
D) It is automatically detected

<details>
<summary>Answer</summary>

**B) By marking it in the Inputs section**

You mark one of the inputs as the Chat input in the Inputs section, then populate it via the Chat box.
</details>

---

**18. Which flow type would you use to compare different model versions?**

A) Standard flow
B) Chat flow
C) Evaluation flow
D) All of the above

<details>
<summary>Answer</summary>

**C) Evaluation flow**

Evaluation flow enables you to assess performance of previous run results and output metrics for comparison.
</details>

---

**19. What is the primary benefit of Chat flow over Standard flow for conversational apps?**

A) Faster execution
B) Enhanced support for chat inputs/outputs and history management
C) Lower cost
D) Better security

<details>
<summary>Answer</summary>

**B) Enhanced support for chat inputs/outputs and history management**

Chat flow provides specialized features for conversational context that Standard flow doesn't have.
</details>

---

**20. Can a Standard flow be used for building a chatbot?**

A) Yes, always
B) No, never
C) Yes, but Chat flow is recommended
D) Only with special configuration

<details>
<summary>Answer</summary>

**C) Yes, but Chat flow is recommended**

While you could build a chatbot with Standard flow, Chat flow provides better support for conversational features.
</details>

---

### Section 3: Connections and Runtimes (10 questions)

**21. What is a "connection" in Prompt Flow?**

A) A network cable
B) A resource linking your flow to external services
C) A database table
D) A user account

<details>
<summary>Answer</summary>

**B) A resource linking your flow to external services**

Connections link your flow to external services like Azure OpenAI, Azure AI Search, etc.
</details>

---

**22. Which of the following is NOT a valid connection type in Prompt Flow?**

A) Azure OpenAI
B) OpenAI
C) AWS S3
D) Azure AI Search

<details>
<summary>Answer</summary>

**C) AWS S3**

Valid connection types include Azure OpenAI, OpenAI, Azure AI Search, and Custom connections, but not AWS S3.
</details>

---

**23. What is a "compute session" in Prompt Flow?**

A) A user login session
B) The computing resources required to run flows
C) A database connection
D) An API key

<details>
<summary>Answer</summary>

**B) The computing resources required to run flows**

A compute session provides the computing resources (including Docker image with dependencies) needed to execute flows.
</details>

---

**24. What is the advantage of compute sessions over compute instances?**

A) They are cheaper
B) They are automatically managed
C) They have more CPU power
D) They support more languages

<details>
<summary>Answer</summary>

**B) They are automatically managed**

Compute sessions automatically manage the lifecycle of sessions and underlying compute, unlike compute instances.
</details>

---

**25. How do you add custom packages to a compute session?**

A) By modifying Azure settings
B) By adding them to `requirements.txt`
C) By calling Azure support
D) By reinstalling the runtime

<details>
<summary>Answer</summary>

**B) By adding them to `requirements.txt`**

Custom packages are added to the `requirements.txt` file in the flow folder, which is installed when the compute session starts.
</details>

---

**26. What should you NOT pin in `requirements.txt` for compute sessions?**

A) Your custom packages
B) `promptflow` and `promptflow-tools` versions
C) Third-party libraries
D) Python version

<details>
<summary>Answer</summary>

**B) `promptflow` and `promptflow-tools` versions**

Don't pin `promptflow` and `promptflow-tools` versions as they're already included in the base image.
</details>

---

**27. What is the idle shutdown timeout for compute sessions when using CLI/SDK?**

A) 15 minutes
B) 30 minutes
C) 1 hour
D) 2 hours

<details>
<summary>Answer</summary>

**C) 1 hour**

The idle shutdown is one hour when using CLI/SDK to submit flow runs.
</details>

---

**28. Where can you create connections in Azure AI Foundry?**

A) Only via CLI
B) Prompt flow → Connections → Create
C) Only via REST API
D) Only via Python SDK

<details>
<summary>Answer</summary>

**B) Prompt flow → Connections → Create**

Connections can be created via Portal UI, REST API, or Python SDK.
</details>

---

**29. What role is required for users to manage compute sessions?**

A) Owner
B) Contributor
C) AzureML Data Scientist
D) Reader

<details>
<summary>Answer</summary>

**C) AzureML Data Scientist**

Users need the AzureML Data Scientist role assigned to the workspace for compute session management.
</details>

---

**30. What is the purpose of the `additional_includes` field in `flow.dag.yaml`?**

A) To add more inputs
B) To reference files outside the flow folder
C) To add more outputs
D) To configure logging

<details>
<summary>Answer</summary>

**B) To reference files outside the flow folder**

The `additional_includes` field lets you reference files like `requirements.txt` from parent folders.
</details>

---

### Section 4: Variants and Monitoring (10 questions)

**31. What is a "variant" in Prompt Flow?**

A) A different flow type
B) A specific version of a tool node with distinct settings
C) A different Azure subscription
D) A type of connection

<details>
<summary>Answer</summary>

**B) A specific version of a tool node with distinct settings**

A variant is a specific version of a tool node (currently only LLM tools) with different settings like prompts or configurations.
</details>

---

**32. Which tool type currently supports variants in Prompt Flow?**

A) Python tool
B) Prompt tool
C) LLM tool
D) All tools

<details>
<summary>Answer</summary>

**C) LLM tool**

Currently, variants are only supported in the LLM tool.
</details>

---

**33. What can you vary in LLM tool variants?**

A) Only the prompt content
B) Only the connection settings
C) Both prompt content and connection settings
D) The flow structure

<details>
<summary>Answer</summary>

**C) Both prompt content and connection settings**

Variants can represent different prompt content or different connection settings (like temperature).
</details>

---

**34. What is the main benefit of using variants?**

A) They make flows run faster
B) They help identify optimal prompt/configuration combinations
C) They reduce Azure costs
D) They simplify deployment

<details>
<summary>Answer</summary>

**B) They help identify optimal prompt/configuration combinations**

Variants enable systematic testing to find the best performing configuration.
</details>

---

**35. How do variants help with prompt engineering?**

A) They eliminate the need for testing
B) They allow tracking and comparing performance of each prompt version
C) They automatically improve prompts
D) They replace manual coding

<details>
<summary>Answer</summary>

**B) They allow tracking and comparing performance of each prompt version**

Variants make it easy to manage prompt tuning history and compare different versions.
</details>

---

**36. What is GenAIOps in the context of Prompt Flow?**

A) A type of flow
B) A template for building LLM apps with best practices
C) A monitoring tool
D) A deployment method

<details>
<summary>Answer</summary>

**B) A template for building LLM apps with best practices**

GenAIOps with Prompt Flow provides templates and guidance for building LLM-infused applications with production best practices.
</details>

---

**37. What feature does GenAIOps provide for comparing flow versions in production?**

A) Blue-green deployment
B) A/B deployment
C) Canary deployment
D) Rolling deployment

<details>
<summary>Answer</summary>

**B) A/B deployment**

GenAIOps implements A/B deployments to compare different flow versions in real-world settings.
</details>

---

**38. What does "centralized code" mean in GenAIOps?**

A) Code is stored on one server
B) Single repository for all flows
C) Code is written by one person
D) Code runs on one machine

<details>
<summary>Answer</summary>

**B) Single repository for all flows**

GenAIOps supports hosting code for multiple prompt flows in a single repository, like a library for flows.
</details>

---

**39. What is the purpose of evaluation flows in the variant testing process?**

A) To deploy flows
B) To assess quality and effectiveness of prompts and flows
C) To create new flows
D) To manage connections

<details>
<summary>Answer</summary>

**B) To assess quality and effectiveness of prompts and flows**

Evaluation flows enable you to assess the quality and effectiveness of your prompts and flows.
</details>

---

**40. What reporting does GenAIOps provide for variant configurations?**

A) No reporting
B) Detailed metrics for each variant configuration
C) Only error logs
D) Only deployment status

<details>
<summary>Answer</summary>

**B) Detailed metrics for each variant configuration**

GenAIOps generates detailed reports with metrics collection, experiments, and variant bulk runs.
</details>

---

### Section 5: Advanced Topics and Best Practices (10 questions)

**41. What is the syntax to reference a node's output in a flow?**

A) `${node.output}`
B) `node.output`
C) `@node.output`
D) `#node.output`

<details>
<summary>Answer</summary>

**A) `${node.output}`**

Node outputs are referenced using `${<node name>.output}` or `${<node name>.output.<field name>}`.
</details>

---

**42. How do you access a specific field from a node's output?**

A) `${node.output.field}`
B) `${node.output.field}`
C) `${node.field.output}`
D) `${field.node.output}`

<details>
<summary>Answer</summary>

**B) `${node.output.field}`**

Use `${<node name>.output.<field name>}` to access specific fields.
</details>

---

**43. What happens when you click "Validate and parse input" in the flow editor?**

A) The flow is deployed
B) The system automatically parses node inputs based on prompts/code
C) The flow is deleted
D) A new node is created

<details>
<summary>Answer</summary>

**B) The system automatically parses node inputs based on prompts/code**

This feature automatically parses node inputs based on prompt templates and Python function inputs.
</details>

---

**44. Can a Chat flow have multiple inputs?**

A) No, only one input is allowed
B) Yes, but only one can be marked as chat input
C) Yes, all can be chat inputs
D) Only if using Standard flow

<details>
<summary>Answer</summary>

**B) Yes, but only one can be marked as chat input**

A chat flow can have multiple inputs, but you mark one as the Chat input in the Inputs section.
</details>

---

**45. What is the purpose of the graph view in the flow editor?**

A) To edit node code
B) To visualize workflow structure only
C) To manage connections
D) To deploy the flow

<details>
<summary>Answer</summary>

**B) To visualize workflow structure only**

The graph view is for visualization only - you cannot edit it directly, but can select nodes to edit in the flatten view.
</details>

---

**46. What is the recommended way to test a Chat flow during development?**

A) Deploy to production
B) Use the Chat box in the authoring page
C) Use CLI commands
D) Wait for user feedback

<details>
<summary>Answer</summary>

**B) Use the Chat box in the authoring page**

You can test Chat flow by selecting "Chat" at the top of the page to open a Chat box for conversation.
</details>

---

**47. What is the purpose of the "flatten" view in Prompt Flow?**

A) To compress files
B) The main working area for authoring flows
C) To flatten the DAG graph
D) To reduce node count

<details>
<summary>Answer</summary>

**B) The main working area for authoring flows**

The Flow or flatten view is the main working area where you author the flow by adding/removing nodes and editing.
</details>

---

**48. How do you switch from compute instance runtime to compute session?**

A) Delete and recreate
B) Modify the runtime settings in the flow
C) Contact Azure support
D) It's not possible

<details>
<summary>Answer</summary>

**B) Modify the runtime settings in the flow**

You can switch by preparing `requirements.txt`, optionally specifying a custom image in `flow.dag.yaml`, and using serverless compute.
</details>

---

**49. What is the status of Prompt Flow as of 2026?**

A) Actively developed with new features
B) Will be retired on April 20, 2027
C) Deprecated immediately
D) Merged into Azure DevOps

<details>
<summary>Answer</summary>

**B) Will be retired on April 20, 2027**

Prompt flow will be retired on April 20, 2027, and is no longer recommended for new development.
</details>

---

**50. What is the recommended alternative to Prompt Flow for new development?**

A) Azure Machine Learning
B) Microsoft Agent Framework
C) Azure DevOps
D) GitHub Actions

<details>
<summary>Answer</summary>

**B) Microsoft Agent Framework**

Microsoft Agent Framework is the recommended alternative for new development after Prompt Flow's retirement.
</details>

---

### Score Tracking

| Section | Questions | Your Score |
|---------|-----------|------------|
| Section 1: Prompt Flow Fundamentals | 1-10 | __ / 10 |
| Section 2: Flow Types | 11-20 | __ / 10 |
| Section 3: Connections and Runtimes | 21-30 | __ / 10 |
| Section 4: Variants and Monitoring | 31-40 | __ / 10 |
| Section 5: Advanced Topics | 41-50 | __ / 10 |
| **Total** | **1-50** | **__ / 50** |

---

*Practice questions created: 2026-08-03 · Based on Microsoft Learn Module 1.4*