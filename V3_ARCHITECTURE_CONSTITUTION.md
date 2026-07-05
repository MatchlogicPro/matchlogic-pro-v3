# V3 Architecture Constitution

## Preamble

This document is the supreme governance authority for MatchLogic Pro V3. It supersedes all informal direction, implementation assumptions, and prior-version practices except where explicit amendments are recorded here through the approved review process.

---

## 1. Purpose and Scope

This constitution defines the non-negotiable architectural laws, truth ownership boundaries, build gates, and governance process for MatchLogic Pro V3. It governs what may be built, in what order, and under what constraints. Detailed specifications, API contracts, data schemas, and implementation plans are subordinate to this document and must be created separately after constitutional approval.

---

## 2. Relationship to V2

MatchLogic Pro V2 is frozen and read-only. V2 exists as evidence and domain reference only. V3 is a clean implementation. No V2 source files, SQL migrations, or application code may be copied, ported, or imported into V3. V2 may be inspected to inform invariant documentation and fresh reimplementation only after explicit approval of the specific invariant being preserved.

---

## 3. Definitions

| Term | Definition |
|------|------------|
| **SALVAGE** | Preserve approved concepts, domain rules, and invariants — not source files. |
| **Canonical truth** | Authoritative state owned by a designated truth owner; the single source of record for a domain. |
| **Derived model** | Rebuildable projection or analytical output computed from canonical truth; never authoritative for match outcomes. |
| **Domain event** | A governed record of a meaningful state change, expressed in platform-agnostic terms. |
| **Truth owner** | The subsystem designated as the sole authoritative source for a class of domain truth. |
| **Entitlement** | Upstream subscription or account-level grant that governs what a user may access. |
| **Capability** | Downstream server-side functional permission evaluated after identity and entitlement validation. |
| **Independently rebuildable** | A derived system that can be destroyed and fully reconstructed from canonical truth without manual repair or hidden coupling. |
| **Proof gate** | A formal verification checkpoint that must pass before downstream work may proceed. |

---

## 4. SALVAGE Policy

SALVAGE means preserving approved concepts, domain rules, and invariants discovered through V2 evidence and independent review. SALVAGE does not mean copying V2 source files, migrations, folder structures, or implementations. Proven V2 invariants may be documented and reimplemented fresh in V3 only after explicit approval of the specific invariant. REFACTOR and REPLACE decisions are recorded separately when invariants are rejected or superseded.

---

## 5. Central Laws of System Invariant Architecture

All V3 systems must obey the following non-negotiable laws.

### 5.1 Analytics Law

**Canonical Match Truth → Domain Events → Independently Rebuildable Derived Models**

The canonical match ledger owns match truth. Stats, ratings, partner chemistry, leaderboards, team records, and all other analytical outputs are derived. They do not own match truth. Every derived data system must be independently rebuildable from canonical truth.

### 5.2 Access Control Law

**Validated Identity Profile → Upstream Subscription Entitlements → Downstream Server-Side Functional Capabilities**

Access control flows in one direction. Identity must be validated before entitlements are evaluated. Entitlements must be resolved before server-side capabilities are granted. Client-side capability hints are permitted for user experience only and are never sole enforcement.

---

## 6. Domain Truth Ownership Map

Each subsystem owns truth only within its assigned domain. No subsystem may claim authority over truth owned by another.

### 6.1 Identity Domain

Owns user accounts, root profile metadata, and player identity linkage records. It does not own competitive match records, payment parameters, or active permission logic.

### 6.2 Entitlements Domain

Owns application access grants, including effective tier, capability allowances, and feature flags. It derives its records from approved entitlement sources including the Billing mirror, explicit Founder overrides, lifetime exemptions, or approved enterprise grants, but does not own raw upstream payment transactions.

### 6.3 Billing Domain

Owns payment-provider interaction events, incoming webhook logs, billing cycles, ledger transactions, and the internal billing subscription mirror state. It informs the downstream Entitlements Domain but does not manage application-level capability logic, profiles, or match data.

### 6.4 Match Engine

Owns the canonical match ledger as the sole source of competitive match truth. All match outcomes enter the system through governed Match Engine flows.

### 6.5 Tennis IQ

Owns educational truth: question bank, quiz sessions, user answers, learning progress, and knowledge gaps. Educational truth is separate from match-derived analytics and is not subordinate to the match ledger.

