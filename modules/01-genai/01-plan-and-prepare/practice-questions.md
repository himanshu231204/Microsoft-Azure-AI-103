# Module 1.1 — Practice Questions: Plan and Prepare to Develop AI Solutions on Azure

> **50 questions** covering AI capabilities, Foundry Tools, Microsoft Foundry, Developer Tools & SDKs, and Responsible AI.
> Answers and explanations at the bottom.

---

## Section A — AI Capabilities (Q1–Q15)

**1.** Which of the following best describes generative AI?
- A) Classifies input data into predefined categories
- B) Generates original content such as text, code, or images from prompts
- C) Extracts structured data from documents
- D) Converts speech to text in real time

**2.** A company wants to extract key-value pairs from thousands of scanned invoices. Which AI capability does this fall under?
- A) Natural Language Processing
- B) Computer Vision
- C) Information Extraction
- D) Generative AI

**3.** Which Azure service is used for entity extraction and sentiment analysis from text?
- A) Azure Speech
- B) Azure Language
- C) Azure Vision
- D) Azure Translator

**4.** An AI agent is defined by which three core components?
- A) LLM, instructions, and tools
- B) Model, database, and API
- C) Prompt, response, and memory
- D) Training data, model weights, and inference endpoint

**5.** Which of the following is NOT one of the five core AI capabilities?
- A) Computer Vision
- B) Natural Language Processing
- C) Database Optimization
- D) Information Extraction

**6.** Traditional AI models typically require what that generative AI models do not?
- A) An internet connection
- B) Labeled training data for specific tasks
- C) A cloud deployment
- D) A REST API endpoint

**7.** What distinguishes a generative AI model from a traditional classification model?
- A) Generative AI only works with text
- B) Generative AI produces open-ended, original outputs
- C) Traditional AI requires more compute
- D) Generative AI cannot be fine-tuned

**8.** You need to build a system that translates customer support tickets from French to English in real time. Which Azure service should you use?
- A) Azure Language
- B) Azure Translator
- C) Azure Speech
- D) Azure Document Intelligence

**9.** Which Azure service enables speech-to-text and text-to-speech capabilities?
- A) Azure Speech
- B) Azure Language
- C) Azure Vision
- D) Azure Translator

**10.** A multimodal AI model can process which combination of inputs?
- A) Text only
- B) Text and images
- C) Text, images, audio, and video
- D) Structured data only

**11.** Azure Content Understanding is best suited for which scenario?
- A) Translating documents between languages
- B) Analyzing text sentiment in customer reviews
- C) Extracting structured data from forms, images, video, and audio streams
- D) Converting text to natural-sounding speech

**12.** What is the primary difference between NLP and Computer Vision?
- A) NLP processes images; Vision processes text
- B) NLP processes text; Vision interprets visual data
- C) Both are identical but use different models
- D) NLP requires a larger model

**13.** Which capability would you use to build an app that reads a photograph of a receipt and returns the total amount?
- A) Natural Language Processing
- B) Computer Speech
- C) Information Extraction (Document Intelligence)
- D) Generative AI

**14.** Foundation models used in generative AI are characterized by:
- A) Being task-specific with small training datasets
- B) Being trained on massive datasets and adaptable to many tasks
- C) Only supporting text output
- D) Requiring labeled training data for every new task

**15.** An AI agent can autonomously execute multi-step tasks because it can:
- A) Only generate text responses
- B) Reason over requests and call tools, APIs, and code
- C) Replace all human oversight entirely
- D) Only retrieve information from a database

---

## Section B — Foundry Tools (Q16–Q25)

**16.** Foundry Tools are best described as:
- A) Custom models you build from scratch
- B) Prebuilt, out-of-the-box AI APIs and models you can integrate
- C) Open-source libraries you must host yourself
- D) Database management systems

**17.** Which Foundry Tool would you use to extract key-value pairs from a scanned tax form?
- A) Azure Language
- B) Azure Document Intelligence
- C) Azure Speech
- D) Azure Translator

**18.** Azure Language provides which of the following capabilities?
- A) Text-to-speech and speech-to-text
- B) Entity extraction, sentiment analysis, and summarization
- C) Image classification and object detection
- D) Document OCR and form extraction

**19.** What was the previous name of the Azure AI services that are now called Foundry Tools?
- A) Azure Machine Learning Services
- B) Azure Cognitive Services
- C) Azure Data Factory
- D) Azure DevOps AI

**20.** How do client applications authenticate with Foundry Tools?
- A) OAuth with GitHub
- B) Project key or token-based authentication (Entra ID)
- C) Username and password only
- D) API gateway with static IP whitelisting

