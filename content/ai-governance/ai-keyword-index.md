---
title: "Enterprise AI: Keywords, Concepts & Frameworks"
url: "/ai-governance/ai-keyword-index/"
slug: "ai-keyword-index"
date: 2026-10-28
lastmod: 2026-10-28
draft: false
description: "A structured index of enterprise AI concepts, failure patterns, and governance frameworks — mapped to original articles by Druhin Dhavala. Built for practitioners searching for answers before the industry has names for the problems."
keywords: ["AI governance", "enterprise AI", "AI security", "AI economics", "AI failure patterns", "RAG", "prompt injection", "AI Gateway", "AI strategy"]
sitemap:
  priority: 0.8
---

This page maps the concepts the industry will be searching for in 1–3 years to the articles that already exist. No AI-generated filler. Every link goes to original, timestamped work built on enterprise platform engineering scars.

---

## Agentic AI Security

| If you're searching for... | Read this |
|---------------------------|-----------|
| **Stored prompt injection** — adversarial text enters your database through a legitimate API, then an AI agent reads it as instruction | [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) |
| **Indirect prompt injection** — same attack vector, different name | [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) |
| **AI data provenance** — tracking where data came from so agents don't execute untrusted text | [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) (provenance tracking + OPA policies) |
| **Agent privilege escalation** — when a poisoned record gives an agent more power than it should have | [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) (thought experiment: finance agent reads HR record) |
| **AI supply chain attacks** — poisoned model weights, poisoned training data, poisoned RAG sources | The API gateway pattern applies: validate provenance at every hop. See [GATES Gate 1 (Secure)](/ai-governance/gates-framework/) and [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) |
| **AI firewall / AI WAF** — content-scanning proxies for AI traffic | I argue this is the wrong approach. Content scanning creates a recursive problem (using AI to police AI). See [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) — "Who governs the governor?" |
| **AI red teaming** — adversarial testing of AI systems | Not covered directly. The stored prompt injection piece is a red teamer's playbook. |
| **AI incident response** — what to do when prompt injection hits production | The 30-second audit checklist in [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) is a starting point. |

---

## AI Economics & FinOps

| If you're searching for... | Read this |
|---------------------------|-----------|
| **AI ROI collapse** — why AI returns flatten after Year 3–4 | [Post-Peak AI Economics](/ai-governance/post-peak-ai-economics/) |
| **AI TCO (total cost of ownership)** — the real cost of running AI at scale | [Post-Peak AI Economics](/ai-governance/post-peak-ai-economics/) |
| **Token cost economics** — per-token pricing vs. enterprise budgets | [Post-Peak AI Economics](/ai-governance/post-peak-ai-economics/) |
| **AI shelfware** — AI tools bought but never deployed | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) (FOMO-driven procurement) |
| **GPU utilization vs. ROI** — infrastructure economics beneath model inference | Not covered directly. The economics model in [Post-Peak AI Economics](/ai-governance/post-peak-ai-economics/) addresses the cost curve. |
| **AI budget correction** — when CFOs realize the AI line item isn't shrinking | [Post-Peak AI Economics](/ai-governance/post-peak-ai-economics/) (Year 4–5 flattening) |

---

## RAG & Data Failures

| If you're searching for... | Read this |
|---------------------------|-----------|
| **RAG hallucination root cause** — why retrieval-augmented generation produces wrong answers | [RAG Data Integrity Model](/ai-governance/rag-hallucination-data-problem/) |
| **Vector index staleness** — embeddings that don't reflect current data | [RAG Data Integrity Model](/ai-governance/rag-hallucination-data-problem/) (CDC-based freshness) |
| **Embedding drift** — when vector representations degrade over time | [RAG Data Integrity Model](/ai-governance/rag-hallucination-data-problem/) |
| **Data reconciliation for AI** — why you must clean data before it enters the vector index | [RAG Data Integrity Model](/ai-governance/rag-hallucination-data-problem/) + [The Data Layer Is Where AI Goes to Die](/ai-governance/the-data-layer-is-where-ai-goes-to-die/) |
| **Garbage semantics in, garbage semantics out** — coined phrase: AI amplifies data mess, it doesn't clean it | [The Data Layer Is Where AI Goes to Die](/ai-governance/the-data-layer-is-where-ai-goes-to-die/) |
| **Data contracts for AI** — enforcing schema and quality at domain boundaries | Mentioned in [RAG Data Integrity Model](/ai-governance/rag-hallucination-data-problem/). Not a standalone framework. |

---

## AI Governance

