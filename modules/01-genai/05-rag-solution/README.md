<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.5: Develop a RAG-based Solution with Your Own Data Using Azure AI Foundry

</div>

> **Source**: [Microsoft Learn — Develop a RAG-based solution with your own data using Azure AI Foundry](https://learn.microsoft.com/training/modules/build-copilot-ai-studio/)
> **Learning objectives**: Identify the need to ground your language model with RAG, index your data with Azure AI Search, build an agent using RAG on your own data in Azure AI Foundry portal

---

## Table of Contents

1. [What is RAG? — Grounding LLMs with Your Data](#1-what-is-rag--grounding-llms-with-your-data)
2. [The RAG Workflow — Retrieve, Augment, Generate](#2-the-rag-workflow--retrieve-augment-generate)
3. [Indexes — Making Your Data Searchable](#3-indexes--making-your-data-searchable)
4. [Azure AI Search — The RAG Index Store](#4-azure-ai-search--the-rag-index-store)
5. [Data Import — Push vs Pull](#5-data-import--push-vs-pull)
6. [Agentic RAG — Modern Retrieval Architecture](#6-agentic-rag--modern-retrieval-architecture)
7. [Building RAG in Azure AI Foundry](#7-building-rag-in-azure-ai-foundry)
8. [RAG Implementation Patterns](#8-rag-implementation-patterns)
9. [Security, Cost, and Troubleshooting](#9-security-cost-and-troubleshooting)
10. [Key Takeaways for AI-103](#10-key-takeaways-for-ai-103)

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

> **Exam insight**: Azure AI Search supports both **classic search** (single index, predictable queries) and **agentic retrieval** (multi-query, LLM-assisted planning).

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

> **Exam insight**: If you need **AI enrichment** or **integrated vectorization**, you MUST use the pull method (indexers).

---

## 6. Agentic RAG — Modern Retrieval Architecture

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

---

## 7. Building RAG in Azure AI Foundry

### RAG in Foundry Portal (No-Code)

1. **Add data** to your Foundry project
2. **Create an index** (or connect to existing Azure AI Search index)
3. **Build an agent** with retrieval as a tool
4. **Test** in the playground

### RAG with Foundry SDK (Code)

```python
from azure.identity import DefaultAzureCredential
from azure.search.documents import SearchClient
from openai import AzureOpenAI

# Connect to Azure AI Search
search_client = SearchClient(
    endpoint=AZURE_SEARCH_SERVICE,
    index_name="your-index",
    credential=DefaultAzureCredential()
)

# Connect to Azure OpenAI
openai_client = AzureOpenAI(
    api_version="2024-06-01",
    azure_endpoint=AZURE_OPENAI_ACCOUNT,
    azure_ad_token_provider=token_provider
)

# RAG workflow
query = "What products do you offer?"

# Step 1: Retrieve relevant documents
search_results = search_client.search(
    search_text=query,
    top=5,
    select=["ProductName", "Description", "Category"]
)

# Step 2: Format grounding data
sources = "\n".join([
    f"{doc['ProductName']}: {doc['Description']}"
    for doc in search_results
])

# Step 3: Generate grounded response
response = openai_client.chat.completions.create(
    messages=[{
        "role": "user",
        "content": f"Answer using only these sources:\n{sources}\n\nQuery: {query}"
    }],
    model="gpt-4"
)

print(response.choices[0].message.content)
```

### RAG with Prompt Flow

```
[Embed Text] → [Vector DB Lookup] → [LLM node]
     ↓                ↓                ↓
  Embed query    Search index    Generate response
```

> **Exam insight**: Know the three approaches: **Foundry Portal** (no-code), **Foundry SDK** (code), and **Prompt Flow** (visual workflow).

---

## 8. RAG Implementation Patterns

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

## 9. Security, Cost, and Troubleshooting

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

## 10. Key Takeaways for AI-103

### Must-Know Facts

1. **RAG** = Retrieve → Augment → Generate — grounds LLMs in your data
2. **Azure AI Search** is the recommended index store for RAG scenarios
3. **Four retrieval modes**: Keyword, Semantic, Vector, Hybrid
4. **Push vs Pull** — Push for real-time/custom; Pull for automated/enrichment
5. **Agentic RAG** = modern approach with parallel subqueries and context awareness
6. **Three implementation paths**: Foundry Portal (no-code), Foundry SDK (code), Prompt Flow (visual)
7. **RAG vs Fine-tuning** — RAG adds knowledge; fine-tuning changes behavior

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| RAG concepts | Module 1.1 (AI capabilities overview) |
| Azure AI Search | Module 3.x (Language solutions), Module 4.x (Vision) |
| Foundry SDK | Module 1.3 (Develop AI app with Foundry SDK) |
| Prompt Flow | Module 1.4 (Get started with Prompt Flow) |
| Agent with retrieval | Module 2.x (Develop AI Agents) |
| Evaluation | Module 1.8 (Evaluate generative AI performance) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*
