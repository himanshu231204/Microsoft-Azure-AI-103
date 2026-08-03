# Module 1.3: Develop an AI App with the Foundry SDK — Practice Questions

> 50 practice questions covering Microsoft Foundry SDK, project connections, and chat app development.

---

## Questions

**1.** What is the primary Python package for connecting to a Microsoft Foundry project?

- A) azure-ai-language
- B) azure-ai-projects
- C) azure-ai-openai
- D) azure-foundry-sdk

**2.** Which authentication method does the Foundry SDK use by default in Python?

- A) API Key authentication
- B) OAuth 2.0 client credentials
- C) DefaultAzureCredential
- D) SAS token authentication

**3.** What is the correct way to create an AIProjectClient in Python?

- A) `AIProjectClient(endpoint, credential)`
- B) `AIProjectClient(credential=DefaultAzureCredential(), endpoint=project_endpoint)`
- C) `AIProjectClient.create(endpoint, credential)`
- D) `FoundryClient(endpoint, credential)`

**4.** Which method returns all connections in a Foundry project?

- A) `project_client.connections.get_all()`
- B) `project_client.connections.list()`
- C) `project_client.get_connections()`
- D) `project_client.connections.fetch()`

**5.** How do you get a connection with its credentials?

- A) `connections.get(name)`
- B) `connections.get(name, include_credentials=True)`
- C) `connections.get_with_credentials(name)`
- D) `connections.fetch(name, credentials=True)`

**6.** What does the `get_openai_client()` method return?

- A) A direct Azure OpenAI client
- B) An OpenAI-compatible client authenticated via the project
- C) A Foundry-specific AI client
- D) A REST API client

**7.** Which package must be installed in addition to `azure-ai-projects` for authentication?

- A) azure-auth
- B) azure-identity
- C) azure-security
- D) azure-core

**8.** What is the purpose of the `DefaultAzureCredential` class?

- A) It generates API keys for Azure services
- B) It authenticates using environment variables, Azure CLI, or managed identity
- C) It encrypts data sent to Azure
- D) It manages Azure subscriptions

**9.** Which SDK parameter specifies which model deployment to use in a chat completion?

- A) `deployment_id`
- B) `model`
- C) `model_name`
- D) `deployment_name`

**10.** What is the correct format for a Foundry project endpoint?

- A) `https://<resource>.openai.azure.com`
- B) `https://<resource>.services.ai.azure.com/api/projects/<project>`
- C) `https://<resource>.cognitiveservices.azure.com`
- D) `https://<resource>.azurewebsites.net`

**11.** Which method is used to list connections filtered by type?

- A) `connections.list(connection_type=ConnectionType.AZURE_OPEN_AI)`
- B) `connections.filter(type="AzureOpenAI")`
- C) `connections.get_by_type("AzureOpenAI")`
- D) `connections.search(connection_type="OpenAI")`

**12.** What authentication is required before running Foundry SDK code?

- A) No authentication needed
- B) Azure CLI `az login` or managed identity
- C) Only API keys
- D) Only environment variables

**13.** Which of the following is TRUE about the Foundry SDK's OpenAI client?

- A) It only works with OpenAI models
- B) It works with any model deployed in the Foundry resource
- C) It requires separate authentication for each model
- D) It can only be used in Python

**14.** What is the role of the `api_version` parameter in `get_openai_client()`?

- A) Specifies the Azure region
- B) Sets the OpenAI API version to use
- C) Defines the model version
- D) Sets the SDK version

**15.** Which of the following is NOT a valid connection type in Foundry?

- A) `AZURE_OPEN_AI`
- B) `AZURE_AI_SEARCH`
- C) `AWS_S3`
- D) `AZURE_BLOB_STORAGE`

**16.** What is the purpose of the `connections` property on `AIProjectClient`?

- A) To create new connections
- B) To access and manage resource connections in the project
- C) To delete connections
- D) To authenticate connections

**17.** Which Python package provides OpenAI-compatible chat completion functionality?

- A) azure-openai
- B) openai
- C) azure-ai-chat
- D) foundry-openai

**18.** What does the `chat.completions.create()` method return?

- A) A string response
- B) A response object with choices containing message content
- C) A JSON object
- D) A stream of tokens

**19.** Which of the following is a valid use case for the Foundry SDK?

- A) Only for chat applications
- B) Accessing models, agents, evaluations, and tracing
- C) Only for image generation
- D) Only for text analysis

**20.** What is the correct way to access the model response from a chat completion?

- A) `response.content`
- B) `response.choices[0].message.content`
- C) `response.message`
- D) `response.text`

**21.** Which of the following languages are supported by the Foundry SDK?

- A) Only Python
- B) Python, C#, JavaScript, Java
- C) Only Python and C#
- D) Python and JavaScript only

**22.** What is the purpose of the `system` role in a chat completion message?

- A) To provide user input
- B) To set the assistant's behavior and instructions
- C) To define the model deployment
- D) To specify the API version

**23.** How do you install the Foundry SDK for Python?

- A) `npm install azure-ai-projects`
- B) `pip install azure-ai-projects`
- C) `dotnet add package Azure.AI.Projects`
- D) `cargo install azure-ai-projects`