### 6.6 Teams / Captain Operational Truth

Owns team structure, roster membership, fixture scheduling, lineup assignments, and captain workflow state. Does not own canonical match outcomes or derived player analytics.

### 6.7 Derived Analytics

Owns rebuildable projections only: stats, ratings, partner chemistry, leaderboards, team records, and other analytical outputs derived from canonical match truth. Derived analytics never own match truth and must remain independently rebuildable.

---

## 7. Core Foundational Invariants

### 7.1 Foundation and Architecture Governance

Architectural decisions are proposed, independently reviewed, approved, and recorded before implementation begins. No implementation work may proceed on assumptions not yet approved through governance.

### 7.2 Technology Stack Decision Status

The V3 technology stack is not yet approved. No stack selection, framework choice, or infrastructure assumption may be treated as decided. Implementation must not proceed on unapproved technology choices.

### 7.3 Shared API and Data Contract Decision Status

Shared API and data contracts are a required early decision domain. Contracts must be defined and approved before dependent systems are built. V2 API shapes may inform discussion but may not be assumed or ported.

### 7.4 Identity and Player Domain

Identity and player domains are foundational. They must be designed and approved before the Match Engine is built. A validated identity profile is a prerequisite for all downstream access control and match attribution.

### 7.5 Permission and Entitlement Domain

Permission and entitlement architecture must be designed and approved before the Match Engine is built. Server-side capability evaluation is the authoritative enforcement layer for all protected operations.

---

## 8. Core Transactional Ledger Engine

### 8.1 Canonical Match Ledger

The canonical match ledger is the only authoritative owner of competitive match truth. All governed match ingestion, logging, correction, and supersession flows must pass through the Match Engine. No downstream system may write, mutate, or assert match outcomes outside this ledger.

### 8.2 Domain Events

Domain events are the governed record of meaningful state changes across truth owners. Events are expressed in platform-agnostic terms. This constitution does not assume queues, webhooks, pub/sub, edge functions, background jobs, or any specific delivery infrastructure. The event model defines what happened and what truth changed; transport and processing mechanisms are separate decisions.

### 8.3 Deterministic Stats and Rebuild Proof Gate

The deterministic Stats Engine is the first major derived system. It must produce identical outputs from identical canonical inputs. Before ratings, partner chemistry, Captain Core, AI Coach, or other downstream analytical or application systems may proceed, V3 must demonstrate a destroy / rebuild / reconcile proof: derived stats can be destroyed, rebuilt from canonical match truth, and reconciled to within defined tolerance with zero unexplained divergence.

---

## 9. Downstream Application & Extension Ecosystems

The following systems are built on proven foundations and must respect truth ownership boundaries and build gates defined in Section 10.

### 9.1 Ratings and Partner Chemistry

Ratings and partner chemistry are derived analytical systems. They are blocked until the deterministic Stats proof gate passes. They must remain independently rebuildable from canonical match truth.

### 9.2 Core Web Experience

The core web experience is the primary user-facing surface for foundational and transactional domains. It is built after identity, permission, Match Engine, and initial derived proof gates are established. It consumes approved shared contracts and does not define them.

### 9.3 Billing Integration

Billing connects payment-provider state to entitlement records. Billing integration must align with the Identity & Entitlements and Billing truth ownership boundaries. Billing does not own match truth or derived analytics.

### 9.4 Captain Core and Competition Intelligence

Captain Core covers team management, roster operations, fixture scheduling, and captain workflows. Competition rules and lineup intelligence are governed extensions built on proven stats and canonical match truth. Captain operational truth is owned separately from match outcomes and derived analytics. Captain Core is blocked until the deterministic Stats proof gate passes.

### 9.5 Unified AI Architecture

V3 defines a single governed AI architecture layer for AI-powered features. All AI integrations must use this layer rather than ad hoc provider-specific implementations embedded in individual features. The unified AI architecture is an extension mechanism, not a truth owner.

### 9.6 AI Coach

AI Coach is a governed analytical feature that provides coaching insights derived from player data. It is blocked until the deterministic Stats proof gate passes. AI Coach consumes derived analytics and may utilize the unified AI architecture; it does not own match truth or educational truth.

### 9.7 Tennis IQ — Launch Requirement

Establishes Tennis IQ as a required launch system with its own authoritative educational truth domain. It is an independent system that may utilize the unified AI architecture for enhanced features, but it is not structurally subordinate to it; its core educational, testing, and progress functions must remain fully valid and operational independently of AI-provider availability.

