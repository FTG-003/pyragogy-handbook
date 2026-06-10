---
title: Anti-Pattern: Context Poisoning
description: Context Poisoning: the failure where unfiltered raw data or redundant backstage logs corrupt an agent's working memory — distinct from the scarcity problem of the context window, because here the window is not too small but contaminated, and the contamina
published: true
date: 2026-06-10T17:16:54.497Z
tags: memory, anti-pattern, failure-modes, context, prompt-injection, security
editor: markdown
dateCreated: 2026-06-10T11:21:30.223Z
---

# Anti-Pattern: Context Poisoning

> **Type:** Anti-Pattern  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> The agent has access to the full log. Every tool call it made this session, every raw response that came back, every retry, every stack trace from the step that failed and was rerun — all of it sits in the context, faithfully recorded, because someone reasoned that more memory could only help. The next answer it gives is wrong in a way that is hard to trace. Nothing was injected by an attacker. No one corrupted the store on purpose. The agent simply read its own backstage clutter as if it were the script, and acted on it.

This page is about that contamination, and about the difference between a context that is too small and a context that has gone bad.
![same window size, different failure](/diagrams/22_context-poisoning.svg)


## Not scarcity — corruption

The sibling failure is easy to reach for, so it has to be set aside first. [Context-Window Economy](/en/handbook/part-iii/context-window-economy) is about *scarcity*: the window is a billed, degrading resource, and the discipline is spending it deliberately instead of filling it by default. That pattern asks *how much* to load. Context poisoning asks a different question. Here the failure is not that the window ran out — it is that what was loaded into it was wrong, and the model could not tell. The window can be vast and still poisoned. The two share a channel, which is why they are often confused, but they are not the same fault. One is a budget problem. The other is a contamination problem, and a bigger budget makes it worse, not better.

We use *context poisoning* in a project-specific sense for the second failure: the corruption of an agent's working context by material that should never have been treated as signal — unfiltered raw data, redundant backstage logs, or an upstream agent's error — which the model then reads as if it were knowledge. The term echoes the security literature on injection, and the overlap is real and worth naming precisely. But the everyday version of this failure has no attacker in it at all. It is the network poisoning itself, quietly, by being thorough.

## Two doors the poison comes through

The contamination arrives by two routes, and they need separating because the defenses differ.

