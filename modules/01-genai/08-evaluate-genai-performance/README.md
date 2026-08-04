<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.8: Evaluate Generative AI Performance in Azure AI Foundry Portal

</div>

> **Source**: [Microsoft Learn — Evaluate generative AI performance in Azure AI Foundry portal](https://learn.microsoft.com/training/modules/evaluate-models-azure-ai-studio/)
> **Learning objectives**: Understand model benchmarks, perform manual evaluations, assess your generative AI apps with AI-assisted metrics, and configure evaluation flows in the Azure AI Foundry portal

---

## Table of Contents

1. [Why Evaluation Matters](#1-why-evaluation-matters)
2. [What You Can Evaluate — Models and Chat Flows](#2-what-you-can-evaluate--models-and-chat-flows)
3. [Model Benchmarks](#3-model-benchmarks)
4. [Manual Evaluations](#4-manual-evaluations)
5. [Automated Evaluations](#5-automated-evaluations)
6. [AI-Assisted Metrics](#6-ai-assisted-metrics)
7. [Natural Language Processing (NLP) Metrics](#7-natural-language-processing-nlp-metrics)
8. [Evaluation Data and Evaluation Flows](#8-evaluation-data-and-evaluation-flows)
9. [The Exercise — Evaluate Generative AI Model Performance](#9-the-exercise--evaluate-generative-ai-model-performance)
10. [Best Practices and Troubleshooting](#10-best-practices-and-troubleshooting)
11. [Key Takeaways for AI-103](#11-key-takeaways-for-ai-103)

---

## 1. Why Evaluation Matters

Evaluating generative AI apps is crucial for **two main reasons**:

| Reason | What it gives you |
|--------|-------------------|
| **Quality assurance** | Identify and address issues so the app provides **accurate and relevant responses** → improved **user satisfaction** and continued use |
| **Continuous improvement** | Analyze evaluation results to identify areas for enhancement and **iteratively improve** performance, staying ahead of user needs and expectations |

> **Exam insight**: Evaluation = **quality assurance** + **continuous improvement**. Evaluation is not a one-time step — it's an iterative loop: build → evaluate → improve → re-evaluate.

---

## 2. What You Can Evaluate — Models and Chat Flows

When developing a generative AI app you use a **language model** in a chat application to generate a response. You can evaluate at two levels:

### Individual Language Model

```
Input (1) → Language Model (2) → Output / Response (3)
```

The model is evaluated by analyzing the **input**, the **output**, and optionally **comparing it to a predefined expected output** (ground truth). Use this to decide **which model** to integrate into your application.

### Complete Chat Flow (Prompt Flow)

```
Input (1) → Executes through various nodes (2) → Output (3)
```

A **chat flow** orchestrates executable flows that can combine **multiple language models and Python code**. You can evaluate a **complete chat flow** *and* its **individual components**.

> **Exam insight**: Start by testing an **individual model**, then test the **complete chat flow** to validate the whole app. Evaluation targets in the Foundry portal include: a **deployed model**, a **prompt flow**, a **dataset** (preexisting outputs), or an **agent**.

---

## 3. Model Benchmarks

**Model benchmarks** are **publicly available metrics across models and datasets**. They help you understand how a model performs **relative to others** — useful before you deploy or select a model.

| Benchmark metric | What it measures |
|------------------|------------------|
| **Accuracy** | Compares generated text with the correct answer per the dataset. Result = 1 if the generated text matches exactly, 0 otherwise |
| **Coherence** | Whether output flows smoothly, reads naturally, and resembles human-like language |
| **Fluency** | How well generated text adheres to grammatical rules, syntactic structures, and appropriate vocabulary — linguistically correct, natural-sounding responses |
| **GPT similarity** | Quantifies the semantic similarity between a ground truth sentence/document and the AI-generated prediction sentence |

In the **Microsoft Foundry portal**, you can explore **model benchmarks for all available models before deploying a model**.

> **Exam insight**: Benchmarks are **public, comparative metrics** used to **compare models against each other** before deployment. They are *not* your own app's evaluation — they're the model catalog's pre-built comparisons.

---

## 4. Manual Evaluations

**Manual evaluations** involve **human raters** who assess the quality of the model's responses. They provide insights that **automated metrics might miss**, such as **context relevance** and **user satisfaction**. Human evaluators can rate responses on criteria like **relevance, informativeness, and engagement**.

### Step 1: Prepare Your Test Prompts

Prepare a **diverse set of test prompts** that reflect the range of queries and tasks your app is expected to handle:

| Prompt category | Purpose |
|-----------------|---------|
| **Common user questions** | Verify typical happy-path behavior |
| **Edge cases** | Probe unusual or boundary inputs |
| **Potential failure points** | Find scenarios where the app degrades |

### Step 2: Test the Model in the Chat Playground

- The **chat playground** lets you interact with a **deployed model**
- **Ideal for early development**: enter a prompt, see how the model responds, **tweak the prompt or system message**, and re-test to see if performance improved
- Use it to verify the **individual model** works before building the chat flow

### Step 3: Evaluate Multiple Prompts with the Manual Evaluations Feature

- Upload a **dataset with multiple questions** and optionally add an **expected response**
- Rate model responses with a **thumbs up / thumbs down** feature
- Based on overall ratings, improve the model by changing:
  - The **input prompt**
  - The **system message**
  - The **model**
  - The **model's parameters**

> **Exam insight**: Manual evaluations = **human raters** applying judgment (e.g., thumbs up/down) to responses across a **test dataset**. They capture what automated metrics miss (**context relevance, user satisfaction, engagement**). This is the correct answer for "apply your own judgment about the quality of responses to a set of specific prompts."

---

## 5. Automated Evaluations

**Automated evaluations** in the Microsoft Foundry portal enable you to assess the **quality and content safety performance** of **models, datasets, or prompt flows**.

### Evaluation Data

To evaluate a model you need a dataset of **prompts and responses** (and optionally expected responses as **ground truth**). You can compile this dataset by:

1. **Manual compilation** — hand-author prompts and responses
2. **Existing application output** — capture real traffic
3. **AI-generated data** — use an AI model to generate a set of prompts/responses related to a subject, then **edit them to reflect your desired output** and use them as ground truth

### Evaluation Metrics — Two Categories of Evaluators

| Evaluator category | What it measures | Example metrics |
|--------------------|------------------|-----------------|
| **AI Quality** | Quality of responses measured by **AI models judging** the response, plus **standard NLP metrics** against ground truth | Coherence, relevance (AI-judged); F1 score, BLEU, METEOR, ROUGE (NLP) |
| **Risk and Safety** | Content safety issues in the responses | Violence, hate, sexual content, self-harm |

> **Exam insight**: Automated evaluations use **evaluators** that compute **metrics**. **AI Quality evaluators** measure quality (AI-judged coherence/relevance + NLP metrics vs. ground truth). **Risk and Safety evaluators** detect harmful content (violence, hate, sexual, self-harm).

---

## 6. AI-Assisted Metrics

**AI-assisted metrics** use LLMs (e.g., GPT-4) as **evaluator models** to score responses similarly to human judgment. They fall into two broad categories and typically require parameters such as the **question, answer, and surrounding context**.

### Generation Quality Metrics

| Metric | What it measures | Scale |
|--------|------------------|-------|
| **Groundedness** | How well generated answers align with information from the input source — answers are verified as **claims against context**; even factually correct answers are **ungrounded** if not verifiable against the source | 1 = ungrounded → 5 = perfect groundedness |
| **Relevance** | How pertinent and directly related the responses are to the given questions | 1 = worst → 5 = best |
| **Coherence** | How well output flows smoothly, reads naturally, and resembles human-like language — the **structure and logical flow of ideas** | 1 = worst → 5 = best |
| **Fluency** | Language proficiency — adherence to grammatical rules, syntactic structures, and appropriate vocabulary | 1 = worst → 5 = best |
| **Similarity** | Semantic similarity between a ground truth sentence/document and the prediction, computed via **sentence-level embeddings** | 1 = nonequivalence → 5 = perfect equivalence |

### Risk and Safety Metrics

Monitor for **high-risk content**:
- **Violence**
- **Self-harm**
- **Sexual content**
- **Hateful content**

### Metric Configuration Requirements

The data columns present determine which metrics can be produced:

| Metric | Prompt | Completion | Context | Ground truth |
|--------|--------|------------|---------|--------------|
| **Coherence** | Required | Required | – | – |
| **Fluency** | Required | Required | – | – |
| **Groundedness** | Required | Required | Required | – |
| **Relevance** | Required | Required | Required | – |
| **Similarity** | Required | Required | – | Required |

> **Exam insight**: Know the **five quality metrics** (groundedness, relevance, coherence, fluency, similarity) and what data each requires. **Groundedness** and **relevance** need **context**; **similarity** needs **ground truth**; **coherence** and **fluency** only need prompt + completion. **Groundedness** is about verifiability against source — even true answers are ungrounded if unsupported by the context.

---

## 7. Natural Language Processing (NLP) Metrics

NLP metrics quantify the **level of overlap** between the model-generated response and the **ground truth** (expected response). They are used by AI Quality evaluators when ground truth is available.

| Metric | Full name | Use |
|--------|-----------|-----|
| **F1-score** | – | Measures the ratio of **shared words** between generated and ground truth answers; balances **precision and recall** — useful for text classification and information retrieval |
| **BLEU** | Bilingual Evaluation Understudy | Compares generated text to ground truth for **translation**-style tasks |
| **METEOR** | Metric for Evaluation of Translation with Explicit Ordering | Translation evaluation with **explicit word ordering** awareness |
| **ROUGE** | Recall-Oriented Understudy for Gisting Evaluation | **Summarization** evaluation, recall-oriented |

> **Exam insight**: **F1-score** is the evaluator that "compares generated responses to ground truth based on standard metrics" (shared-word overlap / precision + recall). Know the metric-to-use-case mapping: **BLEU/METEOR → translation**, **ROUGE → summarization**, **F1/accuracy → classification**, **groundedness/relevance/coherence/fluency → RAG**.

---

## 8. Evaluation Data and Evaluation Flows

### Evaluation Flows in the Foundry Portal

One of the module's learning objectives is to **configure evaluation flows** in the Azure AI Foundry portal:

1. Create or select a **test dataset** (CSV or JSONL) containing prompts and (optionally) ground truth responses
2. Choose an **evaluation target**: a deployed model, a prompt flow, a dataset of preexisting outputs, or an agent
3. Select the **evaluators** you want to run (AI Quality, Risk and Safety, or custom)
4. Run the evaluation and **view results** — aggregate and sample-level metrics, and the ability to **compare results across runs**

### Prerequisites for Evaluation in the Portal

- An **Azure subscription** and a **Microsoft Foundry project**
- For **AI-assisted quality evaluations**: an Azure OpenAI connection with a deployed GPT model (e.g., `gpt-4.1-mini`) that acts as the evaluator model
- **Foundry User** role (previously named Azure AI User) on the project

> **Exam insight**: AI-assisted quality evaluations **require a deployed GPT model** (e.g., `gpt-4.1-mini`) as the evaluator. Evaluation results can be viewed as **aggregate metrics** and **sample-level metrics**, and runs can be **compared** across iterations to track improvement.

---

## 9. The Exercise — Evaluate Generative AI Model Performance

The module's hands-on exercise demonstrates how to **evaluate the performance of a generative AI app** in the Microsoft Foundry portal:

1. Sign in with an **Azure subscription** (or sign up for one with 30-day credits)
2. Use the Microsoft Foundry portal to evaluate a generative AI app
3. Compare model responses and assess performance using the evaluation features described above

> **Note**: The exercise requires an **Azure subscription**. It is launched from the Microsoft Learn module via the exercise link.

---

## 10. Best Practices and Troubleshooting

### Best Practices

| Practice | Why |
|----------|-----|
| Evaluate **early and often** | Catch issues in the model before building the full chat flow |
| Use **model benchmarks** before deployment | Compare candidate models on public metrics to shortlist |
| Prepare **diverse test prompts** | Cover common questions, edge cases, and failure points |
| Start with **manual evaluations** | Get human judgment on context relevance and satisfaction |
| Scale with **automated evaluations** | Apply evaluators to large datasets for consistent measurement |
| **AI-generate + edit** test data | Quickly bootstrap a ground-truth dataset for your subject |
| Provide the right **input columns** | Metrics like groundedness need context; similarity needs ground truth |
| **Compare runs** | Track improvements across evaluation iterations |
| Combine **quality + safety** evaluators | Measure both generation quality and content safety |

### Common Issues and Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| Metric can't be computed | Missing required data column | Check metric config: groundedness/relevance need **context**, similarity needs **ground truth** |
| Benchmarks don't reflect your app | Benchmarks are public/generic | Run **manual or automated evaluations** on your own data |
| Responses sound fluent but wrong | Only checking fluency/coherence | Add **groundedness** and **relevance** evaluators with context |
| Subjective rating inconsistency | Multiple human raters, no rubric | Define clear rating criteria (relevance, informativeness, engagement) |
| Slow manual review of large datasets | Too many prompts for human raters | Move to **automated evaluators**; keep manual for spot checks |

---

## 11. Key Takeaways for AI-103

### Must-Know Facts

1. Evaluation serves **quality assurance** and **continuous improvement**
2. You can evaluate an **individual language model** or a **complete chat flow** (prompt flow with multiple models + Python nodes)
3. **Model benchmarks** = public, comparative metrics (accuracy, coherence, fluency, GPT similarity) used to compare models **before deployment**
4. **Manual evaluations** = human raters; use the **chat playground** for single prompts and the **manual evaluations** feature (thumbs up/down) for a **test dataset**
5. Improve models based on ratings by changing the **input prompt, system message, model, or model parameters**
6. **Automated evaluations** = evaluators that assess **AI Quality** and **Risk and Safety** of models, datasets, or prompt flows
7. **AI Quality metrics**: coherence, relevance (AI-judged) + F1, BLEU, METEOR, ROUGE (NLP vs. ground truth)
8. **Risk and Safety metrics**: violence, hate, sexual content, self-harm
9. **Generation quality metrics**: **groundedness** (verifiable against context), **relevance**, **coherence** (structure/logical flow), **fluency** (grammar), **similarity** (embedding-based vs. ground truth) — all scored 1–5
10. **Metric inputs**: coherence/fluency = prompt + completion; groundedness/relevance = + context; similarity = + ground truth
11. **NLP metrics**: **F1** (shared words/precision+recall), **BLEU/METEOR** (translation), **ROUGE** (summarization)
12. **AI-assisted quality evaluation requires a deployed GPT evaluator model** (e.g., `gpt-4.1-mini`) and an Azure OpenAI connection
13. Evaluation flow: **test dataset → target (model/flow/dataset/agent) → evaluators → results (aggregate + sample-level, comparable across runs)**

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Model selection & benchmarks | Module 1.2 (Choose and deploy models) |
| Evaluation with the Foundry SDK | Module 1.3 (Develop an AI app with the Azure AI Foundry SDK) |
| Evaluating prompt flows | Module 1.4 (Get started with prompt flow) |
| Groundedness & relevance for RAG | Module 1.5 (Develop a RAG-based solution) |
| Measuring harms with safety evaluators | Module 1.7 (Implement a responsible generative AI solution) |
| Evaluators in prompt flow & model monitoring | Module 1.6 (Fine-tune a language model) / GenAIOps post-production monitoring |
| Agent evaluation & continuous monitoring | LP2 (Develop AI agents on Azure) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*
