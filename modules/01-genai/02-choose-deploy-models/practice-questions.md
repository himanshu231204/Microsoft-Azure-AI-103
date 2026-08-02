# Module 1.2 — Practice Questions

> **50 questions** covering the model catalog, deployment, optimization, and responsible AI for Module 1.2.

---

## Section 1: Model Catalog Basics (Q1–15)

**Q1.** What is the primary purpose of the model catalog in Microsoft Foundry?
- A) To train custom models from scratch
- B) To browse, compare, filter, and deploy foundation models
- C) To manage Azure subscriptions and billing
- D) To deploy containerized applications

**Q2.** Which of the following is a category of models available in the Foundry model catalog?
- A) Models sold by Azure
- B) Models from partners and community
- C) Both A and B
- D) Neither A nor B

**Q3.** Which of these models is "sold by Azure" (Azure OpenAI family)?
- A) Llama 4 Scout
- B) Mistral Large
- C) GPT-4o
- D) DeepSeek-R1

**Q4.** How can you filter the model catalog? (Select all that apply)
- A) By Collection (provider/vendor)
- B) By Task (text generation, embeddings, etc.)
- C) By Modality (text, image, audio)
- D) All of the above

**Q5.** What does a model card in the catalog display?
- A) License, modality, supported tasks, deployment templates
- B) Only the model name
- C) Only pricing information
- D) Only the deployment button

**Q6.** Where do you access the model catalog in Foundry?
- A) Build → Models (or Discover → Models)
- B) Settings → Models
- C) Home → Storage
- D) Monitor → Models

**Q7.** What is the difference between "sold by Azure" models and "partner" models?
- A) Sold by Azure models have Microsoft support + enterprise SLA; partner models have provider support
- B) There is no difference
- C) Partner models are free; Azure models are paid
- D) Sold by Azure models can only be deployed to managed compute

**Q8.** Which provider offers the Llama model family in the catalog?
- A) Microsoft
- B) Meta
- C) Google
- D) Amazon

**Q9.** What is a "deployment template" in the context of managed compute?
- A) A pre-configured setup that defines runtime, accelerator family/count, and context length
- B) A Docker container image
- C) A Python script for model training
- D) A pricing calculator

**Q10.** You want to find all embedding models in the catalog. Which filter should you use?
- A) Collection → Azure
- B) Task → Embeddings
- C) Modality → Image
- D) Deployment → Serverless

**Q11.** Which of these is a text embedding model available in the catalog?
- A) DALL·E 3
- B) Whisper
- C) text-embedding-3-large
- GPT-4o-mini

**Q12.** The model catalog allows you to:
- A) Request a model not currently in the catalog
- B) Only use pre-approved models
- C) Deploy models without any selection
- D) None of the above

**Q13.** What is the "New Foundry" toggle in the portal?
- A) A switch between the new and classic Foundry UI
- B) A button to create a new project
- C) A billing toggle
- D) A feature flag for beta models

**Q14.** Which model family is best suited for image generation?
- A) GPT-4o
- B) Phi-4
- C) DALL·E 3
- D) text-embedding-3-small

**Q15.** What information is required when deploying a model via SDK/REST (not portal)?
- A) Model ID, Deployment Template ID, Accelerator type
- B) Only the model name
- C) Only the Azure subscription ID
- D) Only the deployment name

---

## Section 2: Deployment Options (Q16–25)

**Q16.** What are the two main deployment types in Foundry?
- A) Serverless API and Managed Compute
- B) Container Apps and App Service
- C) VM and Kubernetes
- D) Functions and Logic Apps

**Q17.** Which deployment type requires NO infrastructure management?
- A) Serverless API
- B) Managed Compute
- C) Container Apps
- D) Virtual Machines

**Q18.** In a serverless API deployment, how are you billed?
- A) Per inference call (token-based)
- B) Per hour (VM-based)
- C) Per GB of storage
- D) Per network request

**Q19.** What is a "Provisioned Throughput (PTU)" deployment type?
- A) Guaranteed throughput for enterprise SLAs
- B) A free tier for testing
- C) A managed compute option
- D) A deprecated deployment type

**Q20.** When deploying to managed compute, what does the "capacity" value control?
- A) Number of model instances (each instance uses the accelerator count from the template)
- B) Maximum token limit
- C) Number of concurrent users
- D) Storage allocation