**24.** What is the benefit of using the project's OpenAI client over a direct OpenAI client?

- A) It's faster
- B) It automatically manages authentication and endpoint resolution
- C) It supports more models
- D) It has lower latency

**25.** Which of the following is required to run Foundry SDK code?

- A) Azure subscription only
- B) Azure CLI login or managed identity + project endpoint
- C) Only a project endpoint
- D) Only API keys

**26.** What is the structure of a Foundry project's resource hierarchy?

- A) Subscription → Resource Group → Project
- B) Foundry Resource (Hub) → Project → Connections
- C) Account → Project → Model
- D) Tenant → Subscription → Resource

**27.** Which method is used to get a specific connection by name?

- A) `connections.get(connection_name)`
- B) `connections.fetch(connection_name)`
- C) `connections.find(connection_name)`
- D) `connections.retrieve(connection_name)`

**28.** What is the default value of the `include_credentials` parameter in `connections.get()`?

- A) False
- B) True
- C) None
- D) It has no default

**29.** Which of the following is a valid message role in a chat completion?

- A) `assistant`
- B) `user`
- C) `system`
- D) All of the above

**30.** What is the purpose of the `Foundry Toolkit for VS Code`?

- A) To replace the Foundry SDK
- B) To simplify Foundry development with visual tools
- C) To only manage Azure resources
- D) To only test models

**31.** Which of the following is TRUE about the Foundry SDK?

- A) It provides programmatic access for automation and CI/CD
- B) It only works in the Foundry portal
- C) It requires a GUI to function
- D) It only supports REST APIs

**32.** How can models be deployed in Azure AI Foundry?

- A) Only via the portal
- B) Via the portal, Foundry Toolkit for VS Code, or Foundry SDK
- C) Only via CLI
- D) Only via SDK

**33.** What is the role of the `messages` parameter in `chat.completions.create()`?

- A) It defines the model to use
- B) It contains the conversation history (system, user, assistant messages)
- C) It specifies the API endpoint
- D) It sets the temperature

**34.** Which of the following is a connection type supported by Foundry?

- A) `AZURE_OPEN_AI`
- B) `AZURE_AI_SEARCH`
- C) `AZURE_BLOB_STORAGE`
- D) All of the above

**35.** What is the purpose of the `connections.list()` method?

- A) To create new connections
- B) To retrieve all connections in the project
- C) To delete connections
- D) To update connections

**36.** Which of the following is required to use the Foundry SDK in Python?

- A) Only `azure-ai-projects`
- B) `azure-ai-projects` + `azure-identity` + `openai`
- C) Only `openai`
- D) Only `azure-identity`

**37.** What is the correct way to handle exceptions in Foundry SDK code?

- A) Use try-except blocks
- B) Ignore errors
- C) Use only print statements
- D) No error handling needed

**38.** Which of the following is a valid way to authenticate to Azure?

- A) Azure CLI `az login`
- B) Managed Identity
- C) Environment variables
- D) All of the above

**39.** What programming languages does the Foundry SDK support?

- A) Python, C#, Node.js, TypeScript, Java
- B) Only Python and C#
- C) Only JavaScript
- D) Python only

**40.** What is the benefit of using `DefaultAzureCredential`?

- A) It's the only authentication method
- B) It automatically tries multiple authentication methods
- C) It's faster than other methods
- D) It doesn't require Azure CLI

**41.** Which method is used to send a chat completion request?

- A) `chat_client.send(message)`
- B) `chat_client.chat.completions.create(model, messages)`
- C) `chat_client.complete(prompt)`
- D) `chat_client.chat(message)`

**42.** What is the purpose of the `model` parameter in `chat.completions.create()`?

- A) It specifies the API version
- B) It identifies the deployed model to use
- C) It defines the message format
- D) It sets the response type

**43.** Which of the following is TRUE about Foundry project connections?

- A) They are only defined at the project level
- B) They can be defined at both hub and project levels
- C) They cannot be filtered by type
- D) They don't include credentials

**44.** What is the correct way to print a connection's name and type?

- A) `print(connection)`
- B) `print(f"{connection.name} ({connection.type})")`
- C) `print(connection.name, connection.type)`
- D) `print(connection.details)`

**45.** Which of the following is a valid use case for the Foundry SDK?

- A) Creating chat applications
- B) Accessing project connections
- C) Running evaluations
- D) All of the above

**46.** What is the purpose of the `get_openai_client()` method?

- A) To create a new OpenAI account
- B) To get an authenticated OpenAI client for model interaction
- C) To deploy new models
- D) To manage connections

**47.** Which of the following is required to access a Foundry project?

- A) Only the project name
- B) Project endpoint + authentication
- C) Only authentication
- D) Only the endpoint

**48.** What is the correct way to install the `azure-identity` package?

- A) `pip install azure-auth`
- B) `pip install azure-identity`
- C) `pip install azure-security`
- D) `pip install azure-core`

**49.** Which of the following is TRUE about the Foundry SDK?

