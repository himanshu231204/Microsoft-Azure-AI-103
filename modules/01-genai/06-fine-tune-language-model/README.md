<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.6: Fine-tune a Language Model with Azure AI Foundry

</div>

> **Source**: [Microsoft Learn — Fine-tune a language model with Azure AI Foundry](https://learn.microsoft.com/training/modules/finetune-model-copilot-ai-studio/)
> **Learning objectives**: Understand when to fine-tune a model, prepare your data to fine-tune a chat completion model, fine-tune a base model in the Azure AI Foundry portal

---

## Table of Contents

1. [What is Fine-tuning? — Adapting a Base Model to Your Task](#1-what-is-fine-tuning--adapting-a-base-model-to-your-task)
2. [When to Fine-tune — vs Prompt Engineering vs RAG](#2-when-to-fine-tune--vs-prompt-engineering-vs-rag)
3. [Training Methods — SFT, DPO, RFT](#3-training-methods--sft-dpo-rft)
4. [Preparing Data for Chat Completion Fine-tuning](#4-preparing-data-for-chat-completion-fine-tuning)
5. [Dataset Size and Quality](#5-dataset-size-and-quality)
6. [Fine-tuning in the Azure AI Foundry Portal](#6-fine-tuning-in-the-azure-ai-foundry-portal)
7. [Hyperparameters and Training Tiers](#7-hyperparameters-and-training-tiers)
8. [The Fine-tuning Workflow (End to End)](#8-the-fine-tuning-workflow-end-to-end)
9. [Best Practices and Troubleshooting](#9-best-practices-and-troubleshooting)
10. [Key Takeaways for AI-103](#10-key-takeaways-for-ai-103)

---

## 1. What is Fine-tuning? — Adapting a Base Model to Your Task

**Fine-tuning** is the process of taking a pretrained language model and adapting it to perform a specific task or improve its performance on a particular dataset. The model is trained on a smaller, task-specific dataset while its weights are adjusted slightly, **specializing** the model without starting from scratch.

### Why Fine-tuning Exists

Base models are trained on large, diverse public datasets. They don't know your:
- **Task-specific patterns** (e.g., legal document summarization, code review)
- **Output format or schema** requirements
- **Desired style and tone** (e.g., brand voice, customer support tone)

Fine-tuning **leverages the knowledge the model acquired during pretraining**, so you don't need to retrain from zero — this is far more efficient and effective than training a new model.

### How It Works — LoRA

Azure OpenAI in Azure AI Foundry uses **LoRA (Low-Rank Adaptation)** to fine-tune models:

| Aspect | LoRA detail |
|--------|-------------|
| **Mechanism** | Approximates the original high-rank weight matrix with a lower-rank one |
| **Parameters** | Only fine-tunes a small subset of *important* parameters during supervised training |
| **Impact** | Reduces complexity without significantly affecting performance |
| **Benefits** | Training is faster and more affordable than full fine-tuning |

> **Exam insight**: Fine-tuning adjusts the base model's **weights** — the model learns from many more examples than can fit in a prompt, so you no longer need to include as many examples or instructions at inference time.

---

## 2. When to Fine-tune — vs Prompt Engineering vs RAG

### The Model Customization Continuum

```
Prompt Engineering  →  Few-shot Learning  →  RAG  →  Fine-tuning
     (cheapest,             (examples               (grounding      (changes model
      most flexible)        in prompt)              in fresh data)   weights/behavior)
```

### When to Fine-tune

Fine-tuning is suited to scenarios with a **small, high-quality dataset** (hundreds to a few thousand task-specific prompt–response pairs):

| Use case | Description |
|----------|-------------|
| **Reduce prompt engineering overhead** | Embed few-shot examples into the model instead of appending them to every prompt — cuts token counts and latency, valuable with many edge cases |
| **Modify style and tone** | Align outputs with a desired voice (customer service chatbots, brand-specific communication) |
| **Generate specific formats/schemas** | Structured data generation, reports, formatted responses |
| **Enhance tool usage** | Improve accuracy/consistency of tool calling, even without full tool definitions |
| **Enhance retrieval-based performance** | Train the model to use retrieved data effectively and filter irrelevant info |
| **Optimize for efficiency (distillation)** | Transfer knowledge from a larger model to a smaller one — e.g., collect production traffic from a large deployment and use it to fine-tune a smaller, cheaper model |

### When to Use Alternatives

| Approach | Best for |
|----------|----------|
| **Prompt engineering** | Simple adjustments, no training data, quick iteration |
| **Few-shot learning** | Small number of examples that fit in the prompt |
| **RAG** | Fresh/private data, dynamic content, wide topic coverage, limited compute |
| **Fine-tuning** | Task-specific performance, proprietary/unique data, stable content, consistent behavior |

### Fine-tuning vs RAG

| Aspect | Fine-tuning | RAG |
|--------|-------------|-----|
| **What it changes** | Model behavior, style, task performance | Adds knowledge at query time |
| **Data** | Baked into model weights | Retrieved per query |
| **Freshness** | Static (needs retraining for updates) | Dynamic (updates when index updates) |
| **Use case** | Specialized task, consistent output | Up-to-date or private information |

> **Exam insight**: Choose **fine-tuning** when you need top results for a specific task with enough domain data, **RAG** when content changes frequently or you need broad coverage. They can also be **combined** — fine-tune the model to reason over retrieved content.

---

## 3. Training Methods — SFT, DPO, RFT

The model catalog in Azure AI Foundry offers many models that can be fine-tuned. The training method you choose depends on the model and your goal:

| Method | Name | Supported by | What it does |
|--------|------|--------------|--------------|
| **SFT** | Supervised Fine-tuning | All non-reasoning models | Trains on input → output examples (chat completion pairs) |
| **DPO (Preview)** | Direct Preference Optimization | GPT-4o | Trains on preferred vs non-preferred responses (preference optimization) |
| **RFT (Preview)** | Reinforcement Fine-tuning | Reasoning models like o4-mini | Trains with reinforcement learning + graders for reasoning tasks |

### DPO specifics
- Uses paired examples: a **chosen** (preferred) response and a **rejected** response
- The `beta` hyperparameter (0.1–0.5) controls how much the model can drift from the reference model — smaller beta = more drift

### RFT specifics
- Adds hyperparameters: `eval_samples`, `eval_interval`, `compute_multiplier`, `reasoning_effort` (low/medium/high)
- Uses **graders** to evaluate model outputs during training

> **Exam insight**: Not all models support all training methods. SFT = supervised examples; DPO = preference pairs; RFT = reinforcement with graders for reasoning models.

---

## 4. Preparing Data for Chat Completion Fine-tuning

### File Format

Training and validation data **must** be:

- **JSON Lines (JSONL)** format — one JSON object per line
- Formatted in the **conversational format** used by the **Chat Completions API**
- Encoded in **UTF-8 with a byte-order mark (BOM)**
- **Less than 512 MB** in size

### Chat Format Structure

Each line is a chat session with a single `messages` key mapping to an array of message objects:

| Field | Rules |
|-------|-------|
| `role` | `system`, `user`, or `assistant` |
| `content` | The text of the message |
| Ordering | System (optional) must be first; roles alternate user/assistant; **last message must be `assistant`** |
| Minimum | At least one assistant message |

### Example — Single Turn

```json
{"messages": [{"role": "system", "content": "You are a helpful support agent for Contoso Ltd."}, {"role": "user", "content": "How do I reset my password?"}, {"role": "assistant", "content": "To reset your password, go to the sign-in page and select 'Forgot password'."}]}
```

### Example — Multi-turn with weight

```json
{"messages": [{"role": "system", "content": "You are a cheerful travel assistant."}, {"role": "user", "content": "Plan a 3-day trip to Paris."}, {"role": "assistant", "content": "Here's a suggested itinerary for Paris...", "weight": 0}, {"role": "user", "content": "Make it more budget-friendly."}, {"role": "assistant", "content": "Here's a budget-friendly version..."}]}
```

### Key Format Rules

- **`weight`** (optional): skip fine-tuning on specific assistant messages — set to `0` or `1`
- **System message**: recommended to include the instructions/prompts that worked best in *every* training example — especially important with fewer than 100 examples
- **Vision fine-tuning**: gpt-4o (2024-08-06) and gpt-4.1 (2025-04-14) support images in JSONL (JPEG/PNG/WEBP, max 10 MB each, max 64 images per example)

> **Exam insight**: The chat format is the same as the **Chat Completions API**. Always end each conversation with an **assistant** message — that's what the model learns to produce.

---

## 5. Dataset Size and Quality

### Minimums and Recommendations

| Amount | Effect |
|--------|--------|
| < 10 examples | Fine-tuning **job will not proceed** |
| ~10 examples | Job runs, but won't noticeably influence the model |
| 50 well-crafted examples | Recommended starting point |
| Hundreds to thousands | Best practice for real results |

### Quality over Quantity

- **Doubling the dataset can lead to a linear increase in model quality** — but only if the data is high quality
- **Low-quality examples negatively impact performance** — a large dataset of unpruined internal data can produce a model that performs *worse* than expected
- Prune the dataset for only the highest-quality examples before training

> **Exam insight**: More examples ≠ better automatically. Quality matters: 50 well-crafted examples beat thousands of noisy ones. Minimum to start a job = 10.

---

## 6. Fine-tuning in the Azure AI Foundry Portal

### Accessing Fine-tuning

1. Go to the **Azure AI Foundry portal** at `https://ai.azure.com/` and sign in
2. Select your project (or create one)
3. From the left menu, select **Fine-tuning** → **+ Fine-tune model**

### Two Fine-tuning Experiences

| Experience | Scope | Notes |
|------------|-------|-------|
| **Hub/Project view** | Models from multiple providers (Azure OpenAI, Meta Llama, Microsoft Phi, etc.) | General-purpose fine-tuning |
| **Azure OpenAI centric view** | Azure OpenAI models only | Extra features like Weights & Biases (W&B) preview integration |

### The Create a Fine-tuned Model Wizard

| Step | What you choose |
|------|-----------------|
| 1. Confirm model + **training method** | SFT / DPO / RFT (per model support) |
| 2. Select a **base model** | Influences performance and cost |
| 3. Choose **training type** | Standard / Global / Developer tier |
| 4. Choose **training data** | Existing dataset or upload new (JSONL) |
| 5. Optional: **validation data** | JSONL, < 512 MB |
| 6. Optional: **task parameters** | Hyperparameters, suffix, seed |
| 7. Optional: **auto-deployment** | Deploy custom model automatically on success (OpenAI models only; requires Foundry Owner role / deployments/write) |
| 8. Review and **train** | Submit the job |

### Model Identifiability — `suffix`

- Add a **suffix** (up to 18 characters) to distinguish iterations of your fine-tuned model
- The suffix is appended to the generated fine-tuned model name

> **Exam insight**: The wizard order is: training method → base model → training type → training data → (validation data) → (parameters) → (auto-deploy) → train.

---

## 7. Hyperparameters and Training Tiers

### Supported Hyperparameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `batch_size` | integer | Number of training examples per forward/backward pass. Larger batch = fewer updates with lower variance. `-1` = auto (0.2% of examples, max 256) |
| `learning_rate_multiplier` | number | Fine-tuning LR = pretraining LR × multiplier. Recommended range **0.02 – 0.2**. Smaller LR helps avoid overfitting |
| `n_epochs` | integer | One full cycle through the training dataset. `-1` = determined dynamically |
| `seed` | integer | Controls **reproducibility** — same seed + params → same results (rare exceptions). Randomly generated if not specified |
| `beta` (DPO only) | integer | Temperature for DPO loss, 0.1–0.5; smaller beta = more drift from reference model |

### Training Tiers (Training Type)

| Tier | Data residency | Cost | Best for |
|------|----------------|------|----------|
| **Standard** | Yes — trains in your resource's region | Baseline | Workloads requiring data residency |
| **Global (Preview)** | No — data/weights copied to training region | More affordable per token | No residency constraint, faster queue times |
| **Developer** | No guarantees | Significant savings (idle capacity) | Experimentation; jobs may be preempted/resumed, no SLA |

> **Exam insight**: `seed` = reproducibility. `learning_rate_multiplier` recommended range 0.02–0.2. `batch_size` and `n_epochs` accept `-1` for automatic determination.

---

## 8. The Fine-tuning Workflow (End to End)

### Portal Workflow

1. Prepare training and validation data (JSONL chat format)
2. Use the **Create a fine-tuned model** dialog to train your custom model
3. Check the status of your custom fine-tuned model
4. **Deploy** your custom model for use
5. **Use** your custom model (Chat Completions API)
6. Optionally, **analyze** your custom model for performance and fit

### Python SDK Workflow

```python
from azure.ai.resources.entities import AzureOpenAIConnection
from azure.ai.ml import MLClient

# 1. Connect to your project
client = MLClient(
    credential=DefaultAzureCredential(),
    subscription_id=subscription_id,
    resource_group_name=resource_group,
    workspace_name="<your-foundry-project>",
)

# 2. Upload training data
training_dataset = client.data.create_or_update(
    Data(
        path="./training_data.jsonl",
        type=AssetTypes.URI_FILE,
        name="my-training-data",
    )
)

# 3. Submit fine-tuning job
job = client.jobs.create(
    create_job(
        display_name="ft-gpt-4o-mini-support",
        training_data=training_dataset,
        # Base model, method (supervised), and hyperparameters
    )
)
```

> **Exam insight**: The workflow is identical regardless of interface: **prepare data → select base model → upload data → train → check status → deploy → use → analyze**. Auto-deployment is only supported for OpenAI models.

---

## 9. Best Practices and Troubleshooting

### Best Practices

| Practice | Why |
|----------|-----|
| Use the best prompt/instructions in every training example | Especially with < 100 examples, keeps behavior consistent |
| Start with 50 well-crafted examples | Meaningful influence without wasted cost |
| Prune for quality | Low-quality examples degrade the model |
| Use a `suffix` | Distinguish iterations of fine-tuned models |
| Set a `seed` | Reproducible jobs |
| Start with automatic hyperparameters | Recommended for initial training runs |
| Import large files from Azure Blob | Multipart uploads are atomic and can't be retried/resumed — unstable for large files |

### Common Issues and Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| **Job won't start** | Fewer than 10 training examples | Add more examples |
| **Model performs worse than base** | Low-quality training data | Prune dataset to high-quality examples only |
| **Overfitting** | Too many epochs / high LR | Reduce epochs, use smaller learning rate multiplier |
| **Non-deterministic results** | No seed | Pass the same seed for reproducible jobs |
| **Unstable large-file upload** | Multipart form upload | Import from Azure Blob storage instead |

### Cost and Latency Benefits of Fine-tuning

- **Shorter prompts** → fewer tokens per request → cost savings
- **Faster responses** → lower latency, especially with smaller models
- **Smaller models** can match larger model performance on the specific task (distillation)

> **Exam insight**: Fine-tuning is not a substitute for RAG (knowledge freshness) and RAG is not a substitute for fine-tuning (behavior/style). They are complementary and often combined.

---

## 10. Key Takeaways for AI-103

### Must-Know Facts

1. **Fine-tuning** adapts a pretrained model to a specific task by adjusting weights on task-specific data
2. **LoRA** (low-rank adaptation) makes training faster and more affordable by fine-tuning a small subset of parameters
3. **When to fine-tune**: reduce prompt overhead, change style/tone, enforce formats, improve tool use, distill large models into small ones
4. **Fine-tuning vs RAG**: fine-tuning changes behavior; RAG adds fresh/private knowledge — often combined
5. **Training methods**: **SFT** (all non-reasoning), **DPO** (GPT-4o, preference pairs), **RFT** (reasoning models, graders)
6. **Data format**: JSONL, Chat Completions format, UTF-8 + BOM, < 512 MB; roles `system`/`user`/`assistant`, last message must be `assistant`
7. **Minimum 10 examples** to start a job; start with **50 well-crafted**; quality > quantity
8. **Hyperparameters**: `batch_size`, `learning_rate_multiplier` (0.02–0.2), `n_epochs`, `seed`
9. **Training tiers**: Standard (data residency) / Global (cheaper, no residency) / Developer (experimentation, preemptible)
10. **Workflow**: prepare data → select base model → upload → train → check status → deploy → use → analyze

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Base model selection | Module 1.2 (Choose and deploy models from the model catalog) |
| Foundry portal & SDK | Module 1.3 (Develop AI app with the Foundry SDK) |
| Fine-tune vs RAG decision | Module 1.5 (Develop a RAG-based solution) |
| Prompt engineering baseline | Module 1.4 (Get started with prompt flow) |
| Evaluating fine-tuned model | Module 1.8 (Evaluate generative AI performance) |
| Responsible use of custom models | Module 1.7 (Implement a responsible generative AI solution) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*
