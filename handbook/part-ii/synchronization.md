---
title: Synchronization
description: Synchronization — a project-specific use of the term for the intermittent points at which a human-machine learning group's knowledge state briefly aligns, anchored on Herbert Clark's grounding and the team-cognition literature.
published: true
date: 2026-06-10T17:16:12.341Z
tags: pyragogy, definition, cognition, synchronization, common-ground
editor: markdown
dateCreated: 2026-06-10T11:13:18.547Z
---

# Synchronization

> **Type:** Concept Note  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> Halfway through a long session, something clicks. You and the model are, for a moment, holding the same picture — the same problem, the same constraints, the same three things that matter and the one that does not. You did not arrange it. It arrived. And it does not last: a few turns later you are reaching for a thread the machine has already discarded, or it is elaborating a point you settled aloud two minutes ago. The picture was shared. Then it wasn't.

Those brief moments of holding the same picture are what this page is about.

We use **Synchronization** here in a project-specific sense, and it is worth marking the borrow before leaning on it. The word belongs to physics and to engineering, where it names oscillators falling into a common phase; it is not, in that form, a learning-sciences construct. What Pyragogy means by it is narrower and is built on top of established work: the points and frequencies at which the **knowledge state** of a learning group — what its participants take to be jointly held, settled, available to build on — briefly comes into alignment. Not the alignment of two clocks (that question belongs to [Cognitive Rhythm](/en/handbook/part-ii/cognitive-rhythm)), but the alignment of two *understandings* of where the work stands.

