<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.2: Choose and Deploy Models from the Model Catalog in Azure AI Foundry

</div>

> **Learning Objectives**: Select a language model from the model catalog → Deploy it to an endpoint → Test and improve its performance.

---

## 1. What Is the Model Catalog?

The **model catalog** is a curated collection of foundation models available in Microsoft Foundry. It lets you browse, compare, filter, and deploy models — both from Azure/OpenAI and from open-source community providers.

### Two Categories of Models

| Category | Description | Deployment Options | Support |
|----------|-------------|-------------------|---------|
| **Models sold by Azure** | Built by Microsoft (e.g., GPT-4o, GPT-4o-mini, Phi-4) | Serverless API (Global Standard/Standard) | Microsoft support + SLA |
| **Models from partners & community** | Built by third parties (e.g., Llama, Mistral, Cohere, Hugging Face, DeepSeek) | Serverless API or managed compute | Provider support, varies by vendor |

> **Exam insight**: Know which models are "sold by Azure" (Azure OpenAI family) vs "partner models" — this affects billing, SLA, and deployment type.

---

## 2. Navigating the Model Catalog

### Accessing the catalog
1. Sign in to [Microsoft Foundry](https://ai.azure.com) → toggle **New Foundry** on
2. Select **Build** → **Models** (or **Discover** → **Models** in older UI)
3. Browse model cards

### Filtering options
| Filter | Purpose | Example |
|--------|---------|---------|
| **Collection** | Model provider/vendor | Azure, Hugging Face, Meta, Cohere |
| **Task** | What the model does | Text generation, image generation, embeddings, audio |
| **Modality** | Input/output type | Text, image, audio, multimodal |
| **Deployment options** | How you can host it | Serverless API, Managed compute |

### Model card details
Each model card shows:
- **Model name and version** (e.g., GPT-4o version 2024-08-06)
- **License** (MIT, Apache 2.0, custom)
- **Modality** (text, image, multimodal)
- **Supported tasks** (chat, completion, embeddings, image generation)
- **Deployment templates** (for managed compute)
- **Benchmarks** (performance metrics)

---

## 3. Select Models Using Benchmarks

The model catalog provides **benchmark data** and a **leaderboard** to help you compare models objectively before deploying.

### How to Access Benchmarks
1. Go to **Discover** in the Foundry portal navigation bar
2. The model catalog overview shows a **snapshot of the leaderboard** at the top
3. Select **Go to leaderboard** for the full list, or click a model → **Benchmarks** tab

> **Note**: Benchmark data isn't available for all models. If a model doesn't have a **Benchmarks** tab, results haven't been published yet.

### Four Benchmark Dimensions

| Dimension | What It Measures | Interpretation |
|-----------|-----------------|----------------|
| **Quality index** | Reasoning, coding, math, knowledge tasks | Higher = better (0–1 scale) |
| **Safety scores** | Robustness against harmful content (HarmBench) | Lower attack success rate = better |
| **Estimated cost** | Actual cost to run benchmark datasets (USD) | Lower = cheaper |
| **Throughput** | Tokens per second processed | Higher = faster |

### Benchmark Tools in Foundry

| Tool | What It Does |
|------|-------------|
| **Model Leaderboard** | Sortable table of all benchmarked models across all four dimensions |
| **Trade-off charts** | Visual scatter plot comparing two metrics (e.g., quality vs. cost) |
| **Scenario leaderboards** | Filter by use case: Reasoning, Coding, Math, Q&A, Groundedness |
| **Side-by-side comparison** | Select 2–3 models to compare features, performance, and cost |

### Scenario Leaderboards

Use scenario-specific leaderboards to find models optimized for your use case:

| Scenario | Datasets | What It Tells You |
|----------|----------|-------------------|
| **Reasoning** | BIG-Bench Hard (1K subsample) | Logical and multi-step reasoning ability |
| **Coding** | BigCodeBench, LiveBench, MBPPPlus | Code generation accuracy |
| **Math** | MATH (500 subsample) | Mathematical reasoning |
| **Question & Answering** | Arena-Hard, GPQA (diamond) | Adversarial human preference QA |
| **General Knowledge** | MMLU-Pro (1K subsample) | Broad factual knowledge |
| **Groundedness** | TruthfulQA (MC1) | Truthfulness, resistance to hallucination |

### Interpreting Results

- **Quality index**: Average of accuracy scores across datasets (exact_match, pass@1, arena_hard). Higher = stronger.
- **Safety**: Attack Success Rate (ASR) from HarmBench — lower = more robust. Important for customer-facing apps.
- **Performance**: Includes latency (P50/P90/P95/P99), time-to-first-token (TTFT), and throughput (GTPS/TTPS).
- **Cost**: Computed from actual token consumption during benchmarks, not just pricing estimates.

### Trade-off Chart Tips
- Use **Compare quality against** dropdown to switch between cost, throughput, or safety
- Models closer to the **top-right corner** perform well on both axes
- At least **two models** required for trade-off comparisons

### Limitations
- Benchmarks use standardized public datasets — your real-world results may differ
- Performance metrics collected with synthetic workloads (fixed input/output ratio, single region)
- For testing with your own data, use **Evaluate your generative AI apps** instead
- Leaderboard is in **preview** — not all modalities/models are included

### Prerequisites to Access Leaderboard
- Paid Azure subscription (free/trial won't work)
- A Foundry project with at least **Reader** role
- Access to [ai.azure.com](https://ai.azure.com)

---

## 4. Model Families You Should Know

### Azure OpenAI Models (sold by Azure)

| Model | Best For | Notes |
|-------|----------|-------|
| **GPT-4o** | General-purpose, multimodal | Top performance, vision + text |
| **GPT-4o-mini** | Cost-effective general-purpose | Fast, cheap, good for most tasks |
| **GPT-4.1** | Latest generation | Advanced reasoning, code |
| **o3 / o4-mini** | Deep reasoning | Chain-of-thought, complex analysis |
| **Phi-4** | Small, efficient reasoning | On-device potential, lightweight |
| **DALL·E 3** | Image generation | Text-to-image |
| **Whisper** | Speech-to-text | Audio transcription |
| **Text-embedding-3-large/small** | Embeddings for RAG | Vector search, semantic similarity |

### Partner/Community Models

| Provider | Models | Deployment |
|----------|--------|------------|
| **Meta** | Llama 4 Scout, Llama 4 Maverick | Serverless API or managed compute |
| **Mistral** | Mistral Large, Mistral Nemo | Serverless API |
| **Cohere** | Command A, Embed v3 | Serverless API or managed compute |
| **Hugging Face** | Phi-4, Qwen, NVIDIA Nemotron, etc. | Managed compute |
| **DeepSeek** | DeepSeek-R1 | Serverless API |

> **Exam insight**: Match the right model to the scenario. Example: "Low-cost chatbot for internal use" → GPT-4o-mini; "Complex document analysis" → GPT-4o or GPT-4.1; "Embeddings for vector search" → text-embedding-3-large.

---

## 5. Deployment Types

### Serverless API Deployment (most common)
- **No infrastructure to manage** — pay per inference call
- Microsoft manages the endpoint, scaling, and availability
- Available for Azure OpenAI models and many partner models
- **Deployment types**:
  - **Global Standard** — lowest latency, global routing
  - **Standard** — single region
  - **Provisioned Throughput (PTU)** — guaranteed throughput for enterprise SLAs

### Managed Compute Deployment
- Runs on **dedicated VMs** (GPU instances) you control
- You choose the VM SKU (H100, A100, MI-300, etc.)
- Good for: **open-source models**, custom fine-tuned models, models requiring specific hardware
- **Shared quota** option available (168-hour endpoint lifetime)
- You manage: instance count, scaling, VM costs

### Choosing Between Them

| Factor | Serverless API | Managed Compute |
|--------|---------------|-----------------|
| **Infra management** | None | You manage VMs |
| **Cost model** | Per-call (token-based) | Per-hour (VM-based) |
| **Scaling** | Automatic | Manual or autoscale |
| **Model availability** | Azure OpenAI + select partners | Hugging Face collection, open-source |
| **Best for** | Production apps, low ops overhead | Custom models, cost control at scale |

---

## 6. Deploying a Model — Step by Step

### Serverless API Deployment (Portal)
1. Find model in catalog → **Deploy** → **Default settings** (or Custom)
2. Name the deployment (used as `model` parameter in API calls)
3. Select deployment type (Global Standard / Standard)
4. Accept Azure Marketplace terms (for partner models)
5. **Deploy** → status shows **Succeeded**
6. Land in **Playground** to test immediately

### Managed Compute Deployment (Portal)
1. Find model → **Deploy** → **Managed Compute**
2. Select **Deployment template** (matches accelerator type + context length)
3. Choose **Accelerator type** (H100_80GB, A100_80GB, MI_300_192GB)
4. Set **Model instances** (capacity — start with 1)
5. Acknowledge cost → **Deploy** (takes 10–15 minutes)

### Key Values for Code Deployment
When deploying via SDK/REST, you need:
1. **Model ID** — `azureml://registries/azure-huggingface/models/<model>/versions/<ver>`
2. **Deployment Template ID** — `azureml://registries/azure-huggingface/deploymenttemplates/<template>/labels/latest`
3. **Accelerator type** — e.g., `H100_80GB`

---

## 7. Testing Your Model

### Playground (Portal)
- After deployment, you land in the **Foundry Playground**
- Interactive chat interface — send messages, see responses
- Toggle model parameters (temperature, max tokens, top-p, stop sequences)
- Compare outputs across multiple deployed models side-by-side

### Key Parameters to Tune

| Parameter | Range | Effect |
|-----------|-------|--------|
| **Temperature** | 0.0–2.0 | 0 = deterministic, 1+ = more creative/random |
| **Top-p** | 0.0–1.0 | Controls diversity of token sampling |
| **Max tokens** | 1–4096+ | Maximum response length |
| **Stop sequences** | String list | Stop generating when these strings appear |
| **Frequency penalty** | -2.0–2.0 | Reduce repetition of common tokens |
| **Presence penalty** | -2.0–2.0 | Encourage new topics |

> **Exam insight**: Temperature = 0 is best for factual/consistent responses. Higher temperature for creative tasks. Don't confuse temperature with top-p — they control different aspects of randomness.

---

## 8. Optimizing Model Performance

### Prompt Engineering
- **System message** — set role, constraints, format requirements
- **Few-shot examples** — include input/output examples in the prompt
- **Chain-of-thought** — ask model to "think step by step" before answering
- **Structured output** — request JSON, tables, or specific formats

### Grounding with RAG (Retrieval-Augmented Generation)
- Connect model to your **own data** via Azure AI Search
- Retrieve relevant documents → pass as context → model generates grounded answers
- Reduces hallucination, ensures relevance to your domain

### Fine-Tuning
- Train the model on **your specific data** for consistent behavior
- Options: Supervised Fine-Tuning (SFT), Direct Preference Optimization (DPO), Reinforcement with Teacher Feedback (RTF)
- Use when prompt engineering + RAG aren't enough

### Evaluation
- **Manual testing** — playground, compare prompts
- **Automated evaluation** — use Foundry's evaluation tools (groundedness, relevance, coherence metrics)
- **A/B testing** — deploy multiple model versions, compare real user interactions

---

## 9. Responsible AI in Model Selection

### Content Filtering (default: ON)
- Detects harmful content across categories: **Hate, Self-Harm, Sexual, Violence**
- Can be customized per deployment
- Applies to both inputs and outputs

### Content Types for Filtering
| Category | What It Detects |
|----------|----------------|
| **Hate** | Discriminatory language, slurs, hate speech |
| **Self-Harm** | Content promoting self-injury or suicide |
| **Sexual** | Explicit sexual content, non-consensual themes |
| **Violence** | Graphic violence, glorification of harm |

### Grounding / Jailbreak Detection
- **Prompt Shields** — detects prompt injection attempts
- **Indirect prompt injection** — embedded text in images/files
- **User intent classification** — flags potentially harmful requests

---

## 10. Python SDK — Deploying & Consuming a Model

### Install
```bash
pip install "azure-ai-projects>=2.0.0" azure-identity python-dotenv
```

### Minimal Code
```python
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

project = AIProjectClient.from_connection_string(
    conn_str="<PROJECT_ENDPOINT>;subscriptionid=<sub>;resourcegroupname=<rg>;projectname=<proj>",
    credential=DefaultAzureCredential(),
)

# Get OpenAI-compatible client
openai_client = project.inference.get_openai_client()

# Chat completion
response = openai_client.chat.completions.create(
    model="gpt-4o-mini",  # deployment name
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is Azure AI Foundry?"}
    ]
)
print(response.choices[0].message.content)
```

---

## 11. Key Takeaways

1. The **model catalog** is your starting point — filter by collection, task, modality
2. Use **benchmarks** (quality, safety, cost, throughput) to compare models objectively before deploying
3. **Scenario leaderboards** help find models optimized for your specific use case (coding, math, reasoning)
4. **Models sold by Azure** = enterprise SLA + Microsoft support; **Partner models** = specialized + community-driven
5. **Serverless API** = zero infra, pay-per-call; **Managed compute** = dedicated VMs, more control
6. **Deployment name** = the `model` parameter in your API calls
7. **Playground** = instant testing after deployment
8. **Optimize**: prompt engineering → RAG → fine-tuning (progressive complexity)
9. **Content filtering** is on by default — never disable without good reason
10. Match the **model to the scenario** — don't use GPT-4o when GPT-4o-mini suffices

---

## Quick Reference: Model → Scenario Mapping

| Scenario | Recommended Model |
|----------|-------------------|
| Simple chatbot, FAQ | GPT-4o-mini |
| Complex document analysis | GPT-4o / GPT-4.1 |
| Deep reasoning, math, code | o3 / o4-mini |
| Image generation | DALL·E 3 |
| Speech-to-text | Whisper |
| Vector embeddings for RAG | text-embedding-3-large |
| Cost-sensitive high-volume | GPT-4o-mini |
| Enterprise with SLA | GPT-4o (Provisioned PTU) |

---

*Last updated: 2026-08-03 · Source: [Microsoft Learn — Module 1.2](https://learn.microsoft.com/en-us/training/modules/explore-models-azure-ai-studio/)*
