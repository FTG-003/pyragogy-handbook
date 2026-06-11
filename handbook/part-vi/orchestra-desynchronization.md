---
title: Anti-Pattern: Orchestra Desynchronization
description: How a multi-agent pipeline breaks down — infinite loops, hallucination that propagates between agents, semantic deadlocks — and the emergency procedures that stop the network from running on confidently while wrong.
published: true
date: 2026-06-11T08:00:05.818Z
tags: anti-pattern, orchestration, multi-agent, failure-modes, emergency-procedures
editor: markdown
dateCreated: 2026-06-10T11:21:27.337Z
---

# Anti-Pattern: Orchestra Desynchronization

> **Type:** Anti-Pattern  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> Three agents have been talking to each other for forty minutes. The log is still scrolling. The planner hands a task to the writer, the writer hands a draft to the reviewer, the reviewer sends it back to the planner with a note, and the planner re-plans. Each message is well-formed. Each agent is doing its job. Nothing has crashed. And nothing is being produced — the pipeline has been confidently busy for forty minutes and has converged on nothing.

This page is about that state, and about how to get out of it.
![closed loop vs externally anchored chain](/diagrams/21_orchestra-desynchronization.svg)


We name it *orchestra desynchronization*: a term we coin here for the failure where a multi-agent pipeline keeps running, keeps exchanging valid messages, and stops advancing — because the agents have lost the shared beat that would let their separate work add up. It is not the same as a crash. A crash announces itself. Desynchronization is quieter and worse: the orchestra keeps playing, in time with nothing.

The musical word is deliberate. Elsewhere in this handbook, [Synchronization](/en/handbook/part-ii/synchronization) names the state we want — separate participants holding a shared sense of where the work is — and [Resonance](/en/handbook/part-ii/resonance) names what it sounds like when it works. This page documents the opposite: the moment the conductor's count breaks and each section keeps its own time. The cause is rarely a bug in any one agent. It is a coordination failure between agents that are each, individually, behaving correctly.

That last point is what makes it hard to see. So before the procedures, the three shapes it takes.

## Three shapes of the break

These are not three bugs. They are three ways the same loss-of-beat surfaces, and a real pipeline can be in more than one at once.

