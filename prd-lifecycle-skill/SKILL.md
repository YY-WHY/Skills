---
name: prd-lifecycle
description: Convert product notes or incomplete PRDs into readable, traceable, versioned PRDs, or derive role-aware Functional Specifications with workspace behavior, permissions, states, cross-role flows, and acceptance evidence. Also update delivery progress, evidence, blockers, decisions, and release readiness. Do not use for technical design documents that contain no product requirements.
---

# PRD Lifecycle

Create and maintain a PRD that is easy for product, design, engineering, QA, and stakeholders to read while remaining a traceable source of truth.

## Route the request

- To create, normalize, or substantially review a PRD, read [references/function-1-normalize.md](references/function-1-normalize.md) and [references/prd-template.md](references/prd-template.md).
- To create or review a developer-, design-, or QA-readable Functional Specification, read [references/functional-specification.md](references/functional-specification.md). This is a separate behavior-and-layout mode; it does not replace the PRD.
- To apply progress, evidence, blocker, owner, or decision updates, read [references/function-2-track.md](references/function-2-track.md).
- When product definition and functional specification work are both requested, normalize the PRD first, then derive the Functional Specification from the approved or explicitly selected baseline.

Read every supplied source completely before classifying, modifying, or versioning it.

## Required product comprehension

1. Use the readable section order in the canonical template unless the user's established format is clearer.
2. Include both user stories (`US-*`) and use cases (`UC-*`) in every product PRD. Each P0 requirement must trace to at least one user story or use case and to explicit acceptance criteria.
3. When processing changes by entry point or expected output, read [references/io-loop-complexity.md](references/io-loop-complexity.md). Model `Entry Point → Output Complexity Layer → Ordered Loop`; never reuse one generic loop across unlike entries.
4. Keep user stories outcome-focused. Put preconditions, triggers, normal flow, alternatives, errors, permissions, retries, and recovery in use cases and requirement acceptance criteria.
5. Keep `Non-Goals` strategic and `Out of Scope` release-specific; do not duplicate the same list under both.

## Shared invariants

1. Preserve evidence boundaries:
   - `[确认]`: directly supported by supplied input or evidence.
   - `[推断]`: reasonably inferred but unconfirmed.
   - `[建议]`: newly proposed.
   - `待决策 Q-xxx`: a material missing decision.
2. Never promote `[推断]`, `[建议]`, or a missing value into a confirmed requirement, target, implementation state, or approval.
3. Separate requirement maturity from delivery progress:
   - Requirement: `Draft / In Review / Approved / Deferred`.
   - Delivery: `Not Started / In Progress / Blocked / Reported Complete / Verified`.
   - `In Review` requires evidence that review has started. `Accepted` and `Released` are release gates.
4. Record the basis for each delivery status. Observed implementation, owner report, CI evidence, QA verification, and production evidence are not interchangeable.
5. A completion report moves work to `Reported Complete`; only evidence checked against acceptance criteria moves it to `Verified`.
6. Use stable individual IDs. Never use a range such as `Q-001–Q-010` as a tracked row.
7. Keep stable action IDs (`A-*`) separate from their target requirement, risk, or decision ID.
8. Classify dependencies as `Hard`, `Soft`, or `Gate`; only unresolved `Hard` or `Gate` dependencies automatically block delivery.
9. Keep product priority separate from security severity.
10. Do not propagate secrets, credentials, maintenance keys, or unnecessary internal addresses.
11. Give non-functional requirements stable `NFR-*` IDs when they affect acceptance or release.
12. Split substantial API, schema, infrastructure, telemetry, deployment, or workflow mechanics into companion specifications.
13. Treat IO Loop layers as output-complexity classes: `L1 Immediate Result`, `L2 Contextual Insight`, and `L3 Orchestrated Artifact`. Preserve A/B/C only as source aliases when supported, and keep delivery status separate from flow design.
14. Keep document types explicit: a PRD defines product intent, scope, outcomes, and release decisions; a Functional Specification defines observable behavior, workspace information architecture, role differences, states, permissions, cross-role flows, and acceptance-ready feature contracts.
15. For role-heavy products, model user subject, business position, system role, organization relationship, and current context as separate dimensions. Do not collapse them into one role field.

## Validation and delivery

- For canonical Markdown, run `scripts/prd_validate.py --strict` before delivery. Correct errors rather than bypassing validation.
- For a Functional Specification, run the structural review in [references/functional-specification.md](references/functional-specification.md). The PRD validator is not proof that a Functional Specification is complete.
- For progress updates, prefer `scripts/prd_progress.py`; supply the expected document version or SHA when concurrent edits are possible, then validate the output.
- Deliver the versioned PRD, classification and change summary, unresolved decisions, validation result, and every linked companion document.

## Versioning

- Major: product goal, core scope, or role model changes.
- Minor: requirements, priority, business rules, dependencies, user stories/use cases, or acceptance criteria materially change.
- Patch: progress, owner, evidence, dates, or non-substantive wording changes.
- Do not create a version when there is no effective change. Do not reuse or decrease a version number.

If the user has no established output preference, ask once whether they want Markdown, Word, or both. Reuse that preference later.
