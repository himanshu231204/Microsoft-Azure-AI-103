# Module 1.6: Practice Questions — Fine-tune a Language Model with Azure AI Foundry

50 practice questions covering all concepts from this module. Answers at the bottom.

---

## Fine-tuning Fundamentals (Q1–Q10)

**Q1.** What is fine-tuning a language model?
- A) Training a model from scratch on new data
- B) Adapting a pretrained model to a specific task using task-specific data
- C) Changing the model's deployment region
- D) Increasing the model's token limit

**Q2.** What does fine-tuning adjust to improve task performance?
- A) The training dataset
- B) The model's weights
- C) The API endpoint
- D) The content filter settings

**Q3.** What technique does Azure OpenAI use to make fine-tuning faster and more affordable?
- A) Full retraining
- B) LoRA (Low-Rank Adaptation)
- C) Quantization
- D) Distillation only

**Q4.** How does LoRA reduce training cost?
- A) By training on fewer examples
- B) By approximating the high-rank weight matrix with a lower-rank one and fine-tuning only a small subset of important parameters
- C) By using a smaller GPU
- D) By skipping the validation step

**Q5.** What is the main benefit of fine-tuning compared to few-shot learning?
- A) It requires no training data
- B) It trains on many more examples than can fit in a prompt
- C) It is always cheaper
- D) It doesn't change model weights

**Q6.** Which of the following is NOT a benefit of fine-tuned models?
- A) Shorter prompts and token savings
- B) Lower-latency requests
- C) Higher quality results than prompt engineering alone
- D) Automatic access to fresh real-time data

**Q7.** What does "distillation" mean in the context of fine-tuning?
- A) Removing low-quality examples from the dataset
- B) Using a large model's outputs to fine-tune a smaller, more efficient model
- C) Compressing the model's weights
- D) Training with a higher learning rate

**Q8.** Why can fine-tuning reduce inference costs?
- A) The model is deployed on cheaper hardware automatically
- B) Fine-tuned models need shorter prompts, reducing tokens per request
- C) Fine-tuning disables content filtering
- D) The model caches all responses

**Q9.** Which is a valid reason to fine-tune a model?
- A) To add frequently changing private data
- B) To change the model's style and tone
- C) To eliminate the need for a search index permanently
- D) To increase the model's context window

**Q10.** What is the primary difference between fine-tuning and RAG?
- A) Fine-tuning adds knowledge; RAG changes behavior
- B) Fine-tuning changes model behavior; RAG adds fresh/private knowledge at query time
- C) They are identical approaches
- D) RAG modifies model weights; fine-tuning does not

---

## When to Fine-tune (Q11–Q20)

**Q11.** Which scenario is best suited for fine-tuning?
- A) Content that changes frequently, like news
- B) A specific task with proprietary data and stable content
- C) Broad coverage across many unrelated topics
- D) When you have no training data

**Q12.** Which scenario is best suited for RAG?
- A) A specialized task with unique data
- B) Dynamic or changing content and wide topic coverage
- C) When the base model needs style changes
- D) When you need structured output formats

**Q13.** What is the recommended dataset size to START a fine-tuning effort?
- A) 5 examples
- B) 10 examples
- C) 50 well-crafted examples
- D) 10,000 examples

**Q14.** Which use case does fine-tuning help with by embedding examples into the model?
- A) Reducing prompt engineering overhead
- B) Increasing model context window
- C) Reducing inference hardware requirements
- D) Enabling real-time data retrieval

**Q15.** Fine-tuning is especially valuable when a scenario has numerous what?
- A) Edge cases
- B) Users
- C) Models
- D) Regions

**Q16.** What is a common use case for fine-tuning models to produce structured output?
- A) Free-form creative writing
- B) Generating outputs in specific formats or schemas
- C) Translating between languages
- D) Summarizing long documents

**Q17.** When should you choose RAG over fine-tuning?
- A) When you need consistent output style
- B) When you need the most current information
- C) When you have a unique proprietary dataset
- D) When the model must follow a strict format

**Q18.** How can fine-tuning enhance tool usage?
- A) It increases the number of tools available
- B) It improves accuracy and consistency of tool calling, even without full tool definitions
- C) It removes the need for function definitions entirely
- D) It makes tool calls faster

**Q19.** Which combination is often recommended for best performance?
- A) Fine-tuning alone, no RAG
- B) RAG alone, no fine-tuning
- C) Combining fine-tuning with retrieval to better use retrieved data
- D) Neither — always use prompt engineering

**Q20.** If your task doesn't need constant updates and you have unique domain data, what should you choose?
- A) RAG
- B) Fine-tuning
- C) Prompt engineering only
- D) Web search integration

---

## Training Methods (Q21–Q28)

**Q21.** Which training method is supported by all non-reasoning models?
- A) DPO
- B) RFT
- C) SFT (Supervised Fine-tuning)
- D) CPT

**Q22.** Which training method is supported by reasoning models like o4-mini?
- A) SFT
- B) RFT (Reinforcement Fine-tuning)
- C) DPO
- D) LoRA only

**Q23.** Which training method uses chosen vs rejected response pairs?
- A) SFT
- B) DPO (Direct Preference Optimization)
- C) RFT
- D) Continued pretraining

**Q24.** DPO is supported by which model family?
- A) GPT-4o
- B) Llama 4
- C) Phi-3
- D) Mistral

**Q25.** In DPO, what does the `beta` hyperparameter control?
- A) The batch size
- B) How much the model can drift from the reference model
- C) The number of epochs
- D) The learning rate multiplier

