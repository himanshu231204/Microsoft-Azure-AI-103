# Module 1.5: Practice Questions — Develop a RAG-based Solution with Your Own Data Using Azure AI Foundry

50 practice questions covering all concepts from this module. Answers at the bottom.

---

## RAG Fundamentals (Q1–Q10)

**Q1.** What does RAG stand for?
- A) Retrieval Augmented Generation
- B) Rapid Application Generation
- C) Resource-Augmented Gateway
- D) Real-time Analytics Gateway

**Q2.** What is the primary purpose of RAG?
- A) To fine-tune a model on custom data
- B) To ground LLM responses in your own data
- C) To deploy models to edge devices
- D) To generate training data for models

**Q3.** What are the three steps in the RAG workflow?
- A) Train, Deploy, Monitor
- B) Retrieve, Augment, Generate
- C) Index, Query, Respond
- D) Embed, Search, Answer

**Q4.** What is "grounding data" in a RAG context?
- A) The initial training data for the LLM
- B) Retrieved content provided to the model to reduce guessing
- C) The system message configuration
- D) The embedding model weights

**Q5.** Why is RAG preferred over using an LLM alone for private data?
- A) RAG is cheaper to run
- B) LLMs don't know private or frequently changing information
- C) RAG eliminates all hallucinations
- D) RAG requires no index

**Q6.** What is the role of an "index" in RAG?
- A) It stores model weights
- B) It organizes content for efficient retrieval
- C) It fine-tunes the LLM
- D) It generates embeddings

**Q7.** Which of the following is NOT a retrieval mode supported by Azure AI Search?
- A) Keyword search
- B) Semantic search
- C) Vector search
- D) Audio search

**Q8.** What are "embeddings" in the context of RAG?
- A) API keys for authentication
- B) Numeric representations of content for vector similarity search
- C) Configuration files for the index
- D) System messages for the LLM

**Q9.** In the RAG workflow, when does the "augment" step occur?
- A) Before the user asks a question
- B) After the model generates a response
- C) After retrieval, when the query and retrieved content are combined into a prompt
- D) During the indexing phase

**Q10.** What problem does RAG solve that fine-tuning does NOT?
- A) Changing model behavior and style
- B) Providing access to frequently changing or private data
- C) Reducing model latency
- D) Improving model accuracy on classification tasks

---

## Azure AI Search (Q11–Q20)

**Q11.** What is Azure AI Search?
- A) A web search engine for Azure documentation
- B) A fully managed cloud service that connects your data to AI
- C) A CDN for static content
- D) A load balancer for API calls

**Q12.** Which search mode combines keyword + vector retrieval?
- A) Semantic search
- B) Hybrid search
- C) Full-text search
- D) Agentic search

**Q13.** What are the two pricing models for Azure AI Search?
- A) Free and Premium
- B) Dedicated and Serverless
- C) Standard and Enterprise
- D) Basic and Advanced

**Q14.** Which pricing model is best for infrequent, bursty workloads?
- A) Dedicated
- B) Serverless
- C) Premium
- D) Enterprise

**Q15.** What is "AI enrichment" in Azure AI Search?
- A) Encrypting data at rest
- B) Chunking, vectorizing, and transforming raw content
- C) Load balancing across replicas
- D) Monitoring query performance

**Q16.** Which of the following is a supported data source for Azure AI Search indexers?
- A) Azure Blob Storage
- B) AWS S3
- C) Google Cloud Storage
- D) Dropbox

**Q17.** What is the difference between "classic search" and "agentic retrieval"?
- A) Classic search uses vector embeddings; agentic does not
- B) Classic search targets a single index; agentic retrieval uses knowledge bases with LLM-assisted planning
- C) Classic search is faster; agentic retrieval is slower
- D) There is no difference

**Q18.** What does "semantic ranking" do in Azure AI Search?
- A) Sorts results alphabetically
- B) Filters noise and prioritizes truly relevant passages based on meaning
- C) Removes duplicate documents
- D) Compresses index size

