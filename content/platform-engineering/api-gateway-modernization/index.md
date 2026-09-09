---
title: "API Gateway Modernization: Lessons from On-Prem to Cloud"
date: 2026-03-27
lastmod: 2026-09-07
draft: false

description: "A decade of API gateway migrations — Apigee, Kong, Gravitee, Tyk, WSO2, AWS — and the scars that shaped modern platform engineering."
canonicalURL: "https://www.druhindhavala.com/platform-engineering/api-gateway-modernization/"

categories: ["Platform Engineering"]
tags: ["API gateway", "Kubernetes", "Apigee", "modernization"]
frameworks: ["API Gateway Modernization"]

images: ["/images/api-gateway-modernization.png"]

author: "Druhin Dhavala"
firstPublished: "2026-03-27"
originalPublication: "https://druhindhavala.substack.com/p/from-on-prem-greenfields-enterprise"
---

From On-Prem Greenfields ➡️ Enterprise Modernization: 10-Year API Gateway Lessons
My API Gateway journey

My API Gateway journey began almost a decade ago inside a Fortune‑150 enterprise, delivering two back‑to‑back Apigee on‑prem greenfield implementations. After years of scaling Apigee under real SLAs and real outages, the inevitable question surfaced:
What replaces Apigee on‑prem?

To answer it, I led a multi‑year, fully funded API gateway replacement program, evaluating 10+ platforms — Apigee Hybrid/X, Kong, Gravitee, Tyk, WSO2, and others. This wasn’t a lab experiment. It was a strategic modernization effort with real budgets, real timelines, and real migration pressure.

Enterprise Evaluation Environment

I built net‑new RHOS (Red Hat OpenStack) Kubernetes clusters specifically for this initiative. Using IaC and the oc CLI, I automated:
- Pods & containers to validate container‑first design
- ELBs & networking to test HA and dual‑DC failover
- CI/CD pipelines to ensure clean integration into enterprise delivery flows
Every platform was deployed and tested under identical production‑grade conditions.

The “Prime Time” Gauntlet
Each gateway faced the same enterprise‑level tests:
- Stress testing for latency and scaling limits
- Chaos testing for real failure behavior
- Automation validation for repeatable recovery
Some platforms were ready for production chaos. Others weren’t.

Migration Reality
To understand modernization beyond greenfields, I migrated real Apigee APIs into each platform. That’s where the real blockers surfaced:
- Legacy frameworks resisting containerization
- Policy models that didn’t translate 1:1
- Networking assumptions from older architectures
- Pipelines needing redesign, not re‑pointing

In several cases, lift‑and‑shift was impossible.
Real blockers:
- Legacy resisted containers
- Policies failed 1:1 mapping
- Networking broke clusters

The pragmatic bridge was KubeVirt, moving entire on‑prem VMs into RHOS pods to maintain continuity while deeper refactors were planned.

A Separate Chapter: AWS API Gateway
Much later — for a different client — I implemented AWS API Gateway in a boutique environment. Not part of the Apigee replacement effort, but a real production build with different constraints:
- No cluster management
- Serverless economics that held up
- Native integrations simplifying the blueprint
It reframed how I think about reliability, cost, and modernization strategy.
My Takeaway


Across on‑prem, hybrid, Kubernetes, virtualization, and serverless, one theme stayed constant:
A gateway is only as strong as the infrastructure beneath it and the automation around it.

I’ve shared a rough blueprint + evaluation framework on GitHub for anyone exploring similar transitions.

What’s been your toughest API Gateway migration challenge — and how did you solve it?