| If you're searching for... | Read this |
|---------------------------|-----------|
| **AI governance framework** — structured model for governing AI at runtime | [GATES Framework](/ai-governance/gates-framework/) (5 gates, 0–5 maturity) |
| **AI Gateway / LLM Gateway** — the proxy layer between users and models | [AI Gateway Control Plane](/ai-governance/ai-gateway-control-plane/) |
| **AI guardrails** — runtime controls on AI behavior | [GATES Framework](/ai-governance/gates-framework/) (Gates 1, 2, 5) |
| **Prompt governance** — versioning, validating, and controlling prompts | [GATES Framework](/ai-governance/gates-framework/) (Gate 2: Govern) |
| **AI audit trail** — immutable logging of every AI decision | [GATES Framework](/ai-governance/gates-framework/) (Gate 4: Trace) |
| **EU AI Act compliance** — regulatory requirements for AI systems | Not covered directly. GATES maps naturally to regulatory requirements (Trace = auditability, Govern = compliance, Enforce = safety). |
| **Model risk management** — financial services framework for AI risk | Not covered directly. GATES provides the technical controls; model risk management is the governance layer above it. |
| **AI policy-as-code** — enforcing governance rules programmatically | [Who Governs the Governor?](/ai-governance/stored-prompt-injection-api-gateway/) (OPA/Rego examples) + [GATES](/ai-governance/gates-framework/) |

---

## Enterprise AI Failure

| If you're searching for... | Read this |
|---------------------------|-----------|
| **Enterprise AI failure rate** — why 95% of deployments collapse | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) |
| **AI technical debt** — irreversible compounding debt from bolting AI onto fragmented systems | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) |
| **Shadow AI** — unsanctioned AI usage inside organizations | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) |
| **AI FOMO** — competitive panic driving bad AI investments | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) + [AI Hype Cycle](/ai-governance/ai-hype-cycle/) |
| **AI integration debt** — the cost of connecting AI to legacy systems | [Enterprise AI Failure Pattern](/ai-governance/enterprise-ai-failure-pattern/) |

---

## AI Workforce & Cognition

| If you're searching for... | Read this |
|---------------------------|-----------|
| **AI skill atrophy** — developers losing debugging skills from AI reliance | [AI Coding: Journey vs Destination](/perspective/ai-coding-journey-vs-destination-the-skill-atrophy/) |
| **AI coding comprehension loss** — 17-point drop in understanding (Anthropic 2026 study) | [AI Coding: Journey vs Destination](/perspective/ai-coding-journey-vs-destination-the-skill-atrophy/) |
| **AI talent evaluation crisis** — nobody knows how to hire for AI | [We're Hiring AI Talent Nobody Knows How to Evaluate](/perspective/were-hiring-ai-talent-nobody-knows-how-to-evaluate/) |
| **Cognitive debt** — outsourcing thinking to AI, losing the ability to think | [AI & Humanity: The Point of No Return](/perspective/ai-humanity-the-point-of-no-return/) |
| **AI productivity paradox** — saved time goes to more screen time, not meaningful work | [AI Gave Us Superpowers. Now We're Just Scrolling Faster.](/perspective/ai-gave-us-superpowers/) |

---

## AI Infrastructure & Architecture

| If you're searching for... | Read this |
|---------------------------|-----------|
| **AI Gateway control plane** — centralized proxy for all AI traffic | [AI Gateway Control Plane](/ai-governance/ai-gateway-control-plane/) |
| **AI middleware** — the layer between applications and models | [AI Gateway Control Plane](/ai-governance/ai-gateway-control-plane/) |
| **AI observability** — monitoring, logging, and tracing AI transactions | [GATES Framework](/ai-governance/gates-framework/) (Gate 4: Trace) |
| **Multi-agent orchestration** — governing systems where multiple AI agents coordinate | Not covered directly. GATES addresses single-gateway governance. Multi-agent adds coordination complexity. |
| **AI vendor lock-in** — model/provider portability | Not covered directly. The AI Gateway Control Plane architecture implies abstraction, but vendor lock-in is not a dedicated analysis. |
| **AI regression testing** — how to test non-deterministic systems | Not covered. This is an implementation concern outside my architecture/governance lane. |

---

## What I Don't Cover (By Design)

This site is about **architecture, governance, economics, and failure patterns** — not implementation. You won't find:

- LLM fine-tuning guides
- RAG pipeline configuration
- Vector database selection
- Prompt engineering techniques
- Model benchmarking

For those, there are excellent practitioner resources elsewhere. What you'll find here: the structural problems that make all of the above fail at enterprise scale.

---

*This page is updated as new articles are published. Last modified: October 28, 2026.*
