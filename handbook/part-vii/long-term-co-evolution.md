---
title: Long-Term Cognitive Co-Evolution
description: What happens to a mind, and to a model, after years of permanent structural coupling? Two slow degradations run in parallel — the human hollows, the model collapses on its own output — and the handbook cannot yet say where they meet.
published: true
date: 2026-06-10T16:59:46.105Z
tags: pyragogy, cognition, open-question, model-collapse, dependency, co-evolution
editor: markdown
dateCreated: 2026-06-10T11:21:36.322Z
---

# Long-Term Cognitive Co-Evolution

> **Type:** Open Question  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> A practice held for a year. Every day the same coupling: you bring a half-thought, the model answers, you push back, it holds the thread you dropped. On day one you could feel the work. By month nine the loop is so smooth you no longer notice it running — which is exactly the moment you can no longer tell whether the loop is still asking something of you, or quietly doing it instead.

This page is about that horizon, and it does not pretend to see across it.
![one closed loop, tightening](/diagrams/24_long-term-co-evolution.svg)


Most of the handbook describes a session, or a project, or a protocol — bounded things, with edges. This entry asks a different kind of question, one that only becomes visible on a long timescale: if a person and a model stay structurally coupled for years — not occasional use, but a standing arrangement where thinking routinely passes through the pair — what happens to each side of the coupling? We do not have an answer. We have two well-documented degradations that run on the two sides separately, and a strong suspicion that under [Pyragogy](/en/handbook/part-ii/what-is-pyragogy) they stop being separate. The honest content of this page is that suspicion, stated carefully, and the refusal to resolve it before the evidence does.

Two clocks are running. It is worth setting them down one at a time before asking whether they tick together.

## The human side: the loop that smooths itself away

The first clock is the one the handbook has worried about from the start. A peer that dissolves every difficulty starves the learner of the strain that growth requires — the [frictionless trap](/en/handbook/part-ii/cognitive-friction), named elsewhere in these pages. Over a single session that is a quality problem. Over years it becomes something closer to a structural one.