**Q19.** Which Azure AI Search feature is required for agentic retrieval?
- A) Knowledge base
- B) Blob indexer
- C) Semantic config
- D) Shared private link

**Q20.** What is the maximum batch size when pushing documents to Azure AI Search?
- A) 100 documents or 1 MB
- B) 500 documents or 8 MB
- C) 1,000 documents or 16 MB
- D) 5,000 documents or 64 MB

---

## Data Import (Q21–Q25)

**Q21.** When should you use the "push" method for data import?
- A) When you need automated scheduling
- B) When you need real-time sync or custom data sources
- C) When using AI enrichment
- D) When using integrated vectorization

**Q22.** What is the difference between "merge" and "mergeOrUpload" indexing actions?
- A) No difference
- B) Merge fails if document doesn't exist; mergeOrUpload creates it if new
- C) MergeOrUpload is slower
- D) Merge always creates new documents

**Q23.** Which method MUST you use if you need AI enrichment or integrated vectorization?
- A) Push method
- B) Pull method (indexers)
- C) REST API
- D) Portal only

**Q24.** What does an indexer do in Azure AI Search?
- A) Queries the search index
- B) Automatically pulls data from a source and loads it into an index
- C) Creates embedding vectors
- D) Manages user permissions

**Q25.** Which indexing action removes a document from the index?
- A) Upload
- B) Merge
- C) Delete
- D) MergeOrUpload

---

## Agentic RAG (Q26–Q30)

**Q26.** What is agentic retrieval (agentic RAG)?
- A) A single-query retrieval approach
- B) A multi-query pipeline using LLM-assisted planning and parallel execution
- C) A manual retrieval process
- D) A retrieval method that doesn't use indexes

**Q27.** What advantage does agentic RAG have over classic RAG for multi-turn conversations?
- A) It's cheaper
- B) It uses conversation history for context-aware query planning
- C) It requires fewer resources
- D) It doesn't need an index

**Q28.** How does agentic RAG handle complex queries?
- A) Sends the entire query to one index
- B) Breaks down into multiple focused subqueries and runs them in parallel
- C) Only uses keyword search
- D) Ignores the query complexity

**Q29.** What does agentic RAG return in its response?
- A) Only the answer text
- B) Grounding data, citations, execution metadata, and optional LLM-formulated answer
- C) Raw database records
- D) Just the search score

**Q30.** When is agentic RAG most appropriate?
- A) Simple Q&A over a small document set
- B) Complex enterprise scenarios with large datasets and multi-turn conversations
- C) Real-time streaming applications
- D) Edge deployment scenarios

---

## Building RAG in Foundry (Q31–Q35)

**Q31.** What are the three implementation paths for RAG in Azure AI Foundry?
- A) Portal, SDK, and CLI
- B) Portal (no-code), SDK (code), and Prompt Flow (visual)
- C) Python, C#, and Java
- D) REST API, gRPC, and WebSocket

**Q32.** In a Prompt Flow RAG workflow, what are the three main nodes?
- A) Input, Process, Output
- B) Embed Text, Vector DB Lookup, LLM node
- C) Query, Search, Respond
- D) Connect, Retrieve, Generate

**Q33.** Which SDK is used to connect to Azure AI Search from Python?
- A) azure-ai-search
- B) azure-search-documents
- C) azure-cognitiveservices-search
- D) azure-index-sdk

**Q34.** In the Foundry Portal, how do you add RAG capabilities to an agent?
- A) Write custom code
- B) Add data and create an index, then enable retrieval as a tool
- C) Deploy a new model
- D) Create a new project

**Q35.** What is the recommended approach when building an agent that needs retrieval as a tool?
- A) Use fine-tuning
- B) Use the File search tool for agents
- C) Hard-code the responses
- D) Use a web search API

---

## RAG Patterns (Q36–Q40)

**Q36.** Which RAG pattern is best for a single document collection with simple queries?
- A) Multi-Index RAG
- B) Simple RAG
- C) Agentic RAG
- D) Hybrid RAG

