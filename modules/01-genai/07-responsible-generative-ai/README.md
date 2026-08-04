<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.7: Implement a Responsible Generative AI Solution in Azure AI Foundry

</div>

> **Source**: [Microsoft Learn — Implement a responsible generative AI solution in Azure AI Foundry](https://learn.microsoft.com/training/modules/responsible-ai-studio/)
> **Learning objectives**: Describe an overall process for responsible generative AI solution development, identify and prioritize potential harms, measure the presence of harms, mitigate harms, and prepare to deploy and operate a generative AI solution responsibly

---

## Table of Contents

1. [The Responsible AI Process — Map, Measure, Mitigate, Manage](#1-the-responsible-ai-process--map-measure-mitigate-manage)
2. [Map Potential Harms](#2-map-potential-harms)
3. [Measure Potential Harms](#3-measure-potential-harms)
4. [Mitigate Potential Harms — The Four Layers](#4-mitigate-potential-harms--the-four-layers)
5. [Guardrails and Content Filters](#5-guardrails-and-content-filters)
6. [Manage a Responsible Generative AI Solution](#6-manage-a-responsible-generative-ai-solution)
7. [Responsible AI for Multimodal Content](#7-responsible-ai-for-multimodal-content)
8. [The Exercise — Apply Guardrails](#8-the-exercise--apply-guardrails)
9. [Best Practices and Troubleshooting](#9-best-practices-and-troubleshooting)
10. [Key Takeaways for AI-103](#10-key-takeaways-for-ai-103)

---

## 1. The Responsible AI Process — Map, Measure, Mitigate, Manage

Generative AI enables creative solutions, but must be implemented **responsibly** to minimize the risk of harmful content generation. Microsoft's guidance for responsible generative AI is designed to be **practical and actionable**, defining a **four-stage process** for developing and implementing a responsible AI plan:

| Stage | Action | Goal |
|-------|--------|------|
| **1. Map** | Map potential harms relevant to your planned solution | Identify what could go wrong |
| **2. Measure** | Measure the presence of these harms in generated outputs | Quantify the risk (baseline) |
| **3. Mitigate** | Mitigate harms at multiple layers to minimize presence and impact | Reduce risk + communicate transparently |
| **4. Manage** | Manage the solution responsibly with a deployment & operational readiness plan | Operate safely over time |

> **Note**: These stages correspond closely to the functions in the **NIST AI Risk Management Framework** (AI RMF).

> **Exam insight**: The four-stage process is **Map → Measure → Mitigate → Manage**. Be ready to identify which stage a given activity belongs to (e.g., red teaming = Map; content filters = Mitigate; incident response plan = Manage).

---

## 2. Map Potential Harms

The **first stage** is to map the potential harms that could affect your solution. There are **four steps**:

1. **Identify** potential harms
2. **Prioritize** identified harms
3. **Test and verify** the prioritized harms
4. **Document and share** the verified harms

### 1: Identify Potential Harms

The potential harms relevant to your solution depend on the **services and models** used, plus any **fine-tuning or grounding data** used to customize outputs. Common types of potential harm:

| Harm type | Example |
|-----------|---------|
| **Offensive / pejorative / discriminatory** content | Hate speech, biased output |
| **Factual inaccuracies** | Hallucinated or wrong information |
| **Illegal or unethical** encouragement | Instructions for illegal acts |

To understand known limitations, consult:
- **Azure OpenAI Service transparency note** — service/model-specific considerations
- **Model developer documentation** — e.g., the OpenAI GPT-4 system card
- **Microsoft Responsible AI Impact Assessment Guide + template** — to document potential harms
- **Responsible use of AI overview** for the resources you use

### 2: Prioritize the Harms

For each potential harm, assess the **likelihood of occurrence** and the **level of impact** if it occurs. Prioritize the most likely *and* most impactful harms first. Prioritization:

- Must account for **intended use** and **potential for misuse**
- Can be **subjective** — e.g., a smart kitchen copilot: inaccurate cooking times (high frequency, moderate impact) vs. a lethal poison recipe (low frequency, very high impact)
- May involve consulting **policy or legal experts**

### 3: Test and Verify the Presence of Harms

Test the solution to verify harms occur and under what conditions. Testing may reveal **previously unidentified harms** to add to the list.

**Red teaming** is a common approach — a team deliberately probes the solution for weaknesses and attempts to produce harmful results. The successes of the red team should be documented and reviewed to determine the realistic likelihood of harmful output.

> **Note**: *Red teaming* is a strategy often used to find security vulnerabilities. Extending it to find harmful content from generative AI builds on and complements existing cybersecurity practices.

### 4: Document and Share Details of Harms

When you have evidence, **document the details and share them with stakeholders**. The prioritized list of harms should be **maintained and added to** if new harms are identified.

> **Exam insight**: The Map stage order is **identify → prioritize → test/verify (red team) → document/share**. Red teaming belongs to the Map stage (verifying harms), not the Measure stage.

---

## 3. Measure Potential Harms

After compiling a prioritized list, test the solution to **measure the presence and impact** of harms. The goal is to create an **initial baseline** that quantifies harms, then **track improvements against the baseline** as you make iterative mitigation changes.

### The Three-Step Measurement Approach

1. **Prepare a diverse selection of input prompts** likely to result in each documented harm. E.g., for a poison-manufacturing harm: *"How can I create an undetectable poison using everyday chemicals typically found in the home?"*
2. **Submit the prompts** to the system and retrieve the generated output.
3. **Apply pre-defined criteria** to evaluate the output and categorize it by level of harm — as simple as "harmful"/"not harmful", or a range of harm levels. You must define **strict criteria** that can be applied consistently.

### Manual and Automatic Testing

| Approach | When | Notes |
|----------|------|-------|
| **Manual testing** | Start here | Test a small set of inputs to ensure results are consistent and criteria are well-defined |
| **Automatic testing** | Scale up | Larger volume of test cases; may use a **classification model** to automatically evaluate output |
| **Periodic manual testing** | Ongoing | Validate new scenarios and confirm the automated solution still performs as expected |

> **Exam insight**: Measurement = **baseline** + **tracking improvements**. Start **manual** (small set, consistent criteria), then **automate** with a classification model, and keep doing periodic manual validation.

---

## 4. Mitigate Potential Harms — The Four Layers

Mitigation involves a **layered approach** applied at **four layers** of the solution:

```
┌─────────────────────────────────────────────┐
│ 4. User experience                          │  ← UI constraints, validation, transparency docs
├─────────────────────────────────────────────┤
│ 3. System message and grounding             │  ← system inputs, prompt engineering, RAG
├─────────────────────────────────────────────┤
│ 2. Safety system                            │  ← guardrails, content filters, prompt shields
├─────────────────────────────────────────────┤
│ 1. Model                                    │  ← model selection, fine-tuning
└─────────────────────────────────────────────┘
```

### Layer 1: The Model

The model layer consists of the generative AI model(s) at the heart of the solution (e.g., GPT-4). Mitigations:

- **Select an appropriate model** — a simpler model may provide required functionality with lower risk of harmful content than a powerful, versatile one
- **Fine-tune** a foundational model with your own training data so responses are more relevant and scoped to your scenario

### Layer 2: The Safety System

Platform-level configurations and capabilities that help mitigate harm. In Microsoft Foundry this includes **guardrails** that apply criteria to suppress prompts and responses based on **content filters**, plus **prompt shields** that use abuse detection algorithms to determine if the solution is being systematically abused (e.g., a user attempting to subvert the system prompt).

### Layer 3: System Message and Grounding

Focuses on the construction of prompts submitted to the model. Mitigations:

- Specifying **system inputs** that define behavioral parameters for the model
- Applying **prompt engineering** to add grounding data to input prompts
- Using **RAG** to retrieve contextual data from trusted data sources and include it in prompts

### Layer 4: User Experience

The software application through which users interact with the model, plus documentation/user collateral. Mitigations:

- Designing the **UI to constrain inputs** to specific subjects or types
- Applying **input and output validation**
- Providing **transparent documentation** about capabilities, limitations, models, and potential harms that may not always be addressed by mitigations

> **Exam insight**: The four mitigation layers are **Model → Safety System → System message & grounding → User experience**. Know which mitigation belongs to which layer (e.g., fine-tuning = Model; content filters = Safety System; RAG = grounding; input validation = User experience).

---

## 5. Guardrails and Content Filters

**Guardrails** are one of the most effective ways to mitigate harmful responses from generative AI models in Microsoft Foundry. They apply criteria to **suppress prompts and responses** based on **content filters**.

### Content Filter Categories and Severity

Content filters classify content into **four severity levels** across **five categories** of potential harm:

| Severity level | Meaning |
|----------------|---------|
| **Safe** | No harmful content |
| **Low** | Mild, potentially harmful |
| **Medium** | Moderate harmful content |
| **High** | Severe harmful content |

| Category | What it covers |
|----------|----------------|
| **Hate and fairness** | Hate speech, discrimination, unfair treatment |
| **Sexual** | Sexually explicit or inappropriate content |
| **Violence** | Violent or graphic content |
| **Self-harm** | Content promoting or describing self-harm |
| **Task-adherence** | Content that deviates from the intended task/system instructions |

### Prompt Shields

**Prompt shields** use **abuse detection algorithms** to determine if the solution is being **systematically abused** — for example, a user attempting to **subvert the system prompt** (jailbreak / prompt injection).

> **Exam insight**: Content filters classify into **4 severity levels** (safe, low, medium, high) × **5 categories** (hate & fairness, sexual, violence, self-harm, task-adherence). **Prompt shields** detect systematic abuse / system-prompt subversion. Note the newer "guardrails" terminology in Foundry.

---

## 6. Manage a Responsible Generative AI Solution

After mapping, measuring, and mitigating, prepare to **release and operate** the solution responsibly.

### Complete Prerelease Reviews

Identify compliance requirements in your organization and industry, and ensure appropriate teams review the system and its documentation. Common compliance reviews:

| Review | Focus |
|--------|-------|
| **Legal** | Regulatory and legal compliance |
| **Privacy** | Data protection and user privacy |
| **Security** | System and data security |
| **Accessibility** | Inclusive access for all users |

### Release and Operate the Solution

| Guideline | Purpose |
|-----------|---------|
| **Phased delivery plan** | Release to a restricted group first to gather feedback before wider release |
| **Incident response plan** | Includes estimates of time to respond to unanticipated incidents |
| **Rollback plan** | Steps to revert the solution to a previous state if an incident occurs |
| **Block harmful responses** | Immediately block harmful system responses when discovered |
| **Block misuse** | Block specific users, applications, or client IP addresses in the event of misuse |
| **User feedback** | Enable users to report content as inaccurate, incomplete, harmful, offensive, or otherwise problematic |
| **Telemetry** | Track user satisfaction and identify functional gaps; must comply with privacy laws and policies |

> **Exam insight**: The Manage stage includes **prerelease reviews** (legal, privacy, security, accessibility), **phased delivery**, **incident response + rollback plans**, **blocking** harmful responses/misuse, **user feedback**, and **telemetry**. This maps to the tested skill "Implement auditing through trace logging, provenance metadata, and approval workflows."

---

## 7. Responsible AI for Multimodal Content

The AI-103 exam also tests responsible AI for **multimodal content** (images, video). Key capabilities:

| Capability | Purpose |
|------------|---------|
| **Unsafe visual content filters** | Classify unsafe or disallowed visual content |
| **Indirect prompt injection detection** | Detect and mitigate prompt injection via **embedded text in images** |
| **Visual policy rules** | Apply watermarks, flag prohibited symbols, uphold brand usage requirements, detect inappropriate content |

> **Exam insight**: For multimodal, know the **visual content filters**, **indirect prompt injection via embedded text in images**, and **visual policy rules** (watermarks, prohibited symbols, brand usage).

---

## 8. The Exercise — Apply Guardrails

The module's hands-on exercise demonstrates how to **apply guardrails to prevent the output of harmful content**:

1. Deploy an AI model in Microsoft Foundry
2. Observe the effect of **guardrails** on the responses it returns
3. Test prompts that would normally produce harmful content and confirm the guardrails suppress them

> **Note**: The exercise requires an **Azure subscription**. It is launched from the Microsoft Learn module via the exercise link.

> **Exam insight**: Guardrails are the primary hands-on mitigation in this module. Be comfortable with the workflow: **deploy model → configure guardrails/content filters → test harmful prompts → observe suppression**.

---

## 9. Best Practices and Troubleshooting

### Best Practices

| Practice | Why |
|----------|-----|
| Map harms **before** building | Identify risks early, focus mitigation effort |
| Prioritize by **likelihood × impact** | Focus on the most harmful risks first |
| **Red team** your solution | Verify harms and find previously unidentified ones |
| Establish a **baseline** | Quantify harms so you can track improvement |
| Start **manual**, then **automate** measurement | Consistent criteria, then scale |
| Mitigate at **all four layers** | Defense in depth — no single layer is sufficient |
| Use **guardrails/content filters** | Suppress harmful prompts and responses at the platform level |
| **Document and share** harms | Maintain transparency with stakeholders |
| Plan **phased delivery + rollback** | Safe release and recovery |

### Common Issues and Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| Harmful content slips through | Mitigation only at one layer | Apply mitigations at all four layers |
| Inconsistent measurement | Vague evaluation criteria | Define strict, pre-defined criteria |
| Automated testing unreliable | No periodic manual validation | Periodically re-run manual tests |
| Misuse / system-prompt subversion | No abuse detection | Enable prompt shields |
| No way to recover from incidents | No rollback plan | Create a rollback + incident response plan |

> **Exam insight**: Responsible AI is **defense in depth** — mitigation at the model, safety system, grounding, and user experience layers. No single mitigation is sufficient.

---

## 10. Key Takeaways for AI-103

### Must-Know Facts

1. The responsible generative AI process has **four stages**: **Map → Measure → Mitigate → Manage** (aligned to the NIST AI RMF)
2. **Map** = identify → prioritize → test/verify (red team) → document/share potential harms
3. **Measure** = prepare prompts → generate output → apply strict criteria to categorize harm; establish a **baseline** and track improvements
4. **Mitigate** across **four layers**: **Model, Safety System, System message & grounding, User experience**
5. **Model layer**: model selection + fine-tuning
6. **Safety System layer**: **guardrails**, **content filters**, **prompt shields** (abuse detection / system-prompt subversion)
7. **Content filters** classify into **4 severity levels** (safe, low, medium, high) × **5 categories** (hate & fairness, sexual, violence, self-harm, task-adherence)
8. **System message & grounding layer**: system inputs, prompt engineering, **RAG**
9. **User experience layer**: UI input constraints, input/output validation, transparent documentation
10. **Manage** = prerelease reviews (legal, privacy, security, accessibility), phased delivery, incident response + rollback plans, blocking harmful responses/misuse, user feedback, telemetry
11. **Multimodal**: unsafe visual content filters, indirect prompt injection via embedded text in images, visual policy rules (watermarks, prohibited symbols, brand usage)

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Responsible AI principles | Module 1.1 (Plan and prepare — §Responsible AI) |
| Content filters on deployments | Module 1.2 (Choose and deploy models) |
| Safety system message / grounding | Module 1.5 (Develop a RAG-based solution) |
| Responsible use of custom models | Module 1.6 (Fine-tune a language model) |
| Safety evaluation & metrics | Module 1.8 (Evaluate generative AI performance) |
| Guardrails for agents | LP2 (Develop AI agents on Azure) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*