**21.** Which Foundry Tool would you use to convert a podcast audio file into a text transcript?
- A) Azure Language
- B) Azure Translator
- C) Azure Speech
- D) Azure Content Understanding

**22.** Which statement about Foundry Tools is TRUE?
- A) They are always more expensive than generative AI
- B) They are more cost-effective and predictable than generative AI for specific tasks
- C) They require custom model training before use
- D) They only work with English language

**23.** You need to analyze customer feedback text and determine whether the sentiment is positive, negative, or neutral. Which Foundry Tool should you use?
- A) Azure Speech
- B) Azure Language
- C) Azure Translator
- D) Azure Document Intelligence

**24.** Azure Content Understanding differs from Azure Document Intelligence because it:
- A) Only processes text documents
- B) Handles multimodal inputs including forms, images, video, and audio streams
- C) Is limited to PDF file processing
- D) Requires custom model training for every use case

**25.** Which Foundry Tool is best for a scenario where you need to provide real-time voice-based customer service in multiple languages?
- A) Azure Language + Azure Translator
- B) Azure Speech + Azure Translator
- C) Azure Document Intelligence + Azure Vision
- D) Azure Content Understanding + Azure Language

---

## Section C — Microsoft Foundry Platform (Q26–Q35)

**26.** In Microsoft Foundry, what is a "Project"?
- A) A billing unit for Azure resources
- B) An organizational unit that manages models, agents, tools, and knowledge
- C) A specific LLM deployment
- D) A container for storing training data

**27.** Which component of Microsoft Foundry provides the underlying compute, storage, and AI tools?
- A) Project
- B) Foundry Resource
- C) Model deployment
- D) Agent

**28.** How many projects can a single Foundry Resource support?
- A) Exactly one
- B) Up to five
- C) Multiple projects
- D) Unlimited projects with no restriction

**29.** What is Foundry IQ?
- A) A model evaluation metric
- B) A central MCP-based knowledge connection for agent context
- C) A billing management tool
- D) A deployment automation service

**30.** The Foundry Portal provides which of the following?
- A) Only a command-line interface
- B) A web-based visual interface to find, deploy, and test models and agents
- C) Only SDK-based interactions
- D) Only CI/CD pipeline management

**31.** Which of the following is TRUE about the Foundry SDK?
- A) It only works with Python
- B) It provides programmatic access for automation and CI/CD pipelines
- C) It replaces the need for Azure subscriptions
- D) It only supports C# development

**32.** A data scientist wants to deploy a model from the Foundry Models catalog. Where can they do this?
- A) Only via Azure CLI
- B) Only via the Foundry portal
- C) Via the Foundry portal, Foundry Toolkit for VS Code, or Foundry SDK
- D) Only via REST API calls

**33.** What is the relationship between a Foundry Resource and a Project?
- A) Projects contain Resources
- B) Resources contain Projects
- C) They are the same thing
- D) Projects and Resources are independent

**34.** In Microsoft Foundry, "Agents" are defined as:
- A) Pre-trained models from the catalog
- B) Named AI configurations combining an LLM, instructions, and tools
- C) Storage containers for model artifacts
- D) Authentication tokens for API access

**35.** Which of the following is NOT a component managed within a Foundry Project?
- A) Models
- B) Agents
- C) Virtual Machine scale sets
- D) Knowledge stores

---

## Section D — Developer Tools & SDKs (Q36–Q40)

**36.** The Foundry Toolkit for VS Code allows developers to:
- A) Only browse model catalog
- B) Browse project resources, deploy models, test agents, and generate integration code
- C) Only write Python scripts
- D) Only manage Azure billing

**37.** Which IDE is best suited for .NET/C# developers working on Azure AI solutions?
- A) Visual Studio Code
- B) Visual Studio
- C) GitHub Copilot
- D) Azure Cloud Shell

**38.** OpenAI SDKs can be used with Foundry models because:
- A) Foundry models are identical to OpenAI models
- B) Foundry provides an OpenAI-compatible endpoint
- C) OpenAI owns the Foundry service
- D) OpenAI SDKs only work with Foundry

**39.** Which programming languages are supported by the Microsoft Foundry SDK?
- A) Python only
- B) C# only
- C) Python, C#, Node.js, TypeScript, Java, and others
- D) JavaScript only

**40.** What is GitHub Copilot's role in AI development on Azure?
- A) It deploys models to production
- B) It provides AI-assisted coding within VS/VS Code
- C) It replaces the need for Foundry SDK
- D) It manages Azure subscriptions