**Q21.** What happens with the shared quota managed compute endpoint?
- A) It is deleted after 168 hours (7 days)
- B) It runs indefinitely
- C) It is migrated to serverless after 24 hours
- D) It is paused after 48 hours

**Q22.** What is the deployment name used for?
- A) It's the `model` parameter in your API calls to route requests
- B) It's the display name in the portal only
- C) It's the Azure resource group name
- D) It's the storage account name

**Q23.** Which deployment type has the lowest latency?
- A) Global Standard (serverless)
- B) Managed Compute
- C) Standard (serverless)
- D) They all have the same latency

**Q24.** For a partner model deployment, what must you accept before deploying?
- A) Azure Marketplace terms of use
- B) Microsoft Privacy Policy
- C) Azure SLA agreement
- D) Nothing — it's automatic

**Q25.** How long does a managed compute deployment typically take to provision?
- A) 10–15 minutes
- B) 1–2 seconds
- C) 1–2 hours
- D) 24 hours

---

## Section 3: Model Selection & Optimization (Q26–40)

**Q26.** You need a cost-effective model for a high-volume FAQ chatbot. Which should you choose?
- A) GPT-4o
- B) GPT-4o-mini
- C) o3
- D) DALL·E 3

**Q27.** What does the "temperature" parameter control?
- A) Randomness/creativity of the output (0 = deterministic, higher = more random)
- B) Maximum response length
- C) Number of API calls
- D) Model deployment region

**Q28.** Which temperature setting is best for factual, consistent responses?
- A) 0.0
- B) 1.5
- C) 2.0
- D) Any temperature works equally

**Q29.** What is the "top-p" parameter?
- A) Controls diversity of token sampling (nucleus sampling)
- B) Sets the maximum number of tokens
- C) Defines the system message
- D) Configures the deployment region

**Q30.** Which parameter limits the maximum length of the model's response?
- A) Max tokens
- B) Temperature
- C) Top-p
- D) Stop sequences

**Q31.** What are "stop sequences"?
- A) Strings that tell the model to stop generating when encountered
- B) API keys for authentication
- C) Deployment region identifiers
- D) Model version numbers

**Q32.** You want the model to always produce the same output for the same input. What should you set?
- A) Temperature = 0
- B) Temperature = 2.0
- C) Max tokens = 4096
- D) Top-p = 0.5

**Q33.** What is "few-shot learning" in prompt engineering?
- A) Providing a few input/output examples in the prompt
- B) Training the model on a small dataset
- C) Deploying a model with minimal configuration
- D) Using only one API call

**Q34.** What is chain-of-thought prompting?
- A) Asking the model to "think step by step" before answering
- B) Chaining multiple API calls together
- C) Using multiple models in sequence
- D) Storing conversation history in a database

**Q35.** RAG stands for:
- A) Retrieval-Augmented Generation
- B) Random Access Generation
- C) Real-time AI Gateway
- D) Remote Agent Group

**Q36.** How does RAG reduce hallucination?
- A) By grounding the model's responses in retrieved documents from your own data
- B) By increasing the temperature
- C) By using a larger model
- D) By disabling content filtering

**Q37.** Which evaluation metric measures whether the model's response is grounded in the source data?
- A) Groundedness
- B) Coherence
- C) Fluency
- D) Relevance

**Q38.** What is fine-tuning used for?
- A) Training the model on your specific data for consistent behavior
- B) Changing the model's deployment region
- C) Adjusting the VM SKU
- D) Managing Azure billing

**Q39.** Which fine-tuning approach uses reinforcement learning with human feedback?
- A) DPO (Direct Preference Optimization)
- B) SFT (Supervised Fine-Tuning)
- C) Both A and B
- D) Neither A nor B

**Q40.** When should you use fine-tuning instead of prompt engineering?
- A) When prompt engineering + RAG aren't enough to achieve consistent behavior
- B) Always — fine-tuning is always better
- C) Only for image generation models
- D) Never — prompt engineering is always sufficient

---

## Section 4: Testing & Playground (Q41–45)

**Q41.** Where do you test your deployed model interactively in Foundry?
- A) Playground
- B) Azure Portal
- C) Visual Studio Code
- D) GitHub

**Q42.** What can you do in the Foundry Playground?
- A) Send messages, adjust parameters (temperature, max tokens), compare models
- B) Only view the model card
- C) Only manage billing
- D) Only deploy new models

