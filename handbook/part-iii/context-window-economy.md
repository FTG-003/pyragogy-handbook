---
title: Pattern: Context-Window Economy
description: Context-Window Economy: the discipline of treating an agent's context window as a scarce, billed, and degrading resource — deciding what each model is handed rather than passing the whole conversation everywhere, because more context is not more competenc
published: true
date: 2026-06-11T07:59:40.062Z
tags: pyragogy, pattern, context-window, tokens, orchestration, cost, lost-in-the-middle
editor: markdown
dateCreated: 2026-06-10T11:21:04.358Z
---

# Pattern: Context-Window Economy

> **Type:** Pattern  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> Three agents, one task. The orchestration is wired the obvious way: whatever the first agent saw, the second one sees too, and the third sees both. By the fourth handoff the prompt is the entire history of the work — every draft, every objection, every dead end — and it is handed forward in full at every step. The output is worse than it was at step two, the invoice at the end of the month is larger than the team expected, and nobody can say which of the ten thousand tokens in that final prompt actually mattered.

Nothing was misconfigured. The wiring did exactly what wiring does. The mistake was upstream: the context window was treated as free and infinite, and it is neither.

**Context-Window Economy** is the name we use, in a project-specific sense, for the discipline of refusing that assumption. The window each model reads from is a scarce resource on two axes at once — it is **billed**, and it **degrades** — and this pattern is the practice of spending it deliberately instead of filling it by default. The unit of the pattern is a decision made at every handoff: not *can* I pass the whole context forward, but *what does this particular model need to do its particular job*. This page documents how to make that decision, why it is forced rather than optional, and the ways it goes wrong.

It is a pattern, not a concept, and it sits one step downstream of its sibling. [Context Persistence](/en/handbook/part-iii/context-persistence) decides what survives a session; Context-Window Economy decides what is loaded back in. A store can preserve a context perfectly and still hand a model more than it can use — so the two patterns share a border, and a network that runs one without the other gets either a clean archive nobody can read efficiently, or an efficient pass over nothing worth reading.

## What it is not

It is not prompt engineering. Prompt engineering is the craft of phrasing a single instruction well — what to ask, in what order, with which examples. Context-Window Economy operates a layer up, on *flow*: which agent receives which slice of the accumulated context, and which slices are dropped at the boundary between them. You can write an excellent prompt and still pass it the wrong nine thousand tokens of history.

It is not retrieval-augmented generation, though it borrows the instinct. Retrieval fetches relevant external documents *into* a context; this pattern governs what is allowed to stay there across a multi-step pipeline — including, often, deciding that material already retrieved should now be left behind. Retrieval is about pulling the right thing in. Economy is also about the harder, less natural move: pushing the no-longer-needed thing back out.

And it is not compression for its own sake. The goal is not the smallest possible prompt — a model starved of the context it actually needs fails as surely as one drowned in context it does not. The target is *sufficiency*: the slice that lets this model do this job, and not the slice that makes the orchestrator feel thorough. Smaller is not the win. Right-sized is.

## Why the window is scarce: two pressures, not one

The naive instinct — pass everything, let the model sort it out — rests on a belief that more context can only help. Both halves of this pattern exist because that belief is false in two independent ways.

**The window is billed.** Commercial language-model APIs price usage per token, with input and output rated separately; OpenAI's published pricing, for instance, is quoted in dollars [per million tokens](https://developers.openai.com/api/docs/pricing) and charges for every token a model reads, not only the ones it writes. This has a consequence the wiring hides: re-passing the full conversation history at every handoff means re-paying for the entire accumulated context at every step. A history that is read four times is billed four times. In a [multi-agent orchestration](https://n8n.io/) — a pipeline of nodes where each step calls a model — the cost of "pass everything everywhere" does not add; it compounds with the number of handoffs. (This compounding behaviour is a straightforward derivation from per-token pricing mechanics, not a result drawn from a published study: if each of *n* steps re-sends the full accumulated history, the total input-token bill grows with the square of *n*, not linearly.) The economic scarcity is not a metaphor. It is a line item that grows faster than the per-call price suggests while the team is watching that price and thinking it cheap.

