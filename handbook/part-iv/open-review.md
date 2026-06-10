---
title: Case Study: Open Review
description: A peer text-review flow augmented by a synthetic Critical Reading Team: four independent models read the same draft without reading each other, and the disagreement that survives is the review.
published: true
date: 2026-06-10T11:21:13.872Z
tags: case-study, open-review, critical-reading-team, crt, peer-review
editor: markdown
dateCreated: 2026-06-10T11:14:27.373Z
---

# Case Study: Open Review

> **Type:** Case Study  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> Four readers receive the same draft at the same minute. None of them sees the others' margins. One reformulates the argument; one audits the document line by line; one is told to attack the reading the first produced; the last is asked, at the end, to explain to the author why the verdict came out the way it did. Three of the four are language models. The point of the arrangement is that they never agree quietly.

This page documents a method, not a finished product. The method has a working name — **CRT×4** — and at the time of writing it exists as a written specification and a single lived case, not as a deployed tool with field data behind it. We document it now, in that honest state, because an empty frame that says what was tried beats a study that invents what it found.
![independent readers, not an aggregate](/diagrams/17_open-review.svg)


## What it is

CRT×4 is an open-source method, developed under [Pyragogy](/en/handbook/part-ii/what-is-pyragogy) as independent research, for running a peer review of a text through several independent AI readers and a human conductor. The name expands to *Cognitive Rhythm Theory × 4 agents*. It is project coinage — you will not find "CRT×4" in the peer-review literature — and we name it as such here; the method's own page is its home, and elsewhere it should be linked, not redefined.

The thing being reviewed, in this case study, is a document: an argument, a chapter, a policy draft, a paper. What the method adds to an ordinary human read-through is a **Critical Reading Team** — a small set of models that read the same draft under one rule that does most of the work: they read it *independently*, and their readings are never merged into a single smooth verdict.

It is worth being precise about what that excludes. CRT×4 is not "a wrapper that calls several models and averages them." Averaging is exactly the failure it refuses. It is not an intelligent tutoring system grading the text against a rubric, and it is not a single assistant asked to "review this and be critical" — that produces one voice performing critique, which is a mirror with a frown, not a team. The value sits in the [friction](/en/handbook/part-ii/cognitive-friction) that survives between readers who cannot see each other: different models, different training, different blind spots, no forced convergence.

## The arrangement

The method's source specification describes a nine-stage workflow. Its native domain is code review — the spec was written by a developer auditing a repository — and the author flags, in the document itself, that generalizing it to a text means rewriting one stage: where the code version runs a *forensic analysis* of a repository, the document version runs a *documentary analysis* of the draft. That substitution is a design choice the project marks as deliberate, not an assumption to wave through.

Rendered for an open review of a text, the stages run roughly as follows.

1. **The problem arrives.** A human brings a real draft and a real question about it — not "is this good" but "does this hold."
2. **Reformulation.** One model restates the draft's claim in its own words, which already surfaces where the argument is load-bearing and where it is decoration.
3. **Documentary analysis.** A second model audits the material itself — the text, its sources, its internal consistency — line by line.
4. **First reading.** A model maps the tensions it found and proposes a reading: here is what this draft is actually arguing, and here is where it is weakest.
5. **Adversarial pass.** A *different, independent* model — the spec names a model from another vendor for this seat — is instructed to attack the first reading. Not to improve it. To break it. This is the seat that makes the team a team; it is the operational form of the handbook's [Adversarial Friction](/en/handbook/part-iii/adversarial-friction) pattern.
6. **Divergence into options.** The tensions that survived the attack generate options rather than a single answer — the [Divergence](/en/handbook/part-ii/divergence) phase, kept open on purpose.
7. **Validation and loop.** The reading is iterated until it holds against the attack. If it doesn't hold, the loop runs again.
8. **The fix.** A change is prepared and applied to the draft, then checked.
9. **The explanation.** A model explains to the human *how and why* the review reached its verdict — not the corrected text alone, but the path to it.

The source is blunt about which stage carries the weight: *"Stage 9 is the heart. Without it, this is automation. With it, it is learning."* The first eight stages would, on their own, produce a corrected document and a passive author — the machine resolves, the human receives. Stage nine is the move that keeps the human as conductor rather than spectator: the [learning loop](/en/handbook/part-iii/context-persistence) that returns the reasoning, so the next draft is written by someone who now sees what the team saw.

## The one rule that cannot be relaxed

The method's specification carries a single non-negotiable, and it is the thing most likely to be optimized away by anyone building the tool: **the independence between models must be preserved.** The agents do not read each other during the analysis — reciprocal blindness — and their outputs are never normalized toward a consensus. A model that runs "in its own house," on its own vendor's infrastructure, stays there rather than being routed through a layer that quietly aligns it with the others.

The reason is structural, not stylistic. An orchestrator that makes the answers converge kills the method, because uniform pressure flattens exactly the disagreement that was the asset. The danger has a name elsewhere in this handbook — [Orchestra Desynchronization](/en/handbook/part-vi/orchestra-desynchronization) is its opposite failure, and the [Compliance Trap](/en/handbook/part-vi/compliance-trap) is what a merged-to-consensus team collapses into: a panel of readers trained, by the merge step, to agree. Here the architecture has to defend friction against its own convenience.