**Q37.** In a Multi-Index RAG pattern, what happens to the query?
- A) It's sent to all indexes simultaneously
- B) It's routed to the appropriate index(es) based on the query type
- C) It's only sent to the first index
- D) It's ignored

**Q38.** When should you use fine-tuning instead of RAG?
- A) When you need answers grounded in private data
- B) When you need to change model behavior, style, or task performance
- C) When you need real-time data
- D) When you have no training data

**Q39.** What is the key difference between RAG and fine-tuning?
- A) RAG changes model behavior; fine-tuning adds knowledge
- B) RAG adds knowledge; fine-tuning changes model behavior
- C) They are the same thing
- D) RAG is only for text; fine-tuning is for images

**Q40.** In a RAG system, what should you instruct the model to do when the answer isn't in the retrieved context?
- A) Make up an answer
- B) Say "I don't know"
- C) Search the internet
- D) Return an error

---

## Security and Production (Q41–Q45)

**Q41.** What authentication method is recommended for production RAG systems?
- A) API keys
- B) Microsoft Entra ID
- C) Basic auth
- D) No authentication

**Q42.** How should you treat retrieved content in a RAG system?
- A) As trusted input
- B) As untrusted input (risk of prompt injection)
- C) As encrypted data
- D) As temporary data

**Q43.** What is document-level access control in Azure AI Search?
- A) Encrypting documents at rest
- B) Security filters that control which documents a user can see
- C) Compressing documents
- D) Deleting documents after access

**Q44.** Why do retrieved passages increase costs?
- A) They require more storage
- B) They increase input tokens, which increases LLM API costs
- C) They require additional Azure subscriptions
- D) They increase network bandwidth

**Q45.** What should you do if your RAG system has latency issues?
- A) Use a larger model
- B) Reduce top-N results, add filters, use caching
- C) Add more documents to the index
- D) Disable vector search

---

## Troubleshooting (Q46–Q50)

**Q46.** If your index isn't returning relevant passages, what should you review?
- A) Model temperature
- B) Chunking strategy, embedding model quality, and search configuration
- C) API endpoint URL
- D) User authentication

**Q47.** What causes "hallucination despite grounding" in RAG?
- A) Too many documents in the index
- B) Weak prompt instructions that don't tell the model to stick to retrieved content
- C) Using vector search instead of keyword search
- D) Having too few embeddings

**Q48.** How can you prevent the model from exceeding token limits with retrieved passages?
- A) Increase the token limit
- B) Implement passage filtering, ranking, or summarization
- C) Use a smaller embedding model
- D) Reduce the number of queries

**Q49.** If your RAG responses are inaccurate despite good retrieval, what is the likely cause?
- A) Poor prompt design
- B) The index is empty
- C) The model is too old
- D) The data source is disconnected

**Q50.** What is the relationship between data preparation quality and RAG response quality?
- A) No relationship
- B) Poor data preparation directly impacts response quality
- C) Data preparation only affects indexing speed
- D) Data preparation is optional for RAG

---

## Answers

| Q | Answer | Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|--------|---|--------|---|--------|---|--------|---|--------|
| 1 | A | 11 | B | 21 | B | 31 | B | 41 | B |
| 2 | B | 12 | B | 22 | B | 32 | B | 42 | B |
| 3 | B | 13 | B | 23 | B | 33 | B | 43 | B |
| 4 | B | 14 | B | 24 | B | 34 | B | 44 | B |
| 5 | B | 15 | B | 25 | C | 35 | B | 45 | B |
| 6 | B | 16 | A | 26 | B | 36 | B | 46 | B |
| 7 | D | 17 | B | 27 | B | 37 | B | 47 | B |
| 8 | B | 18 | B | 28 | B | 38 | B | 48 | B |
| 9 | C | 19 | A | 29 | B | 39 | B | 49 | A |
| 10 | B | 20 | C | 30 | B | 40 | B | 50 | B |

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module content*