---

## Section E — Responsible AI (Q41–Q50)

**41.** How many Responsible AI principles does Microsoft define?
- A) 4
- B) 5
- C) 6
- D) 8

**42.** A loan approval AI system must not discriminate based on gender or ethnicity. Which Responsible AI principle does this relate to?
- A) Privacy & Security
- B) Fairness
- C) Transparency
- D) Accountability

**43.** Which principle requires that AI systems are understandable and their limitations are disclosed to users?
- A) Fairness
- B) Inclusiveness
- C) Transparency
- D) Accountability

**44.** A medical diagnosis AI system must function reliably under all conditions because failure could endanger lives. This is an example of which principle?
- A) Reliability & Safety
- B) Fairness
- C) Inclusiveness
- D) Privacy & Security

**45.** Which Responsible AI principle addresses the need to protect training data and respect user privacy?
- A) Fairness
- B) Privacy & Security
- C) Accountability
- D) Transparency

**46.** What does the Inclusiveness principle ensure?
- A) AI models are free from bias
- B) AI systems empower everyone and engage all people regardless of ability
- C) AI predictions are explainable
- D) Developers are legally responsible

**47.** Which principle ensures that people remain responsible for AI systems and their outcomes?
- A) Fairness
- B) Reliability & Safety
- C) Transparency
- D) Accountability

**48.** Azure AI Content Safety is used for:
- A) Deploying models to production
- B) Detecting and managing harmful content in text and images
- C) Managing Azure billing
- D) Training custom models

**49.** When evaluating an AI model for fairness, you should:
- A) Only measure overall accuracy
- B) Test for fairness across subgroups, not just overall accuracy
- C) Ignore edge cases
- D) Only test with the training dataset

**50.** Which Azure tool provides prompt injection and jailbreak detection for AI agents?
- A) Azure Monitor
- B) Azure AI Content Safety (risk detection)
- C) Azure Key Vault
- D) Azure Application Insights

---

## Answers & Explanations

### Section A — AI Capabilities

| Q | Answer | Explanation |
|---|--------|-------------|
| 1 | **B** | Generative AI generates original content (text, code, images) from natural language prompts, unlike traditional AI that classifies or predicts. |
| 2 | **C** | Extracting structured data (key-value pairs) from documents falls under Information Extraction, which combines language, vision, and speech processing. |
| 3 | **B** | Azure Language provides entity extraction, sentiment analysis, summarization, and other text analytics capabilities. |
| 4 | **A** | An AI agent combines an LLM (reasoning engine), instructions (scope/role/rules), and tools (APIs, code, databases, search). |
| 5 | **C** | Database Optimization is not an AI capability. The five are: Generative AI/Agents, NLP, Computer Speech, Computer Vision, Information Extraction. |
| 6 | **B** | Traditional AI models typically require labeled training data for specific tasks, while generative AI uses prompt-based, few-shot learning. |
| 7 | **B** | Generative AI produces open-ended, original outputs; traditional AI produces fixed outputs (labels, numbers). |
| 8 | **B** | Azure Translator provides state-of-the-art translation across many languages, suitable for real-time text translation. |
| 9 | **A** | Azure Speech provides text-to-speech, speech-to-text, real-time live speech, and conversational voice apps. |
| 10 | **C** | Multimodal AI models can process text, images, audio, and video — enabling richer understanding and generation. |
| 11 | **C** | Azure Content Understanding handles multimodal analysis — extracting structured data from forms, images, video, and audio streams. |
| 12 | **B** | NLP processes and understands text; Computer Vision interprets images, video, and visual data. |
| 13 | **C** | Reading a receipt photograph and extracting the total is Information Extraction using Document Intelligence. |
| 14 | **B** | Foundation models are trained on massive datasets and are adaptable to many tasks without task-specific retraining. |
| 15 | **B** | Agents can reason, plan, and call tools/APIs to execute multi-step tasks autonomously or semi-autonomously. |

### Section B — Foundry Tools