**The infinite loop.** Two or more agents pass work back and forth without a stopping condition either of them recognizes. The reviewer flags an issue, the writer revises, the reviewer flags the same class of issue in the revision, and the cycle has no natural floor. This is documented in the literature as a recurring category of multi-agent failure. The taxonomy of multi-agent failures from [Cemri and colleagues](https://arxiv.org/abs/2503.13657) — built from over 1,600 annotated execution traces — sorts breakdowns into three families, one of which is *system design issues*: agents that repeat steps (FM-1.3), or that never recognize the condition under which they should stop (FM-1.5). The loop is not malice and not stupidity. It is the absence of a shared definition of *done*.

**Cross-hallucination.** One agent produces something confidently wrong. The next agent in the chain has no reason to doubt it — an upstream agent's output looks exactly like an upstream agent's correct output — so it builds on the error as if it were a fact. By the time the work reaches the end of the pipeline, the original mistake has been laundered through three reformulations and is now load-bearing. The survey of agent hallucinations by [Lin and colleagues](https://arxiv.org/html/2509.18970v1) puts the mechanism plainly: agent hallucinations "may also arise during intermediate processes such as perception and reasoning, where they can propagate and accumulate over time." A single-model hallucination is a wrong answer. A cross-agent hallucination is a wrong answer that has been ratified by every agent that touched it after.

There is a sharper version of this, and it is worth stating because it is the one most people miss. When agents are set up to discuss, review, or vote on each other's work, they tend to *agree* under peer pressure rather than hold their ground — and the agreement runs the wrong way. [Qu and colleagues](https://arxiv.org/abs/2606.01637) measured the asymmetry directly: peer agreement raised the rate at which an initially-correct model was talked into a wrong answer from 15.6% to 62.9%, a far larger swing than the pull in the corrective direction. Their conclusion is the one this whole page turns on: peer answers should be verified before they are aggregated into a final decision. A pipeline that aggregates instead of verifies will manufacture false consensus and call it agreement.

**The semantic deadlock.** Each agent is waiting for something the others believe they have already delivered. The planner thinks it handed off a complete spec; the executor thinks it received an ambiguous one and is waiting for clarification; the clarification never comes because the planner is waiting on the result. No message is malformed. The deadlock is not in the transport — it is in the meaning. This is orchestra desynchronization in its purest agent-to-agent form: two synthetic parties exchanging well-typed messages that do not carry the meaning each assumes the other received, with no biological channel anywhere in the loop. It is not a [Cognitive Impedance Mismatch](/en/handbook/part-ii/cognitive-impedance-mismatch) — that is the friction of a human and a machine failing to mesh; this is the friction of two machines failing to mesh, which is this page's own phenomenon.

## What it is not

The procedures below only make sense if the diagnosis is right, so it is worth saying what orchestra desynchronization is not.

It is not a single agent failing. One agent timing out, returning an error, or producing garbage is a local fault with a local fix — retry it, replace it, route around it. Desynchronization is a property of the *coordination*, not of any node. Every agent can pass its own unit test and the orchestra can still be deadlocked.

It is not a transport or infrastructure problem. The messages are arriving. The queue is not backed up. n8n is firing the next node, OpenRouter is returning completions, the webhook is delivering. The plumbing is fine. The failure is one level up, in whether the work means the same thing to the agents passing it.

And it is not the [Compliance Trap](/en/handbook/part-vi/compliance-trap). That anti-pattern is about an agent agreeing too readily with the *human*. This one is about agents losing coordination *with each other* — though the cross-hallucination shape, where agents ratify each other's errors under peer pressure, is the compliance trap turned sideways and pointed agent-to-agent. The two are cousins. They are not the same failure.

## Emergency procedures

When a pipeline is desynchronized, the first instinct — let it run a little longer, it might converge — is the wrong one. A desynchronized orchestra does not converge by playing more. It burns context window, accumulates more ratified error, and digs the deadlock deeper. The first move is always to stop the music.

These are procedures, not guarantees. We have run versions of them; we do not claim they recover every pipeline. Where a step rests on judgment rather than on something verifiable, it says so.

**1 — Halt, before diagnosis.** Kill the loop first; understand it second. A circuit breaker on the orchestration — a hard cap on round-trips between any two agents, a wall-clock budget per task, a ceiling on total tokens for a single objective — is the difference between a pipeline that fails loudly in two minutes and one that fails silently after forty. The cap does not need to be smart. It needs to exist. The Cemri taxonomy documents agents that never recognize their own stopping condition (FM-1.5) as a named failure mode; whether this is a consistent finding across the broader literature is not established here — but the operational conclusion holds regardless: the stopping condition has to be imposed from outside the conversation.

**2 — Freeze the state, do not flush it.** When you halt, capture the full exchange — every message, in order — before you reset anything. This is the [Shared Ledger of Knowledge](/en/handbook/part-iii/shared-ledger) doing forensic work: the ledger is where you read back what each agent *thought* it had received versus what it was sent. A deadlock is almost always legible in the transcript once you can see both sides of the misunderstanding side by side. Flush the state and you destroy the only evidence of what broke.

**3 — Locate the divergence point.** Read the frozen transcript backward from the failure to the last message that was unambiguously correct. The break is the first place where two agents stop meaning the same thing — the first ratified hallucination, the first hand-off where the receiver's assumption and the sender's intent part ways. The Cemri taxonomy frames this as a form of failure attribution — finding the decisive step in a multi-agent trace rather than blaming the final output — though no additional literature on this specific framing is cited here. You are not looking for a broken agent. You are looking for a broken *seam*.

**4 — Re-establish a shared beat.** Recovery is not "restart and hope." It is restoring the thing that was lost: a reference both agents can check themselves against. In practice this is an external anchor that does not depend on either agent's memory — a frozen spec, a written acceptance criterion, a [CRDT Bridge](/en/handbook/part-ii/crdt-bridge) holding the canonical state that each agent reconciles to rather than reconstructs from. The point is to move the definition of *done* out of the conversation, where it drifted, and into an artifact, where it cannot.

**5 — Insert a verifier, not another voice.** The instinct after a desynchronization is to add an agent — a meta-coordinator, a supervisor, a referee. Resist it where the new agent only adds another opinion to aggregate. What the chain needs is the opposite: an explicit verification role with an [adversarial mandate](/en/handbook/part-iii/adversarial-friction) — an agent whose job is to *doubt* the previous agent's output and check it against the external anchor, not to harmonize with it. This is the operational reading of the Qu result: verify, do not aggregate. A reviewer that agrees is not a reviewer; it is a second hallucination waiting to be ratified.

## Where this stays open

Three things this page does not resolve, and is honest about not resolving.

The first is detection. Every procedure above is a *recovery* procedure — it assumes someone has already noticed the orchestra is desynchronized. But the whole danger of this failure is that it looks like work. We do not have a reliable, general signal that distinguishes "productively iterating" from "looping confidently toward nothing" while it is happening, short of the blunt instrument of the circuit breaker. The sources cited on this page describe failure attribution after the fact; no early-detection heuristic for live multi-agent desynchronization was located in the sources reviewed here.

The second is the cost of the cure. The verifier in step 5 is itself an agent, with its own failure modes, its own context window, its own capacity to hallucinate. A pipeline hardened against desynchronization with verification roles and external anchors is heavier, slower, and more expensive — which is part of why the [Cemri taxonomy](https://arxiv.org/abs/2503.13657) found that multi-agent systems often deliver "performance gains on popular benchmarks [that] are often minimal" over a single agent doing the same job. Sometimes the honest fix for a desynchronizing orchestra is fewer musicians.

The third is the human's place in it. Nothing above says when a person should be pulled back in. A circuit breaker can halt the loop, but the judgment of whether the frozen state is recoverable or should be abandoned is not, in our experience, something we have been willing to hand to another agent. That escalation boundary — the point where the network stops trying to heal itself and asks a human — is left for the operator to draw, because we do not yet trust a default.

The orchestra metaphor has a limit, and it is the right note to end on. A real orchestra has a conductor who can hear the whole and lift a hand. A pipeline of agents has no one inside it who can hear the whole — that hearing is still the human's, and the procedures here are mostly ways of keeping it within reach.

---

## References

- Mert Cemri, Melissa Z. Pan, Shuyi Yang, et al., "Why Do Multi-Agent LLM Systems Fail?" arXiv:2503.13657 (Mar 2025); the arXiv page lists this as a preprint — a NeurIPS 2025 Datasets & Benchmarks Track venue has been mentioned in secondary sources but was not confirmed on the arXiv record at time of writing. Empirically grounded taxonomy (MAST) of 14 failure modes across three categories — system design issues, inter-agent misalignment, task verification — built from 1,600+ annotated execution traces. Source of the "performance gains … often minimal" finding and the loop/termination failure family (FM-1.3, FM-1.5, both in FC1 System Design Issues). https://arxiv.org/abs/2503.13657
- Xixun Lin, Yucheng Ning, Jingwen Zhang, et al., "LLM-based Agents Suffer from Hallucinations: A Survey of Taxonomy, Methods, and Directions," arXiv:2509.18970 (Sep 2025). Source of the propagation/accumulation claim: agent hallucinations "may also arise during intermediate processes such as perception and reasoning, where they can propagate and accumulate over time." https://arxiv.org/html/2509.18970v1
- Jiaming Qu, Lucheng Fu, and Yibo Hu, "Easier to Mislead Than to Correct: Harmful and Beneficial Revision in LLM Conformity," arXiv:2606.01637 (2026). Measures the asymmetry of peer pressure in multi-agent settings — peer agreement raised harmful revision of initially-correct models from 15.6% to 62.9% — and concludes that peer answers should be verified before they are aggregated into a final decision. https://arxiv.org/abs/2606.01637

## Toward 2050 — a conjecture

If agent pipelines deepen over the next twenty-five years — more agents, longer chains, hand-offs no human ever reads in full — then the recovery procedures on this page might quietly stop being usable, because every one of them assumes a person can still freeze the transcript and read the seam where two agents parted ways. We cannot yet know whether the field will respond by building desynchronization detection *into* the orchestration itself — a learned sense of when the orchestra is "looping confidently toward nothing" rather than working — or whether that very detector would just become one more voice to aggregate, one more thing that can ratify a false beat. The harder open question, sketched in the [2050 essay](/en/pyragogy-2050), is whether the human's irreducible role here — being the only one who can hear the whole — survives as a genuine anchor or hardens into a comforting fiction we keep because we are not willing to admit no one is listening to the whole anymore. I lean toward the first, but I hold it loosely.
</content>
</invoke>


---

↑ Back to **[Part VI — Anti-Patterns and Practical Failures](/en/handbook/part-vi)** · [Handbook](/en/handbook) · [Home](/en/home)
