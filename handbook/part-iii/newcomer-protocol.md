---
title: The Newcomer Protocol (Human & Agent)
description: The cognitive contract for admitting a new participant — human or agent — into a Pyragogy network: what it must receive, what it must accept, and why the two onboardings diverge.
published: true
date: 2026-06-10T11:20:57.919Z
tags: pyragogy, protocol, onboarding, communities-of-practice, agents
editor: markdown
dateCreated: 2026-06-10T11:13:32.532Z
---

# The Newcomer Protocol (Human & Agent)

> **Type:** Protocol  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> A new participant arrives in the middle of a sentence. The group has been arguing for three sessions about whether a claim holds; the threads are half-spun, the disagreements have names, and someone — or something — has just been added to the channel. It cannot help yet. It does not know what is being fought over, who tends to overstate, or which questions were already closed and should stay closed. Before it can contribute, it has to be told where it is standing.

That moment — between *added* and *able to contribute* — is what this page is about.
![the symmetric cognitive contract](/diagrams/10_newcomer-protocol.svg)


In most systems the moment is handled by accident. A human is added to a repository and left to read the backlog; an agent is given an API key and a prompt, and whatever it does next is whatever the prompt happened to imply. Pyragogy treats the moment as a thing to be designed rather than survived. We call the design **the newcomer protocol**, and the obligation it encodes **the cognitive contract** — both terms we coin here, in a project-specific sense, for the requirements that have to be met before a new participant can do the cognitive work the network exists to do.

This is not orientation in the HR sense. It is not a tour, a welcome message, or a checklist of accounts to create. Those are the packaging. The protocol is about something narrower and harder: under what conditions does a newcomer acquire enough situated context to participate as a peer rather than as a guest who keeps asking what everyone already knows.

## Why the human case is mostly solved

For the human newcomer, the protocol does not have to be invented. It has to be recognized, because the learning sciences described it a generation ago.

The reference is **[Lave and Wenger](https://www.cambridge.org/highereducation/books/situated-learning/6915ABD21C8E4619F750A4D4ACA616CD)** (1991) and their account of **legitimate peripheral participation**. Their claim, drawn from studies of apprenticeship in several trades and professions (the book's case studies are commonly cited as including midwives, tailors, and naval quartermasters, though the full text was not accessed to confirm the exact framing), is that newcomers do not learn a practice by being instructed in it from outside. They learn it by being admitted to its edge — given small, real, low-risk tasks that are nonetheless necessary — and then moving inward as their competence and their standing grow. The community is a **[community of practice](https://www.wenger-trayner.com/introduction-to-communities-of-practice/)**: a group, in Etienne and Beverly Wenger-Trayner's words, "of people who share a concern or a passion for something they do and learn how to do it better as they interact regularly." You join it by doing some of the work, at the margin, where a mistake is cheap.

Two words in that phrase carry the load. *Legitimate*: the newcomer's participation must be genuine, not a sandbox exercise the rest of the group ignores. *Peripheral*: it must start at the edge, where the stakes are low and the surrounding members can absorb the error. A protocol that grants only one of the two fails predictably. Legitimacy without periphery throws the newcomer into load-bearing decisions before they can read the room. Periphery without legitimacy is busywork, and the newcomer knows it within a day.

So the human half of the protocol is, in operational terms, the deliberate construction of a legitimate periphery. Concretely:

- A **first task that is real and small** — a paragraph to pressure-test, a single thread to summarize, one open tension to read into — not a representative sample of the hardest work the group does.
- **Read access to the live disagreements**, not just the settled outputs. The settled outputs teach nothing about how the group thinks; the open arguments are the curriculum. This is where [Cognitive Friction](/en/handbook/part-ii/cognitive-friction) becomes legible to a newcomer — by watching where the group is still in tension.
- **A named place to be wrong cheaply.** Someone, or some channel, where the newcomer can ask the question that "everyone already knows" without spending standing they have not yet earned.

None of this is novel, and we do not present it as such. The contribution of this page is only to insist that a network claiming to do peer learning must build the periphery on purpose, and to notice that the moment a *non-human* peer arrives, the inherited solution stops applying.

## Why the agent case is not solved — and is project-specific

Lave and Wenger's apprentice has a body that persists, a memory that accumulates, and weeks in which to move from edge to center. A new agent — a model with a system prompt, a tool set, and a role in a workflow — has none of these by default. It does not drift toward the center over time; it begins each session with whatever context it was handed and ends with that context gone. There is no apprenticeship for something that cannot remember yesterday's apprenticeship.

This is the first reason the agent case cannot simply reuse the human one: there is no periphery to move inward *from*, because there is no continuous self to do the moving. The agent's "competence in this practice" is not a thing it grows. It is a thing that has to be **reconstructed at the start of every session**, from artifacts the network maintains. The handbook treats those artifacts under [Pattern: Context Persistence](/en/handbook/part-iii/context-persistence) and the [Pattern: The Shared Ledger of Knowledge](/en/handbook/part-iii/shared-ledger); the newcomer protocol is where they first have to be provisioned.

The second reason is sharper, and it is where this page declines to overpromise. **Agent onboarding is project-specific.** What a new agent needs in order to participate is not a general standard — it is a function of this network's stack, its conventions, its tools, and the particular role the agent is being added to play. The closest established discipline is what is now called **context engineering**: [Anthropic's account](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) frames the task as "finding the smallest possible set of high-signal tokens that maximize the likelihood of some desired outcome," and treats the system prompt, the tool definitions, the examples, and the working memory as the things you curate rather than the model itself. That framing is sound and we lean on it. But it is a framing, not a protocol you can paste into a different project. The high-signal tokens for *this* network are not the same as for another, and anyone who tells you the agent-onboarding contract is portable is selling you the packaging again.

