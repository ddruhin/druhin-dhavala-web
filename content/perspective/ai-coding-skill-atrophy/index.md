---
title: "AI Coding Journey vs Destination, the Skill atrophy"
date: 2026-09-25
lastmod: 2026-09-25
draft: false

description: "AI ships better code faster — but the debugging sessions, wrong turns, and war-room scars that once built engineers into experts are quietly disappearing with it."
canonicalURL: "https://www.druhindhavala.com/perspective/ai-coding-skill-atrophy"

categories: ["Perspective"]
tags: ["AI coding", "software engineering", "skill atrophy", "developer culture"]
frameworks: ["The Road vs. The Destination"]

author: "Druhin Dhavala"
firstPublished: "2026-09-25"
originalPublication: "https://www.druhindhavala.com/perspective/ai-coding-skill-atrophy"
---

**We Already Left the Road**

*AI writes better code, faster. What it's quietly taking with it is the debugging sessions, wrong turns, and war-room scars that used to turn people into engineers.*

There's a difference between traveling and arriving, and I don't think enough people are talking about it.

Picture a group of friends driving an SUV from point A to point B. You don't just cover distance — you get a flat tire at 2 AM and it becomes a story. You take a wrong turn that costs three hours and it becomes a scar you're weirdly fond of. Someone forgets to fill the tank and you're all pushing the damn thing half a mile down a dark road, laughing because what else are you going to do. You arrive tired, dirty, and a little different than when you left.

Now picture everyone on a bus instead, asleep from A to B. You arrive faster. Cleaner. Nobody's back hurts. And there's nothing to talk about when you get there.

That's roughly what's happening to software engineering right now. AI coding assistants aren't producing worse code — the output is better, faster, cheaper, genuinely. **What they're quietly killing is the process that used to turn a junior developer into someone who actually understands the system they're shipping.**

You wouldn't know it from LinkedIn, though. Ninety percent of what shows up in my feed these days is some flavor of AI content — tools, prompts, "10 ways Copilot made me 10x." It's a bus terminal. Everyone comparing arrival times. Nobody asking what happened to the road, or whether it mattered that we drove it.

**The old way: slow, expensive, and how people actually learned**

**I wrote my first book eleven years ago**. No AI, no Grammarly, just me and a very patient editor. After four rounds of proofreading it still had mistakes in it — mistakes that were mine, that I could point to and say, yeah, that one's on me. It took months. It was not efficient. But everyone on that project grew through it, in the unglamorous way people grow: bonding over deadlines, debugging sessions that went nowhere for hours before they suddenly went somewhere. When we finally cracked something, it wasn't just a fix — it became a story we told for years. And those stories are part of how coding stopped being a niche skill and became something people pass down.

**The human wasn't a checkpoint in that process**. Not a reviewer signing off at the end of someone else's work. **The human was inside every decision, every mistake, every recovery**. That's not nostalgia talking — that tight coupling of people, problems, and time was the actual substance of the thing.

*I want to be fair to the other side of this, because it's real too*. AI standardized a lot of sloppy process. It added guardrails that were overdue. It cut costs and time-to-market in ways that matter to people who aren't me — a startup with six months of runway doesn't care about anyone's character arc. And it took a real load off individual engineers; you can ask a model a question instead of grinding alone for three hours at 11 PM. I'm not going to pretend that's nothing.

But there's a cost sitting underneath the savings, and it's not showing up on anyone's dashboard.

That twenty-hour triaging call where five engineers slowly, painfully uncovered a race condition in production? An AI model would surface that fix in seconds now. The fix would be correct. **And the five engineers would learn essentially nothing from it**, because they were never really in the room for it — the room happened somewhere else, inside a context window, and then it was gone.

The commit that became famous inside a company because of everything around it — the war room, an SVP on the phone, a junior engineer who noticed something three seniors missed — none of that context ever made it into a doc. It lived in the people who were there, in the specific way that only lived experience sticks. AI doesn't produce those people anymore, because it skips the room.

**What the research is starting to show**

Here's the part that actually worries me, and it's not just a hunch — Anthropic ran a study on almost exactly this question in early 2026. They took 52 mostly junior developers, all with at least a year of Python, and had them learn an unfamiliar async library called Trio. Half worked with an AI assistant, half worked from docs alone. The AI group finished about two minutes faster — not a meaningful difference. But on a comprehension quiz given right after, they scored seventeen points lower on average. The ones who fully offloaded the task to the model did worst of all; the ones who kept asking it "why," rather than "what's the fix," did almost as well as the group with no AI at all. Anthropic's own conclusion, more or less: **the productivity gains might be quietly eating the skills you'd need later to catch the AI when it's wrong.**

That tracks with what I'd guess is happening industry-wide, even if nobody's measured all of it yet. We're producing more code than any point in history, and — I suspect — fewer people who could explain, from first principles, why any specific piece of it exists.

**Who fixes it when it breaks**

Here's where it gets uncomfortable.

A few years from now, some system built largely with AI assistance is going to fail in a way nobody predicted. Who fixes it? You can't point AI at a problem AI created if the failure was never in anyone's training data. And you can't point humans at it either, if those humans never went through the process that would've taught them how the system actually thinks — because they were reviewing, not building. Reviewing ten thousand lines of generated code is not the same thing as understanding it. Understanding comes from building something, breaking it, fixing it badly, then fixing it right. From the trip, not the destination.

*The bus gets you there faster. Nobody on it knows how to change a tire when it blows.*

I genuinely don't know if AI is going to end anything as dramatic as "humanity" — that's above my pay grade. But I do know this: if the journey disappears, the next generation shows up at the destination with clean hands and no memory of how they got there. That's not a skill gap you patch with a training course. That's a break in the line, and unlike code, a broken line doesn't get rewritten from a prompt.

If there's a hopeful version of this, it isn't refusing to use the tools — that ship left the dock a while ago. It's something smaller: using AI to sharpen what a human built first, instead of letting AI build while a human just signs off. That's a small difference in how you use the tool. It's the entire difference in the trip. It's the gap between letting the model drive while you sleep, and keeping your hands on the wheel while it tells you what's around the next curve.
