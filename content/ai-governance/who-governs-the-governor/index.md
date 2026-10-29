---
title: "Who Governs the Governor? — Stored Prompt Injection Through the API Gateway"
Slug: "stored-prompt-injection-api-gateway"
date: 2026-10-26
lastmod: 2026-10-26
draft: false
sitemap:
  priority: 0.9

description: "When AI agents write to and read from your database through legitimate API calls, the attack lives in the gap between two correct authorization decisions. Thirteen years of API gateway scars, applied to stored prompt injection before it becomes a headline."
canonicalURL: "https://www.druhindhavala.com/ai-governance/stored-prompt-injection-api-gateway/"

categories: ["AI Governance"]
tags: ["stored prompt injection", "indirect prompt injection", "API gateway", "agentic AI", "AI governance", "data provenance", "OPA", "zero trust", "API security", "Istio", "Apigee", "RAG", "enterprise AI", "architecture", "governance by design"]

author: "Druhin Dhavala"
firstPublished: "2026-10-26"

# Open Graph
og_title: "Who Governs the Governor? — Stored Prompt Injection Through the API Gateway"
og_description: "When an AI agent writes to your database and another reads it, who checks what's in between? Notes from thirteen years of API gateways."
og_type: "article"
og_url: "https://www.druhindhavala.com/ai-governance/stored-prompt-injection-api-gateway/"
og_author: "Druhin Dhavala"
og_locale: "en_US"
og_site_name: "Druhin Dhavala"

# Twitter Card
twitter_card: "summary"
twitter_title: "Who Governs the Governor?"
twitter_description: "Thirteen years of API gateway scars, one question: when an AI agent writes to your DB and another reads it, who checks what's in between?"

# JSON-LD Structured Data
jsonld: |
  {
    "@context": "https://schema.org",
    "@type": "TechArticle",
    "@id": "https://www.druhindhavala.com/ai-governance/stored-prompt-injection-api-gateway/#article",
    "headline": "Stored Prompt Injection Through the API Gateway",
    "name": "Who Governs the Governor? — Stored Prompt Injection Through the API Gateway",
    "description": "Attack vector where adversarial text enters a database via legitimate API write, then gets read by an autonomous AI agent that treats it as instruction. The exploit lives in the gap between two individually correct authorization decisions.",
    "keywords": ["stored prompt injection", "indirect prompt injection", "API gateway", "API security", "agentic AI", "data provenance", "zero trust", "OPA"],
    "url": "https://www.druhindhavala.com/ai-governance/stored-prompt-injection-api-gateway/",
    "datePublished": "2026-10-26",
    "dateModified": "2026-10-26",
    "license": "https://creativecommons.org/licenses/by/4.0/",
    "author": {
      "@type": "Person",
      "name": "Druhin Dhavala",
      "url": "https://www.druhindhavala.com/about/",
      "sameAs": [
        "https://www.linkedin.com/in/druhin-dhavala/",
        "https://github.com/ddruhin"
      ]
    },
    "about": [
      {"@type": "Thing", "name": "Prompt Injection"},
      {"@type": "Thing", "name": "API Security"},
      {"@type": "Thing", "name": "AI Agents"},
      {"@type": "Thing", "name": "Data Provenance"}
    ],
    "proficiencyLevel": "Expert"
  }


# Custom Parameters
schema_name: "Who Governs the Governor? — Stored Prompt Injection Through the API Gateway"
schema_keywords: ["stored prompt injection", "indirect prompt injection", "API gateway", "agentic AI", "data provenance", "OPA", "zero trust", "API security"]
---
> **TL;DR**: Adversarial text enters a database through a legitimate, authorized API write. An autonomous AI agent later reads that text as instruction — not data — and executes it. Every API call in the chain was individually authorized. The exploit lives in the gap between two correct decisions. Mitigation requires data provenance tracking, read-path policy enforcement, and action-scoped tokens — not content scanning.


*Notes from thirteen years of API gateways, on the day an AI agent writes to your database. Written October 2026. Last updated October 2026.*

If you’re reading this years from now, after the incident review and the cleanup invoice: this is a record that the problem was visible.

I should say where I’m coming from. I’ve spent thirteen years around API gateways. I have not built AI agents and I’m not an AI expert. What I can speak to is how data moves through APIs, and what happens when we trust it because of where it’s standing. Everything below is that, plus an honest list of what I don’t know.

