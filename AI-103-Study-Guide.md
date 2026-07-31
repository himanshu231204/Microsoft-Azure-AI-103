# Study guide for Exam AI-103: Developing AI Apps and Agents on Azure

## Purpose of this document

This study guide should help you understand what to expect on the exam and includes a summary of the topics the exam might cover and links to additional resources. The information and materials in this document should help you focus your studies as you prepare for the exam.

| Useful links | Description |
| --- | --- |
| How to earn the certification | Some certifications only require passing one exam, while others require passing multiple exams. |
| [Certification renewal](https://learn.microsoft.com/en-us/credentials/certifications/renew-your-microsoft-certification) | Microsoft associate, expert, and specialty certifications expire annually. You can renew by passing a **free** online assessment on Microsoft Learn. |
| [Your Microsoft Learn profile](https://learn.microsoft.com/en-us/users/) | Connecting your certification profile to Microsoft Learn allows you to schedule and renew exams and share and print certificates. |
| [Exam scoring and score reports](https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports) | A score of 700 or greater is required to pass. |
| [Exam sandbox](https://aka.ms/examdemo) | You can explore the exam environment by visiting our exam sandbox. |
| [Request accommodations](https://learn.microsoft.com/en-us/credentials/certifications/request-accommodations) | If you use assistive devices, require extra time, or need modification to any part of the exam experience, you can request an accommodation. |

## Updates to the exam

Our exams are updated periodically to reflect skills that are required to perform a role. We have included two versions of the Skills Measured objectives depending on when you are taking the exam.

We always update the English language version of the exam first. Some exams are localized into other languages, and those are updated approximately eight weeks after the English version is updated. While Microsoft makes every effort to update localized exams as noted, there may be times when the localized versions of an exam are not updated on this schedule. Other available languages are listed in the **Schedule Exam** section of the **Exam Details** webpage. If the exam isn't available in your preferred language, you can request an additional 30 minutes to complete the exam.

> **Note:** The bullets that follow each of the skills measured are intended to illustrate how we are assessing that skill. Related topics may be covered in the exam.

> **Note:** Most questions cover features that are general availability (GA). The exam may contain questions on Preview features if those features are commonly used.

## Skills measured as of April 16, 2026

### Audience profile

As a candidate for this Microsoft Certification, you're an Azure AI engineer who builds, manages, and deploys agents and AI solutions that take advantage of Microsoft Foundry.

For this exam, you should have experience developing apps by using Python, and you need to be familiar with the capabilities of general AI, generative AI, and Azure services.

Your responsibilities include:

- Planning and managing Azure AI solutions.
- Implementing generative AI and agentic solutions.
- Implementing computer vision solutions.
- Implementing text analysis solutions.
- Implementing information extraction solutions.

In this role, you collaborate with business stakeholders, solution architects, data scientists, DevOps engineers, and cloud security engineers to design, implement, and maintain AI solutions.

### Skills at a glance

- Plan and manage an Azure AI solution (25–30%)
- Implement generative AI and agentic solutions (30–35%)
- Implement computer vision solutions (10–15%)
- Implement text analysis solutions (10–15%)
- Implement information extraction solutions (10–15%)

---

### Plan and manage an Azure AI solution (25–30%)

#### Choose the appropriate Foundry services for generative AI and agents

- Choose an appropriate model for each task, including large language models (LLMs), small language models, multimodal models, and Foundry Tools
- Choose the appropriate Foundry services for generative tasks, grounding, vector search, agent workflows, or multimodal processing
- Choose an appropriate method for retrieval and indexing
- Choose appropriate memory, tool, and knowledge integration services for agent solutions

#### Set up AI solutions in Foundry

- Design Azure infrastructure for AI apps and agent-based solutions
- Choose appropriate deployment options
- Configure model and agent deployments
- Integrate Foundry projects with continuous integration and continuous deployment (CI/CD) pipelines

#### Manage, monitor, and secure AI systems

- Manage quotas, scaling, rate limits, and cost footprints for model and agent workloads
- Monitor model performance, drift, safety events, and grounding quality
- Monitor data ingestion quality, search index health, and relevance performance
- Configure security, including managed identity, private networking, keyless credentials, and role policies

#### Implement responsible AI across generative AI and agentic systems

- Configure safety filters, guardrails, risk detection, and content moderation
- Apply responsible AI instrumentation, including evaluators, safety evaluations, and explanation tooling
- Implement auditing through trace logging, provenance metadata, and approval workflows
- Govern agent behavior with oversight modes, constraints, and tool-access controls

---

### Implement generative AI and agentic solutions (30–35%)

#### Build generative applications by using Foundry

- Deploy and consume LLMs, small models, code models, and multimodal models
- Implement retrieval-augmented generation (RAG) in an application
- Design workflows, tool-augmented flows, and multistep reasoning pipelines
- Evaluate models and apps, including detecting fabrications, relevance, quality, and safety
- Integrate generative workflows into applications by using Foundry SDKs and connectors
- Configure an application to connect to a Foundry project

#### Build agents by using Foundry

- Define agent roles, goals, conversation-tracking approach, and tool schemas
- Build agents that integrate retrieval, function-calling, and conversation memory
- Integrate agent tools, including APIs, knowledge stores, search, content understanding, and custom functions
- Implement orchestrated multi-agent solutions
- Build autonomous or semiautonomous workflows with safeguards and approval flow controls
- Integrate monitoring into deployed agents, evaluate agent behavior, and perform error analysis

#### Optimize and operationalize generative AI systems

- Tune generation behavior, such as prompt engineering and adjusting model parameters
- Implement model reflection, chain-of-thought evaluations, and self-critique loops
- Set up observability by implementing tracing, token analytics, safety signals, and latency breakdowns
- Orchestrate multiple models, flows, or hybrid LLM and rules engines

---

### Implement computer vision solutions (10–15%)

#### Design and implement image- and video-generation solutions

- Implement a solution that generates images from text prompts and reference media
- Implement a solution that generates videos from text prompts and reference media
- Configure image-editing workflows, including inpainting, mask-based edits, and prompt-driven modifications
- Implement workflows to edit generated videos
- Select and apply appropriate generation and editing controls provided by the platform

#### Design and implement multimodal understanding workflows

- Build a solution that analyzes visual context by using multimodal models
- Configure apps to produce concise or detailed captions for single or multiple images
- Implement a solution that enables question-answering grounded in visual evidence
- Configure generation of alt-text and extended image descriptions aligned to accessibility guidelines
- Implement visual understanding by configuring Azure Content Understanding in Foundry Tools to extract visual characteristics
- Implement video analysis workflows to process and interpret video segments
- Configure single-task and pro-mode Content Understanding pipelines
- Implement solutions that identify objects, components, or regions within images or video

#### Implement responsible AI for multimodal content

- Implement filters to classify unsafe or disallowed visual content
- Detect and mitigate indirect prompt injection by using embedded text in images
- Enforce visual policy rules, such as applying watermarks, flagging prohibited symbols, upholding brand usage requirements, and detecting potentially inappropriate content

---

### Implement text analysis solutions (10–15%)

#### Apply language model text analysis

- Implement solutions to extract entities, topics, summaries, and structured JSON outputs by using generative prompting and Foundry Tools
- Configure detection of sentiment, tone, safety issues, and sensitive content
- Build solutions that translate text by using Azure Translator in Foundry Tools or LLM-powered translation flows
- Customize language model outputs for domain tasks, such as compliance summarization and domain extraction

#### Implement speech solutions

- Implement workflows to convert speech to text and text to speech for agentic interactions
- Integrate speech as an agent modality, including custom speech models
- Enable multimodal reasoning from audio inputs
- Translate speech into other languages by using language models and Foundry Tools

---

### Implement information extraction solutions (10–15%)

#### Build retrieval and grounding pipelines

- Ingest and index content, such as documents, images, audio, and video
- Configure semantic search, hybrid search, and vector search for grounding
- Implement enrichment by using custom or built-in skills for text, images, and layout
- Configure RAG ingestion flow, including documents and using optical character recognition (OCR)
- Connect retrieval pipelines directly to workflows and agent tools

#### Extract content from documents

- Extract information by using multimodal pipelines that combine OCR, layout analysis, and field extraction
- Produce clean, grounded representations to use with agents and RAG by using Content Understanding
- Implement analyzers for generating structured or markdown outputs for downstream reasoning by using Content Understanding

---

## Study resources

We recommend that you train and get hands-on experience before you take the exam. We offer self-study options and classroom training as well as links to documentation, community sites, and videos.

| Study resources | Links to learning and documentation |
| --- | --- |
| Get trained | [Choose from self-paced learning paths and modules or take an instructor-led course](https://learn.microsoft.com/en-us/credentials/certifications/exams/AI-103#two-ways-to-prepare) |
| Find documentation | [Azure AI services](https://learn.microsoft.com/en-us/azure/ai-services/) |
| | [Azure AI Vision](https://learn.microsoft.com/en-us/azure/cognitive-services/computer-vision/) |
| | [Azure AI Video Indexer](https://learn.microsoft.com/en-us/azure/azure-video-indexer/) |
| | [Azure AI Language](https://learn.microsoft.com/en-us/azure/cognitive-services/luis/) |
| | [Azure AI Speech](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/) |
| | [Azure AI Search](https://learn.microsoft.com/en-us/azure/search/) |
| | [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) |
| | [Azure AI Document Intelligence](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/) |
| Ask a question | [Microsoft Q&A](https://learn.microsoft.com/en-us/answers/products/) |
| Get community support | [AI - Machine Learning - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/ai-machine-learning/bd-p/MachineLearning) |
| | [AI - Machine Learning Blog - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/ai-machine-learning-blog/bg-p/MachineLearningBlog) |
| Follow Microsoft Learn | [Microsoft Learn - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/microsoft-learn/ct-p/MicrosoftLearn) |
| Find a video | [The AI Show](https://learn.microsoft.com/en-us/shows/ai-show/) |
| | [Browse other Microsoft Learn shows](https://learn.microsoft.com/en-us/shows/browse) |