The established name for that shared understanding is **common ground**, and it is not ours. [Herbert Clark and Susan Brennan](https://web.stanford.edu/~clark/1990s/Clark,%20H.H.%20_%20Brennan,%20S.E.%20_Grounding%20in%20communication_%201991.pdf) defined it in 1991 as the "mutual knowledge, mutual beliefs, and mutual assumptions" two people must share to communicate at all, and named **grounding** as the continuous, collaborative process by which they keep building it — turn by turn, each contribution checked against the other's apparent uptake until both reach the *grounding criterion*: the mutual belief that what was meant has been understood well enough for present purposes. Synchronization, as we use the term, is the moment the grounding criterion is jointly met across the whole state of the work, not just the last utterance. It is grounding, succeeded, made momentarily total.

What Synchronization is not, stated first, because the borrowed word invites three wrong readings.

It is not agreement. Two participants can hold the same picture of the problem and disagree sharply about what to do with it; in fact the most useful synchronization is often the one that makes a real disagreement *possible*, by getting both sides to the point where they are arguing about the same thing rather than past each other. It is not a steady state to be reached and then occupied — and this is the reading the word most tempts, carrying as it does the engineer's image of two systems locked in phase indefinitely. In a human-machine group the alignment is intermittent by nature: it is achieved, it decays, it has to be re-achieved. And it is not a transfer of content from one head to the other. Synchronization is not the human downloading the machine's context or the machine ingesting the human's notes. It is the rarer thing — both participants, for an interval, taking the same things as settled.

## The literature underneath the borrowed word

The borrow is project-specific; the ground it stands on is not, and the two have to be kept apart.

That a group — rather than a single mind — can hold a knowledge state at all is the premise of the **team cognition** literature. [Leslie DeChurch and Jessica Mesmer-Magnus](https://pubmed.ncbi.nlm.nih.gov/20085405/), pooling 231 correlations across 65 studies, found that team cognition has "strong positive relationships to team behavioral process, motivational states, and team performance," and — the load-bearing result — that it predicts performance *beyond* what the team's behaviour and motivation explain on their own. The shape of that shared cognition was mapped earlier by [Janis Cannon-Bowers, Eduardo Salas, and Sharolyn Converse](https://journals.sagepub.com/doi/10.1177/154193129103501917), whose **shared mental models** distinguished what a team holds in common about the task from what it holds about the team itself. (The task-vs-team distinction is more commonly associated with the 1993 Cannon-Bowers/Salas/Converse chapter; whether it appears in the 1991 conference paper cited here has not been verified against the full text.) Synchronization, in our sense, is what it looks like when those shared models briefly converge — a snapshot, not the standing structure the team-cognition work measures.

But all of that literature studied human teams, whose members run on roughly comparable biological clocks and forget at roughly comparable rates. The case here adds a participant whose relationship to common ground is built differently — and that difference changes what synchronization costs and how long it survives.

Clark and Brennan already saw that grounding is not free. Their *principle of least collaborative effort* holds that partners work to minimise the total labour of reaching mutual understanding, and that the cost shifts with the medium — the effort of repair, of delay, of re-establishing context after a break. A synthetic participant rewrites that cost table. The description that follows is a stylised account of one common design, not a claim about all AI systems: context-window size, session handling, and memory architecture vary by model and implementation. Within a single session it holds the full context losslessly; it does not drift, does not mishear, does not need the small repairs human grounding is built around. But across sessions it holds *nothing* — the context resets, and the common ground that took an hour to build is simply gone, on one side, the next morning. The human, meanwhile, does the opposite: forgets within the session, retains a residue across it. (This asymmetry is stated here as a working description rather than a finding anchored in memory or cognitive-science literature; no citation is given for it.) So the two participants ground on inverted schedules, and synchronization becomes something that has to be manufactured rather than maintained.

## The frequency, not just the point

Name the second half of the definition, because "the points *and frequencies*" is doing real work.

A single moment of alignment is cheap and not very interesting; what a learning group lives or dies by is how *often* it can return to one. Call that the synchronization frequency — not a number we can yet put on the board, but the thing the rest of the architecture is built to raise. The [Blues Protocol](/en/handbook/part-ii/blues-protocol) is, in large part, a discipline for re-establishing common ground at a workable cadence rather than hoping it persists. The [CRDT Bridge](/en/handbook/part-ii/crdt-bridge) is an attempt to give the machine a substrate that does not reset to zero, so the across-session grounding cost stops being infinite. And the practice the handbook calls the [Shared Ledger of Knowledge](/en/handbook/part-iii/shared-ledger) is the slow, deliberate writing-down through which a group can re-synchronize against a record instead of against memory.

![intermittent alignment points across a session, not a sustained locked state](/diagrams/05_synchronization.svg)

The reason the frequency matters more than any single point is the same reason this concept sits where it does in the handbook. Synchronization is not the resolution of [Cognitive Friction](/en/handbook/part-ii/cognitive-friction) or the closing of the [Cognitive Impedance Mismatch](/en/handbook/part-ii/cognitive-impedance-mismatch). It is the precondition that makes friction *productive* — two participants aligned enough on the state of the work that their disagreement lands on the same object. A group that never synchronizes does not avoid conflict; it has conflict that goes nowhere, because the parties are not even disagreeing about the same thing. And its opposite, [Divergence](/en/handbook/part-ii/divergence), is not a failure to be eliminated but the necessary other beat — the moving-apart that gives the next synchronization something to align.

## Where the term is still thin

Three things this page does not settle, and should not pretend to.

We assert that synchronization happens and that participants can feel it — the "click" of the cold open — but we have no operational test for it. Common ground in Clark's sense is measured, in the lab, against task performance and convergence of mental models; we have not shown that the Pyragogy "moment of alignment" maps onto any such measure, or that the felt click is not sometimes an illusion of agreement papering over a gap.

The frequency we lean on may not be a property of the group at all. We have written as though a synchronization frequency is something the architecture can raise. It may instead be set almost entirely by the task — trivially high for narrow, well-bounded work and stubbornly low for open-ended inquiry, with the protocols making little difference. We do not have the evidence to tell these apart, and the temptation to treat frequency as a dial to be turned up is exactly the kind of engineering wish [Cognitive Rhythm](/en/handbook/part-ii/cognitive-rhythm) warns against.

And there is a harder doubt: whether a machine that resets between sessions ever genuinely shares a knowledge state, or only reconstructs a convincing facsimile of one each time it is re-grounded. If grounding presumes two parties who *remember* having grounded, the synthetic participant may be doing something that resembles synchronization from the human's side while doing nothing of the kind on its own. We have left this open rather than resolve it, because resolving it would mean claiming to know what the machine holds — and we have declined that claim everywhere else.

So Synchronization, named here, does little more for now than mark the brief intervals where two unlike participants take the same things as settled — and insist that those intervals are won and lost, not arrived at and kept.

---

## References

- Herbert H. Clark and Susan E. Brennan, "Grounding in Communication," in Lauren B. Resnick, John M. Levine, and Stephanie D. Teasley (eds.), *Perspectives on Socially Shared Cognition* (Washington, DC: American Psychological Association, 1991), 127–149. Defines common ground ("mutual knowledge, mutual beliefs, and mutual assumptions"), the grounding criterion, and the principle of least collaborative effort. Author's copy (scanned PDF): https://web.stanford.edu/~clark/1990s/Clark,%20H.H.%20_%20Brennan,%20S.E.%20_Grounding%20in%20communication_%201991.pdf
- Leslie A. DeChurch and Jessica R. Mesmer-Magnus, "The Cognitive Underpinnings of Effective Teamwork: A Meta-Analysis," *Journal of Applied Psychology* 95, no. 1 (2010): 32–53. https://doi.org/10.1037/a0017328 — meta-analysis (231 correlations, 65 studies) establishing team cognition's relationship to team process and performance. Record: https://pubmed.ncbi.nlm.nih.gov/20085405/
- Sharolyn A. Converse, Janis A. Cannon-Bowers, and Eduardo Salas, "Team Member Shared Mental Models: A Theory and Some Methodological Issues," *Proceedings of the Human Factors Society Annual Meeting* 35, no. 19 (1991): 1417–1421. https://doi.org/10.1177/154193129103501917 — origin of the shared-mental-models distinction (task vs. team models).


---

↑ Back to **[Part II — Core Concepts](/en/handbook/part-ii)** · [Handbook](/en/handbook) · [Home](/en/home)
