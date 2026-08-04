<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.5: Develop a RAG-based Solution with Your Own Data Using Azure AI Foundry

</div>

> **Source**: [Microsoft Learn — Develop a RAG-based solution with your own data using Azure AI Foundry](https://learn.microsoft.com/training/modules/build-copilot-ai-studio/)
> **Learning objectives**: Identify the need to ground your language model with Retrieval Augmented Generation (RAG), index your data with Azure AI Search to make it searchable for language models, build an agent using RAG on your own data in the Azure AI Foundry portal
> **Module units (8)**: Introduction · Understand how to ground your language model · Make your data searchable · Create a RAG-based client application · Implement RAG in a prompt flow · Exercise · Module assessment · Summary

---

## Table of Contents

1. [What is RAG? — Grounding LLMs with Your Data](#1-what-is-rag--grounding-llms-with-your-data)
2. [The RAG Workflow — Retrieve, Augment, Generate](#2-the-rag-workflow--retrieve-augment-generate)
3. [Indexes — Making Your Data Searchable](#3-indexes--making-your-data-searchable)
4. [Azure AI Search — The RAG Index Store](#4-azure-ai-search--the-rag-index-store)
5. [Data Import — Push vs Pull](#5-data-import--push-vs-pull)
6. [Agentic RAG vs Classic RAG — Choosing a Retrieval Architecture](#6-agentic-rag-vs-classic-rag--choosing-a-retrieval-architecture)
7. [Content Preparation and Relevance](#7-content-preparation-and-relevance)
8. [Building RAG in Azure AI Foundry](#8-building-rag-in-azure-ai-foundry)
9. [RAG Implementation Patterns](#9-rag-implementation-patterns)
10. [Security, Cost, and Troubleshooting](#10-security-cost-and-troubleshooting)
11. [Key Takeaways for AI-103](#11-key-takeaways-for-ai-103)

---

## 1. What is RAG? — Grounding LLMs with Your Data

**Retrieval Augmented Generation (RAG)** is a pattern that combines search with large language models (LLMs) so responses are **grounded in your data**.

LLMs are trained on public data available at training time. They don't know about:
- Your private documents or internal knowledge bases
- Frequently changing information (prices, policies, product catalogs)
- Domain-specific content not in public training data

RAG addresses this by **retrieving relevant content from your data** and including it in the model input.

### Why RAG Matters

| Problem | RAG Solution |
|---------|--------------|
| LLM hallucinations | Ground responses in real documents |
| Outdated knowledge | Retrieve current data at query time |
| No access to private data | Index and search your own documents |
| Generic responses | Provide context-specific answers |

### Key RAG Concepts

| Concept | Definition |
|---------|------------|
| **Grounding data** | Retrieved content you provide to the model to reduce guessing |
| **Index** | A data structure optimized for retrieval (keyword, semantic, vector, or hybrid search) |
| **Embeddings** | Numeric representations of content used for vector similarity search |
| **System message** | Instructions that guide how the model uses retrieved content |

### The Challenges of RAG

While conceptually simple, RAG implementations face real challenges:

| Challenge | Description |
|-----------|-------------|
| **Query understanding** | Users ask complex, conversational, or vague questions. Keyword search fails when queries don't match document terminology — retrieval must understand intent, not just match words |
| **Multi-source data access** | Enterprise content spans SharePoint, databases, blob storage, and more. Creating a unified search corpus without disrupting data operations is essential |
| **Token constraints** | LLMs accept limited token inputs. Retrieval must return highly relevant, concise results — not exhaustive document dumps |
| **Response time expectations** | Users expect AI-powered answers in seconds. Retrieval must balance thoroughness with speed |
| **Security and governance** | Opening private content to LLMs requires granular access control — users and agents must only retrieve authorized content |

> **Exam insight**: Know the difference between RAG and fine-tuning. RAG adds **fresh knowledge**; fine-tuning changes **model behavior/style**.

---

## 2. The RAG Workflow — Retrieve, Augment, Generate

RAG follows a **three-step flow**:

```
User Query → [Retrieve] → [Augment] → [Generate] → Grounded Response
                ↓              ↓            ↓
           Search Index    Build Prompt   LLM Call
```

### Step 1: Retrieve
When a user asks a question, your application queries an **index or data store** to find relevant content.

### Step 2: Augment
The app combines the **user's question** and the **retrieved content** (grounding data) into a prompt.

### Step 3: Generate
The model receives the **augmented prompt** and generates a response grounded in the retrieved content, reducing inaccuracies and enabling accurate citations.

> **Exam insight**: RAG = Retrieve → Augment → Generate. The model doesn't access your data directly — it receives retrieved content as part of the prompt.

---

## 3. Indexes — Making Your Data Searchable

RAG works best when you can retrieve relevant content **quickly and consistently**. An **index** organizes your content for efficient retrieval.

### Retrieval Modes

| Mode | How it works | Best for |
|------|--------------|----------|
| **Keyword search** | Exact term matching using inverted indexes | Known terminology, product IDs |
| **Semantic search** | Understands meaning and context | Natural language questions |
| **Vector search** | Compares embedding vectors for similarity | Conceptual/semantic queries |
| **Hybrid search** | Combines keyword + vector (sometimes + semantic ranking) | Best overall results |

### What an Index Stores

- **Searchable content** (text fields, vector embeddings)
- **Citation metadata** (document titles, URLs, file names)
- **Filterable fields** (categories, dates, permissions)

> **Exam insight**: Azure AI Search is the **recommended index store** for RAG scenarios. It supports all retrieval modes.

---

## 4. Azure AI Search — The RAG Index Store

**Azure AI Search** is a fully managed, cloud-hosted service that connects your data to AI. It's the backbone of RAG in Azure.

### Core Capabilities

| Capability | Description |
|------------|-------------|
| **Full-text search** | Keyword matching with Lucene syntax |
| **Vector search** | Embedding-based similarity search |
| **Hybrid search** | Combined keyword + vector retrieval |
| **Multimodal search** | Search across text and images |
| **AI enrichment** | Chunk, vectorize, and transform raw content |
| **Agentic retrieval** | LLM-assisted multi-query pipeline |

### Pricing Models

| Model | Billing | Best for |
|-------|---------|----------|
| **Dedicated** | Fixed hourly (Search Units) | Steady, predictable workloads |
| **Serverless** | Consumption-based (CU/hr + storage) | Infrequent, bursty workloads |

### Supported Data Sources

| Source | Type |
|--------|------|
| Azure Blob Storage | Object storage |
| Azure Cosmos DB | NoSQL database |
| Azure SQL Database | Relational database |
| SharePoint (M365) | Documents |
| OneLake | Lakehouse storage |

### Choosing Between Agentic Retrieval and Classic RAG

| Use **agentic retrieval** when… | Use **classic RAG** when… |
|--------------------------------|---------------------------|
| Your client is an agent or chatbot | You need generally available (GA) features only |
| You need the highest possible relevance and accuracy | Simplicity and speed are priorities over advanced relevance |
| Your queries are complex or conversational | You have existing orchestration code you want to preserve |
| You want structured responses with citations and query details | You need fine-grained control over the query pipeline |
| You're building **new** RAG implementations | |

> **Exam insight**: Azure AI Search supports both **classic search** (single index, predictable queries) and **agentic retrieval** (multi-query, LLM-assisted planning). Microsoft recommends **agentic retrieval for new RAG builds**; classic RAG for GA features, simplicity, and existing orchestration.

---

## 5. Data Import — Push vs Pull

Azure AI Search supports two methods for populating an index:

### Push Method

| Aspect | Details |
|--------|---------|
| **How** | Upload documents via REST API or SDK |
| **Control** | Full control over data, timing, and format |
| **Batch size** | Up to 1,000 documents or 16 MB per batch |
| **Best for** | Real-time sync, custom data sources |

**Indexing Actions**:
- **Upload**: Insert new or replace existing document
- **Merge**: Update existing document (fails if not found)
- **MergeOrUpload**: Merge if exists, upload if new
- **Delete**: Remove document from index

### Pull Method

| Aspect | Details |
|--------|---------|
| **How** | Use indexers + Logic Apps workflows |
| **Automation** | Scheduled refresh, change tracking |
| **Supports** | AI enrichment, integrated vectorization |
| **Best for** | Supported data sources, automated pipelines |

### Knowledge Sources (Agentic Retrieval)

For **agentic retrieval**, Azure AI Search uses **knowledge sources** that **auto-generate the chunking and vectorization pipelines** for you — no need to build a custom indexer/skillset.

| Approach | Pipeline |
|----------|----------|
| **Agentic retrieval** | Use knowledge sources (auto chunking + vectorization) |
| **Classic RAG** | Use indexers and skillsets to build custom pipelines, or push pre-processed content via the push API |

> **Exam insight**: If you need **AI enrichment** or **integrated vectorization**, you MUST use the pull method (indexers). For agentic retrieval, **knowledge sources** auto-generate chunking and vectorization.

---

## 6. Agentic RAG vs Classic RAG — Choosing a Retrieval Architecture

**Agentic retrieval** (agentic RAG) is an evolution that uses a model to break down complex queries into multiple focused subqueries.

### Classic RAG vs Agentic RAG

| Aspect | Classic RAG | Agentic RAG |
|--------|-------------|-------------|
| **Query plan** | Single query | Multiple focused subqueries |
| **Execution** | Sequential | Parallel |
| **Context** | No conversation history | Context-aware (multi-turn) |
| **Response** | Flattened search results | Structured (citations, metadata, optional answer) |
| **Semantic ranking** | Optional | Built-in |

### Agentic RAG Advantages

1. **Context-aware query planning** — Uses conversation history for follow-up questions
2. **Parallel execution** — Multiple subqueries run simultaneously
3. **Structured responses** — Returns grounding data, citations, and execution metadata
4. **Built-in semantic ranking** — Filters noise, prioritizes relevant passages
5. **Optional answer synthesis** — Can include LLM-formulated answers directly

> **Exam insight**: Agentic RAG is ideal for **complex multi-turn conversations** and **enterprise scenarios** with large datasets.

### Choosing an Approach in Foundry

Foundry supports multiple patterns for working with private data. Choose based on your use case complexity and how much control you need:

| Need | Approach |
|------|----------|
| Answers grounded in **private or frequently changing data** | **RAG** |
| Change **model behavior, style, or task performance** (not fresh knowledge) | **Fine-tuning** |
| Building an **agent** that needs retrieval as a tool | **Agent tools** (e.g., File search tool for agents) |

> **Exam insight**: RAG = grounding in private data · Fine-tuning = changing behavior · Agent tools = retrieval as a tool for agents. These are complementary, not interchangeable.

---

## 7. Content Preparation and Relevance

RAG quality depends on how you prepare content for retrieval and how you query the index.

### Content Preparation

| Content challenge | How Azure AI Search helps |
|-------------------|---------------------------|
| **Large documents** | Automatic chunking (built-in or via skills) |
| **Multiple languages** | More than 50 language analyzers, multilingual vectors |
| **Images and PDFs** | OCR, image analysis, image verbalization, document extraction skills |
| **Need for similarity search** | Integrated vectorization (Azure OpenAI, Azure Vision, custom) |
| **Terminology mismatches** | Synonym maps, semantic ranking |

### Data Pipeline Steps

When indexing, each media file goes through the data pipeline:

```
Chunk → Enrich (metadata) → Embed (vectorize) → Persist (search index)
```

1. **Chunking** — break the file into semantically relevant parts, ideally one idea/concept per chunk
2. **Enrich chunks** — add metadata fields (title, summary, keywords)
3. **Embed chunks** — use an embedding model to vectorize the chunk + metadata used for vector search
4. **Persist chunks** — store the chunks in the search index

### Maximizing Relevance and Recall

During indexing:

- **Chunking** subdivides large documents so portions can be matched independently
- **Vectorization** creates the embeddings used for vector queries

On the query side, to ensure the most relevant results:

1. **Use hybrid queries** — combine keyword (nonvector) + vector search for maximum recall. A text string and its vector equivalent generate parallel queries, returning the most relevant matches from each in a unified result set
2. **Use semantic ranking** — built into agentic retrieval, optional for classic RAG
3. **Apply scoring profiles** — boost specific fields or criteria
4. **Tune vector query parameters** — vector weighting and minimum thresholds to exclude low-scoring results

> **Exam insight**: RAG quality = **content preparation** (chunking, enrichment, embedding) + **retrieval configuration** (hybrid queries, semantic ranking, scoring profiles). Poor data preparation directly impacts response quality.

---

## 8. Building RAG in Azure AI Foundry

### Getting Started with RAG in Foundry

Implementing RAG in Foundry typically follows this workflow:

1. **Prepare your data** — organize and chunk your private documents or knowledge base into searchable content
2. **Set up an index** — create an Azure AI Search index (or use another retrieval service)
3. **Connect to Foundry** — create a connection from your Foundry project to your index (represented as a project connection or an *index asset ID*)
4. **Build your RAG application** — integrate retrieval with your LLM calls using the Foundry SDK or REST APIs
5. **Test and evaluate** — verify retrieval quality and that responses are accurate and properly cited

### RAG in Foundry Portal (No-Code)

1. **Add data** to your Foundry project
2. **Create an index** (or connect to existing Azure AI Search index)
3. **Build an agent** with retrieval as a tool
4. **Test** in the playground

### RAG with the Azure OpenAI Client ("On Your Data")

The module's client application uses the **Azure OpenAI SDK** with the Chat Completions API and the **`data_sources` extension** to ground responses directly in an Azure AI Search index:

```python
from openai import AzureOpenAI

client = AzureOpenAI(
    azure_endpoint=AZURE_OPENAI_ENDPOINT,
    api_key=AZURE_OPENAI_KEY,
    api_version="2024-06-01",
)

response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Which tent is the most waterproof?"}],
    extra_body={
        "data_sources": [{
            "type": "azure_search",
            "parameters": {
                "endpoint": AZURE_SEARCH_ENDPOINT,
                "index_name": "products-index",
                "authentication": {"type": "api_key", "key": AZURE_SEARCH_KEY},
            },
        }],
    },
)
print(response.choices[0].message.content)
```

### RAG with the Foundry SDK (`azure-ai-projects`)

For a code-first approach, use the **`azure-ai-projects`** SDK with `AIProjectClient` and a `.prompty` prompt template that instructs the model to ground answers in retrieved documents:

```python
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

project = AIProjectClient.from_connection_string(
    conn_str=os.environ["AIPROJECT_CONNECTION_STRING"],
    credential=DefaultAzureCredential(),
)

# Retrieve relevant product documents from the search index
documents = get_product_documents(project, query)

# Generate a response grounded in the retrieved documents
response = project.inference.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": grounded_prompt(query, documents)}],
)
```

### RAG with Prompt Flow

```
[Embed Text] → [Vector DB Lookup] → [LLM node]
     ↓                ↓                ↓
  Embed query    Search index    Generate response
```

> **Exam insight**: Know the approaches: **Foundry Portal** (no-code), **Azure OpenAI client "on your data"** (Chat Completions `data_sources` extension), **Foundry SDK** (`azure-ai-projects` + `.prompty`), and **Prompt Flow** (visual workflow).

---

## 9. RAG Implementation Patterns

### Pattern 1: Simple RAG

```
User → Search Index → Top N Results → LLM → Response
```

**Best for**: Straightforward Q&A over a single document collection.

### Pattern 2: Multi-Index RAG

```
User → Route Query → Index A / Index B / Index C → Merge Results → LLM → Response
```

**Best for**: Multiple data sources with different schemas.

### Pattern 3: Agentic RAG

```
User → Agent → Query Planning → Parallel Subqueries → Knowledge Sources → Synthesize → Response
```

**Best for**: Complex enterprise scenarios, multi-turn conversations.

### Choosing the Right Approach

| Scenario | Approach |
|----------|----------|
| Single document collection, simple queries | Simple RAG |
| Multiple data sources, different schemas | Multi-Index RAG |
| Complex queries, multi-turn conversations | Agentic RAG |
| Agent that needs retrieval as a tool | File search tool for agents |

> **Exam insight**: Use **RAG** for grounding in private data. Use **fine-tuning** for changing model behavior. Use **agent tools** when building an agent with retrieval capabilities.

---

## 10. Security, Cost, and Troubleshooting

### Security Considerations

| Concern | Mitigation |
|---------|------------|
| **Access control** | Apply document-level security filters in Azure AI Search |
| **Authentication** | Prefer Microsoft Entra ID over API keys for production |
| **Prompt injection** | Treat retrieved content as untrusted input; use safety system messages |
| **Data leakage** | Control access to source content |

### Cost and Latency

| Factor | Impact |
|--------|--------|
| **Retrieval costs** | Querying an index adds round trips and compute |
| **Embedding costs** | Vector search requires embeddings at indexing and query time |
| **Token usage** | Retrieved passages increase input tokens |

### Common Issues and Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| **Poor retrieval quality** | Bad chunking or search config | Review chunking strategy, try hybrid search |
| **Hallucination despite grounding** | Weak prompt instructions | Add clear system message: "Answer ONLY from provided sources" |
| **Latency too high** | Large indexes, too many results | Reduce top-N, add filters, use caching |
| **Token budget exceeded** | Too many passages in context | Summarize passages, implement ranking |

> **Exam insight**: RAG quality depends on **content preparation**, **retrieval configuration**, and **prompt design**. Poor data preparation directly impacts response quality.

---

## 11. Key Takeaways for AI-103

### Must-Know Facts

1. **RAG** = Retrieve → Augment → Generate — grounds LLMs in your data
2. **Azure AI Search** is the recommended index store for RAG scenarios
3. **Four retrieval modes**: Keyword, Semantic, Vector, Hybrid
4. **Push vs Pull** — Push for real-time/custom; Pull for automated/enrichment
5. **Agentic RAG vs Classic RAG** — agentic for new builds/agents/complex queries; classic for GA features/simplicity/existing orchestration
6. **RAG challenges**: query understanding, multi-source data, token constraints, response time, security/governance
7. **Content preparation**: chunk → enrich → embed → persist; hybrid queries + semantic ranking maximize relevance
8. **Implementation paths**: Foundry Portal (no-code), Azure OpenAI client "on your data", Foundry SDK (`azure-ai-projects` + `.prompty`), Prompt Flow (visual)
9. **RAG vs Fine-tuning** — RAG adds knowledge; fine-tuning changes behavior
10. **Agent tools** — use retrieval as a tool when building an agent

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| RAG concepts | Module 1.1 (AI capabilities overview) |
| Azure AI Search | Module 3.x (Language solutions), Module 4.x (Vision) |
| Foundry SDK | Module 1.3 (Develop AI app with Foundry SDK) |
| Prompt Flow | Module 1.4 (Get started with Prompt Flow) |
| Agent with retrieval | Module 2.x (Develop AI Agents), Module 2.4 (Foundry IQ knowledge) |
| RAG vs fine-tuning decision | Module 1.6 (Fine-tune a language model) |
| Evaluation | Module 1.8 (Evaluate generative AI performance) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Updated: 2026-08-04 · Source: Microsoft Learn module via MCP*
