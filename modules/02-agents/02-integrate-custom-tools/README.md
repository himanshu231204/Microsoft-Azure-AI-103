<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 2.2: Integrate Custom Tools into Your Agent

</div>

> **Source**: [Microsoft Learn — Integrate custom tools into your agent](https://learn.microsoft.com/training/modules/build-agent-with-custom-tools/)
> **Learning objectives**: Describe the benefits of custom tools, explore the options for custom tools, build an agent that integrates custom tools using the Microsoft Foundry Agent Service

---

## Table of Contents

1. [Why Use Custom Tools](#1-why-use-custom-tools)
2. [Options for Implementing Custom Tools](#2-options-for-implementing-custom-tools)
3. [How to Integrate Custom Tools](#3-how-to-integrate-custom-tools)
4. [Exercise — Build an Agent with Custom Tools](#4-exercise--build-an-agent-with-custom-tools)
5. [Key Takeaways for AI-103](#5-key-takeaways-for-ai-103)

---

## 1. Why Use Custom Tools

**Built-in tools** (web search, code interpreter, file search, function calling) cover common scenarios, but they may not meet every need. **Custom tools** let you extend an agent with your own APIs, services, and business logic.

### The three core benefits (memorize this)

| Benefit | What it means |
|---------|---------------|
| **Enhanced productivity** | Automate repetitive tasks and streamline workflows specific to your use case |
| **Improved accuracy** | Provide precise, consistent outputs and reduce the likelihood of human error |
| **Tailored solutions** | Address specific business needs and optimize processes |

### How an agent uses a custom tool

The agent decides *when* to call a tool based on the user prompt — you don't hard-code the call:

1. A user asks the agent a question (e.g., weather at a ski resort)
2. The agent determines it has a tool that can retrieve the info and calls it
3. The tool returns the result, and the agent informs the user

> **Exam insight**: Custom tools are **declarative** — the agent "figures out" when and how to call a function from its name and parameter descriptions. You don't write code that explicitly invokes the tool.

### Common scenarios

| Scenario | Tool connects to | Agent functionality |
|----------|------------------|---------------------|
| **Customer support** | CRM system | Retrieve order history, process refunds, shipping status |
| **Inventory management** | Inventory system | Check stock, predict restocking, place supplier orders |
| **Healthcare scheduling** | Scheduling tool | Access patient records, suggest slots, send reminders |
| **IT helpdesk** | Ticketing + knowledge base | Troubleshoot, escalate, track ticket status |
| **E-learning / training** | Learning management system (LMS) | Recommend courses, track progress, answer content questions |

> **Exam insight**: Be ready to match a business scenario to the right custom tool approach (e.g., "connect agent to CRM" → function calling or Azure Functions; "call an existing REST API" → OpenAPI tool).

---

## 2. Options for Implementing Custom Tools

Foundry Agent Service offers several custom tool options for scalable interoperability with existing infrastructure and web services.

### Custom tool options (memorize this table)

| Option | Description | Best for |
|--------|-------------|----------|
| **Function calling** | Describe custom function structures to the agent; the agent returns the functions to call + their arguments | Custom logic and workflows in your choice of language |
| **Azure Functions** | Serverless, event-driven functions with triggers and bindings | Event-driven workflows, HTTP/queue-triggered actions |
| **OpenAPI specification tools** | Connect the agent to an external HTTP API via an OpenAPI 3.0 spec | Standardized, automated, scalable API integrations |
| **Azure Logic Apps** | Low-code/no-code workflows connecting apps, data, and services | Visual workflow orchestration without code |

### Key distinctions

- **Function calling** — the agent dynamically identifies and calls functions you define *in code*; your app executes them.
- **Azure Functions** — serverless compute; **triggers** determine when a function executes, **bindings** streamline connections to input/output data sources.
- **OpenAPI tools** — use an **OpenAPI 3.0** specification to describe an HTTP API so the agent can call it.
- **Azure Logic Apps** — low-code/no-code alternative for building workflows.

> **Exam insight**: Know the difference between **function calling** (your code executes the function) and **Azure Functions** (serverless service executes it). Both are tested as distinct options.

---

## 3. How to Integrate Custom Tools

Custom tools can be defined in a handful of ways depending on your scenario — you may already have Azure Functions, or a public OpenAPI spec may give you the functionality you need.

### 3.1 Function calling

Define a function, register it as a `FunctionTool`, and attach it to the agent. The agent calls it dynamically when the prompt requires it.

```python
import json

def recent_snowfall(location: str) -> str:
    """Fetches recent snowfall totals for a given location."""
    mock_snow_data = {"Seattle": "0 inches", "Denver": "2 inches"}
    snow = mock_snow_data.get(location, "Data not available.")
    return json.dumps({"location": location, "snowfall": snow})

# Register the function as a tool for the model
function_tool = FunctionTool(
    name="recent_snowfall",
    parameters={
        "type": "object",
        "properties": {
            "location": {"type": "string", "description": "The city name to check snowfall for."},
        },
        "required": ["location"],
        "additionalProperties": False
    },
    description="Get recent snowfall totals for a given location.",
    strict=True,
)

tools: list[Tool] = [function_tool]

agent = project_client.agents.create_version(
    name="snowfall-agent",
    definition=PromptAgentDefinition(
        model="gpt-4.1",
        instructions="You are a weather assistant tracking snowfall. Use the provided functions to answer questions.",
        tools=tools,
    )
)
```

### 3.2 Azure Functions

Develop and deploy an Azure Function, then add it to the agent as an `AzureFunctionTool` with input/output storage-queue bindings. The agent sends requests to the function via a storage queue and processes the results.

```python
tool = AzureFunctionTool(
    azure_function=AzureFunctionDefinition(
        input_binding=AzureFunctionBinding(
            storage_queue=AzureFunctionStorageQueue(
                queue_name="STORAGE_INPUT_QUEUE_NAME",
                queue_service_endpoint="STORAGE_QUEUE_SERVICE_ENDPOINT",
            )
        ),
        output_binding=AzureFunctionBinding(
            storage_queue=AzureFunctionStorageQueue(
                queue_name="STORAGE_OUTPUT_QUEUE_NAME",
                queue_service_endpoint="STORAGE_QUEUE_SERVICE_ENDPOINT",
            )
        ),
        function=AzureFunctionDefinitionFunction(
            name="queue_trigger",
            description="Get weather for a given location",
            parameters={
                "type": "object",
                "properties": {"location": {"type": "string", "description": "location to determine weather for"}},
            },
        ),
    )
)

agent = project_client.agents.create_version(
    agent_name="MyAgent",
    definition=PromptAgentDefinition(
        model="gpt-4.1",
        instructions="You are a helpful weather assistant. Use the provided Azure Function to get weather information for a location when needed.",
        tools=[tool],
    ),
)
```

### 3.3 OpenAPI specification

Create a JSON file describing the API (OpenAPI 3.0/3.1), then register it as an `OpenApiTool`.

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "get weather data",
    "description": "Retrieves current weather data for a location based on wttr.in.",
    "version": "v1.0.0"
  },
  "servers": [ { "url": "https://wttr.in" } ],
  "auth": [],
  "paths": {
    "/{location}": {
      "get": {
        "description": "Get weather information for a specific location",
        "operationId": "GetCurrentWeather",
        "parameters": [
          { "name": "location", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": {
          "200": { "description": "Successful response" },
          "404": { "description": "Location not found" }
        }
      }
    }
  }
}
```

```python
from azure.ai.projects.models import OpenApiTool, OpenApiAnonymousAuthDetails

with open(weather_asset_file_path, "r") as f:
    openapi_weather = cast(dict[str, Any], jsonref.loads(f.read()))

tool = OpenApiTool(
    openapi=OpenApiFunctionDefinition(
        name="get_weather",
        spec=openapi_weather,
        description="Retrieve weather information for a location.",
        auth=OpenApiAnonymousAuthDetails(),
    )
)

agent = project_client.agents.create_version(
    agent_name="openapi-agent",
    definition=PromptAgentDefinition(
        model="gpt-4.1",
        instructions="You are a weather assistant. Use the API to fetch weather data.",
        tools=[openapi_tool],
    ),
)
```

> **Exam insight**: OpenAPI 3.0 tools currently support **three authentication types**: *anonymous*, *API key*, and *managed identity*. Know these three.

> **Exam insight**: The **declarative** nature is a common point of confusion — the agent decides to call tools based on prompt messages; you provide functions with meaningful names and well-documented parameters and the agent "figures out" when and how to call them.

---

## 4. Exercise — Build an Agent with Custom Tools

**Duration**: ~30 minutes

In this exercise you create an agent **in code** and connect the tool definition to a custom tool function.

### High-level steps
1. Ensure you have an Azure subscription (or sign up for a free account with 30-day credits)
2. Create an agent in code using the Foundry Agent Service SDK
3. Define a custom tool function
4. Connect the tool definition to the custom function
5. Test the agent's ability to call the tool
6. **Clean up** — delete the Azure resources you created after finishing

> **Exam insight**: The exercise reinforces the pattern of defining a function, registering it as a tool, and attaching it to a `PromptAgentDefinition` — the same flow shown in §3.1.

---

## 5. Key Takeaways for AI-103

### Must-Know Facts
1. **Custom tools** extend agents beyond built-in tools with your own APIs, services, and logic
2. **Three benefits**: enhanced productivity, improved accuracy, tailored solutions
3. **Four custom tool options**: function calling, Azure Functions, OpenAPI 3.0 tools, Azure Logic Apps
4. **Function calling** = your code executes the function; **Azure Functions** = serverless service executes it
5. **OpenAPI 3.0 tools** support anonymous, API key, and managed identity auth
6. **Azure Functions** use **triggers** (when to run) and **bindings** (input/output data connections)
7. **Custom tools are declarative** — the agent decides when to call them based on prompt messages
8. **SDK pattern** = `project_client.agents.create_version(...)` with a `PromptAgentDefinition` + `tools` list

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Custom tools (function calling, OpenAPI) | Module 2.1 (agent fundamentals + tool types) |
| Custom tools vs. built-in tools | Module 2.3 (MCP tools — another custom tool mechanism) |
| Function calling / Azure Functions | Module 2.6 (agent-driven workflows) |
| Tool integration patterns | Module 2.7 (Agent Framework), 2.8 (multi-agent orchestration) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*