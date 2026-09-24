---
title: GenAI Security Controls
---

# GenAI Security for ISAs

### Based on the ISA GenAI Security Guide

> Full guide, security controls & case studies: [ISA GenAI Threat Modeling Guide](https://isa-genai-threatmodelingguide.pages.mercedes-benz.ghe.com/)

---

## Lesson Objectives

* Understand the  GenAI technology landscape at a high level
* Know the general best practices across the AI lifecycle
* Understand and apply the GenAI-specific security controls catalogue
* Use the provided case studies as a reference for your own threat models
* Know where to find further resources

> This lesson focuses on **security controls** - non-GenAI threats still apply.

---

## What is Generative AI?

| Term | What it means |
|---|---|
| **Artificial Intelligence** | Automates intelligent tasks; responds to a specific set of inputs |
| **Machine Learning** | Algorithms that learn from data to make decisions or predictions |
| **Deep Learning** | ML using deep neural networks; improves accuracy at scale |
| **Generative AI** | Creates new content - text, images, code, audio - from learned patterns |

GenAI models are trained on large datasets and generate new data that resembles the training set.

---

## Large Language Models & RAG

**LLMs** (e.g. GPT, Claude) are trained on massive text corpora and generate responses based on learned patterns - but have a fixed knowledge cutoff and can hallucinate.

**Retrieval Augmented Generation (RAG)** addresses this by adding an external retrieval step:

1. User prompt > converted to a vector embedding
2. Vector DB searched for relevant document chunks
3. Retrieved chunks + prompt sent to the LLM
4. LLM generates a grounded, fact-based response

RAG keeps knowledge cu rrent without retraining - but introduces new attack surfaces on the retrieval layer.

---

## Popular GenAI Use Cases

| Use Case | Examples |
|---|---|
| Chatbots / Assistants | Q&A, summarization, task execution |
| Text-to-Image / Video | Marketing, product viz, content creation |
| Text-to-Code | Code gen, debugging, test creation |
| Content Summarization | Docs, emails, meeting transcripts |
| Audio / Speech Synthesis | TTS, voice cloning, music generation |
| AI Agents | RPA, autonomous workflows, multi-agent systems |

---

# General Best Practices

---

## Best Practices: Project Initiation

* **AI Governance** - Pass governance process; assess risk based on purpose, scope, training data
* **Privacy by Design** - Evaluate PII / confidential data early; implement safeguards from the start
* **Regulatory Compliance** - EU AI Act, GDPR; plan for risk-level-dependent controls
* **(AI) Supply Chain Security** - Validate LLMs, plugins, and third-party components from trustworthy sources

---

## Best Practices: Development

* **Secure SDL** - Integrate security throughout; configure dev environments securely
* **Robustness Testing** - Adversarial testing: prompt injection, jailbreak attempts, harmful content generation
* **GenAI-Specific Controls** - Content filtering, output validation, prompt protection, retrieval safeguards
* **Knowledge Source Validation** - Validate quality, trustworthiness and integrity of knowledge bases and vector DBs

---

## Best Practices: Operation

* **Continuous Monitoring** - Detect in real-time: model behavior, abuse, prompt injection, policy violations
* **Information Protection** - Protect training data, model artifacts, embeddings, prompts, system parameters
* **Secure Model Sharing** - Protect IP; prevent reverse-engineering when sharing models
* **Continuous Security Validation** - Reassess AI risks regularly; validate controls after model updates or knowledge source changes

[Google GenAI Best Practices](https://docs.cloud.google.com/docs/security/genai-security-bps) | [Azure GenAI Best Practices](https://techcommunity.microsoft.com/t5/azure-architecture-blog/security-best-practices-for-genai-applications-openai-in-azure/ba-p/4027885)

---

# Vulnerabilities

Showing some samples

---

## Sensitive Information Disclosure

How GenAI systems leak data — often without the attacker needing special access:

| Vector | What happens |
|---|---|
| Training data memorization | Model reproduces exact or near-exact training data in responses |
| System prompt exfiltration | Crafted user input tricks the model into revealing its system prompt |
| RAG over-retrieval | Retrieval returns documents the querying user should not see |
| Log exposure | Prompts and completions stored in plaintext; accessed by attacker |

---

## GenAI Supply Chain

Third-party models, datasets, and plugins are hard to inspect — and they run with your application's trust level.

| Vector | What happens |
|---|---|
| Compromised pre-trained model | Backdoors or biases embedded before you fine-tune |
| Transfer learning attack | Malicious behaviors in the base model persist through fine-tuning |
| Poisoned dataset | Training data sourced from an attacker-controlled or tampered source |
| Malicious plugin / tool | Plugin executes unintended actions using the model's credentials |

---

# Security Controls

---

## Controls Overview

| Category | Controls | Focus |
|---|---|---|
| **AS** - Architecture & Stability | AS1-AS8 | Robustness, separation, data integrity |
| **ACS** - Access Control | ACS1-ACS2 | Model, data, user, service access |
| **DS** - Data Science | DS1-DS2 | Data minimization, human oversight |
| **VSES** - Validation & Security | VSES1-VSES2 | Input / output validation |
| **ELV** - Evaluation & Logging | ELV1-ELV2 | Monitoring, anomaly detection |
| **AM** - Asset Management | AM1 | SBOM / AIBOM |

[Full Controls Catalogue](https://isa-genai-threatmodelingguide.pages.mercedes-benz.ghe.com/03-genai-security/security-controls/)

---

## GenAI_VSES1.1 - Input Validation and Sanitization

> Validation & Security (Scope: Development, Operation)

Implement input validation and sanitization so user input adheres to defined limits and malicious content is filtered. Critical to prevent adversarial attacks, prompt injection, and concept drift.

| What to implement | Detail |
|---|---|
| Enforce limits | Format, range, and token limits on all inputs at the API boundary |
| Filter malicious patterns | Known injection attempts, jailbreak templates, instruction overrides |
| Detect out-of-distribution input | Flag inputs that differ significantly from expected usage patterns |
| Validate model -> backend calls | Typed params and range checks before executing downstream functions |

---

## GenAI_ACS2.1 - Limit Privileges of Model

> Access Control (Scope: Development)

Limit the privileges of the model to prevent unwanted autonomous actions. Applies especially when plugins or tools are in use.

| What to implement | Detail |
|---|---|
| Define action scope explicitly | The model may only take actions within a defined, approved set |
| One scoped token per plugin | Not a global key — each plugin route gets its own credential |
| Require human authorization | For high-risk or irreversible actions, a human must confirm |
| Regularly prune permissions | Review and reduce model and plugin permissions over time |

---

## Case Studies Overview

| Case Study | Technology | Key Threat Areas |
|---|---|---|
| RAG Chatbot | Azure OpenAI + AI Search | Prompt injection, info disclosure, DoS |
| Image Generation | AWS EKS + HuggingFace + Stable Diffusion | Data poisoning, model theft, adversarial inputs |
| [RPA Multi-Agent](https://isa-genai-threatmodelingguide.pages.mercedes-benz.ghe.com/04-case-studies/Multi-Agent%20System/) | LLM agents + RAG + Finance system | Goal hijack, tool misuse, memory poisoning |

> Threat models focus on GenAI-specific findings only.

---

## CS: RPA Multi-Agent System

<img src="../assets/rpa-multi-agent-c1.png" alt="RPA Multi-Agent C1" style="width: 40%;">

Agents involved: OCR Agent > Policy Validation Agent > Decision-Making Agent > Execution Agent  

---

## CS: RPA Multi-Agent - Key Threats & Controls

| Threat | Category | Controls |
|---|---|---|
| Misaligned / Goal Hijack via prompt injection | ASI01 | Instruction-precedence rules, trust boundaries, separate business content from instructions |
| Tool Misuse via injected content | ASI02 | Least privilege (ACS2.1), authorization before tool invocation, anomaly detection |
| Memory & Context Poisoning | ASI06 | Validate before storing, memory integrity checks, access control on memory stores |
| Model Inconsistency > variable approval | LLM07 | Deterministic settings, duplicate detection, cache prior decisions |
| Human-in-the-Loop Manipulation | ASI09 | Expose raw evidence to reviewer; require secondary approval for high-risk |
| Insufficient Decision Traceability | LLM01 | End-to-end audit trail, append-only logs, correlated transaction IDs |

[Full case study](https://isa-genai-threatmodelingguide.pages.mercedes-benz.ghe.com/04-case-studies/Multi-Agent%20System/)

---

## Agentic AI: Special Considerations

Agentic systems amplify existing threats - small misconfigurations have large blast radius:

* **Goal Hijack** - injected instructions override agent's intended objective
* **Tool Misuse** - agent is tricked into invoking privileged tools
* **Memory Poisoning** - poisoned data persists and influences future decisions
* **Cascading Actions** - one compromised agent propagates to downstream agents
* **Non-Determinism** - same input can yield different decisions across runs

**Design principles:**
* Minimal tool scope per agent
* Human approval gates for irreversible actions
* Immutable audit logs across the full agent chain

---

## Internal Resources

Following are the main MB specific internal AI Security resources

| Resource | Details |
|---|---|
[AppStandardInsights (ASI)](https://asi.app.corpintra.net/) | Contains 4 AI specific requirements (covering: Secure Defaults like Skills, company-approved AI models, protect secrets, human-in-the-loop)
[ASRG Module (on ASI)](https://pages.i.mercedes-benz.com/gcs/KB/docs/Tools-and-Platforms/asi/how-to-asrg/) | The MB specific integration of OWASP AISVS
[AI Model Garden](https://odp.i.mercedes-benz.com/aiecosystem/modelgarden) | Main overview of compliant AI models and their usage

---

## Further Resources

| Resource | Link |
|---|---|
| OWASP GenAI LLM Top 10 (2026) | [genai.owasp.org](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/) |
| OWASP Top 10 for Agentic AI | [genai.owasp.org](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) |
| Multi-Agentic TM Guide v1.0 | [genai.owasp.org](https://genai.owasp.org/resource/multi-agentic-system-threat-modeling-guide-v1-0/) |
| AISVS (AI Security Verification) | [owasp.org/aisvs](https://owasp.org/www-project-artificial-intelligence-security-verification-standard-aisvs-docs/) |
| OWASP AI Exchange | [owaspai.org](https://owaspai.org/) |
| OWASP ML Top 10 | [mltop10.info](https://mltop10.info/) |
| MAESTRO Framework | [cloudsecurityalliance.org](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro) |
| MITRE ATLAS | [atlas.mitre.org](https://atlas.mitre.org/) |
| Azure GenAI Security | [techcommunity.microsoft.com](https://techcommunity.microsoft.com/t5/azure-architecture-blog/security-best-practices-for-genai-applications-openai-in-azure/ba-p/4027885) |

[ISA GenAI Threat Modeling Guide](https://isa-genai-threatmodelingguide.pages.mercedes-benz.ghe.com/)

---

## Key Takeaways

1. **Basics first** - understand RAG, use cases, and the full AI pipeline before threat modeling
2. **Lifecycle coverage** - apply controls at initiation, development, **and** operation
3. **Controls are grouped** - AS (robustness/separation), ACS (access), DS (data), VSES (validation), ELV (monitoring), AM (inventory)
4. **Prompt injection is the #1 AI-specific threat** - direct and indirect variants; treat all external content as untrusted
5. **Least privilege for everything** - model, plugins, data sources, backend systems
6. **Human-in-the-Loop** is a control, not just a UX feature - mandatory for high-impact decisions
7. **Agentic systems** need end-to-end audit trails, action boundaries, and cascading-failure thinking
8. **Use the case studies** - RAG, Image Gen, and RPA MAS give you concrete threat/control mappings