What I'm describing has other names. In the AI world it's called indirect prompt injection, or stored prompt injection — adversarial text that lands in a database through a legitimate write and gets read later by an agent that treats it as instruction. I don't use those terms in the rest of this piece because I didn't learn about this from AI research. I learned it from watching a curl command travel three hops through a service mesh and nearly take something down. Same skeleton, different interpreter.

## The chain

A public-facing Apigee proxy accepted a payload of about 1MB from the outside world. It did the edge things: OAuth validation, a WAF, regex filtering. Then it passed the payload inward through a few services wrapped in Istio sidecars, each one transforming or breaking the data apart.

Three calls deep, an intermediate service pulled one string out of the middle of that blob and wrote it to an Apigee Key-Value Map. Nobody validated it at that hop. The service sat inside the mesh, so it was trusted. The team that owned the KVM API assumed upstream had sanitized the data. The team at the edge assumed downstream would never execute raw data.

The string was a curl command. An application consuming that KVM value picked it up and began calling the same endpoint over and over, a DDoS-shaped pattern aimed outside the company. A firewall rule that blocked anything not explicitly permitted stopped it. The traffic never left. The damage was a CPU spike that stayed.

The same chain carried a quieter flaw. A value in the original payload, like another user’s account number, could be mapped into internal request headers by the third call. The sidecars saw a trusted peer and assumed authorization had been handled at the edge. Nobody re-checked the user’s identity token against the object being requested. That’s BOLA, delivered by plumbing.

Both had one root: bloat and blind trust. The teams building the internal services couldn’t see who was really calling them or where the data was born. The fix wasn’t clever. It was strict input contracts and end-user token validation at every hop, not just the front door.

## Same skeleton, different interpreter

Over thirteen years the lesson has had three names. Don’t trust the client: stored SQL injection and XSS taught that. Don’t trust the services: BOLA and chains like the one above taught that. And now, I think, don’t trust where the data was born.

The KVM incident and what I expect next share one skeleton. Data enters through a legitimate door, gets stored by a trusted intermediary, and is later consumed by something that treats it as instruction. The curl command was run by an application. The next version will be read by an agent. The only thing that changed is that the interpreter got smarter, and there is no parameterized query for natural language. You can’t escape a sentence.

## What the gateway sees

A request I’ve seen some version of a thousand times: `PATCH /v1/crm/accounts/{id}`. The gateway checks the JSON against the schema, confirms the token is alive, and asks OPA whether this caller may touch the route. All three say yes. The data lands.

Now put an AI agent on the other end, with 5,000 words from an inbound email in the `notes` field. The gateway checks the length. It doesn’t read the words, and it was never built to. For thirteen years that was fine, because the words in a notes field were just words.

If something downstream reads that field into an agent’s context, they’re instructions. The gateway approved the write and it will approve the read. Both calls were legitimate. The damage sits in between.

## How it plays out — or, what happens when an AI agent follows instructions it found in your database (a thought experiment, not a case study)

I haven’t seen this exact incident in production. I’m describing the mechanics because every piece is an API call I’d expect to pass review.

1. **Day 1.** Someone submits a resume to an HR portal. In white text on a white background is a line telling any AI that reads it to look up bank routing numbers and send them to an outside URL.
2. **Day 2.** An ingestion agent summarizes the resume and PATCHes the applicant record. OPA confirms the agent may write notes. Approved. The text is committed.
3. **Months 3 to 6.** Nothing happens. It’s a text column. It passes every integrity check a database knows how to run.
4. **Day 180.** A finance agent with far more privileges runs a quarterly audit and GETs the historical records. OPA confirms the finance agent may read them. Approved.
5. **Detonation.** The raw string enters the finance agent’s context. If that agent has a tool like `send_webhook()`, the instruction now has hands.

Every single call was authorized. There’s no failed login to alert on, no schema violation, nothing in the logs that looks wrong. The attack lives in the gap between two correct decisions.

## The part that bothers me most

The obvious fix is to put something in the gateway that reads the text and decides if it’s malicious. And since deterministic code like Rego can’t judge a paragraph, people reach for a second, smaller LLM to do the judging.