**Q43.** What does "frequency penalty" do?
- A) Reduces repetition of common tokens
- B) Increases response length
- C) Changes the model's personality
- D) Adds new training data

**Q44.** What does "presence penalty" do?
- A) Encourages the model to introduce new topics
- B) Limits the number of API calls
- C) Changes the deployment type
- D) Disables content filtering

**Q45.** You want to compare two model versions side-by-side. What feature should you use?
- A) Playground comparison mode
- B) Azure Monitor
- C) Cost Management
- D) Resource Groups

---

## Section 5: Responsible AI & Content Filtering (Q46–50)

**Q46.** Content filtering in Foundry detects harmful content across which categories?
- A) Hate, Self-Harm, Sexual, Violence
- B) Spam, Phishing, Malware, Ransomware
- C) Low, Medium, High, Critical
- D) Input, Output, Process, Storage

**Q47.** Is content filtering enabled by default for new deployments?
- A) Yes — it's on by default
- B) No — you must enable it manually
- C) Only for serverless deployments
- D) Only for Azure OpenAI models

**Q48.** What is "prompt injection"?
- A) An attack where malicious instructions are embedded in user input to manipulate model behavior
- B) A way to improve model performance
- C) A deployment configuration
- D) A billing optimization

**Q49.** What are "Prompt Shields"?
- A) A feature that detects prompt injection attempts
- B) A firewall for Azure resources
- C) A deployment template
- D) A model variant

**Q50.** What is "indirect prompt injection"?
- A) Malicious instructions embedded in images or files the model processes
- B) A type of serverless deployment
- C) A model optimization technique
- D) A content filtering category

---

## Answer Key

| Q | Answer | Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|--------|---|--------|---|--------|---|--------|---|--------|
| 1 | B | 11 | C | 21 | A | 31 | A | 41 | A |
| 2 | C | 12 | A | 22 | A | 32 | A | 42 | A |
| 3 | C | 13 | A | 23 | A | 33 | A | 43 | A |
| 4 | D | 14 | C | 24 | A | 34 | A | 44 | A |
| 5 | A | 15 | A | 25 | A | 35 | A | 45 | A |
| 6 | A | 16 | A | 26 | B | 36 | A | 46 | A |
| 7 | A | 17 | A | 27 | A | 37 | A | 47 | A |
| 8 | B | 18 | A | 28 | A | 38 | A | 48 | A |
| 9 | A | 19 | A | 29 | A | 39 | A | 49 | A |
| 10 | B | 20 | A | 30 | A | 40 | A | 50 | A |

---

## Explanations

**Q1 (B):** The model catalog lets you browse, compare, filter, and deploy models — not train them.

**Q3 (C):** GPT-4o is an Azure OpenAI model ("sold by Azure"). Llama, Mistral, DeepSeek are partner models.

**Q7 (A):** "Sold by Azure" = Microsoft support + enterprise SLA. Partner models = provider support, varying SLAs.

**Q15 (A):** SDK/REST deployment requires Model ID, Deployment Template ID, and Accelerator type — the portal wizard provides these values.

**Q18 (A):** Serverless = pay per inference call (token-based). Managed compute = pay per VM hour.

**Q20 (A):** Capacity = number of model instances. Each instance uses the accelerator count from the template (e.g., 1 template = 1 H100).

**Q22 (A):** The deployment name becomes the `model` parameter in API calls — pick a stable, application-friendly name.

**Q27 (A):** Temperature controls randomness. 0 = deterministic, 1+ = more creative. It does NOT affect max tokens or API calls.

**Q32 (A):** Temperature = 0 ensures the model always picks the most probable token = same output for same input.

**Q35 (A):** RAG = Retrieval-Augmented Generation. Retrieve relevant docs → pass as context → model generates grounded answers.

**Q40 (A):** Fine-tuning is used when prompt engineering + RAG can't achieve consistent behavior. It's not always better — it adds complexity and cost.

**Q47 (A):** Content filtering is ON by default for all new deployments. You can customize it but should never disable it.

**Q48 (A):** Prompt injection = malicious instructions in user input that trick the model into ignoring its system prompt.

**Q50 (A):** Indirect prompt injection = malicious text embedded in images or documents the model processes, triggering unintended behavior.