- A) It only works with OpenAI models
- B) It works with any model in the Foundry resource
- C) It requires a specific model version
- D) It only supports chat models

**50.** What is the purpose of the `try-except` block in the chat example?

- A) To catch and handle authentication errors
- B) To catch and handle any exceptions during SDK operations
- C) To retry failed requests
- D) To log all operations

---

## Answer Key

| Q | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | `azure-ai-projects` is the core Python package for connecting to Foundry projects. |
| 2 | **C** | `DefaultAzureCredential` is the default authentication method, supporting Azure CLI, managed identity, and environment variables. |
| 3 | **B** | The correct syntax uses keyword arguments: `AIProjectClient(credential=DefaultAzureCredential(), endpoint=project_endpoint)`. |
| 4 | **B** | `connections.list()` returns a collection of all connection objects in the project. |
| 5 | **B** | Set `include_credentials=True` to retrieve the connection with its authentication credentials. |
| 6 | **B** | `get_openai_client()` returns an OpenAI-compatible client that is already authenticated via the project. |
| 7 | **B** | `azure-identity` provides `DefaultAzureCredential` for authentication. |
| 8 | **B** | `DefaultAzureCredential` tries multiple authentication methods: Azure CLI, environment variables, managed identity, etc. |
| 9 | **B** | The `model` parameter specifies which deployed model to use for the chat completion. |
| 10 | **B** | Foundry project endpoints follow the format: `https://<resource>.services.ai.azure.com/api/projects/<project>`. |
| 11 | **A** | Use `connections.list(connection_type=ConnectionType.AZURE_OPEN_AI)` to filter by connection type. |
| 12 | **B** | You must be authenticated via `az login` or managed identity before the SDK can access your project. |
| 13 | **B** | The OpenAI client works with any model deployed in the Foundry resource, including non-OpenAI models. |
| 14 | **B** | `api_version` specifies which OpenAI API version to use for the client. |
| 15 | **C** | AWS_S3 is not a supported connection type in Azure Foundry. |
| 16 | **B** | The `connections` property provides access to manage and retrieve resource connections. |
| 17 | **B** | The `openai` package provides OpenAI-compatible functionality used with the Foundry SDK. |
| 18 | **B** | The response object contains `choices` with message content accessible via `response.choices[0].message.content`. |
| 19 | **B** | The Foundry SDK supports accessing models, agents, evaluations, tracing, and more. |
| 20 | **B** | Access the response content via `response.choices[0].message.content`. |
| 21 | **B** | The Foundry SDK supports Python, C#, JavaScript, TypeScript, and Java. |
| 22 | **B** | The `system` role sets the assistant's behavior and instructions for the conversation. |
| 23 | **B** | Use `pip install azure-ai-projects` to install the Python package. |
| 24 | **B** | The project's OpenAI client automatically manages authentication and endpoint resolution. |
| 25 | **B** | You need Azure CLI login (or managed identity) plus the project endpoint. |
| 26 | **B** | The hierarchy is: Foundry Resource (Hub) → Project → Connections. |
| 27 | **A** | Use `connections.get(connection_name)` to retrieve a specific connection. |
| 28 | **B** | The default value is `True`, so credentials are included by default. |
| 29 | **D** | Valid roles are `system`, `user`, and `assistant`. |
| 30 | **B** | The Foundry Toolkit for VS Code simplifies development with visual tools and integrated testing. |
| 31 | **A** | The Foundry SDK provides programmatic access for automation and CI/CD pipelines. |
| 32 | **B** | Models can be deployed via the portal, Foundry Toolkit for VS Code, or the SDK. |
| 33 | **B** | The `messages` parameter contains the conversation history with role/content pairs. |
| 34 | **D** | All three are valid connection types in Azure Foundry. |
| 35 | **B** | `connections.list()` retrieves all connections in the project. |
| 36 | **B** | You need all three packages: `azure-ai-projects`, `azure-identity`, and `openai`. |
| 37 | **A** | Use try-except blocks to catch and handle exceptions in SDK code. |
| 38 | **D** | All three methods are valid ways to authenticate to Azure. |
| 39 | **A** | The SDK supports Python, C#, Node.js, TypeScript, and Java. |
| 40 | **B** | `DefaultAzureCredential` automatically tries multiple authentication methods. |
| 41 | **B** | Use `chat_client.chat.completions.create(model, messages)` to send a chat completion request. |
| 42 | **B** | The `model` parameter identifies which deployed model to use. |
| 43 | **B** | Connections can be defined at both the hub and project levels. |
| 44 | **B** | Use an f-string to print the connection name and type. |
| 45 | **D** | The Foundry SDK supports all three use cases and more. |
| 46 | **B** | `get_openai_client()` returns an authenticated OpenAI client for model interaction. |
| 47 | **B** | You need both the project endpoint and authentication to access a Foundry project. |
| 48 | **B** | Use `pip install azure-identity` to install the package. |
| 49 | **B** | The Foundry SDK works with any model in the Foundry resource. |
| 50 | **B** | The try-except block catches and handles any exceptions during SDK operations. |

---

*Questions created: 2026-08-03 · Based on Microsoft Learn Module 1.3*