| Q | Answer | Explanation |
|---|--------|-------------|
| 16 | **B** | Foundry Tools are prebuilt, out-of-the-box AI APIs and models that you can integrate without building custom AI. |
| 17 | **B** | Azure Document Intelligence provides pre-built and custom models for extracting data from invoices, receipts, forms, and tax documents. |
| 18 | **B** | Azure Language provides entity extraction, sentiment analysis, summarization, conversational models, and Q&A capabilities. |
| 19 | **B** | Foundry Tools were previously called "Azure AI Services" and "Azure Cognitive Services" (still reflected in some APIs/SDKs). |
| 20 | **B** | Client apps authenticate using a project key or token-based authentication via Microsoft Entra ID. |
| 21 | **C** | Azure Speech handles speech-to-text conversion, making it suitable for transcribing audio files to text. |
| 22 | **B** | Foundry Tools are more cost-effective and predictable than generative AI for specific, well-defined tasks. |
| 23 | **B** | Azure Language provides sentiment analysis capabilities to classify text as positive, negative, or neutral. |
| 24 | **B** | Azure Content Understanding handles multimodal inputs (forms, images, video, audio), while Document Intelligence focuses on documents. |
| 25 | **B** | Azure Speech (voice I/O) combined with Azure Translator (multi-language) enables real-time voice-based multilingual customer service. |

### Section C — Microsoft Foundry Platform

| Q | Answer | Explanation |
|---|--------|-------------|
| 26 | **B** | A Project is the organizational unit that manages models, agents, tools, knowledge, and connections within a Foundry Resource. |
| 27 | **B** | The Foundry Resource is the Azure resource that provides compute, storage, AI tools, and services. |
| 28 | **C** | A single Foundry Resource supports multiple projects. |
| 29 | **B** | Foundry IQ is the central MCP-based knowledge connection that provides agent context from data stores. |
| 30 | **B** | The Foundry Portal is a web-based visual interface for finding, deploying, testing models and agents, managing resources, and finding endpoints. |
| 31 | **B** | The Foundry SDK provides programmatic access for automation and CI/CD pipelines via scripts or DevOps. |
| 32 | **C** | Models can be deployed via the Foundry portal, Foundry Toolkit for VS Code, or Foundry SDK — multiple options. |
| 33 | **B** | A Foundry Resource contains one or more Projects. Projects are managed within Resources. |
| 34 | **B** | Agents are named AI configurations combining an LLM, instructions, and tools. |
| 35 | **C** | Virtual Machine scale sets are Azure infrastructure, not a component within a Foundry Project. Projects manage Models, Agents, Tools, and Knowledge. |

### Section D — Developer Tools & SDKs

| Q | Answer | Explanation |
|---|--------|-------------|
| 36 | **B** | The Foundry Toolkit for VS Code lets developers browse project resources, deploy models, test agents in playgrounds, and generate integration code. |
| 37 | **B** | Visual Studio is best suited for .NET/C# developers and Windows-focused development. |
| 38 | **B** | Foundry provides an OpenAI-compatible endpoint, so OpenAI SDKs work seamlessly with Foundry model deployments. |
| 39 | **C** | The Foundry SDK supports Python, C#, Node.js, TypeScript, Java, and other languages. |
| 40 | **B** | GitHub Copilot provides AI-assisted coding within VS and VS Code, helping developers write code faster. |

### Section E — Responsible AI

| Q | Answer | Explanation |
|---|--------|-------------|
| 41 | **C** | Microsoft defines 6 Responsible AI principles: Fairness, Reliability & Safety, Privacy & Security, Inclusiveness, Transparency, Accountability. |
| 42 | **B** | Fairness ensures AI systems treat all people fairly without bias based on gender, ethnicity, or other characteristics. |
| 43 | **C** | Transparency requires AI systems to be understandable and disclose limitations, training data usage, and confidence scores. |
| 44 | **A** | Reliability & Safety requires AI systems to perform reliably under all conditions — critical for systems where failure risks lives. |
| 45 | **B** | Privacy & Security addresses protecting training data, respecting user privacy, and securing prediction data. |
| 46 | **B** | Inclusiveness ensures AI empowers everyone and engages all people regardless of ability, gender, or other characteristics. |
| 47 | **D** | Accountability ensures people remain responsible for AI systems — developers must validate models and ensure legal/responsible standards. |
| 48 | **B** | Azure AI Content Safety detects and manages harmful content in both text and images, including violence, hate, sexual content, and self-harm. |
| 49 | **B** | Fairness evaluation requires testing across subgroups, not just overall accuracy, to identify bias against specific populations. |
| 50 | **B** | Azure AI Content Safety provides risk detection including prompt injection and jailbreak detection for AI agents. |

---

## Score Guide

| Score | Rating |
|-------|--------|
| 45–50 | 🏆 Excellent — Ready for the exam |
| 35–44 | 👍 Good — Review weak areas |
| 25–34 | 📚 Fair — Re-read module notes |
| Below 25 | ⚠️ Needs work — Study the module thoroughly |

---

*Generated: 2026-08-02 · Based on Module 1.1 notes from Microsoft Learn*
