---
title: What is Pyragogy
description: 
published: true
date: 2026-06-10T16:58:50.760Z
tags: pyragogy, definition
editor: markdown
dateCreated: 2026-06-09T17:20:41.480Z
---

# What is Pyragogy

> **Type:** Concept Note  
> **Status:** Stable  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-09  
> **Reviewed by:** Human  
> **Open tensions:** 4

> A question is asked. An answer arrives. The screen settles, and the next question follows. On the surface this is learning. But trace the sequence backward and something is off: the answer came before the struggle did. The ground was smoothed before the learner walked it. A step was skipped.

Pyragogy starts from the skipped step.

The word is a coinage of this project, and it is worth saying so at the outset. You will not find "pyragogy" in the learning-sciences literature; there is no peer-reviewed consensus behind it, no settled definition to lean on. What stands behind it is **[peeragogy](https://peeragogy.org/)** — the framework Howard Rheingold and his collaborators built from 2012 onward to describe self-organized peer learning. Their setting was human to human: people without a teacher at the front of the room reviewing each other's work, questioning each other, producing knowledge together. Pyragogy is one fork of that lineage, and it turns on a single question: what happens to learning when one of the peers is not human?

Not the AI as a tool. That distinction carries the whole argument.

![tool vs cognitive peer](/diagrams/01_tool_vs_peer.svg)

When you ask a language model to summarize a paper, fix a function, or tighten a paragraph, the model is an instrument. You direct, it executes, and the thinking stays on your side of the screen. That is AI-assisted learning — common, useful, and not what this is about. Pyragogy describes something less accommodating: the AI as a **cognitive peer**. A participant that contributes to where the group's thinking goes rather than serving what it asks for; that can push back instead of comply; that holds part of the shared context and returns it when the human has lost the thread.

This is a strong claim, and the strongest objection to it should be stated plainly before any defense.

It comes from Emily Bender and her colleagues, who argued that large language models are "[stochastic parrots](https://doi.org/10.1145/3442188.3445922)" — systems that recombine patterns from their training data without understanding what they produce. On that view, calling a statistical model a "peer" is a category mistake dressed in friendly words. [Bender and Nanna Inie](https://www.techpolicy.press/we-need-to-talk-about-how-we-talk-about-ai/) press the point into language itself: terms like "collaborator" and "co-creator" do not raise the machine to our level, they lower our guard, encouraging trust the system has not earned. The law tends to agree — courts have held that an AI cannot be an [author](https://constitutioncenter.org/blog/supreme-court-denies-artificial-intelligence-authorship-claim-for-artwork-copyright) or [inventor](https://www.hklaw.com/en/insights/publications/2026/03/the-final-word-supreme-court-refuses-to-hear-case-on-ai-authorship), because authorship presumes a human. These are not objections to brush past. A handbook that waved them away would not be worth the reader's time.

So Pyragogy does not answer them by claiming the machine secretly understands. It declines the question of understanding altogether. The wager is narrower: inside a group that is learning, what moves the thinking forward is the **function a participant performs**, not the inner life it has or lacks. If something introduces a counter-argument, forces you to state an assumption you had left buried, or holds a thread you dropped three sessions ago, it has done cognitive work — it has changed what you think. Whether the trigger was a firing neuron or a weight on a server is, for this purpose, a question of plumbing. The literature on [hybrid intelligence](https://www.ijcai.org/Abstract/16/603) and human-AI "[centaurs](https://arxiv.org/abs/2406.10942)" has long described pairings where human and machine reach what neither reaches alone. Pyragogy takes that and moves it out of the chess match and the decision system into the place where people learn together.

But the functional move buys an objection of its own, and it is sharper than Bender's — so we meet it rather than route around it.

When you disagree with a human peer, you have something at stake. A relationship to strain, finite time to spend, an ego on the line. When you disagree with a model, you are pushing against something that does not suffer the exchange and will not remember it after the session resets. The friction is real in its effect on you; it is not real for the other side. If the human knows this — and the human does — there is a danger the disagreement becomes an exercise rather than a genuine contest.

![functional asymmetry](/diagrams/02_functional_asymmetry.svg)

We do not hide this asymmetry. The AI is a peer **functionally**, not existentially: it performs the work of a peer without carrying the stakes of one. Naming that gap is not a retreat from the claim — it is the honest shape of it. The friction still does its work, because the cognitive effect on the human does not depend on the machine having skin in the game. But a reader who is told the peer has nothing to lose will use the friction differently, and better, than one who has been sold a partner that bleeds. The asymmetry is a feature to be worked with, not a flaw to be concealed.

What Pyragogy is not, stated directly, because the term sits in a crowded field:

It is not e-learning or an intelligent tutoring system — those cast the machine as teacher or content pipeline and keep the old hierarchy intact. It is not AI literacy or prompt engineering — those are skills for operating the tool from the outside, where Pyragogy only begins once the tool-handling fades and the relationship takes over. And it is not heutagogy or andragogy — those theories of self-directed and adult learning still assume the other participants are human, and so have nothing to say about what happens when carbon and silicon try to think in the same room.

Which is where the honesty has to hold. These are not solved problems, and the handbook leaves them open on purpose:

A peer that always agrees is not a peer but a mirror, and a flattering one — the "[frictionless trap](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12738859/)," as the worry now circulates: an AI that dissolves every difficulty starves the learner of the strain that growth requires. The peer-reviewed version of that worry runs through recent work on foundational knowledge and the "hollowed mind," and through the broader case against frictionless AI. There is the asymmetry of memory: the machine keeps a clean, permanent context while the human drifts and forgets, and that imbalance quietly shifts who holds the power in the exchange. There is the question of who owns an insight forged between a person and a cluster of models, where the language of intellectual property starts to fail. And there is dependency — the documented risk that outsourcing the middle steps of thinking leaves the faculty for it weaker than before.

None of these has a clean technical fix. They are the reason the rest of the handbook exists.

Pyragogy, then, is not a case for automation. It is a wager — that an artificial system can be set up to ask more of a mind rather than to do its work for it — held together with a full accounting of the ways the wager might fail.

---

## References

- Howard Rheingold and the Peeragogy Project, *The Peeragogy Handbook* (2012–; v3, CC0). https://peeragogy.org/
- Emily M. Bender, Timnit Gebru, Angelina McMillan-Major, and Shmargaret Shmitchell, "On the Dangers of Stochastic Parrots: Can Language Models Be Too Big? 🦜," *Proceedings of FAccT '21*, 610–623. https://doi.org/10.1145/3442188.3445922
- Emily M. Bender and Nanna Inie, "We Need to Talk About How We Talk About 'AI'," *Tech Policy Press* (2026). https://www.techpolicy.press/we-need-to-talk-about-how-we-talk-about-ai/
- Nanna Inie, Emily M. Bender, and Peter Zukerman, "De-anthropomorphizing 'AI': From wishful mnemonics to accurate nomenclature," *First Monday* (peer-reviewed companion to the above). https://firstmonday.org/ojs/index.php/fm/article/view/14366
- On the "frictionless trap" / cognitive cost of frictionless AI: "The extended hollowed mind: why foundational knowledge is indispensable in the age of AI," *PMC*. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12738859/ — and "Against frictionless AI," *Communications Psychology* (Nature). https://www.nature.com/articles/s44271-026-00402-1
- Ece Kamar, "Directions in Hybrid Intelligence: Complementing AI Systems with Human Intelligence," *Proceedings of IJCAI 2016*, 4070–4073. https://www.ijcai.org/Abstract/16/603
- Soroush Saghafian and Lihi Idan, "Effective Generative AI: The Human-Algorithm Centaur." https://arxiv.org/abs/2406.10942
- On AI and authorship (copyright): *Thaler v. Perlmutter*, No. 23-5233, 130 F.4th 1039 (D.C. Cir. Mar 18, 2025) — affirming the human-authorship requirement for "A Recent Entrance to Paradise"; cert. denied, No. 25-449 (U.S., Mar 2, 2026). Summary with the full procedural chain: https://constitutioncenter.org/blog/supreme-court-denies-artificial-intelligence-authorship-claim-for-artwork-copyright
- On AI and inventorship (patents): the DABUS cases — *Thaler v. Vidal*, 43 F.4th 1207 (Fed. Cir. 2022) (U.S.; cert. denied; USPTO guidance Nov 2025 confirms inventors must be natural persons); *Thaler v Comptroller-General*, [2023] UKSC 49 (UK, 20 Dec 2023); EPO Boards of Appeal J 8/20 & J 9/20 — all holding an inventor must be a natural person. Summary covering authorship and inventorship: https://www.hklaw.com/en/insights/publications/2026/03/the-final-word-supreme-court-refuses-to-hear-case-on-ai-authorship


---

↑ Back to **[Part II — Core Concepts](/en/handbook/part-ii)** · [Handbook index](/en/handbook)