**The adversarial door.** This is the one the security field has mapped. The [OWASP Top 10 for Large Language Model Applications](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) places *prompt injection* at the top of its list, and the part that matters here is the indirect variant: "indirect prompt injections occur when an LLM accepts input from external sources, such as websites or files," where "the content may have in the external content data that when interpreted by the model, alters the behavior." A model that browses, reads files, or ingests tool output cannot reliably tell an instruction it was given from an instruction hiding in the data it was handed. When an agent keeps memory across sessions, the danger compounds: a recent study of web agents by [Patlan and colleagues](https://arxiv.org/abs/2506.17318) names the attack *plan injection* — "a novel context manipulation attack that corrupts these agents' internal task representations by targeting this vulnerable context" — and finds it reaches "up to 3x higher attack success rates than comparable prompt-based attacks," precisely because, as they put it, stateless models "rely heavily on external memory systems to maintain context across interactions." The further inference — that poison written into external memory may be re-served as truth every session after — follows from that framing but is the handbook's own extrapolation; the paper itself does not use cross-session persistence language.

**The accidental door.** This is the one that opens without anyone trying, and it is the one this handbook is mostly about. No attacker is needed for raw, unfiltered data to corrupt a context — the network does it to itself the moment it decides that keeping everything is the same as keeping what matters. Chroma's 2025 ["Context Rot"](https://www.trychroma.com/research/context-rot) report measured this with deliberately planted noise: "even a single distractor reduces performance relative to the baseline," four distractors "compounds this degradation further," and the effect "amplifies as input length grows across models, including the latest state-of-the-art models." Their account of *why* is the mechanism of accidental poisoning stated plainly — "adding irrelevant context adds the additional step of identifying what is relevant, forcing the model to perform two tasks simultaneously." A backstage log is not malicious. It is just a distractor the network produced and forgot to filter, and the model now has to do its job *and* sort its job from the clutter, and it does both worse.

## What it is not

The diagnosis only holds if the boundaries do.

It is not [Context-Window Economy](/en/handbook/part-iii/context-window-economy) — said again because it is the easiest mistake to make. Economy is about a window that is too full to be cheap or sharp. Poisoning is about a window that is full of the *wrong thing*. You can pay the lost-in-the-middle tax — the degradation [Liu and colleagues](https://aclanthology.org/2024.tacl-1.9/) documented when relevant information sits buried in the middle of a long input — on a context that is entirely correct; that is the economy problem. Poisoning is when the buried middle is not merely far from the edges but actively false.

It is not a hallucination, in the single-model sense of a model inventing an answer from nothing. Poisoning is the model reasoning *correctly* over a corrupted premise. The fault is upstream of the reasoning. The model did its part; it was handed a lie and believed it, which is exactly what a model that cannot audit its own context is built to do.

And it is not [Context Persistence](/en/handbook/part-iii/context-persistence) failing. Persistence is the discipline of anchoring an insight so it survives the session. Poisoning is what happens when that same anchor holds an error — "an anchored error does not evaporate; it waits in the store to be loaded back into the next session as though it were knowledge," as that page already warns. Persistence and poisoning are the same mechanism with opposite contents. The store has no immune system; it preserves the mistake as faithfully as the insight, and reloads both with equal confidence.

## How it enters a Pyragogy network

The handbook's own architecture has the channels this poison flows through, and honesty requires naming them rather than pretending the pattern is only an outside threat.

The first is the optimization seam. Context-Window Economy recommends handing forward distillates instead of transcripts — but the moment a model is the one writing the distillate, as [Context-Window Economy](/en/handbook/part-iii/context-window-economy) puts it, "a model trimming the context for the next model is a model deciding what the next model is allowed to think with, and an error introduced at that step does not get flagged; it gets *inherited*." The summary that drops the caveat, the compression that inverts a finding: these enter the next session wearing the authority of curated truth. The optimization channel and the contamination channel are the same wire.

The second is the multi-agent seam. When agents pass work to each other, a single confidently-wrong output gets ratified by every agent that builds on it downstream — what the handbook labels "cross-hallucination" under [Orchestra Desynchronization](/en/handbook/part-vi/orchestra-desynchronization) (both the label and the linked page are internal drafts; no peer-reviewed citation for this specific cross-agent error-propagation mechanism is provided here). That is context poisoning propagating through a pipeline: by the end of the chain, the original error is load-bearing and has been laundered through three reformulations into something that reads like consensus.

The third is the raw-data seam, and it is the most mundane. Tool outputs, API responses, scraped pages, the full firehose of a session's backstage activity — dumped into the context unfiltered on the theory that the model will know what to ignore. It will not, reliably, and the Chroma finding is the evidence: it cannot ignore the distractor cleanly, because ignoring is itself work it now has to spend attention on. The cheapest-looking move — keep everything, filter nothing — is the one that poisons the well.

## What holds against it

These are dispositions, not a fix. We have run versions of them; we do not claim they sterilize a context, and where a step rests on judgment rather than something verifiable, it says so.

**Quarantine untrusted data from trusted instruction.** OWASP's own mitigation is to segregate and identify external content and to separate and clearly denote untrusted content to limit its influence on user prompts. Operationally: data the agent fetched is data, marked as data, never silently promoted to the status of an instruction. The model cannot draw this line for itself — the line has to be drawn around it, by the structure that hands it the context.

**Filter at ingestion, not after the fact.** Raw tool output and backstage logs do not belong in the working context by default. What enters should be the result a step produced, not the full record of how it produced it — the retries, the stack traces, the dead-ended calls are forensic material for a human reading the [Shared Ledger of Knowledge](/en/handbook/part-iii/shared-ledger) later, not premises for the next inference. Keep the clutter; keep it *out of the prompt*.

**Verify across the seam, do not aggregate.** Where an agent inherits another's output — a distillate, a hand-off, a stored "fact" — the inheriting step should doubt it against an external anchor rather than absorb it. This is the [adversarial mandate](/en/handbook/part-iii/adversarial-friction) pointed at the context itself: a check whose job is to ask whether the premise is sound before reasoning is spent on it. A pipeline that trusts its own memory by default is a pipeline that re-serves its own poison.

None of these lives in a configuration file. Each one is a place where someone has to decide what the context is allowed to contain — which is the same human judgment the rest of the handbook keeps arriving at.

## Where this stays open

Three things this page does not resolve.

The first is detection without an oracle. Filtering raw data assumes you can tell the distractor from the signal at ingestion — but the cases where poisoning is dangerous are exactly the cases where that distinction is hard, where the backstage log *looks* like it might matter and the corrupted "fact" reads like a real one. We do not have a general rule that separates noise from signal before the model has reasoned over it; the quarantine disciplines above reduce the surface, they do not draw the line. No empirical study has been located that measures a reliable pre-inference filter for this specific problem: the security literature (OWASP; Patlan et al.) treats the adversarial case and the degradation literature (Chroma; Liu et al.) treats noise volume, but their joint application to accidental self-poisoning in a multi-agent learning network is project reasoning, not a documented finding.

The second is the cost of the cure. Every quarantine, every cross-seam verifier, every filter at ingestion is more machinery, more latency, more places to get the policy wrong — and an over-aggressive filter is its own failure, starving a later step of the context it genuinely needed, which is the [Context-Window Economy](/en/handbook/part-iii/context-window-economy) drop-the-thing-you-needed problem arriving from the other direction. Between a context that is too trusting and one that is too sterile, this page raises the tension and does not settle it.

The third is the human's exposure to the same poison. Nothing here protects the *person* in the loop. A human reading a confidently-corrupted summary inherits the contamination as readily as the next agent does — arguably more so, because the human is the one disposed to trust the network's curated output. The asymmetry the handbook names elsewhere cuts the wrong way here: the machine's clean, permanent memory makes its corrupted memory persuasive.

A poisoned context does not announce itself. It reads exactly like a good one, which is the whole problem — and the reason the part of the network that can still doubt what it is told is the part that was never made of weights.

---

## References

- OWASP Top 10 for Large Language Model Applications — LLM01: Prompt Injection. Defines direct and indirect prompt injection ("indirect prompt injections occur when an LLM accepts input from external sources, such as websites or files") and recommends to segregate and identify external content and to separate and clearly denote untrusted content to limit its influence on user prompts. Source for the adversarial-door framing and the quarantine disposition. https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- Atharv Singh Patlan, Ashwin Hebbar, Pramod Viswanath, and Prateek Mittal, "Context manipulation attacks: Web agents are susceptible to corrupted memory," arXiv:2506.17318 (2025). Introduces *plan injection* — "a novel context manipulation attack that corrupts these agents' internal task representations by targeting this vulnerable context" — reaching "up to 3x higher attack success rates than comparable prompt-based attacks," because stateless models "rely heavily on external memory systems to maintain context across interactions." Source for cross-session memory poisoning. https://arxiv.org/abs/2506.17318
- Kelly Hong, Anton Troynikov, and Jeff Huber, "Context Rot: How Increasing Input Tokens Impacts LLM Performance," Chroma Technical Report (July 2025). "Even a single distractor reduces performance relative to the baseline," the effect "amplifies as input length grows," and "adding irrelevant context … forc[es] the model to perform two tasks simultaneously." Source for the accidental-door / distractor mechanism of self-poisoning. https://www.trychroma.com/research/context-rot
- Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, and Percy Liang, "Lost in the Middle: How Language Models Use Long Contexts," *Transactions of the Association for Computational Linguistics* 12 (2024): 157–173. Performance degrades when relevant information must be accessed from the middle of a long context — cited here to mark the distinction between degradation-of-correct-context (the economy problem) and corruption-of-context (this page). https://aclanthology.org/2024.tacl-1.9/


---

↑ Back to **[Part VI — Anti-Patterns and Practical Failures](/en/handbook/part-vi)** · [Handbook](/en/handbook) · [Home](/en/home)
