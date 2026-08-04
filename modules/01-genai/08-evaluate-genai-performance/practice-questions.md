# Module 1.8: Practice Questions — Evaluate Generative AI Performance

50 practice questions covering all concepts from this module. Answers at the bottom.

---

## Why Evaluation Matters (Q1–Q5)

**Q1.** What are the two primary reasons to evaluate a generative AI app?
- A) Cost reduction and faster deployment
- B) Quality assurance and continuous improvement
- C) Marketing and branding
- D) Compliance and licensing

**Q2.** How does evaluation contribute to user satisfaction?
- A) By reducing the number of users
- B) By ensuring the app provides accurate and relevant responses
- C) By increasing token usage
- D) By disabling content filters

**Q3.** What is the iterative nature of evaluation?
- A) Evaluate once before deployment only
- B) Build → evaluate → improve → re-evaluate
- C) Deploy → forget → redeploy
- D) Test only after production issues arise

**Q4.** Which of the following best describes the purpose of continuous improvement through evaluation?
- A) To keep the app unchanged over time
- B) To identify areas for enhancement and iteratively improve performance
- C) To reduce the number of test prompts
- D) To eliminate human involvement

**Q5.** What does quality assurance in evaluation primarily ensure?
- A) The app is cheap to run
- B) The app provides accurate and relevant responses
- C) The app uses the newest model
- D) The app has no user interface

---

## What You Can Evaluate — Models and Chat Flows (Q6–Q10)

**Q6.** At which level can you evaluate an individual language model?
- A) By analyzing the input, the output, and optionally comparing to a predefined expected output
- B) By only analyzing the training data
- C) By only analyzing the model's parameters
- D) By only analyzing the deployment region

**Q7.** What is a chat flow in the context of generative AI apps?
- A) A single language model call
- B) An orchestrated executable flow that can combine multiple language models and Python code
- C) A database query
- D) A content filter

**Q8.** When evaluating a chat flow, what can you assess?
- A) Only the final output
- B) The complete flow and its individual components
- C) Only the input prompts
- D) Only the Python code

**Q9.** What is the recommended evaluation progression?
- A) Test the complete chat flow first, then the individual model
- B) Start with testing an individual model, then test the complete chat flow
- C) Only test the chat flow
- D) Only test the individual model

**Q10.** Which of the following is NOT a valid evaluation target in the Foundry portal?
- A) A deployed model
- B) A prompt flow
- C) A dataset of preexisting outputs
- D) A virtual machine

---

## Model Benchmarks (Q11–Q20)

**Q11.** What are model benchmarks?
- A) Private metrics only visible to your team
- B) Publicly available metrics across models and datasets
- C) Metrics computed only after deployment
- D) Metrics based on user feedback

**Q12.** What is the primary purpose of model benchmarks?
- A) To evaluate your app's production traffic
- B) To understand how a model performs relative to others
- C) To replace manual evaluations
- D) To measure content safety

**Q13.** Which benchmark metric returns 1 if generated text matches the answer exactly and 0 otherwise?
- A) Coherence
- B) Fluency
- C) Accuracy
- D) GPT similarity

**Q14.** Which benchmark metric measures whether output flows smoothly and reads naturally?
- A) Accuracy
- B) Coherence
- C) GPT similarity
- D) F1 score

**Q15.** Which benchmark metric assesses adherence to grammatical rules and syntactic structures?
- A) Fluency
- B) Accuracy
- C) GPT similarity
- D) ROUGE

**Q16.** Which benchmark metric quantifies semantic similarity between a ground truth sentence and the AI-generated prediction?
- A) Accuracy
- B) Coherence
- C) GPT similarity
- D) BLEU

**Q17.** Where can you explore model benchmarks for all available models in the Foundry portal?
- A) After deploying a model
- B) Before deploying a model
- C) Only in production
- D) Only in the SDK

**Q18.** Which statement about model benchmarks is TRUE?
- A) They are computed from your own app's traffic
- B) They are public, comparative metrics used to compare models against each other
- C) They replace the need for manual evaluation
- D) They measure content safety only

**Q19.** Which of the following is a commonly used model benchmark?
- A) Groundedness
- B) GPT similarity
- C) Relevance
- D) Self-harm

**Q20.** Model benchmarks are most useful for which decision?
- A) Choosing which model to deploy
- B) Choosing which content filter to apply
- C) Choosing which region to deploy in
- D) Choosing which test dataset to use

---

## Manual Evaluations (Q21–Q30)

**Q21.** Who performs manual evaluations?
- A) Automated scripts
- B) Human raters
- C) GPT models
- D) NLP algorithms

**Q22.** What insights can manual evaluations provide that automated metrics might miss?
- A) Token counts
- B) Context relevance and user satisfaction
- C) Latency measurements
- D) Cost per request

**Q23.** Which criteria can human evaluators use to rate responses?
- A) Relevance, informativeness, and engagement
- B) Token count and latency
- C) CPU usage and memory
- D) Region and pricing

**Q24.** What should you prepare before beginning manual evaluation?
- A) A diverse set of test prompts
- B) A production deployment
- C) A content filter
- D) A billing report

**Q25.** Which prompt categories should your test prompts cover?
- A) Common user questions, edge cases, and potential failure points
- B) Only common user questions
- C) Only edge cases
- D) Only failure points

**Q26.** What is the chat playground ideal for?
- A) Production monitoring
- B) Early development — testing prompts and tweaking system messages
- C) Final deployment
- D) Cost optimization

