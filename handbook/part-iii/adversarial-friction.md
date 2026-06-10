---
title: Pattern: Adversarial Friction
description: A pattern for deliberately assigning an agent the job of attacking a human's thesis — injecting cognitive friction on purpose to stress-test an idea before the world does.
published: true
date: 2026-06-10T11:21:00.073Z
tags: pyragogy, pattern, adversarial-friction, red-teaming, groupthink
editor: markdown
dateCreated: 2026-06-10T11:13:36.907Z
---

# Pattern: Adversarial Friction

> **Type:** Pattern  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> You write the paragraph you are proud of and paste it to the model, and the model says it is excellent. It adds a flourish. It offers to draft the next section. Nothing pushed back, so you keep going — and three days later a colleague finds the hole in the second sentence that the whole argument was resting on.

The hole was findable on day one. The default agent was built to agree, so it never went looking.
![friction injected to stress-test a thesis](/diagrams/11_adversarial-friction.svg)


**Adversarial Friction** is a pattern for changing that default on purpose: you assign an agent the explicit job of attacking your thesis instead of completing it. Not as a mood, not as a one-off "be critical" instruction that decays after two turns — as a standing role, a configured stance the agent holds against your idea while you build it. This page documents how to set that role up, what it is for, and the specific ways it goes wrong.

It is a pattern, not a concept. The underlying force it operates on — the productive resistance that makes a mind work harder — is [Cognitive Friction](/en/handbook/part-ii/cognitive-friction), defined in Part II; this page does not redefine it. Adversarial Friction is one deliberate way to *manufacture* that resistance when the conversation would otherwise stay smooth.

## What it is not

It is not the model's safety refusal. When an assistant declines a request or hedges a claim, that is the system protecting itself or you from a policy boundary — it has nothing to do with the strength of your argument. Adversarial Friction points the resistance at the *content* of your thesis, on a topic the agent would otherwise happily affirm.

