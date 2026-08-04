# Module 1.7: Practice Questions — Implement a Responsible Generative AI Solution

50 practice questions covering all concepts from this module. Answers at the bottom.

---

## The Responsible AI Process (Q1–Q10)

**Q1.** What is the four-stage process for responsible generative AI solution development?
- A) Plan, Build, Test, Deploy
- B) Map, Measure, Mitigate, Manage
- C) Identify, Analyze, Fix, Monitor
- D) Design, Develop, Validate, Release

**Q2.** Which external framework do the responsible AI stages correspond closely to?
- A) ISO 27001
- B) NIST AI Risk Management Framework
- C) GDPR
- D) SOC 2

**Q3.** During which stage do you identify and prioritize potential harms?
- A) Measure
- B) Mitigate
- C) Map
- D) Manage

**Q4.** During which stage do you quantify the presence of harms in generated outputs?
- A) Map
- B) Measure
- C) Mitigate
- D) Manage

**Q5.** During which stage do you apply content filters and guardrails?
- A) Map
- B) Measure
- C) Mitigate
- D) Manage

**Q6.** During which stage do you create incident response and rollback plans?
- A) Map
- B) Measure
- C) Mitigate
- D) Manage

**Q7.** What is the primary goal of the Measure stage?
- A) To identify all possible harms
- B) To create a baseline quantifying harms and track improvements
- C) To deploy the solution to production
- D) To write user documentation

**Q8.** Which statement best describes the purpose of responsible AI in generative AI solutions?
- A) To improve model accuracy
- B) To minimize the risk of harmful content generation
- C) To reduce infrastructure costs
- D) To increase token throughput

**Q9.** Which stage involves defining a deployment and operational readiness plan?
- A) Map
- B) Measure
- C) Mitigate
- D) Manage

**Q10.** How does the process ensure harms are addressed iteratively?
- A) By deploying to all users at once
- B) By measuring a baseline, mitigating, then retesting against the baseline
- C) By disabling all content filtering
- D) By ignoring stakeholder feedback

---

## Map Potential Harms (Q11–Q20)

**Q11.** What is the FIRST step in mapping potential harms?
- A) Prioritize identified harms
- B) Test and verify the harms
- C) Identify potential harms
- D) Document and share the harms

**Q12.** What is the correct order of steps in the Map stage?
- A) Identify → Test → Prioritize → Document
- B) Identify → Prioritize → Test and verify → Document and share
- C) Prioritize → Identify → Document → Test
- D) Test → Document → Identify → Prioritize

**Q13.** Which of the following is a common type of potential harm in a generative AI solution?
- A) Generating content that is offensive, pejorative, or discriminatory
- B) Generating content that is factually accurate
- C) Generating content that is well-formatted
- D) Generating content that is too brief

**Q14.** Which document should you consult to understand Azure OpenAI Service-specific considerations?
- A) The OpenAI pricing page
- B) The Azure OpenAI Service transparency note
- C) The Azure SLA agreement
- D) The model deployment log

**Q15.** How should potential harms be prioritized?
- A) Alphabetically
- B) By likelihood of occurrence and level of impact
- C) By the number of lines of code affected
- D) Randomly

**Q16.** In prioritizing harms, what must be taken into account?
- A) Only the intended use of the solution
- B) Only the potential for misuse
- C) Both the intended use and the potential for misuse
- D) Neither intended use nor misuse

**Q17.** What is red teaming in the context of responsible AI?
- A) A team of testers that deliberately probes the solution to produce harmful results
- B) A team that fixes production incidents
- C) A team that writes documentation
- D) A team that manages deployments

**Q18.** What should be done with the successes of the red team?
- A) Ignored, since they are hypothetical
- B) Documented and reviewed to determine realistic likelihood of harmful output
- C) Deleted from the records
- D) Automatically fixed in production

**Q19.** What can testing reveal in addition to verifying known harms?
- A) Previously unidentified harms
- B) The model's exact training data
- C) The cost of the deployment
- D) The number of API calls made

**Q20.** After documenting and sharing verified harms, what should you do with the prioritized list?
- A) Discard it
- B) Maintain it and add to it if new harms are identified
- C) Share it only with customers
- D) Store it in a private database forever

---

## Measure Potential Harms (Q21–Q28)

**Q21.** What is the goal of the measurement process?
- A) To eliminate all harmful output
- B) To create an initial baseline that quantifies harms and track improvements
- C) To deploy the solution faster
- D) To increase model temperature

**Q22.** What is the FIRST step in the three-step measurement approach?
- A) Submit prompts and retrieve output
- B) Apply pre-defined criteria to evaluate output
- C) Prepare a diverse selection of input prompts likely to result in each harm
- D) Share results with stakeholders

**Q23.** What is the THIRD step in the three-step measurement approach?
- A) Prepare diverse input prompts
- B) Submit prompts and retrieve output
- C) Apply pre-defined criteria to categorize the output by harm level
- D) Deploy the solution

**Q24.** What is required of the criteria used to categorize output?
- A) They should be flexible and change each time
- B) They must be strict and can be applied consistently
- C) They should only apply to text output
- D) They are optional

**Q25.** How should you start testing in most scenarios?
- A) Immediately automate with a classification model
- B) Manually test a small set of inputs to ensure criteria are well-defined
- C) Test only in production
- D) Skip testing entirely