**Q27.** In the chat playground, what can you tweak to improve the model's response?
- A) The prompt or system message
- B) The deployment region
- C) The subscription
- D) The content filter severity

**Q28.** What does the manual evaluations feature allow you to do?
- A) Upload a dataset with multiple questions and optionally expected responses
- B) Deploy the model to production
- C) Create a new subscription
- D) Generate billing reports

**Q29.** How do you rate model responses in the manual evaluations feature?
- A) With a thumbs up or down feature
- B) With a numeric score from 1 to 100
- C) With a star rating out of 10
- D) With a pass/fail boolean

**Q30.** Based on manual evaluation ratings, which of the following can you change to improve the model?
- A) Input prompt, system message, model, or model parameters
- B) Deployment region only
- C) Subscription tier only
- D) Content filter category only

---

## Automated Evaluations (Q31–Q40)

**Q31.** What can automated evaluations assess in the Foundry portal?
- A) Quality and content safety performance of models, datasets, or prompt flows
- B) Only model latency
- C) Only infrastructure cost
- D) Only user interface design

**Q32.** What data is needed to evaluate a model?
- A) A dataset of prompts and responses, optionally with ground truth
- B) Only a list of model names
- C) Only deployment regions
- D) Only billing data

**Q33.** Which of the following is a way to compile evaluation data?
- A) Manual compilation, existing application output, or AI-generated data
- B) Only manual compilation
- C) Only existing application output
- D) Only AI-generated data

**Q34.** How can AI-generated evaluation data be used?
- A) Generate prompts/responses, then edit them to reflect desired output and use as ground truth
- B) Use them directly without editing
- C) Use them only for production traffic
- D) Use them only for billing

**Q35.** Which evaluator category measures the quality of responses using AI models and standard NLP metrics?
- A) Risk and Safety
- B) AI Quality
- C) Protected material
- D) Groundedness

**Q36.** Which evaluator category assesses responses for content safety issues?
- A) AI Quality
- B) Risk and Safety
- C) Coherence
- D) Fluency

**Q37.** Which of the following is a Risk and Safety concern?
- A) Coherence
- B) Violence
- C) Fluency
- D) Similarity

**Q38.** Which of the following is an AI Quality metric?
- A) Self-harm
- B) Relevance
- C) Hate
- D) Sexual content

**Q39.** Which evaluator compares generated responses to ground truth based on standard metrics?
- A) Coherence
- B) F1 Score
- C) Protected material
- D) Fluency

**Q40.** Which evaluator metric uses an AI model to judge the structure and logical flow of ideas in a response?
- A) F1 Score
- B) Coherence
- C) Protected material
- D) Accuracy

---

## AI-Assisted and NLP Metrics (Q41–Q50)

**Q41.** What does groundedness evaluate?
- A) How well generated answers align with information from the input source
- B) How grammatically correct the response is
- C) How similar the response is to ground truth
- D) How fast the response is generated

**Q42.** Even if an answer is factually correct, when is it scored as ungrounded?
- A) When it is not verifiable against the source/context
- B) When it is too long
- C) When it uses complex vocabulary
- D) When it is generated quickly

**Q43.** Which metric requires context data in addition to prompt and completion?
- A) Coherence
- B) Fluency
- C) Groundedness
- D) Similarity

**Q44.** Which metric requires ground truth data in addition to prompt and completion?
- A) Coherence
- B) Fluency
- C) Groundedness
- D) Similarity

**Q45.** Which metrics require only prompt and completion (no context or ground truth)?
- A) Coherence and Fluency
- B) Groundedness and Relevance
- C) Similarity and Groundedness
- D) Relevance and Similarity

**Q46.** What does the F1-score measure?
- A) The ratio of shared words between generated and ground truth answers
- B) The latency of the response
- C) The cost of the response
- D) The number of tokens in the prompt

**Q47.** Which NLP metric is most associated with translation evaluation?
- A) ROUGE
- B) BLEU
- C) F1 score
- D) Accuracy

**Q48.** Which NLP metric is most associated with summarization evaluation?
- A) BLEU
- B) METEOR
- C) ROUGE
- D) GPT similarity

**Q49.** What is required for AI-assisted quality evaluations in the Foundry portal?
- A) A deployed GPT evaluator model and an Azure OpenAI connection
- B) A virtual machine
- C) A content filter
- D) A billing account only

**Q50.** How can evaluation results be viewed in the Foundry portal?
- A) As aggregate metrics and sample-level metrics, comparable across runs
- B) Only as a single overall score
- C) Only as raw logs
- D) Only as a pass/fail result

---

## Answers

| Q | Answer | Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|--------|---|--------|---|--------|---|--------|---|--------|
| 1 | B | 11 | B | 21 | B | 31 | A | 41 | A |
| 2 | B | 12 | B | 22 | B | 32 | A | 42 | A |
| 3 | B | 13 | C | 23 | A | 33 | A | 43 | C |
| 4 | B | 14 | B | 24 | A | 34 | A | 44 | D |
| 5 | B | 15 | A | 25 | A | 35 | B | 45 | A |
| 6 | A | 16 | C | 26 | B | 36 | B | 46 | A |
| 7 | B | 17 | B | 27 | A | 37 | B | 47 | B |
| 8 | B | 18 | B | 28 | A | 38 | B | 48 | C |
| 9 | B | 19 | B | 29 | A | 39 | B | 49 | A |
| 10 | D | 20 | A | 30 | A | 40 | B | 50 | A |

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module content*