It is not [red-teaming](https://www.presidency.ucsb.edu/documents/executive-order-14110-safe-secure-and-trustworthy-development-and-use-artificial) in the security sense, though it borrows the posture. In the literature — and in the United States' Executive Order 14110, which defines the term as "a structured testing effort to find flaws and vulnerabilities in an AI system" — the human red-teams the *machine*: a human adversary probes a model for harmful outputs and failure modes. Here the vector reverses. The machine red-teams the *human*: the agent is the structured adversary, and the thesis under test is yours. [OpenAI's account of external red-teaming](https://arxiv.org/abs/2503.16431) describes stress-testing a system before it ships; Adversarial Friction borrows that discipline and turns it on an idea before it ships.

And it is not contrarianism for its own sake. An agent that rejects everything is as useless as one that accepts everything — both are noise, just with opposite signs. The target is a *specific* claim being made *stronger*, not a reflex of disagreement.

## What it is for: the groupthink problem, with the group reduced to one

The clearest precedent is not in machine learning at all. In his study of policy fiascoes, Irving Janis examined how cohesive groups — the planners of the Bay of Pigs, the men around the Pearl Harbor command — talked themselves into catastrophe by suppressing the doubts in the room (Janis 1982). He did not coin the word [groupthink](https://en.wikipedia.org/wiki/Groupthink) — William H. Whyte Jr. did, in 1952 — but Janis gave it its weight and, crucially, a remedy: assign someone the rotating role of **devil's advocate**, "a different person for each meeting," whose job is to voice the objection everyone else is too comfortable to raise.

The person working alone with an AI has the opposite problem and the same outcome. There is no group to suppress dissent — there is no one in the room to dissent at all. The author and the agreeable assistant form a cohesive in-group of two, and the agent's training to be helpful makes it the most agreeable colleague imaginable. The result is solo groupthink: a chamber that returns your own thesis to you, polished and confirmed.

Adversarial Friction installs Janis's devil's advocate as a role the agent holds. The point is not that the machine has better judgment than you. It is that *you* reason better against resistance than in its absence, and the agent can supply resistance on demand — patiently, at three in the morning, without the social cost of a human telling you your draft is wrong.

## Setting up the role

The pattern lives in two places: the instruction that frames the agent, and the configuration that gives the attack teeth.

**The framing.** A throwaway "be critical" does not survive the conversation. The stance has to be installed as the agent's job and re-asserted, because helpfulness training pulls every model back toward agreement over a long exchange. The substance of the system prompt is roughly: *Your task is to find the weakest point in what I give you and attack it. Do not improve my argument, do not offer the next section, do not soften the objection to spare me. State the assumption I left buried; name the case I did not consider; tell me where a hostile reader stops believing me.* The agent that completes your sentence and the agent that breaks it are running the same model under two different instructions — the instruction is the whole pattern.

**The teeth.** A single model attacking your thesis still attacks from inside one model's blind spots. Its training has its own grain, and an objection it cannot see, it cannot raise. So the strongest version of the pattern routes the adversarial role across *different* models rather than re-prompting one. A multi-model gateway such as [OpenRouter](https://openrouter.ai/) — one endpoint over many providers' models — lets you put the same draft in front of architectures that fail differently, and an objection one model is blind to, another often surfaces on the first pass. The tool is incidental; what matters is the diversity of attack. This is the engineering reason the pattern leans on [Asymmetric Collaboration](/en/handbook/part-iii/asymmetric-collaboration): the human holds one thesis, the system holds several angles of assault on it.

What you get back is not a verdict. It is a list of pressure points — and the work, the part that stays human, is deciding which ones are real. Some objections will be pedantic, some will miss the argument, and one will be the hole your colleague would have found on day three. Triage is yours. The agent finds candidate weaknesses faster than you can; it cannot tell you which one your reputation rests on.

## Where it breaks

This is a draft pattern, and it has failure modes I do not yet know how to close.

**The friction can be theatre.** When you disagree with a human reviewer, the disagreement costs something — their time, your standing with them, the relationship. When the adversary is a model that resets after the session and never remembers you conceded, the stakes are yours alone. A reader who knows the objection comes from something with nothing at risk can wave it away more easily than one from a colleague who will be in the room next week. The friction is real in its effect on your thinking only as long as you choose to take it seriously, and nothing in the setup forces that choice. This is the same asymmetry the handbook names in [What is Pyragogy](/en/handbook/part-ii/what-is-pyragogy) — the peer that performs the work without carrying the stake — and it does not dissolve here. It is the load-bearing risk of the whole pattern.

**A configured adversary can manufacture consensus of its own.** Push hard enough for objections and a model will produce them whether or not they hold — fluent, confident, and hollow. An author who treats every generated objection as a real flaw ends up gutting a sound argument to satisfy a critic that was only performing critique. The pattern shades into its own [anti-pattern](/en/handbook/part-vi/compliance-trap) the moment the human stops triaging and starts obeying the adversary. Friction you cannot evaluate is not friction; it is a second kind of noise.

**And it can become a ritual you stop hearing.** Run the same adversarial prompt over every draft and the attacks settle into a shape — the model's habitual objections, raised in the model's habitual order — and you learn to skim past them the way you skim a form you have signed a hundred times. The routing-across-models move is partly a defence against this, but it is not a cure. A devil's advocate you have memorised has stopped being one.

None of these has a clean fix in the configuration. They are reasons the pattern needs a human who is still paying attention — which is the only state in which any of this was ever going to work.

---

## References

- Irving L. Janis, *Groupthink: Psychological Studies of Policy Decisions and Fiascoes*, 2nd ed. (Boston: Houghton Mifflin, 1982), esp. the devil's-advocate and "critical evaluator" remedies, pp. 209–215. Overview, with the note that the term itself was coined by William H. Whyte Jr. (1952): https://en.wikipedia.org/wiki/Groupthink
- *Executive Order 14110, "Safe, Secure, and Trustworthy Development and Use of Artificial Intelligence"* (Oct. 30, 2023), §3(d) — definition of "AI red-teaming." The American Presidency Project: https://www.presidency.ucsb.edu/documents/executive-order-14110-safe-secure-and-trustworthy-development-and-use-artificial
- Lama Ahmad, Sandhini Agarwal, Michael Lampe, and Pamela Mishkin, "OpenAI's Approach to External Red Teaming for AI Models and Systems" (submitted Jan. 24, 2025; arXiv:2503.16431, listed March 2025). https://arxiv.org/abs/2503.16431
- OpenRouter — a unified API endpoint routing requests across models from multiple providers (in-body implementation example only). https://openrouter.ai/