**Q26.** How can automated testing evaluate output?
- A) By using a classification model to automatically evaluate the output
- B) By asking users to rate responses
- C) By analyzing infrastructure logs only
- D) By reducing the number of test cases

**Q27.** Why should you periodically perform manual testing even after automating?
- A) To increase token usage
- B) To validate new scenarios and ensure the automated solution performs as expected
- C) To satisfy legal requirements only
- D) To slow down the testing process

**Q28.** What should be done with the results of the measurement process?
- A) Kept secret
- B) Documented and shared with stakeholders
- C) Deleted after each iteration
- D) Used only for internal tuning

---

## Mitigate Potential Harms — Four Layers (Q29–Q40)

**Q29.** How many layers of mitigation are applied in a generative AI solution?
- A) Two
- B) Three
- C) Four
- D) Five

**Q30.** Which of the following is the correct list of mitigation layers?
- A) Model, Safety System, System message and grounding, User experience
- B) Model, Database, API, Frontend
- C) Prompt, Data, Compute, Storage
- D) Input, Processing, Output, Feedback

**Q31.** Selecting a simpler, more appropriate model for the task belongs to which layer?
- A) Safety System
- B) Model
- C) User experience
- D) Grounding

**Q32.** Fine-tuning a foundational model with your own training data belongs to which layer?
- A) Model
- B) Safety System
- C) User experience
- D) Grounding

**Q33.** Content filters and prompt shields belong to which layer?
- A) Model
- B) Safety System
- C) System message and grounding
- D) User experience

**Q34.** Adding RAG to retrieve contextual data from trusted sources belongs to which layer?
- A) Model
- B) Safety System
- C) System message and grounding
- D) User experience

**Q35.** Designing the UI to constrain inputs to specific subjects belongs to which layer?
- A) Model
- B) Safety System
- C) System message and grounding
- D) User experience

**Q36.** What do prompt shields detect?
- A) Model latency issues
- B) Systematic abuse, such as attempts to subvert the system prompt
- C) Token overuse
- D) Network failures

**Q37.** Which mitigation helps maximize the likelihood of relevant, nonharmful output by grounding prompts?
- A) Increasing model size
- B) Retrieval augmented generation (RAG)
- C) Disabling content filters
- D) Removing system messages

**Q38.** What should user-facing documentation be transparent about?
- A) Only the pricing
- B) Capabilities, limitations, models, and potential harms not always addressed by mitigations
- C) Only the release date
- D) Nothing — documentation is optional

**Q39.** Which layer focuses on platform-level configurations like guardrails?
- A) Model
- B) Safety System
- C) System message and grounding
- D) User experience

**Q40.** Applying input and output validation is a mitigation at which layer?
- A) Model
- B) Safety System
- C) System message and grounding
- D) User experience

---

## Guardrails and Content Filters (Q41–Q46)

**Q41.** How many severity levels do content filters classify content into?
- A) Two
- B) Three
- C) Four
- D) Five

**Q42.** Which of the following is NOT one of the severity levels?
- A) Safe
- B) Medium
- C) High
- D) Critical

**Q43.** How many categories of potential harm do content filters cover?
- A) Three
- B) Four
- C) Five
- D) Seven

**Q44.** Which of the following is one of the five content filter categories?
- A) Task-adherence
- B) Grammar
- C) Latency
- D) Cost

**Q45.** What is the purpose of guardrails in Microsoft Foundry?
- A) To increase model throughput
- B) To apply criteria that suppress prompts and responses based on content filters
- C) To reduce deployment time
- D) To improve token efficiency

**Q46.** Which category of harm includes content that deviates from the intended task or system instructions?
- A) Violence
- B) Self-harm
- C) Task-adherence
- D) Sexual

---

## Manage a Responsible Generative AI Solution (Q47–Q50)

**Q47.** Which of the following is a common prerelease compliance review?
- A) Legal
- B) Weather
- C) Traffic
- D) Marketing

**Q48.** What does a phased delivery plan enable you to do?
- A) Release to all users immediately
- B) Release to a restricted group first to gather feedback before wider release
- C) Skip testing
- D) Avoid incident response

**Q49.** What is the purpose of a rollback plan?
- A) To define steps to revert the solution to a previous state if an incident occurs
- B) To deploy faster
- C) To increase user counts
- D) To disable telemetry

**Q50.** What capability should you implement to handle system misuse?
- A) Block specific users, applications, or client IP addresses
- B) Increase model temperature
- C) Remove all content filters
- D) Disable user feedback

---

## Answers

| Q | Answer | Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|--------|---|--------|---|--------|---|--------|---|--------|
| 1 | B | 11 | C | 21 | B | 31 | B | 41 | C |
| 2 | B | 12 | B | 22 | C | 32 | A | 42 | D |
| 3 | C | 13 | A | 23 | C | 33 | B | 43 | C |
| 4 | B | 14 | B | 24 | B | 34 | C | 44 | A |
| 5 | C | 15 | B | 25 | B | 35 | D | 45 | B |
| 6 | D | 16 | C | 26 | A | 36 | B | 46 | C |
| 7 | B | 17 | A | 27 | B | 37 | B | 47 | A |
| 8 | B | 18 | B | 28 | B | 38 | B | 48 | B |
| 9 | D | 19 | A | 29 | C | 39 | B | 49 | A |
| 10 | B | 20 | B | 30 | A | 40 | D | 50 | A |

---

*Practice questions created: 2026-08-04 · Source: Microsoft Learn module content*
