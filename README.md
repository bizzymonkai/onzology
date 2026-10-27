# Onzology

Onzology is the laboratory for the MonkeyBusiness conceptual ontology.

MonkeyBusiness is the open, peer-to-peer business protocol: the conceptual system that has to describe real coordination without a platform in the middle. [Notention](https://github.com/autonull/notention9) is a candidate implementation and experimental tool. It is not the definition of the ontology, and its wire format is not the protocol.

This repository does not yet contain protocol code. It holds the plan, the baseline against Notention, and the rules for what may be reused. The next artifact is a tested conceptual model, not a user interface.

Notention is useful because it already matches structured intent, keeps an editable vocabulary, and can run multi-agent scenarios. Onzology keeps that experimental method and does not inherit Notention's type hierarchy.

## Status

| Step | Work | State |
|---|---|---|
| 0 | Establish the baseline | Done. Inventory is below. Reviewed Notention `47075c86` (2026-10-26). |
| 1 | Define the conceptual model | Next. `ontology-v0.1.md` and a concept registry. No UI. |
| 2 | Adapt the semantic kernel | Not started. Adapters only after the model exists. |
| 3 | Rebuild the simulator around situations | Not started. |
| 4 | Test interoperability | Not started. |
| 5 | Build the user-facing super-app | Not started. Blocked on the model surviving scenarios. |

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
- Identity, peer, account, object, and address stay distinct concepts.
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

**MonkeyBusiness commitments**

- No administrators and no gatekeepers. Participation does not depend on a registrar, a permit, or a platform account.
- Peer-to-peer by structure, not by slogan. A required relay, indexer, or operator is an adapter under test, not the protocol.
- Encrypted by default. Publication is explicit. Hashing a tag while sending the body is not encryption.
- Rules, not rulers. Order comes from explicit records and peer challenge, not from a higher authority inside the protocol.
- Collaboration of records, not a central registration.
- Endorsements and peer advocacy, not licenses or permits, as the trust signal.
- The business vocabulary evolves from use. Designers do not own the language.
- No structural counterparty. Two peers can bind a record without a platform standing between them.
- Success may be copied. This repository is AGPL-3.0 so network improvements stay available. The protocol is not a licensing business.

## Conceptual model the plan requires

Notention's four functions — fact, constraint, attestation, transition — stay as **semantic roles**. They are not the ontology.

Three questions are different dimensions and must not be collapsed into one note type:

| Question | Examples |
|---|---|
| What is being described? | Person, resource, place, service, request, offer, agreement, situation |
| What is being asserted? | Fact, intention, requirement, observation, opinion, hypothetical |
| What happened? | Event, response, acceptance, cancellation, payment, correction, dispute |

An offer is an object. It contains assertions about price and availability. A later acceptance is an event that references it.

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

### Three distinctions step 1 must settle

| Distinction | Why it cannot stay fuzzy |
|---|---|
| Identity vs account vs peer | Keys, login accounts, and the party to a situation are different objects |
| Object vs type | A roof repair is not the class "job-request" |
| Reference vs ownership | Pointing at a record does not transfer it |

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

Reviewed [autonull/notention9](https://github.com/autonull/notention9) at `47075c86e106ac0273021725e9db57abc553aaad` (2026-10-26, `main`). Installed with pnpm 9.15.9 on Node 22. Notention's own `README2.md` is a normative spec plus a status inventory. Several inventory rows do not match the tree. This section records what ran, not what the inventory claims.

### What ran

| Package | Tests | Build |
|---|---|---|
| `@notention/core` | 34 files, 251 tests passed | `tsc` failed. `core/src/network/nostr/relay.ts` imports `ws` with no type declarations |
| `@notention/agent` | 4 files, 17 tests passed | `tsc` passed |
| `@notention/cli` | 1 file, 6 tests passed | `tsc` failed on the same `ws` import, through core sources |
| `simulator` | No unit suite. Playwright e2e not run | `tsc` and the studio UI build passed |
| `@notention/ui` | Full `vitest run` died at the heap limit. File by file: 33 of 36 passed | Vite production build passed |

UI failures that are real, not environmental:

- `src/tests/App.test.tsx` — render throws. `upsertNote` is missing from the notes mock, then `agentService.isConnected` is not a function. The smoke test is behind the app.
- `src/tests/plugins/MetaphorPlugin.test.tsx` — import of `components/metaphor/MetaphorRenderer` does not resolve.
- `src/tests/components/EditorManager.test.tsx` — process ran out of memory before assertions. Not counted as a product failure.

`pnpm test` at the root is not a reliable gate. The UI script is `vitest` without `run`, so it does not exit.

### Reuse, after the license gate

Worth adapting once upstream's license is actually granted. Do not copy the tree in before that. Notention's `package.json` files say MIT. `README2.md` says the license file is still to be added. There is no `LICENSE` file in the commit reviewed.

| Piece | Why it is reusable | Limit |
|---|---|---|
| `MatchEngine` and `matchers.ts` | Constraint-against-fact scoring with reasons: string, number, date, enum, geo distance, aliases | Score is not the spec's required/total ratio. Numeric `is` is a silent 5% tolerance. String `is` falls through to substring at 0.8. Missing operators: `approx`, `in`, `inter`, `exists` |
| Property parsers | Canonical `[key:op:value]`, symbolic, and word forms | Values are strings. Typed money, time, duration, and references are unspecified in the running code |
| Ontology helpers | Alias index, traversal, local add/rename/merge | Helpers edit a tree in memory. They do not version or content-address a vocabulary |
| Note privacy default | New notes start private | Spec says private notes are sealed and local data is encrypted at rest. The running README says the body is still published and encryption at rest is not provided |
| Scenario runner shape | Named agents, timed events, shared matching core | See the simulator row under Replace |

### Change before it can serve MonkeyBusiness

| Notention today | What has to change |
|---|---|
| `createNote` assigns `crypto.randomUUID()` and later writes `updatedAt` on the same id | Records are immutable. A change is a new record that references the previous one. Identity is content-addressed |
| `utils/inference.ts` only guesses string, number, or date | Lifecycle is inferred from later records, not stored as a status enum |
| `README2.md` points at `utils/canonicalization.ts` and `inferState` | Neither exists. The inventory is not a source of truth |
| Bare keys (`price`, `role`, `status`) in `domains.ts` | Inventory claims a `dsn:` namespace hardcoded in the ontology. The domains do not use it |
| `job-request` extends `job` and `request` | Those parent nodes are not defined |
| Four domain skill classes: Indeed, Craigslist, GitHub, Reminder | Inventory says five signed ontology skills. They are application adapters, and they are TypeScript classes |
| Matching service treats a note as either the request or the offer | The protocol needs bidirectional claims, missing fields, and contradiction, not one score |

### Do not inherit

| Notention idea | Why it conflicts |
|---|---|
| The default ontology tree as the protocol | Entity, message, event, job-request, freelance-offer, product, and a `status` enum collapse object, assertion, and event. Channels are Slack, Teams, WhatsApp, Discord. That is an application vocabulary frozen in the kernel |
| Fact / constraint / attestation / transition as the whole model | They are roles. Using them as the type system hides disputes, partial knowledge, and "both completion and dispute" |
| "The developer maintains the language of the network" (`ARCHITECTURE.md`) | The vocabulary evolves from peers. A maintainer role is a gatekeeper |
| Spec §9.5 token gating, "circle admin threshold", "higher-authority transition" | Permits and in-protocol authority. Trust is endorsement and challenge, not a gate or an admin |
| Simulator as specified by its code | Every agent receives one `DEFAULT_ONTOLOGY`. Coordination is a WebSocket relay. Every agent of a role acts in lockstep. Chat is the literal string `Hello!` on a public event. Traits are unused. Scenarios are `publish_job`, `publish_offer`, and that chat. No expiration, acceptance, invoice, or dispute. A relay may exist later as an adapter under test. It is not the laboratory |
| Kind 35000 property tags as the object format | Transport-specific encoding cannot be the protocol |
| Price, budget, and rate as bare numbers | Money is untyped. A Bitcoin unit of account cannot be retrofitted onto an untyped float without lying about what matched |
| `ARCHITECTURE.md` as current design | It still points matching at `utils/matching.ts`, the simulator at `SimulatorView.tsx`, and the score at matches/constraints. The code does not |

### Spec that is written and not implemented

Confirmed absent or unwired, not merely "partial" in the inventory:

- Canonical CBOR, content-addressed note ids, protocol signing digest, verification procedure
- Sealed envelopes. `privacy.ts` hashes tags. It does not seal
- Transition, endorsement, invoice, payment, escrow, receipt, refund, revocation, and key-rotation records
- Native peer id. Running identity is `nostr:` or `mesh:`
- Bitcoin and BOLT-12 aliases. `pay.btc` / `pay.lightning` are types only
- Circle keys, key rotation, social recovery
- Mesh integration, libp2p, HTTP client binding
- Tombstones (a `deletedAt` field is the current stand-in)
- Realtime merge, trust graph, dispute and governance records
- Conformance tests for canonicalization: 0 of 5. The core profile in §21 is not met

Notention is usable as a local semantic notebook with request/offer matching. It is not a conforming implementation of its own protocol, and that protocol is not yet MonkeyBusiness.

## Plan

### 0. Establish the baseline

Done. Deliverable: the reuse / change / replace inventory above.

### 1. Define the conceptual model

Create `ontology-v0.1.md` and a small machine-readable concept registry.

Do not import Notention's types. Define foundational objects and relationships, and how situations, claims, evidence, and events are represented.

`ontology-v0.1.md` contains:

1. Purpose and scope
2. Foundational concepts
3. Relationship vocabulary
4. Initial semantic registry
5. Situation representation
6. Vocabulary extension model
7. Scenario test suite
8. Revision procedure

Deliverable: a tested conceptual model, not a new UI.

### 2. Adapt the semantic kernel

Keep the matching engine, parser, ontology helpers, and validation only where they fit the model. Put adapters between the conceptual model and Notention's note objects.

Notention's current wire format does not become the standard by default.

No upstream source is vendored until its license file exists and is compatible with this repository's AGPL-3.0.

Deliverable: a small, independently testable core.

### 3. Rebuild the simulator around situations

Participants are independent peers. Each has its own information, preferences, and claims. Runs are replayable. The log records proposed ontology changes.

For every scenario, record:

1. Initial conditions — peers, resources, intentions, constraints, what each peer knows
2. Published objects — what each peer asserts, requests, or offers
3. Interpretation — how each object maps to the current ontology
4. Matching — what was found, why, what is missing or contradictory
5. Interaction — replies, negotiation, agreements, cancellations, other events
6. Evaluation — whether the situation was representable, and which concept was missing

The question is not "did the workflow succeed?" It is "could the ontology say what happened without a new application rule?"

Deliverable: the ontology feedback laboratory.

### 4. Test interoperability

Two independent implementations publish, discover, reference, and interpret the same objects. Cases include a different transport, unfamiliar vocabulary, missing fields, conflicting claims, and incompatible ontology versions.

Deliverable: a minimal conformance suite.

### 5. Build the user-facing super-app

Only after the conceptual model survives the scenarios. Interface, identity experience, marketplace, messaging, media, and payments are applications of the protocol. They are not how the protocol is discovered.

## First experiment

One thin slice, then the same slice in other domains:

1. A peer publishes a situation.
2. Another peer publishes an offer that references it.
3. The first peer discovers and evaluates the offer.
4. Both peers exchange signed records.
5. The interaction ends in completion, cancellation, or dispute.
6. The simulator checks that every step was representable without application-specific code.

Motivating situation: a roof repair. The customer requests repair and attaches photographs. Two roofers offer different prices and schedules. One offer expires before a response. The customer accepts the other. The work is completed, and the customer disputes the invoice. The model has to keep each peer's claims.

Repeat the same sequence for a ride, a rental, a freelance job, a delivery, and an equipment loan. A concept added for the roof is re-run against the others before it is kept.

That is the first milestone: a working laboratory, built from proven components where the license and the model allow it, without committing the protocol to Notention's architecture.

## What will not be added early

- A unified super-app, before step 5
- A required relay, indexer, or hosted agent
- Token gates, admin roles, or permits
- A native token, or a fee taken by the protocol
- Domain skills hard-coded as classes
- A second status document that can drift from this one

Until `ontology-v0.1.md` exists, this README is the only plan.

## Layout

Nothing below exists yet. Step 1 creates the first two.

```text
ontology-v0.1.md     conceptual model
registry/            machine-readable concepts and relationships
scenarios/           situation fixtures and their expected readings
```

Adapters, a kernel, and a simulator come in steps 2 and 3. They are not sketched here in advance.

## License

[GNU Affero General Public License v3.0](LICENSE) only.

Notention code is not included. It stays out until that project ships a license file and the terms are compatible with this one.

## Sources

- This plan: the rebuild sequence for using Notention as a MonkeyBusiness workbench, consolidated on 2026-10-27. [Conversation](https://chatgpt.com/share/6ae07b3d-ade4-83e9-a062-1fc430688791).
- Upstream reviewed: [autonull/notention9](https://github.com/autonull/notention9) `47075c86`.
- Public commitments used as the conflict check: [MonkeyBusiness.systems](https://monkeybusiness.systems/).
