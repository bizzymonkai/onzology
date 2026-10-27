# Onzology

Onzology is the laboratory for the MonkeyBusiness conceptual ontology.

MonkeyBusiness is the open, peer-to-peer business protocol: the conceptual system that has to describe real coordination without a platform in the middle.

This repository holds the plan and the working layout. [Notention](https://github.com/autonull/notention9) remains the starting point for semantic matching and for generalized object strategies. It is not the definition of the ontology, and its wire format is not the protocol. Its test suites, UI, command-line tool, and agent framework are disregarded.

## Status

| Step | Work | State |
|---|---|---|
| 0 | Establish the baseline | Done. Conclusion is below. Reviewed Notention `47075c86` (2026-10-26). |
| 1 | Define the conceptual model | Started. The lexicon lives in [`ontology/`](ontology/). |
| 2 | Adapt the semantic kernel | Not started. Matching and object strategy only. |
| 3 | Simulator | Placeholder. [`simulator/`](simulator/) creates and tests situations. |
| 4 | Test interoperability | Not started. |
| 5 | User-facing interfaces | Not started. [`ui/`](ui/), [`agent/`](agent/), and [`cli/`](cli/) are placeholders. |

Do not merge this work back over Notention, and do not replace Notention's specification. Onzology is a staged experiment.

## The distinction to keep

| Name | What it is | What it is not |
|---|---|---|
| **MonkeyBusiness** | The protocol and conceptual system | An app, a note editor, or a marketplace workflow |
| **Notention** | A candidate semantic engine and scenario tool | The ontology, the wire standard, or the product |
| **Onzology** | The place the ontology is defined, tested, and revised | A fork that silently adopts Notention's schema |

An application feature is a solution to a situation. The ontology describes the participants, things, claims, possibilities, events, and outcomes that make the situation sayable. If a new domain requires a new hard-coded workflow, the ontology is too narrow.

## Rules that constrain the work

These are design constraints, not aspirations. A change that breaks one of them does not land.

**Protocol shape**

- The object and relationship model is independent of any note editor.
- Ontology definitions are versioned, extensible, and tested on their own.
- Transport encoding is an adapter. Nostr, mesh, HTTP, and local storage do not define the objects.
- A peer is the wide-area network endpoint, usually the TCP/IP address assigned to the point of contact. An identity is one signing key. The main key is recovered from a [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) mnemonic. An account is a child key derived from that main key, not a login. Objects stay distinct from all of those.
- A signature establishes who asserted something. It does not establish that the assertion is true.
- Personal knowledge management, dashboards, browser agents, and marketplace screens are applications. They are not requirements of the protocol.

**What must be representable**

- Competing claims, partial knowledge, disputed facts, and failed interactions.
- Incomplete, hypothetical, and still-changing situations.
- A shared situation with no shared database and no unanimous account of what happened.

**How the ontology is allowed to grow**

- The semantic graph is the structure.
- Peer vocabulary (folksonomy) is how words appear, including synonyms and local terms. Original wording is kept when it is mapped.
- A tag cloud is a view of frequency. It is not the ontology.
- The situation is the unit of analysis. Ride-sharing, repair, rental, delivery, and a loan are applications of the same situation structure, not separate kernels.
- Nothing in the model may assume that every request becomes an offer, every offer an agreement, or every agreement a completion.

**Assent**

- An offer may receive zero or more acceptance records.
- An agreement becomes mutually assented to only when every required party has assented to the same agreement, or to its terms.
- The model must represent incomplete assent, withdrawn assent, conflicting terms, and disputed claims without treating them as a completed contract.

**MonkeyBusiness commitments**

- No administrators and no gatekeepers. Participation does not depend on a registrar, a permit, or a platform account.
- Peer-to-peer by structure, not by slogan. A required relay, indexer, or operator is an adapter under test, not the protocol.
- Private by default. Publication is explicit, and in this version a published note is public. Hashing a tag while sending the body is not encryption.
- Rules, not rulers. Order comes from explicit records and peer challenge, not from a higher authority inside the protocol.
- Collaboration of records, not a central registration.
- Endorsements and peer advocacy, not licenses or permits, as the trust signal.
- The business vocabulary evolves from use. Designers do not own the language.
- No structural counterparty. Two identities can bind a record without a platform standing between them. The addresses they happen to hold are not the parties.
- Success may be copied. This repository is AGPL-3.0 so network improvements stay available. The protocol is not a licensing business.

## Conceptual model the plan requires

Notention's four functions — fact, constraint, attestation, transition — stay as **semantic roles**. They are not the ontology.

Three questions are different dimensions and must not be collapsed into one note type:

| Question | Examples |
|---|---|
| What is being described? | Person, resource, place, service, request, offer, agreement, situation |
| What is being asserted? | Fact, intention, requirement, observation, opinion, hypothetical |
| What happened? | Event, response, acceptance, cancellation, payment, correction, dispute |

An offer is an object. It contains assertions about price and availability. It may receive zero acceptance records, or many. An acceptance is its own record. It does not rewrite the offer. Mutual assent is not any one of those records.

### Layers

| Layer | Holds |
|---|---|
| **Situation** | The real, imagined, or disputed context. Not one signed object. |
| **Objects** | Descriptions, requests, offers, agreements, records |
| **Assertions and relationships** | Claims, constraints, evidence, references, challenges |
| **Events and outcomes** | Responses, changes, settlements, failures, disputes |

### Situation dimensions

Candidate dimensions, not mandatory fields. A record may leave any of them empty.

| Dimension | Examples |
|---|---|
| Participants | Peers, identities, groups, roles |
| Context | Time, place, resources, constraints |
| Assertions | Needs, observations, claims, intentions |
| Possibilities | Requests, offers, alternatives, agreements |
| Events | Messages, changes, actions, decisions |
| Outcomes | Completion, failure, cancellation, dispute |

A dispute is not the opposite of completion. Both can be true in one situation.

### Relationships

Explicit and extensible. Initial set, not a closed list:

`describes` · `involves` · `requests` · `offers` · `responds_to` · `references` · `supports` · `challenges` · `agrees_with` · `supersedes` · `results_in`

### Distinctions

Revised 2026-10-27. Device is not an object in this model. It is the point of contact for a peer. Key management is the identity layer.

**Decided**

- A peer is a participant on the wide-area network, reached at the address that network assigns. Usually TCP/IP. The address is how the peer is reached. The device is only the point of contact.
- Key management follows [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki). A mnemonic plus an optional passphrase is stretched with PBKDF2-HMAC-SHA512 for 2048 rounds into a 512-bit seed. [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) says that seed is what generates a deterministic wallet, by [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) or a method like it. The mnemonic, the passphrase, and the seed stay on the point of contact. Other peers never see them.
- An identity is one signing key. One key, one identity. Other peers check the signature, not the address and not the mnemonic.
- The main key is the [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) master key of the tree grown from that seed. The same mnemonic and the same passphrase restore the same main key on any point of contact.
- An account is a child key derived from that main key. It is its own identity. It is not a login. Derivation is not authority: the main key does not sign for the account, and it cannot revoke it.
- The same words with a different passphrase are a different seed and different identities. A new mnemonic is a new seed. Other peers cannot tell that two keys came from one seed unless some identity signs a record that says so. That record is not part of this layer.
- Restoring the mnemonic restores the identities. The wide-area network still assigns the point of contact a new address, so the peer is new.
- A signature over a hash does not prove possession of the file. A hash can be copied. If no one can produce the original, the claim is unproven either way. Holding the file is not an argument and not an agreement.
- There is no default MonkeyBusiness agreement. Terms bind only the identities that assent to them.

Until a later wording pass, the rest of this file sometimes says "peer" for the party to a situation. That party is the identity. The peer is the network endpoint.

**Still to solve before the lexicon is tested**

- Object versus type. What the first roof record is, if it is not a job class and not the situation itself. What a matcher may compare.
- Which identities are the required parties to a given agreement. Being named in someone else's record is not assent.

**Left unsettled on purpose**

- A signed association between two published keys that came from one seed. Local derivation already restores them. Publishing that they are related is a later choice.
- A new mnemonic claiming an old identity. Later. Not step 1.
- Default terms inside agreements: succession, arbitration, payment, custody. Downstream of a record both identities sign.
- Who assigns an address when there is no ISP and no DHCP. The peer is an assigned address. The assigner is not specified, and it cannot be a registrar.
- Enforcing who owns a file. The model can hold a claim and a challenge. It does not pick a winner.
- What a screen may call settled. Display is local.

### What stays stable, and what does not

| Layer | Rule |
|---|---|
| Core conventions | Small, slow to change: object envelope, signature-as-provenance, situation linkage, revision rules |
| Semantic vocabulary | Free to grow from peer use and scenario failure |
| Local behavior | An application may specialize. That specialization is not the protocol |

## How a change is accepted

Ontology work is itself peer-to-peer: propose, show that it helps, expose where it fails, revise, keep the decision history.

A proposal is not accepted because the wording sounds clean. It has to improve what the model can represent. Every proposal records:

| Field | Content |
|---|---|
| Problem | The situation the current model cannot say |
| Current representation | How it is forced into the model today, or why it cannot be |
| Proposed change | Concept, relationship, or convention |
| Examples | Cases it makes representable |
| Counterexamples | Cases it makes worse or falsely collapses |
| Compatibility | Which existing scenarios still pass |
| Decision history | What was tried and rejected |

The acceptance test: the same core model represents the new situation without an application-specific rule, and every previous scenario still passes.

## Baseline (step 0)

Reviewed [autonull/notention9](https://github.com/autonull/notention9) at `47075c86` (2026-10-26). The test inventory is not kept. What matters:

- Conflicts in matching are workable. Notention's semantic matching and its generalized object strategy are the starting point. Its type hierarchy is not.
- Conflicts in revision are real, and unresolved. Updating a private object is easy: it has not been published. Updating a network object is difficult: other identities may already have referenced it. Network garbage disposal is an open question. None of that is settled in this step.
- Disregarded: Notention's test suites, UI, CLI, and agent framework.

Notention code is not in this repository. It stays out until that project ships a license file and the terms are compatible with this one.

## Plan

### 0. Establish the baseline

Done. Deliverable: the conclusion above.

### 1. Define the conceptual model

Started. The evolving semantic lexicon is [`ontology/`](ontology/). Reusable situations go in [`ontology/known/`](ontology/known/).

Do not import Notention's types. Do not treat a job class as the ontology.

The lexicon has to be able to say:

1. Purpose and scope
2. Foundational concepts
3. Relationship vocabulary
4. Initial semantic registry
5. Situation representation
6. Vocabulary extension model
7. Scenario test suite
8. Revision procedure

Deliverable: a tested conceptual model. Not a user interface.

### 2. Adapt the semantic kernel

Keep matching and the generalized object strategy only where they fit the lexicon. Notention's wire format does not become the standard.

No upstream source is vendored until its license file exists and is compatible with this repository's AGPL-3.0.

### 3. Simulator

[`simulator/`](simulator/) is where situations are created and tested. It does not import Notention's simulator.

### 4. Test interoperability

Two independent implementations publish, discover, reference, and interpret the same objects. Cases include a different transport, unfamiliar vocabulary, missing fields, conflicting claims, and incompatible ontology versions.

### 5. Interfaces

Only after the conceptual model survives the scenarios. [`ui/`](ui/), [`agent/`](agent/), and [`cli/`](cli/) are placeholders for those interfaces. They are applications of the protocol, not how the protocol is discovered.

## First experiment

One thin slice, then the same slice in other domains:

1. A peer publishes a situation.
2. Another peer publishes an offer that references it.
3. The first peer discovers and evaluates the offer.
4. Both peers exchange signed records.
5. The interaction may include completion, cancellation, withdrawn assent, or a dispute. More than one can be true. None of the incomplete cases is a completed contract.
6. The simulator checks that every step was representable without application-specific code.

Motivating situation: a roof repair. The customer describes the roof and attaches photographs. Two roofers offer different prices and schedules. Those offers conflict. Neither is an agreement. One offer expires with no acceptance. The customer accepts the other. That acceptance is one record. It is mutual assent only if every required party has assented to those same terms. The work can be completed, and the customer can still dispute the invoice. The dispute is not a completed contract, and it does not erase the assent already given.

Repeat the same sequence for a ride, a rental, a freelance job, a delivery, and an equipment loan. A concept added for the roof is re-run against the others before it is kept.

That is the first milestone: a working laboratory, built from proven components where the license and the model allow it, without committing the protocol to Notention's architecture.

## What will not be added early

- A unified interface, before the lexicon survives a scenario
- A required relay, indexer, or hosted agent
- Token gates, admin roles, or permits
- A native token, or a fee taken by the protocol
- Domain skills hard-coded as classes
- Notention's test suites, UI, CLI, or agent framework
- A second status document that can drift from this one

## Layout

```text
ontology/            evolving semantic lexicon
ontology/known/      reusable situations
simulator/           create and test situations
ui/                  placeholder for interface work
agent/               placeholder for agent interfaces
cli/                 placeholder for command interfaces
```

`ui/`, `agent/`, and `cli/` do not import Notention. `simulator/` does not import Notention's simulator.

## License

[GNU Affero General Public License v3.0](LICENSE) only.

Notention code is not included. It stays out until that project ships a license file and the terms are compatible with this one.

## Sources

- This plan: the rebuild sequence for using Notention as a MonkeyBusiness workbench, consolidated on 2026-10-27. [Conversation](https://chatgpt.com/share/6ae07b3d-ade4-83e9-a062-1fc430688791).
- Upstream reviewed: [autonull/notention9](https://github.com/autonull/notention9) `47075c86`.
- Public commitments used as the conflict check: [MonkeyBusiness.systems](https://monkeybusiness.systems/).
