# Onzology

Onzology is the laboratory for the MonkeyBusiness conceptual ontology.

MonkeyBusiness is the open, peer-to-peer business protocol: peers coordinate through the records they sign.

This repository holds the plan and the working layout. [Notention](https://github.com/autonull/notention9) remains the starting point for semantic matching and for generalized object strategies. The ontology and the wire format are defined here. Notention's test suites, UI, command-line tool, and agent framework stay in that project.

## Status

| Step | Work | State |
|---|---|---|
| 0 | Establish the baseline | Done. Conclusion is below. Reviewed Notention `47075c86` (2026-10-26). |
| 1 | Define the conceptual model | Started. The lexicon lives in [`ontology/`](ontology/). |
| 2 | Adapt the semantic kernel | Not started. Matching and object strategy only. |
| 3 | Simulator | Placeholder. [`simulator/`](simulator/) creates and tests situations. |
| 4 | Test interoperability | Not started. |
| 5 | User-facing interfaces | Not started. [`ui/`](ui/), [`agent/`](agent/), and [`cli/`](cli/) are placeholders. |

Onzology is its own repository. Notention's specification stays in Notention. Onzology is a staged experiment.

## The distinction to keep

| Name | What it is |
|---|---|
| **MonkeyBusiness** | The open peer-to-peer business protocol and conceptual system |
| **Notention** | A candidate semantic engine and scenario tool for matching and generalized objects |
| **Onzology** | The laboratory where the ontology is defined, tested, and revised |

An application feature is a solution to a situation. The ontology describes the participants, things, claims, possibilities, events, and outcomes that make the situation sayable. If a new domain requires a new hard-coded workflow, the ontology is too narrow.

## Rules that constrain the work

These are design constraints. A change lands when it satisfies every constraint in this section.

**How a definition is written**

- A definition says what a thing is.
- A sentence of the form "it is not X, it is Y" is published only after it is approved.

**Protocol shape**

- The object and relationship model is independent of any note editor.
- Ontology definitions are versioned, extensible, and tested on their own.
- Transport encoding is an adapter. The objects are defined here. Nostr, mesh, HTTP, and local storage carry them.
- A peer is the wide-area network endpoint, usually the TCP/IP address assigned to the point of contact. An identity is one signing key. The main key is recovered from a [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) mnemonic. An account is a child key derived from that main key. Objects stay distinct from all of those.
- A signature establishes who asserted something. Whether the assertion holds is a later record: support, challenge, or assent.
- Personal knowledge management, dashboards, browser agents, and marketplace screens are applications.

**What must be representable**

- Competing claims, partial knowledge, disputed facts, and failed interactions.
- Incomplete, hypothetical, and still-changing situations.
- A shared situation with no shared database and no unanimous account of what happened.

**How the ontology is allowed to grow**

- The semantic graph is the structure.
- Peer vocabulary (folksonomy) is how words appear, including synonyms and local terms. Original wording is kept when it is mapped.
- A tag cloud is a view of frequency.
- The situation is the unit of analysis. Ride-sharing, repair, rental, delivery, and a loan are applications of the same situation structure.
- Nothing in the model may assume that every request becomes an offer, every offer an agreement, or every agreement a completion.

**Assent**

- An offer may receive zero or more acceptance records.
- An agreement is two or more identities. Each has signed the same agreement, or the same terms. Those signers are the parties.
- The model must represent incomplete assent, withdrawn assent, conflicting terms, and disputed claims without treating them as a completed contract.

**MonkeyBusiness commitments**

- Anyone holding a key may publish and sign.
- Peers reach each other directly. A relay, an indexer, or an operator is an adapter under test.
- Private by default. Publication is explicit, and in this version a published note is public. Encryption hides the body from peers who lack the key. A hash of a tag leaves the body readable.
- Order comes from explicit records and peer challenge.
- Peers collaborate by exchanging records.
- The trust signal is an endorsement one identity signs about another.
- The business vocabulary evolves from use.
- The parties to a record are the identities that sign it. An address is how a peer is reached.
- Success may be copied. This repository is AGPL-3.0 so network improvements stay available.

## Conceptual model the plan requires

Notention's four functions — fact, constraint, attestation, transition — stay as **semantic roles** inside the lexicon.

Three questions stay separate dimensions:

| Question | Examples |
|---|---|
| What is being described? | Person, resource, place, service, request, offer, agreement, situation |
| What is being asserted? | Fact, intention, requirement, observation, opinion, hypothetical |
| What happened? | Event, response, acceptance, cancellation, payment, correction, dispute |

An offer is an object. It contains assertions about price and availability. It may receive zero acceptance records, or many. An acceptance is its own record. Mutual assent is two or more identities each signing the same agreement, or the same terms.

### Layers

| Layer | Holds |
|---|---|
| **Situation** | The real, imagined, or disputed context. Many records may refer to one situation. |
| **Objects** | Descriptions, requests, offers, agreements, records |
| **Assertions and relationships** | Claims, constraints, evidence, references, challenges |
| **Events and outcomes** | Responses, changes, settlements, failures, disputes |

### Situation dimensions

Candidate dimensions. A record may leave any of them empty.

| Dimension | Examples |
|---|---|
| Participants | Peers, identities, groups, roles |
| Context | Time, place, resources, constraints |
| Assertions | Needs, observations, claims, intentions |
| Possibilities | Requests, offers, alternatives, agreements |
| Events | Messages, changes, actions, decisions |
| Outcomes | Completion, failure, cancellation, dispute |

A dispute and a completion can both be true in one situation.

### Relationships

Explicit and extensible. Initial set:

`describes` · `involves` · `requests` · `offers` · `responds_to` · `references` · `supports` · `challenges` · `agrees_with` · `supersedes` · `results_in`

### Distinctions

Revised 2026-10-27. The device is the point of contact for a peer. Key management is the identity layer.

**Decided**

- A peer is a participant on the wide-area network, reached at the address that network assigns. Usually TCP/IP. The address is how the peer is reached. The device is only the point of contact.
- Key management follows [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki). A mnemonic plus an optional passphrase is stretched with PBKDF2-HMAC-SHA512 for 2048 rounds into a 512-bit seed. [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) says that seed is what generates a deterministic wallet, by [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) or a method like it. The mnemonic, the passphrase, and the seed stay on the point of contact.
- An identity is one signing key. One key, one identity. Other peers check the signature.
- The main key is the [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) master key of the tree grown from that seed. The same mnemonic and the same passphrase restore the same main key on any point of contact.
- An account is a child key derived from that main key. It is its own identity. The account signs for itself.
- The same words with a different passphrase are a different seed and different identities. A new mnemonic is a new seed. Other peers treat two keys as related when an identity signs a record that says so. That record comes later.
- Restoring the mnemonic restores the identities. The wide-area network still assigns the point of contact a new address, so the peer is new.
- A signature over a hash says the signer asserted that hash. A hash can be copied. The file is shown by producing the original. Otherwise the claim stays open.
- Terms bind only the identities that assent to them.
- The first roof record is an object. A matcher compares its tokens. Strict comparison of `type` to `type` is allowed, and optional. An object with `type:foo` matches every index of the token `foo`, whatever key holds that token. `type:bar` against an index entry `type:bar` is a higher-certainty match. An object with no `type` property matches on its other tokens.
- An agreement is two or more identities. Each has signed the same agreement, or the same terms. Those signers are the parties.

Until a later wording pass, the rest of this file sometimes says "peer" for the party to a situation. That party is the identity. The peer is the network endpoint.

**Left unsettled on purpose**

- A signed association between two published keys that came from one seed. Local derivation already restores them. Publishing that they are related is a later choice.
- A new mnemonic claiming an old identity. Later, after step 1.
- Default terms inside agreements: succession, arbitration, payment, custody. Downstream of the records the parties sign.
- Who assigns an address when there is no ISP and no DHCP. The peer is an assigned address. The assigner is open.
- Who owns a file. The model holds a claim and a challenge. The outcome is a later record.
- What a screen may call settled. Display is local.

### What stays stable, and what changes

| Layer | Rule |
|---|---|
| Core conventions | Small, slow to change: object envelope, signature-as-provenance, situation linkage, revision rules |
| Semantic vocabulary | Free to grow from peer use and scenario failure |
| Local behavior | An application may specialize. The shared conventions are the protocol |

## How a change is accepted

Ontology work is itself peer-to-peer: propose, show that it helps, expose where it fails, revise, keep the decision history.

A proposal is accepted when it improves what the model can represent. Every proposal records:

| Field | Content |
|---|---|
| Problem | The situation the current model cannot say |
| Current representation | How it is forced into the model today, or why it cannot be |
| Proposed change | Concept, relationship, or convention |
| Examples | Cases it makes representable |
| Counterexamples | Cases it makes worse or falsely collapses |
| Compatibility | Which existing scenarios still pass |
| Decision history | What was tried and rejected |

The acceptance test: the same core model represents the new situation, and every previous scenario still passes.

## Baseline (step 0)

Reviewed [autonull/notention9](https://github.com/autonull/notention9) at `47075c86` (2026-10-26). What the review concluded:

- Conflicts in matching are workable. Notention's semantic matching and its generalized object strategy are the starting point. The lexicon written here is the vocabulary. Re-read of the matcher at the same commit: [`PropertyIndex`](https://github.com/autonull/notention9/blob/47075c86/core/src/matching/PropertyIndex.ts) indexes property keys, and a candidate must carry every request key. [`MatchEngine`](https://github.com/autonull/notention9/blob/47075c86/core/src/matching/MatchEngine.ts) compares a request property to an offer property on that key, or on an ontology alias of it. The score is satisfied constraints over the request's properties. In [`matchers.ts`](https://github.com/autonull/notention9/blob/47075c86/core/src/matching/matchers.ts), "type" is the value's datatype (string, number, date, geo, enum), inferred from the operator. A `type:foo` property matches an offer property whose key is `type` or an alias of `type`. The token `foo` under another key is a separate comparison. A type-to-type hit scores as an ordinary exact key hit. Onzology's rule is under Decided.
- Conflicts in revision are real, and unresolved. Updating a private object is easy: it is still on the point of contact. Updating a published object is difficult: other identities may already have referenced it. Network garbage disposal is an open question. Both stay open in this step.
- Notention's test suites, UI, CLI, and agent framework stay in that project.

This repository contains Onzology's plan and layout. Notention source waits on a license file compatible with AGPL-3.0.

## Plan

### 0. Establish the baseline

Done. Deliverable: the conclusion above.

### 1. Define the conceptual model

Started. The evolving semantic lexicon is [`ontology/`](ontology/). Reusable situations and vocabularies go in [`ontology/known/`](ontology/known/). The first vocabulary is [`ontology/known/consumer-spending.md`](ontology/known/consumer-spending.md). It names kinds of spending.

The lexicon is written here, from situations.

The lexicon has to be able to say:

1. Purpose and scope
2. Foundational concepts
3. Relationship vocabulary
4. Initial semantic registry
5. Situation representation
6. Vocabulary extension model
7. Scenario test suite
8. Revision procedure

Deliverable: a tested conceptual model.

### 2. Adapt the semantic kernel

Keep matching and the generalized object strategy only where they fit the lexicon. The lexicon defines the objects. Notention's wire format is one adapter among others.

An upstream source is vendored when its license file exists and is compatible with this repository's AGPL-3.0.

### 3. Simulator

[`simulator/`](simulator/) is where situations are created and tested.

### 4. Test interoperability

Two independent implementations publish, discover, reference, and interpret the same objects. Cases include a different transport, unfamiliar vocabulary, missing fields, conflicting claims, and incompatible ontology versions.

### 5. Interfaces

Only after the conceptual model survives the scenarios. [`ui/`](ui/), [`agent/`](agent/), and [`cli/`](cli/) are placeholders for those interfaces. They are applications. The protocol is the lexicon and the records peers sign.

## First experiment

One thin slice, then the same slice in other domains:

1. A peer publishes a situation.
2. Another peer publishes an offer that references it.
3. The first peer discovers and evaluates the offer.
4. Both peers exchange signed records.
5. The interaction may include completion, cancellation, withdrawn assent, or a dispute. More than one can be true. A completed contract is two or more identities that have each signed the same agreement, or the same terms.
6. The simulator checks that the lexicon already had the words for every step.

Motivating situation: a roof repair. The customer describes the roof and attaches photographs. Two roofers offer different prices and schedules. Those offers conflict. Each offer is its own record. One offer expires with zero acceptances. The customer accepts the other. That acceptance is one signature. The roofer's offer is the other. Those two identities, on the same terms, are the parties. The work can be completed, and the customer can still dispute the invoice. The dispute is a claim about the invoice. Assent already given stays on the record.

Repeat the same sequence for a ride, a rental, a freelance job, a delivery, and an equipment loan. A concept added for the roof is re-run against the others before it is kept.

That is the first milestone: a working laboratory, built from proven components where the license and the model allow it. The objects of the protocol are the ones defined in this repository.

## Early work

The lexicon and the simulator come first. Interfaces follow a lexicon that has survived a scenario. This file is the status document.

## Layout

```text
ontology/            evolving semantic lexicon
ontology/known/      reusable situations
simulator/           create and test situations
ui/                  placeholder for interface work
agent/               placeholder for agent interfaces
cli/                 placeholder for command interfaces
```

`ui/`, `agent/`, and `cli/` hold Onzology's interfaces. `simulator/` tests situations against the lexicon.

## License

[GNU Affero General Public License v3.0](LICENSE) only.

This repository contains Onzology's own files. Notention source waits on a license file compatible with AGPL-3.0.

## Sources

- This plan: the rebuild sequence for using Notention as a MonkeyBusiness workbench, consolidated on 2026-10-27. [Conversation](https://chatgpt.com/share/6ae07b3d-ade4-83e9-a062-1fc430688791).
- Upstream reviewed: [autonull/notention9](https://github.com/autonull/notention9) `47075c86`.
- Public commitments used as the conflict check: [MonkeyBusiness.systems](https://monkeybusiness.systems/).