### 9.8 Screenshot Import

Screenshot import is a governed ingestion pathway. It must produce canonical match truth through approved Match Engine domain flows. Import pipelines do not bypass the ledger, permission checks, or entitlement gates.

### 9.9 Mobile Positioning

Mobile is out of scope until V3 shared contracts stabilize. Mobile must consume approved API and data contracts. Mobile does not define contracts and is not built until foundational and launch-scope web systems are governed and stable.

---

## 10. Launch Scope and Build Gates

### 10.1 Reconciled Dependency Order

V3 is built in the following order. Steps may not be reordered without constitutional amendment.

1. Foundation and architecture governance
2. Technology stack decision
3. Shared API/data contract decision
4. Identity + Player domain
5. Permission + Entitlement domain
6. Canonical Match Engine
7. Domain Event architecture
8. Deterministic Stats Engine
9. Destroy / rebuild / reconcile proof gate
10. Ratings + Partner Chemistry
11. Core web experience
12. Billing
13. Captain Core
14. Competition Rules + Lineup Intelligence
15. Unified AI architecture
16. AI Coach
17. Tennis IQ — required for launch
18. Screenshot Import
19. Remaining governed launch systems
20. Mobile — only after V3 contracts stabilize

### 10.2 Strict Gates

The following gates are non-bypassable:

- Identity is built before the Match Engine.
- Permission and Entitlement architecture is built before the Match Engine.
- Ratings and Partner Chemistry are blocked until deterministic Stats proof passes.
- Captain Core is blocked until deterministic Stats proof passes.
- AI Coach is blocked until deterministic Stats proof passes.
- Tennis IQ is required for launch and may not be classified as post-launch.
- No V2 SQL migration may be copied into V3.
- No V2 source file may be directly ported into V3.
- Proven V2 invariants may be documented and reimplemented fresh after explicit approval.
- The V3 technology stack is not yet approved.

### 10.3 V2 Evidence Use Rules

V2 may be inspected read-only to extract evidence, domain rules, and invariants for independent review. Extracted invariants must be documented explicitly before reimplementation. Direct reuse of V2 files, migrations, source code, folder structures, or configurations is prohibited.

---

## 11. Review, Amendment, and Compliance Process

### 11.1 Roles and Governance Authority

- **Shaun Lackey (Founder and Product Owner):** Holds final absolute authority over product scope, feature inclusion or removal, intended feature behavior, launch requirements, pricing/tier configurations, and overall product experience. No feature or feature scope may be formally approved for implementation until Shaun explicitly confirms the feature and its intended behavior. Product-scope constitutional amendments require Shaun's explicit written approval.

- **ChatGPT and Gemini (Independent Architecture & Product Reviewers):** Act as independent analytical reviewers. They assess architecture models, evaluate code viability, identify product and technical regression risks, and verify compliance with this Constitution. AI reviewer reconciliation cannot change approved product scope, release tiers, or launch requirements without Shaun's explicit approval.

- **Cursor (Implementation Engineer / Technical Evidence Collector):** Functions strictly as an implementation engineer and technical evidence collector. Cursor operates inside read-only boundaries for historical code and implements approved technical decisions within the greenfield V3 repository as explicitly directed by the reconciled, human-approved architecture pipeline.

### 11.2 Documentation Hierarchy

This constitution is the root authority. Subordinate documents, in order:

1. V3 Architecture Constitution (this document)
2. Approved architectural decision records (ADRs)
3. Domain specifications
4. API and data contract specifications
5. Implementation plans and runbooks

When documents conflict, this constitution prevails unless formally amended.

### 11.3 Amendment Process

Amendments to this constitution require independent review by ChatGPT and Gemini and explicit reconciliation before taking effect. Amendments are recorded with date, rationale, and approving reviewers. Implementation in progress that violates an amendment must stop until realigned.

### 11.4 Compliance and Enforcement

All proposed V3 work is checked against the Central Laws, Domain Truth Ownership Map, and Strict Gates before implementation begins. Work that violates central laws, claims truth outside its domain, bypasses build gates, or assumes unapproved technology or contracts must not proceed. Compliance failures are resolved through governance review, not silent implementation workarounds.

---

*MatchLogic Pro V3 — Architecture Constitution*