**The window degrades.** Even setting cost aside, a longer prompt is not a more capable one. The finding here is established, not ours: in **["Lost in the Middle"](https://aclanthology.org/2024.tacl-1.9/)**, Nelson Liu and colleagues showed that model performance "is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades when models must access relevant information in the middle of long contexts" — a degradation present even in models built explicitly for long inputs. Chroma's 2025 ["Context Rot"](https://www.trychroma.com/research/context-rot) report pushed the same result across eighteen models — frontier and open-weights both: performance varies significantly as input length grows, even on tasks deliberately kept simple. Put together, the two findings say something the "pass everything" instinct cannot survive. The relevant claim buried in the middle of a ten-thousand-token prompt is not merely paid for four times. It is *read less reliably* than the same claim in a prompt a tenth the size. More context can actively bury the part that mattered.

So the window is scarce twice over, and the two pressures point the same way. Cost says: do not re-send what this model does not need. Degradation says: do not even *include* what this model does not need, because the noise lowers the signal it does. The pattern is the single discipline that answers both.

![context passed in full vs context budgeted per handoff](/diagrams/13_context-window-economy.svg)

## The discipline: budgeting the handoff

Stated operationally, Context-Window Economy is a set of obligations applied at every boundary where context crosses from one step to the next. The implementation is unglamorous on purpose — a clever token-economy layer is one nobody will trust enough to run.

- **Budget per node, not per pipeline.** Each agent in the orchestration gets the context its job requires and not the union of everything seen so far. The summarizer needs the draft, not the brainstorm that produced it; the critic needs the claim, not the retrieval logs. The default has to be *exclusion* — context is added to a handoff because a reason was named, not passed through because dropping it took effort.
- **Hand forward distillates, not transcripts.** Between steps, what crosses the boundary should usually be the *result* of the prior step — the decision, the surviving claim, the corrected draft — not the full conversation that reached it. This is the move that turns linear history into a bounded payload, and it is the operational seam with [Context Persistence](/en/handbook/part-iii/context-persistence): persistence curates what is kept; economy hands the curated form, not the raw log, to the next model.
- **Place what matters at the edges.** Because of the lost-in-the-middle finding, *where* a critical instruction sits in the prompt is not cosmetic. The constraint the model must not miss belongs near the start or the end of its context, not lodged in the middle of a long preamble. This obligation costs nothing to honor and quietly raises the floor on reliability.

None of the three is difficult to build. All three are easy to skip, because the lazy wiring — pass everything, change nothing at the boundary — is also the wiring that runs without any decisions being made at all. The pattern is, in the end, the insistence that a decision *be* made at each handoff, by someone who can say what this model needs and why.

## Where it breaks

This is a draft pattern, and it has failure modes I do not yet know how to close cleanly.

**Distillation drops the thing you needed.** Every time a handoff carries the result instead of the transcript, a judgment is made about what was load-bearing in the prior step — and that judgment can be wrong. The objection that gets summarized away, the caveat that did not make the distillate, the dead end that was actually a clue: the same move that saves cost and signal can amputate the context a later step required, and the failure is silent, because nothing errors when a model reasons confidently over a context that is missing its crucial line. Aggressive economy and lost context are the same action seen from two sides.

**The budget can be drawn by the wrong hand.** Deciding what each model needs is itself cognitive work, and it is tempting to automate it — to let a model summarize the context before passing it on. But a model trimming the context for the next model is a model deciding what the next model is allowed to think with, and an error introduced at that step does not get flagged; it gets *inherited*, loaded into the next session as though it were the curated truth. That is the failure the handbook treats under [Anti-Pattern: Context Poisoning](/en/handbook/part-vi/context-poisoning), and Context-Window Economy is one of the places it enters, because the optimization and the contamination ride the same channel.

**Optimizing the window can starve the friction.** The point of a multi-agent network in Pyragogy is not throughput; it is that the participants push on each other — the resistance the handbook calls [Cognitive Friction](/en/handbook/part-ii/cognitive-friction). A context budget tuned only for cost and only for retrieval accuracy will, left alone, prune exactly the dissenting history that made the friction possible — the objection from two steps ago, the version the group rejected and why. Cheaper and cleaner is not the same as better when the thing you economized away was the disagreement. Where the line sits between a window that is lean and a window that is lobotomized, this pattern raises but does not resolve. The cost finding (per-token pricing) and the degradation findings (Liu et al.; Chroma) are each independently established; their joint tension with friction-preservation — the claim that optimizing the window risks pruning exactly the disagreement that makes a multi-agent learning network worth running — is this project's working hypothesis, not something an empirical study has yet measured directly.

None of these has a fix in the configuration. They are reasons the pattern needs a human who can still say what was worth keeping — which, again, is the only condition under which the network was ever going to be worth running.

---

## References

- Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, and Percy Liang, "Lost in the Middle: How Language Models Use Long Contexts," *Transactions of the Association for Computational Linguistics* 12 (2024): 157–173. Performance is highest when relevant information sits at the start or end of the input and degrades significantly when it must be accessed from the middle of a long context — including in models designed for long inputs. https://aclanthology.org/2024.tacl-1.9/ (preprint: https://arxiv.org/abs/2307.03172)
- Kelly Hong, Anton Troynikov, and Jeff Huber, "Context Rot: How Increasing Input Tokens Impacts LLM Performance," Chroma Technical Report (July 14, 2025). Eighteen models (frontier and open-weights — Claude, GPT, Gemini, Qwen) show performance varying significantly as input length grows, even on deliberately simple tasks — the basis for treating a longer window as lower-signal, not merely more expensive. https://www.trychroma.com/research/context-rot
- OpenAI API pricing — usage billed per token, input and output rated separately, quoted per million tokens; the basis for the claim that re-passing accumulated context at every handoff re-incurs its full input cost each time (in-body example of a commercial per-token pricing model). https://developers.openai.com/api/docs/pricing


---

↑ Back to **[Part III — Protocols and Practices](/en/handbook/part-iii)** · [Handbook](/en/handbook) · [Home](/en/home)