**Q26.** What does RFT use to evaluate model outputs during training?
- A) Human reviewers only
- B) Graders
- C) The validation set only
- D) Rule-based regex

**Q27.** Which of the following is an RFT-specific hyperparameter?
- A) batch_size
- B) n_epochs
- C) reasoning_effort
- D) seed

**Q28.** Which statement is true about training methods?
- A) All models support all training methods
- B) Not all models support all training methods
- C) DPO is supported by all models
- D) RFT is only for non-reasoning models

---

## Data Preparation (Q29–Q38)

**Q29.** What file format is required for fine-tuning training data?
- A) CSV
- B) JSONL (JSON Lines)
- C) Parquet
- D) XML

**Q30.** Which API's conversational format must the data use?
- A) Completion API
- B) Chat Completions API
- C) Embeddings API
- D) Fine-tuning API

**Q31.** What encoding is required for training data files?
- A) UTF-8 with a byte-order mark (BOM)
- B) ASCII
- C) UTF-16
- D) Base64

**Q32.** What is the maximum file size for training/validation data?
- A) 100 MB
- B) 512 MB
- C) 1 GB
- D) 10 MB

**Q33.** What are the three allowed roles in a chat-format message?
- A) user, bot, admin
- B) system, user, assistant
- C) prompt, response, context
- D) input, output, error

**Q34.** What rule applies to the last message in each training conversation?
- A) It must be a user message
- B) It must be an assistant message
- C) It can be any role
- D) It must be a system message

**Q35.** What does the optional `weight` key/value pair do?
- A) Increases the model's learning rate
- B) Skips fine-tuning on specific assistant messages
- C) Changes the response length
- D) Sets the number of epochs

**Q36.** What values can the `weight` parameter take?
- A) Any number
- B) 0 or 1
- C) Only 1
- D) 0.5 only

**Q37.** Why should you include your best instructions/prompts in every training example?
- A) To increase file size
- B) To get the best results, especially with fewer than 100 examples
- C) To speed up training
- D) To reduce the token limit

**Q38.** Which models support vision fine-tuning with images in JSONL?
- A) gpt-4o (2024-08-06) and gpt-4.1 (2025-04-14)
- B) Only Llama models
- C) Phi-3 only
- D) All models

---

## Dataset Size and Quality (Q39–Q42)

**Q39.** What is the MINIMUM number of training examples for a fine-tuning job to proceed?
- A) 5
- B) 10
- C) 50
- D) 100

**Q40.** What happens if you train with only 10 examples?
- A) The job fails
- B) The model is noticeably improved
- C) The job runs but won't noticeably influence model responses
- D) The job automatically generates more data

**Q41.** What is the effect of doubling the dataset size?
- A) No effect on quality
- B) Can lead to a linear increase in model quality
- C) Always halves training time
- D) Guarantees the model improves

**Q42.** What can happen if you train on a large amount of low-quality data?
- A) The model performs better than expected
- B) The model can perform much worse than expected
- C) Nothing changes
- D) Training automatically stops

---

## Portal Workflow and Hyperparameters (Q43–Q50)

**Q43.** In the Azure AI Foundry portal, where do you start fine-tuning?
- A) Deployments → New deployment
- B) Fine-tuning → + Fine-tune model
- C) Models → Train
- D) Evaluation → Create job

**Q44.** What does the `suffix` parameter do?
- A) Sets the learning rate
- B) Identifies the fine-tuned model (up to 18 characters appended to the name)
- C) Defines the training region
- D) Controls the batch size

**Q45.** Which hyperparameter controls reproducibility of a fine-tuning job?
- A) batch_size
- B) seed
- C) n_epochs
- D) beta

**Q46.** What is the recommended range for `learning_rate_multiplier`?
- A) 0.02 to 0.2
- B) 1 to 10
- C) 0.5 to 0.9
- D) 100 to 1000

**Q47.** When `batch_size` is set to -1, how is it calculated?
- A) Fixed at 128
- B) 0.2% of examples in the training set (max 256)
- C) Equal to the number of epochs
- D) Half the file size

**Q48.** Which training tier guarantees data residency?
- A) Global
- B) Developer
- C) Standard
- D) Free

**Q49.** Which training tier uses idle capacity and may preempt jobs?
- A) Standard
- B) Global
- C) Developer
- D) Premium

**Q50.** What is required for automatic deployment of a fine-tuned model?
- A) A valid API key only
- B) Foundry Owner role or deployments/write permission; OpenAI models only
- C) A subscription with Enterprise Agreement
- D) At least 1000 training examples

---

## Answers

| Q | Answer | Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|--------|---|--------|---|--------|---|--------|---|--------|
| 1 | B | 11 | B | 21 | C | 31 | A | 41 | B |
| 2 | B | 12 | B | 22 | B | 32 | B | 42 | B |
| 3 | B | 13 | C | 23 | B | 33 | B | 43 | B |
| 4 | B | 14 | A | 24 | A | 34 | B | 44 | B |
| 5 | B | 15 | A | 25 | B | 35 | B | 45 | B |
| 6 | D | 16 | B | 26 | B | 36 | B | 46 | A |
| 7 | B | 17 | B | 27 | C | 37 | B | 47 | B |
| 8 | B | 18 | B | 28 | B | 38 | A | 48 | C |
| 9 | B | 19 | C | 29 | B | 39 | B | 49 | C |
| 10 | B | 20 | B | 30 | B | 40 | C | 50 | B |

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module content*