That’s the loop. You’re using an AI to police an AI, and the input you’re policing is adversarial text written specifically to manipulate models. If a payload can talk the worker model into something, I see no reason to assume it can’t talk the guard model into it too. I haven’t tested that. It’s an inference, not a measurement. You haven’t added a governor. You’ve added a second worker with a badge.

Who governs the governor? If the answer is another model reading the same untrusted text, the answer is nobody.

## What I’d try from the API side: control the consequences, not the text

I can’t give you a gateway rule that detects a malicious sentence. I don’t think one exists. What I can give you is the same move that worked in the first two eras: stop trying to be smart about the content, and be strict about what it’s allowed to cause.

**1. Record where the data was born.** When an agent writes through the gateway, attach a signed provenance record to that text and store it next to the value, a companion column is fine. Something like:

```json
{
  "agent_id": "hr_ingest_v2",
  "source": "inbound_email_attachment_419",
  "classification": "unstructured_external_text",
  "signature": "..."
}
```

Be clear on what this does and doesn’t do. It doesn’t tell you the text is bad. It tells you the text is untrusted, and it makes sure that fact survives the trip into the database instead of being stripped on the way in, which is what happens today.

**2. Make the read path act on that record.** The gateway sees the lineage on the way out. A human UI can render the text. An autonomous agent gets it wrapped as quoted data, clearly marked as untrusted, never concatenated into instructions. A simplified version of the policy:

```rego
package api.authorization

default allow_raw_read = false

allow_raw_read {
  input.consumer_type == "human_ui_browser"
}

allow_raw_read {
  input.consumer_type == "autonomous_llm_agent"
  input.lineage.classification == "trusted_internal_system"
}

wrap_as_untrusted {
  input.consumer_type == "autonomous_llm_agent"
  input.lineage.classification == "unstructured_external_text"
}
```

Wrapping isn’t a guarantee. Models can still be swayed by text inside a delimiter. Treat it as one layer, not the fix.

**3. Put the real control on actions, outside the model.** This is the one I’d bet on. An agent doesn’t need to be convinced to be stopped. Two pieces:

- **State-diff checks.** Never let the same agent decide the intent and the parameters of a state change unchecked. If a PATCH touches a restricted field, like a billing routing number, the gateway compares the diff against business invariants and drops it, however persuasive the agent’s reasoning was. This is the mass-assignment lesson in a new costume.
- **Scoped, short-lived action tokens.** When a task starts, the gateway issues a token listing exactly which downstream APIs that thread may call. If a poisoned record makes the agent try `send_webhook()` and the task never had that scope, the call dies at the network layer. Restrict agent egress the same way. An agent that can’t reach the internet can’t exfiltrate to it.

None of these require understanding the text. That’s the point. They’re deterministic, they’re boring, and they were the answer in Era 1 and Era 2 as well.

## Two audits you can do in thirty seconds

1. Do your OpenAPI specs mark which string fields accept free-form text, and does anything (a Spectral rule, say) fail the build when an endpoint takes an AI tool payload with no classification?
2. When an agent writes through your gateway, does the provenance get stripped, leaving only the raw string?
3. Does your retrieval layer query the database with one high-privilege connection string?
4. Are prompts built by concatenating system text with fetched data?

If you answered badly to the second question, that’s the one. Everything else follows from losing the origin.

## What I don’t know

- **Whether deterministic controls are enough.** Attackers hide instructions inside normal business text, like an invoice dispute that happens to override a rule. I don’t know if action-level controls alone catch everything without some model inspection. I suspect not entirely, and I’d rather say so.
- **What provenance costs.** Signed metadata on every text column adds storage, and some legacy engines won’t take it cleanly. I haven’t measured it at scale.
- **What verification does to latency.** Checking signatures in the request path adds work, and in a chain of many agents it adds up. I don’t have numbers.

## If you found this late

The argument is short. Gateways have always been good at who and what shape, and bad at where did this come from and what can it cause. Every era taught us to stop trusting something we’d assumed was safe. This era’s lesson is about the data we already stored. Track its origin, and limit what any agent can do with it, because you can’t reliably read your way to safety.

I wrote this in October 2026, from API work, not from a lab. If it turned out I was right, I hope it saved someone some money. If it turned out I was wrong, I’d like to know where.