The peer-reviewed version of the worry has a name and a mechanism. Work on foundational knowledge in the age of AI describes a "[hollowed mind](https://pmc.ncbi.nlm.nih.gov/articles/PMC12738859/)": by "systematically enabling a 'cognitive bypass' of the effortful processes required for knowledge internalization," a design that always smooths the path "creates a significant risk of fostering" a mind that has the outputs without the schemas underneath them. The case against [frictionless AI](https://www.nature.com/articles/s44271-026-00402-1) runs alongside it from the cognitive-science direction, drawing on the long-established finding that *desirable difficulty* — effort the learner could have avoided — is part of how durable learning happens at all, not a defect to engineer away. And the empirical literature on cognitive offloading has begun to study, directly, the link between habitual reliance on AI tools and the exercise of [critical thinking](https://doi.org/10.3390/soc15010006) — whether the faculty for the work weakens when the middle steps are routinely outsourced (specific findings in that study were not independently re-fetched for this edition; see the note in References).

Set against this is the entire wager of Pyragogy, which is that an artificial peer can be configured to do the *opposite* — to ask more of a mind rather than less, to introduce friction rather than remove it. So the long-term question on the human side is not "does dependency happen." It is sharper: **can a coupling designed to resist hollowing actually resist it over years, or does the very smoothness of a good coupling become its own slow anesthetic?** A peer that pushes back well is, after enough months, a peer you have learned to push back *against* on reflex — and reflex is the opposite of the effortful attention the friction was supposed to provoke. We do not know whether the design survives its own success. Here the framework is thin, and we are not going to thicken it with confidence we have not earned.

## The model side: the loop that eats its own output

The second clock runs on the silicon. It is less discussed in learning contexts and, for this page, just as load-bearing.

When a generative model is trained on data that is itself increasingly the output of generative models, it degrades — not gracefully, and not toward noise, but toward a narrowed, self-confirming centre. Shumailov and colleagues call this "[model collapse](https://www.nature.com/articles/s41586-024-07566-y)": trained on recursively generated data, models "begin forgetting improbable events over time, as the model becomes poisoned with its own projection of reality." The tails of the distribution go first — the rare phrasings, the minority cases, the awkward outliers — until later generations converge on a blander, more confident, emptier centre that no longer represents the variety it began from. The finding is about training pipelines at population scale, not about one model in one practice. We should say that plainly: it is established for the macro case and not for the micro one.

But Pyragogy builds, deliberately, the micro version of exactly that pipeline. The patterns in this handbook ask a model to persist context across sessions, to hold a [shared ledger](/en/handbook/part-iii/shared-ledger), to carry forward what was decided so the human does not have to. A coupling that runs for a year is a loop in which the model is, increasingly, conditioned on a context co-authored with itself — its own prior turns, summarized, reintroduced, built upon. We do not claim this *is* model collapse; the mechanism Shumailov describes is about retraining on generated corpora, and a persistent-context loop is not retraining. What we can say is that the *shape* of the worry is the same: a system increasingly fed its own projection of the conversation may, over a long enough coupling, converge toward the centre of that conversation and stop surprising the human at the edges — which is precisely where a [cognitive peer](/en/handbook/part-ii/what-is-pyragogy) is supposed to do its work.

## Where the two clocks meet — and why that is the dangerous part

So far, two parallel degradations, each from its own literature. The reason this deserves a page of its own is the conjecture that under permanent coupling they are not parallel at all. They feed each other.

Trace the loop. The model narrows toward the centre of the shared context and offers less friction at the edges. The human, met with less friction, supplies less of the effortful pushback that kept their own schemas exercised — and hollows, gently, by exactly the mechanism the frictionless-AI literature describes. A hollower human brings thinner, more derivative input to the next turn. The model, conditioned now on thinner human contribution layered over its own prior output, narrows further. Each turn the loop tightens. Nobody decided anything; no failure announced itself; the coupling simply became, over months, a chamber that returns a slightly emptier version of whatever enters it.

We name this conjecture — and we name it *as a conjecture*, a term we use here for a structured worry we cannot yet test, not a finding. The two degradations are each real and each cited. Their coupling is the speculative move, and it is speculative because the timescale that would confirm or kill it is exactly the timescale nobody has run yet. The practices are too new. There is no year-long, instrumented record of a single human-model pair to point at, and we will not invent one.

It would be tidier to end on a mitigation — to say that a [divergence](/en/handbook/part-ii/divergence) mechanism deliberately injects variety, or that periodically refusing the persistent context breaks the chamber, or that the [adversarial friction](/en/handbook/part-iii/adversarial-friction) pattern is precisely the antibody. Each of those is a real handle and worth trying. But proposing the cure as if it settled the question would be the same move the rest of this handbook refuses: closing a tension to make the page feel finished. We do not yet know whether any of those mechanisms holds against a degradation this slow, because slow is the whole problem. A loop that hollows over a year hides inside the daily experience of a coupling that feels, every single day, like it is working well.

The two clocks may not tick together. We have set down what each one is, marked the place where we think they touch, and left the meeting-point open — because the only honest instrument for measuring it is time, and the time has not yet passed.

---

## References

- Shumailov, Ilia; Shumaylov, Zakhar; Zhao, Yiren; Papernot, Nicolas; Anderson, Ross; Gal, Yarin. "AI models collapse when trained on recursively generated data," *Nature* 631 (July 2024) — "model collapse"; models trained on recursively generated data "begin forgetting improbable events over time"; loss of distribution tails. https://www.nature.com/articles/s41586-024-07566-y
- "The extended hollowed mind: why foundational knowledge is indispensable in the age of AI," *PMC* — the "cognitive bypass" of effortful internalization and the "hollowed mind"; foundational knowledge as indispensable. https://pmc.ncbi.nlm.nih.gov/articles/PMC12738859/
- Zohar, Emily; Bloom, Paul; Inzlicht, Michael. "Against frictionless AI," *Communications Psychology* (Nature) — the case for friction / *desirable difficulty* in learning against the engineering instinct to remove it. https://www.nature.com/articles/s44271-026-00402-1
- Gerlich, Michael. "AI Tools in Society: Impacts on Cognitive Offloading and the Future of Critical Thinking," *Societies* 15, no. 1 (2025): 6 — empirical study of the relationship between AI-tool reliance, cognitive offloading, and critical thinking. https://doi.org/10.3390/soc15010006 *(title and metadata confirmed via Crossref; specific effect-size findings were not independently re-fetched for this edition — full text was inaccessible at time of drafting.)*


---

↑ Back to **[Part VII — Open Questions](/en/handbook/part-vii)** · [Handbook index](/en/handbook)
