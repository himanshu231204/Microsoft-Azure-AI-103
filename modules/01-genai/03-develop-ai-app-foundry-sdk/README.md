<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.3: Develop an AI App with the Foundry SDK

</div>

> **Source**: [Microsoft Learn — Develop an AI app with the Microsoft Foundry SDK](https://learn.microsoft.com/training/modules/ai-foundry-sdk/)
> **Learning objectives**: Describe Foundry SDK capabilities, work with project connections, develop a chat app using the SDK

---

## Table of Contents

1. [What is the Microsoft Foundry SDK?](#1-what-is-the-microsoft-foundry-sdk)
2. [Connecting to a Project](#2-connecting-to-a-project)
3. [Working with Project Connections](#3-working-with-project-connections)
4. [Creating a Chat Client](#4-creating-a-chat-client)
5. [SDK Packages and Installation](#5-sdk-packages-and-installation)
6. [Key Takeaways for AI-103](#6-key-takeaways-for-ai-103)

---

## 1. What is the Microsoft Foundry SDK?

The Microsoft Foundry SDK enables developers to write code that uses resources in a Foundry project. With this SDK, you can:

- **Connect to projects** — Establish programmatic access to your Foundry resources
- **Access connections** — Retrieve and use connected services (Azure Storage, AI Search, OpenAI)
- **Consume models** — Send prompts to generative AI models and process responses
- **Manage agents** — Create and interact with AI agents programmatically

> **Exam insight**: The Foundry SDK provides a unified way to access all project resources without managing individual service endpoints separately.

### Core Library: Azure AI Projects

| Package | Language | Install Command |
|---------|----------|-----------------|
| **azure-ai-projects** | Python | `pip install azure-ai-projects` |
| **Azure.AI.Projects** | .NET | NuGet package |
| **@azure/ai-projects** | JavaScript | npm package |

### What You Can Do with the Foundry SDK

| Capability | Description |
|------------|-------------|
| Access Foundry Models | Connect to deployed models including Azure OpenAI |
| Use Foundry Agent Service | Create and interact with AI agents |
| Run batch evaluations | Evaluate model performance at scale |
| Enable app tracing | Monitor and debug AI applications |
| Fine-tune models | Train models on custom data |
| Get endpoints/keys | Retrieve connection details for Foundry Tools |

---

## 2. Connecting to a Project

Every Foundry project has a **unique endpoint** — the entry point for SDK access.

### Project Endpoints

| Endpoint Type | Purpose |
|---------------|---------|
| **Project endpoint** | Access project connections, agents, and models |
| **Azure OpenAI endpoint** | Direct access to OpenAI Service APIs |
| **Foundry Tools endpoint** | Access Vision, Language, and other tool APIs |

### Creating a Project Client (Python)

```python
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

project_endpoint = "https://<resource-name>.services.ai.azure.com/api/projects/<project-name>"
project_client = AIProjectClient(            
    credential=DefaultAzureCredential(),
    endpoint=project_endpoint
)
```

**Key components:**
- `DefaultAzureCredential` — Authenticates using Azure CLI, environment variables, or managed identity
- `AIProjectClient` — The main client object for project interaction

> **Exam insight**: You must be authenticated (via `az login` or managed identity) before the SDK can access your project.

---

## 3. Working with Project Connections

Foundry projects contain **connected resources** — links to external services like Azure Storage, AI Search, or OpenAI.

### Connection Hierarchy

```
Foundry Resource (Hub)
  └── Project(s)
       └── Connections  ← defined at both hub and project levels
            ├── Azure OpenAI
            ├── Azure AI Search
            ├── Azure Storage
            └── Other Foundry Resources
```

### Listing Connections

```python
# List all connections in the project
connections = project_client.connections
for connection in connections.list():
    print(f"{connection.name} ({connection.type})")
```

### Filtering by Connection Type

```python
from azure.ai.projects.models import ConnectionType

# List only Azure OpenAI connections
openai_connections = project_client.connections.list(
    connection_type=ConnectionType.AZURE_OPEN_AI
)
```

### Getting a Specific Connection

```python
# Get connection with credentials
connection = project_client.connections.get(
    connection_name="my-openai-connection",
    include_credentials=True  # Returns API key or token
)
```

> **Exam insight**: Use `include_credentials=True` when you need to authenticate directly to the connected service.

---

## 4. Creating a Chat Client

The SDK simplifies model access by providing an **OpenAI-compatible client** from your project.

### Why Use the Project's OpenAI Client?

| Direct OpenAI SDK | Foundry Project Client |
|-------------------|------------------------|
| Manually manage endpoint URLs | Endpoint auto-resolved from project |
| Configure authentication per service | Uses project-level authentication |
| Switch models requires code changes | Just change the deployment name parameter |
| Works with OpenAI models only | Works with ANY model in the resource (including Phi, Mistral) |

### Complete Chat Example (Python)

```python
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

try:
    # Connect to the project
    project_endpoint = "https://<resource>.services.ai.azure.com/api/projects/<project>"
    project_client = AIProjectClient(            
        credential=DefaultAzureCredential(),
        endpoint=project_endpoint
    )
    
    # Get an OpenAI-compatible chat client
    chat_client = project_client.get_openai_client(api_version="2024-10-21")
    
    # Send a chat completion request
    user_prompt = input("Enter a question:")
    
    response = chat_client.chat.completions.create(
        model="gpt-4",  # Your deployment name
        messages=[
            {"role": "system", "content": "You are a helpful AI assistant."},
            {"role": "user", "content": user_prompt}
        ]
    )
    
    print(response.choices[0].message.content)

except Exception as ex:
    print(ex)
```

### Required Packages

```bash
pip install azure-ai-projects azure-identity openai
```

> **Exam insight**: The `get_openai_client()` method returns a standard OpenAI client — you use the same code patterns as with the OpenAI SDK directly.

---

## 5. SDK Packages and Installation

### Essential Python Packages

| Package | Purpose | Install |
|---------|---------|---------|
| **azure-ai-projects** | Core Foundry SDK | `pip install azure-ai-projects` |
| **azure-identity** | Authentication (DefaultAzureCredential) | `pip install azure-identity` |
| **openai** | OpenAI-compatible API calls | `pip install openai` |

### Authentication Flow

```
1. az login (or managed identity)
        ↓
2. DefaultAzureCredential
        ↓
3. AIProjectClient (authenticated)
        ↓
4. get_openai_client() → OpenAI client with project credentials
```

### Supported Languages

| Language | Package | Status |
|----------|---------|--------|
| Python | azure-ai-projects | ✅ Generally available |
| .NET/C# | Azure.AI.Projects | ✅ Generally available |
| JavaScript | @azure/ai-projects | ✅ Generally available |
| Java | Azure AI Projects | ✅ Generally available |

> **Exam insight**: Python examples are used in the module, but all supported languages have equivalent functionality.

---

## 6. Key Takeaways for AI-103

### Must-Know Facts

1. **Foundry SDK** = `azure-ai-projects` package — the core library for project access
2. **AIProjectClient** = main entry point for all SDK operations
3. **Connections** = linked external resources (Azure services) accessible via the SDK
4. **get_openai_client()** = returns OpenAI-compatible client for model interaction
5. **DefaultAzureCredential** = authentication mechanism (requires `az login` or managed identity)
6. **Model deployment name** = the parameter that selects which model to use

### Code Patterns to Remember

| Task | Code Pattern |
|------|--------------|
| Connect to project | `AIProjectClient(credential, endpoint)` |
| List connections | `project_client.connections.list()` |
| Get connection | `project_client.connections.get(name, include_credentials=True)` |
| Get chat client | `project_client.get_openai_client(api_version)` |
| Chat completion | `chat_client.chat.completions.create(model, messages)` |

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Foundry SDK basics | Module 1.1 (Foundry platform overview) |
| Project connections | Module 1.2 (Model catalog & deployment) |
| Chat client creation | Module 1.4 (Prompt Flow), Module 1.5 (RAG solutions) |
| SDK authentication | Module 2.x (Agent development on Foundry) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-03 · Source: Microsoft Learn module via MCP*