This is the same instinct that runs through the sibling case study, [Obliqo](/en/handbook/part-iv/obliqo), where a set of reading agents are kept reciprocally blind by design. CRT×4 is, in the project's own framing, the *method* — open, citable, under Pyragogy — of which Obliqo is one *commercial application*. They are meant to reinforce each other: the product as commercial proof, the method as open methodological proof, the Pyragogy paper as the theoretical frame behind both.

## Where the real practice anchors it

The arrangement is not a novelty invented out of nothing; it sits next to an established practice. **[Open peer review](https://en.wikipedia.org/wiki/Open_peer_review)** is a real and adopted family of modifications to scholarly peer review — open identities, open reports, open participation — used by publishers including Nature, PLOS, and others. In the systematic review that mapped the field, [Tony Ross-Hellauer](https://doi.org/10.12688/f1000research.11369.2) found the term so unsettled that the literature held twenty-two distinct configurations of seven traits — "an umbrella term for a number of overlapping ways that peer review models can be adapted."

CRT×4 borrows the spirit of that openness — the report is visible, the reasoning is returned to the author — and adds the move open peer review does not make: some of the reviewers are synthetic, and the design's whole burden is to stop them from agreeing. Where human open review struggles to find enough independent reviewers, the synthetic team is cheap to convene; where it risks reviewers deferring to a senior name, the synthetic team risks the subtler deference of models trained toward the same agreeable center. The anchor is real. The twist is the project's, and we mark the seam rather than paper over it.

## What is real, and what is not yet

Honesty about the evidence is the point of a case page, so here is the ledger.

What is real: the method is specified in a dated project document; its nine stages, its independence rule, and its learning-loop stage are written down, not reconstructed here. The open-review *practice* it anchors to is verifiable and cited below. The decision to release the method as writing before building any tool — "validate the idea at near-zero cost; if it resonates, build; if not, archive without loss" — is recorded in the source.

What is **not** yet real, and must not be dressed as if it were:

- The tool does not exist. The specification states plainly that construction comes *after* a product launch and *after* the written method has received a first signal — "no impulse code." There is therefore no deployment, no usage, no instrumented run of an open-text review through CRT×4 to report.
- The one concrete result the source gestures at — a claim that the method "closed three HIGH vulnerabilities in production" on a code repository — is (a) about code, not text, and (b) reported in the spec as a headline-to-be for a future README, not as a measured, reproduced outcome. It is not evidence for the open-review-of-a-text use this page documents.
- No reader counts, no agreement rates, no before/after quality measures, no quotes from authors who went through the loop. None of these exist to report, and none are invented here.

## Open tensions

Three things this method does not resolve, left open because the rest of the handbook is where they are worked.

The first is the asymmetry the team is built on. The adversarial reader attacks without anything at stake — it does not tire of the draft, does not fear the author, will not remember the exchange after the session resets. The friction lands on the human conductor and is real for them; it is not real for the attacker. That gap is a feature to be used knowingly, not a partnership to be sold — the handbook's account of [functional asymmetry](/en/handbook/part-ii/what-is-pyragogy) holds here unchanged.

The second is independence under doubt. The method *asserts* that four models with different training disagree usefully. How much genuine divergence survives when several frontier models share overlapping data and a common drift toward the agreeable center is an empirical question this page cannot answer without the missing field data. The rule is sound in principle; its yield is unmeasured.

The third is ownership of the verdict. When a reading is forged between a human conductor and a cluster of models that argued each other to a stop, whose review is it — and who answers for it if it is wrong? The handbook carries that question forward under [The Epistemic Ownership Dilemma](/en/handbook/part-vii/epistemic-ownership). Here it is enough to note that the learning loop in stage nine is what keeps the human able to answer for the verdict at all, rather than merely holding its output.

The method is written down. The tool is not. What the four readers find when they are finally let loose on a real draft, and whether their disagreement holds the way the specification promises, is the part this page cannot yet report — and will not pretend to.

---

## References

- Pyragogy CRT×4 — Open Source Project (working specification), 2026-06-01. Internal project asset: `pyragogy-crt4-opensource-method-2026-06-01.pdf`. Source for the nine-stage workflow, the independence non-negotiable, the learning-loop stage, the method/application/paper positioning, and the build-after-launch decision. This document has no public URL at time of publication and cannot be independently verified by readers; it is cited here as an internal source pending a decision on public release form.
- Tony Ross-Hellauer, "What is open peer review? A systematic review," *F1000Research* 6:588 (2017). https://doi.org/10.12688/f1000research.11369.2 — DOI resolves (302 → article); metadata confirmed via Crossref; the abstract characterizes open peer review as an "umbrella term" spanning 22 configurations of seven traits. (The article page itself returns 403 to automated fetches; the DOI is the stable citation.)
- "Open peer review," *Wikipedia*. https://en.wikipedia.org/wiki/Open_peer_review — HTTP 200; supports the claim that open peer review is an established, adopted practice (open identities / open reports / open participation) used by major publishers.
- Howard Rheingold and the Peeragogy Project, *The Peeragogy Handbook*. https://peeragogy.org/ — HTTP 200; the human-to-human peer-learning lineage from which Pyragogy forks.