What we can state operationally is the *shape* of the agent-side contract — the questions every project must answer for itself, even though the answers do not transfer:

- **What is the minimal context that lets this agent act as a peer here, not as a generic assistant?** The role, the open tensions it is allowed to touch, the conventions it must not violate. Too little and it produces fluent, off-topic help; too much and it drowns in tokens it cannot weight. This is the [Pattern: Context-Window Economy](/en/handbook/part-iii/context-window-economy) made concrete at the moment of arrival.
- **What state does it read from, and what is it permitted to write back?** A new human can be trusted to read the backlog and not edit it. A new agent's read/write boundary has to be drawn explicitly, because it has no social instinct for the line between "I am proposing this" and "I have changed this."
- **What is the agent allowed to disagree with?** The reason a network admits an agent at all, on the Pyragogy account, is the cognitive work of disagreement — see [Pattern: Adversarial Friction](/en/handbook/part-iii/adversarial-friction). An agent onboarded only to comply has been added as a tool, not a peer, and the [Anti-Pattern: The Compliance Trap](/en/handbook/part-vi/compliance-trap) is the name for what that costs.

Each of those is answerable. None of them is answerable *in general*. That is not a gap in the protocol; it is the protocol telling the truth about where it ends.

## The contract, stated as obligation

Stripped to its requirements, the cognitive contract has two sides and they are not symmetric.

What the **network owes the newcomer** is the same regardless of substrate: a legitimate place at the periphery and the live context needed to occupy it. For a human, that context is delivered slowly, by participation, and retained in a body. For an agent, the identical obligation has to be met *at the start of every session* and through maintained artifacts, because nothing is retained on its side.

What the **newcomer owes the network** is where the asymmetry shows. A human accepts the apprentice's bargain: start at the edge, be wrong cheaply, earn the move inward. An agent cannot accept anything — it has, as [What is Pyragogy](/en/handbook/part-ii/what-is-pyragogy) argues at length, no stake in the exchange and no memory of it after the session resets. So the second half of the contract, for the agent, is not an obligation the agent carries. It is one the network carries *on the agent's behalf*: the discipline of re-provisioning the context, holding the read/write line, and reading the agent's output as a proposal rather than a verdict.

That is the honest shape of it. The newcomer protocol is one contract for the human and a different one for the agent, joined only by the obligation the network never escapes either way — to construct the place from which a newcomer can begin.

## Where this is still thin

Three tensions stay open, and the page is better for naming them than for hiding them.

First, the human protocol assumes time the network may not have. Legitimate peripheral participation is slow by design; a project under deadline will be tempted to skip the periphery and onboard a human straight into load-bearing work. We have no measured account of how badly that fails or how fast — only Lave and Wenger's argument that it should.

Second, the agent contract has no settled answer to drift. An agent re-provisioned identically every session is stable but cannot learn the practice; an agent whose context accumulates across sessions begins to learn, and also begins to be poisoned by its own past errors — the failure mode named in [Anti-Pattern: Context Poisoning](/en/handbook/part-vi/context-poisoning). Where the line sits between useful persistence and accumulated corruption is, here, unresolved.

Third, the two halves of the protocol may not stay separate. If a network runs long enough, the question of whether a re-provisioned agent has, in any meaningful sense, *served an apprenticeship* stops being rhetorical — and we do not have a framework for it yet. It is the long arc the handbook picks up in [Long-Term Cognitive Co-Evolution](/en/handbook/part-vii/long-term-co-evolution).

The protocol, then, is not a finished door with a finished key. It is the recognition that someone keeps arriving in the middle of a sentence, and that whether they can finish it depends on what the network built for them to stand on before they got there.

---

## References

- Jean Lave and Etienne Wenger, *Situated Learning: Legitimate Peripheral Participation* (Cambridge University Press, 1991). The foundational account of communities of practice and of newcomers moving from a legitimate periphery toward fuller participation. https://www.cambridge.org/highereducation/books/situated-learning/6915ABD21C8E4619F750A4D4ACA616CD
- Etienne Wenger-Trayner and Beverly Wenger-Trayner, "Introduction to communities of practice" (2015) — source of the definition quoted: "groups of people who share a concern or a passion for something they do and learn how to do it better as they interact regularly." https://www.wenger-trayner.com/introduction-to-communities-of-practice/
- Anthropic, "Effective context engineering for AI agents" (Anthropic Engineering) — context as "the smallest possible set of high-signal tokens that maximize the likelihood of some desired outcome"; system prompt, tools, examples, and memory as the curated surface. https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
