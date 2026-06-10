---
title: Synthesis Architecture
description: Synthesis Architecture — the logical topology of the self-hosted infrastructure that supports a human–machine learning graph, drawn as an abstraction of guarantees rather than a setup tutorial: what the architecture must hold, kept separate from the swapp
published: true
date: 2026-06-10T11:21:21.972Z
tags: pyragogy, infrastructure, architecture, topology, self-hosting, synthesis
editor: markdown
dateCreated: 2026-06-10T11:21:21.972Z
---

# Synthesis Architecture

> **Type:** Synthesis Note  
> **Status:** Published  
> **Version:** v0.2  
> **Last synthesized:** 2026-06-10  
> **Reviewed by:** AI-drafted; human content-review pending  
> **Open tensions:** 3

> A diagram of the same system, drawn by two people. The first draws boxes with product names in them — a server here, a workflow engine there, a database, a model gateway — and arrows for the wires between them. The second draws no product at all. They draw what has to stay true no matter which box you swap out: where the durable record lives, who is allowed to write into it, what survives a session ending and what does not. Both diagrams are of one infrastructure. Only the second one will still be correct next year.

This page draws the second diagram. It is the one place in the handbook that steps back from any single pattern and asks what the whole arrangement has to provide for the rest of them to work — and it asks that as a question about *shape*, not about *parts*.

The distinction is borrowed, and worth naming as a borrow before it does any work. Network engineering separates the **[physical topology](https://en.wikipedia.org/wiki/Network_topology)** of a system — the literal placement of machines and cables — from its **logical topology**, which describes how data actually flows, independent of where the hardware sits. The two are routinely different: the same logical arrangement can run on entirely different physical layouts, and "their logical topologies may be identical" even when the wiring is not. We take exactly that separation and apply it one level up. The Synthesis Architecture is the *logical* topology of a [Pyragogy](/en/handbook/part-ii/what-is-pyragogy) network: the set of guarantees the infrastructure must make to the graph of human and synthetic peers learning on it. The machines that happen to make those guarantees are the physical layer, and the physical layer is interchangeable by design.

This is not a setup tutorial, and the difference is the whole point of the page.

## Why the abstraction, and not the stack

A handbook that documented the stack would be obsolete the day a tool was replaced — and tools get replaced. So this page documents the topology and treats the tools as examples of it, never as the thing itself. The rule is the same one the rest of the handbook applies to its concepts: a structure named after a tool dies when the tool changes. Here it is applied to the infrastructure.

There is a concrete way to feel the difference. A running Pyragogy network does, in fact, sit on specific software: a self-hostable deployment platform such as [Coolify](https://coolify.io/) standing up services on a rented virtual server from a provider such as [Hetzner](https://www.hetzner.com/cloud); a workflow engine such as [n8n](https://n8n.io/) routing events between the parts; a backend platform such as [Appwrite](https://appwrite.io/) holding identity and the structured store; a model gateway such as [OpenRouter](https://openrouter.ai/) putting many language models behind one interface; a note vault such as [Obsidian](https://obsidian.md/) holding the human-readable half of the record. Every one of those names is an example, and every one is replaceable. None of them belongs in a definition, and you will not find one in this page's title or in any claim about what the architecture *is*. What the architecture is, is the set of properties that survives swapping all of them out at once.

So the page is organized around guarantees, not components. Four of them carry the weight.

## The four guarantees

State them as obligations the infrastructure owes the graph, because that is how the patterns consume them.

**One — a durable record that outlives the session.** The architecture must hold a store that does not reset when a conversation ends. This is the substrate every persistence pattern leans on: it is what the [Pattern: Context Persistence](/en/handbook/part-iii/context-persistence) anchors a transient brainstorm *to*, and what the [Pattern: The Shared Ledger of Knowledge](/en/handbook/part-iii/shared-ledger) accrues entries *into*. The topological requirement is precise and tool-free: there exists a node in the system whose state survives the end of any single participant's session — and survives, in particular, the model's reset, which is total. Whether that node is a database, a versioned file tree, a note vault, or all three at once is a physical-layer decision. That *some* node holds across the boundary is the guarantee.

**Two — a record legible to two unlike readers.** The same durable store has to be readable by a human who forgets and by a model that resets, and those are not the same kind of reader. The human reads prose and recognizes it next morning; the model is *loaded* with tokens it can weight. This is the [Cognitive Impedance Mismatch](/en/handbook/part-ii/cognitive-impedance-mismatch) showing up as an infrastructure constraint rather than a cognitive one: a record stored in a form only one of the two can use has deposited for one participant and let the insight evaporate for the other. Topologically, the durable node is double-faced — one face human-legible, one face machine-loadable — and the architecture's job is to keep both faces written from a single act of deposit. In a running stack the two faces might live in different products; in the logical topology they are one obligation.

**Three — convergence with no central authority.** The architecture must let shared knowledge settle across participants who edit it independently — across sessions, across the gap between carbon and silicon — *without* a node that adjudicates what is true. This is the property the [CRDT Bridge](/en/handbook/part-ii/crdt-bridge) borrows and holds against this exact setting: agreement as a consequence of how the record is shaped, not of who is allowed to approve a change. The topological consequence is a refusal, and it is unusual: the diagram has no master node. No box validates. There is deliberately no place in the architecture where a single authority — human or model — decides what the group knows, because the moment such a place exists, the network stops being a graph of peers and becomes a hierarchy with a tool at the top of it. The guarantee here is the *absence* of a guarantor.

**Four — many models behind one boundary.** The synthetic peers are not one model, and the architecture should not assume they are. A learning network that runs its [adversarial friction](/en/handbook/part-iii/adversarial-friction) through a single fixed model inherits that model's particular blind spots as if they were the shape of the world. So the topology puts a boundary between the graph and the models it draws on, behind which the specific model can change — can be plural, can be swapped, can be chosen per task — without the rest of the architecture noticing. A model gateway is the physical-layer name for that boundary. The logical requirement is that no part of the network upstream of the boundary is wired to one model's identity. The peers are functional, in the sense the [What is Pyragogy](/en/handbook/part-ii/what-is-pyragogy) page sets out; the architecture keeps them swappable so that no single provider's weights become load-bearing for what the group can think.

Read together, the four describe a shape: a durable, double-faced record at the center; a graph of human and synthetic peers writing into it; no authority above the graph; and a permeable boundary to the models, behind which the particular intelligence is replaceable. That shape is the Synthesis Architecture. Everything else is wiring.

![logical topology of the synthesis architecture](/diagrams/19_synthesis-architecture.svg)

## Self-hosting is a topological commitment, not a preference

One physical-layer choice does press up into the logical topology, and it deserves naming because it looks like a deployment detail and is not.

The architecture is **self-hosted** — run on infrastructure under the network's own administrative control rather than on a third party's managed service. The established framing of [self-hosting](https://en.wikipedia.org/wiki/Self-hosting_(web_services)) is about control, privacy, and independence: running a service "instead of using a service outside of the administrator's own control." For most projects that is a preference, weighed against the convenience of a managed platform. For this one it follows from guarantee three. An architecture whose entire point is *convergence with no central authority* cannot route its durable record through a node that a third party can read, freeze, price out, or switch off at will — because that node would then *be* the central authority, sitting outside the graph and above it, regardless of how peer-to-peer the diagram looks on the inside. The refusal of a master node has to extend to the infrastructure, or it is not a refusal at all. Self-hosting is the logical topology keeping its own promise down to the metal.

This is also where the page is honest that the promise is partial. Self-hosting moves the authority, it does not abolish it: the rented server still sits in someone's data center, the model gateway still terminates at providers the network does not own, and the boundary to the models (guarantee four) is precisely a place where the graph reaches outside itself for an intelligence it cannot host. The architecture controls its *record*. It does not control the *models*, and pretending otherwise would reintroduce the central authority by the back door — as a dependency rather than a server.

## What this page does not do

It does not tell you how to install any of it. The operational specifics — how the workflow engine is wired, how the deposit moment fires, how a model is selected per task — live inside the patterns that use them, not here. This page exists so those patterns have one shared map to point back to when they say "the store that persists" or "the record both readers can use," and do not each have to redraw the whole topology. The pattern owns the operation; the synthesis owns the shape.

## Where this is still thin

Three tensions stay open, and an architecture page that hid them would be drawing the diagram it wished it had rather than the one it has.

First, **the no-authority topology is a target, not a measured property.** Guarantee three asks the infrastructure to host convergence without a validating node — but as the [CRDT Bridge](/en/handbook/part-ii/crdt-bridge) already flags, the mathematics that makes convergence-without-authority *safe* applies to data structures whose merge is correct by construction, not to a group's shared knowledge. Shapiro et al. establish the eventual-consistency result for CRDTs; the claim that this safety property does not transfer to a learning network's shared knowledge is an interpretive extension, not an argument made in that paper. The architecture can refuse a master node. It cannot, on its own, guarantee that the convergence which then happens is earned rather than a quiet [capitulation](/en/handbook/part-vi/compliance-trap) recorded as agreement. Removing the authority is a structural choice; making the result trustworthy is not something the topology delivers by itself.

Second, **a durable record is also a durable liability.** Guarantee one keeps everything that was deposited — including the session's mistakes. The same store that lets an insight survive lets an anchored error survive beside it, waiting to be loaded back with the authority of a written record, which is the failure the handbook treats under [Anti-Pattern: Context Poisoning](/en/handbook/part-vi/context-poisoning). The architecture provides persistence; it does not provide an immune system, and where the curation that would catch the bad entry should sit in the topology — and whether it can sit anywhere without becoming the authority guarantee three forbids — we do not resolve here.

Third, **we have no instrumented network to measure this against.** The four guarantees are stated as what the architecture *must* provide, in the prescriptive — because we have not yet run a documented Pyragogy network long enough to observe which guarantee fails first under load, what the self-hosting boundary actually costs when the rented server or the model gateway goes down, or whether the no-authority refusal survives contact with a group that wanted someone in charge. No instrumented, logged deployment of a full Pyragogy synthesis architecture has been located. The component literatures (network topology, self-hosting, CRDTs, context engineering) are established and cited; their composition into this specific learning-infrastructure topology is project practice, not a documented finding.

The Synthesis Architecture, then, is not a system you can boot. It is the set of promises a bootable system would have to keep — a durable record two unlike readers can use, no node above the graph, and the models held at arm's length — written down so the rest of the handbook can lean on the shape without inheriting the tools, and honest that the shape has so far only been drawn, not yet run hard enough to fail.

---

## References

- Network topology, *Wikipedia*. https://en.wikipedia.org/wiki/Network_topology — defines network topology as "the arrangement of the elements (links, nodes, etc.) of a communication network" and distinguishes **physical topology** ("the placement of the various components of a network") from **logical topology** ("how data flows within a network"), noting that "a network's physical topology is not necessarily the same as its logical topology" and that two networks with different physical layouts "may be identical" logically. Used here for the borrowed logical-vs-physical separation that the whole page rests on. (Distinction verified verbatim against the article.)
- Self-hosting (web services), *Wikipedia*. https://en.wikipedia.org/wiki/Self-hosting_(web_services) — defines self-hosting as running a service "using a private server, instead of using a service outside of the administrator's own control," motivated by control, privacy, and independence from a for-profit intermediary. Used for the claim that self-hosting is the infrastructure-level form of the no-central-authority guarantee. (Definition and motivation verified verbatim.)
- Marc Shapiro, Nuno Preguiça, Carlos Baquero, and Marek Zawirski, "Conflict-Free Replicated Data Types," in *Stabilization, Safety, and Security of Distributed Systems — SSS 2011*, Lecture Notes in Computer Science 6976 (Berlin: Springer, 2011), 386–400. https://doi.org/10.1007/978-3-642-24550-3_29 — the convergence-without-a-central-authority result that guarantee three borrows, cited in full on the [CRDT Bridge](/en/handbook/part-ii/crdt-bridge) page. Listed here because the "no master node" property of the topology rests on that borrow; the established result concerns data structures, and its application to a learning network's shared knowledge is, as flagged, a wager rather than a theorem.
- Tool examples named in the body are products, not citations, and appear only as illustrations of the physical layer: the self-hostable deployment platform [Coolify](https://coolify.io/) ("an open-source & self-hostable alternative to Vercel, Heroku, Netlify and Railway"); cloud hosting from [Hetzner](https://www.hetzner.com/cloud); the source-available workflow-automation engine [n8n](https://n8n.io/); the open-source backend platform [Appwrite](https://appwrite.io/) (Auth, Databases, Storage, Functions, Realtime); the model gateway [OpenRouter](https://openrouter.ai/) ("the unified interface for LLMs," routing to many providers behind one API); and the note vault [Obsidian](https://obsidian.md/). Each was reachable (HTTP 200) and its description verified at synthesis time; none is load-bearing for any definition on this page, and each is expected to change.
