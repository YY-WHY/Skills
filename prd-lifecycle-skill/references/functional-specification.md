# Functional Specification Mode

Use this mode when the deliverable must explain how a product behaves across workspaces, roles, permissions, states, and cross-role workflows. It is appropriate for a developer-facing FSD, a design/QA functional baseline, or a readable feature specification derived from a PRD. It is not a substitute for product strategy, release metrics, or technical architecture.

## Functional differences from a PRD

| PRD | Functional Specification |
|---|---|
| Why the product exists, who it serves, desired outcomes, scope, priorities, metrics, and release decisions | What the user sees, can do, cannot do, what the system reads/writes, how state changes, and how the result is verified |
| Product-level requirements and user stories | Workspace, role, object, action, state, permission, failure, recovery, and acceptance behavior |
| Release boundary and business decisions | Operational boundary and functional layout |
| May link to a companion specification | Links back to the source PRD and exposes unresolved product decisions |

Keep the relationship explicit: derive from a named source and expose gaps or contradictions. Do not invent product decisions to make the layout look complete.

## Reader order and layout

Use this order unless an established source has a clearer structure:

1. Document positioning: product, version, audience, purpose, MVP/release boundary, source documents, evidence legend, and implementation-status legend.
2. Shared principles and system-wide rules: identity, permission-before-retrieval, raw-input preservation, confirmation gates, auditability, correction/versioning, idempotency, and AI boundaries when applicable.
3. Functional structure overview: primary workspaces, supporting/admin workspaces, the problem each workspace solves, and the capabilities covered. Treat workspaces as views over shared business data, not automatically as separate data modules.
4. Core business objects and relationships: subject, object, organization, membership, ownership, source, status, effective time, history, and allowed actions.
5. Role model and data scope: separate user subject, business position, system/admin role, organization relationship, field sensitivity, and current context. Include permission calculation dimensions.
6. Role/workspace behavior: organize by workspace and role. For each area state purpose, core capabilities, inputs/outputs, state/rules, permissions, exceptions, and cross-role impact. Reuse common capability definitions and document only role deltas where behavior is shared.
7. System roles and control surfaces: administration, organization, permissions, temporary authorization, workflow configuration, notifications, operations, failed work, audit, and service ownership boundaries.
8. Cross-cutting AI, knowledge/resource, simulation, and test surfaces when in scope. Keep simulated/test records separate from formal business records.
9. End-to-end scenarios: named scenarios that prove handoffs across roles, objects, permissions, statuses, notifications, and audit history.
10. State and result requirements: shared state vocabulary, operation-result vocabulary, timeline/source requirements, retry behavior, and recovery behavior.
11. Privacy, access, and audit requirements.
12. Current implementation/demo correspondence: map displayed pages and interactions to the specification and label every capability as verified production, observed implementation, simulated/demo, planned, or unresolved.

The structure is intentionally different from a conventional PRD. A role list, page list, or navigation sitemap alone is not a Functional Specification.

## Feature contract

Every substantial feature or workspace capability should be expressible with this contract:

```markdown
### <ID> <Feature name>

- Purpose: <user or operational outcome>
- Scope / actor: <role, workspace, object, organization range>
- Inputs: <user input, source objects, prerequisites>
- Core behavior: <observable normal flow>
- Outputs: <screen result, created/updated object, notification, next task>
- States and rules: <allowed states, transitions, invariants, effective dates>
- Permission boundary: <view, sensitive field, create, submit, approve, publish, export, retry>
- Exceptions and recovery: <missing data, ambiguity, denial, duplicate, failure, manual takeover>
- Cross-role impact: <who receives what, handoff, disclosure, follow-up>
- Source / evidence: <PRD, flow, UI, policy, or decision; evidence class>
- Acceptance: <observable checks>
```

Use stable IDs for features, objects, states, scenarios, and acceptance criteria when the document will be maintained. A table may summarize a feature, but behavior affecting permission, state, data, or recovery must remain readable without a screenshot.

## Role and workspace modeling

Build a capability matrix before writing repeated role sections:

| Capability | Workspace | Object | Actor / position | Data scope | Allowed actions | Sensitive fields | State constraints | Role delta |
|---|---|---|---|---|---|---|---|---|
| <capability> | <workspace> | <object> | <role> | <scope> | <actions> | <fields> | <rules> | <difference from shared behavior> |

Then write reader-facing role sections. Use the matrix to prevent contradictions such as granting access solely because of a broad system role. State effective-date behavior for membership, assignment, temporary authorization, transfer, expiry, and revocation.

## Cross-role scenarios

Select scenarios that demonstrate a complete business loop, not isolated screens. Each scenario identifies:

- starting actor, current identity/context, and source object;
- ordered actions and responsible role at each handoff;
- permission checks and confirmation points;
- created or changed records, notifications, and audit events;
- success, partial completion, failure, retry, and manual takeover;
- final visible result for each affected role.

Prefer scenarios that expose functional differences such as record-first capture, approval before publication, temporary authorization, relationship changes with task handover, or AI draft versus confirmed action.

## Shared states and operation results

Define common states once, then add domain-specific states only where necessary. Distinguish at least draft, awaiting confirmation, awaiting submission, awaiting approval, needs more information, in progress, waiting for response, awaiting review, published, completed, cancelled, rejected, revoked, expired, failed, paused, and partially completed when the product uses them.

Every user-visible operation must resolve to an explicit result such as success, awaiting confirmation, needs more information, no permission, object not found, insufficient source, workflow conflict, failed, or partially completed. A success toast is not evidence of a business state change. Retries preserve the original task/idempotency identity and show attempt history.

## AI and simulated surfaces

When AI is included, specify trigger, current user context, permitted capability calls, source/grounding, uncertainty, clarification, confirmation, failure, and human takeover. AI operates only within the current user's effective interface permissions. Keep original input, AI draft, confirmed content, and formal record separate.

When simulators or test tools are included, define identity/data reset behavior, fixture scope, time and failure controls, output records, and the boundary preventing test results from entering formal business records.

## Evidence and implementation boundary

For every mapped page, interaction, backend capability, or integration, use one of these labels:

- `Verified production`: runtime and acceptance evidence checked.
- `Observed implementation`: visible or executable implementation observed, acceptance or backend completeness not fully checked.
- `Simulated/demo`: interaction or data is intentionally simulated.
- `Planned`: specified but not observed.
- `Unresolved`: source conflict or missing decision prevents classification.

Never infer backend authorization, persistence, notifications, AI grounding, external-account integration, or production recovery from a static page. Record the gap in an implementation correspondence table:

| Surface / capability | Spec location | Current evidence | Status label | Missing verification or decision |
|---|---|---|---|---|
| <surface> | <section/ID> | <observed source> | <label> | <gap> |

## Completion review

Before delivery, verify:

- shared principles, objects, roles, workspaces, and permission dimensions are defined before role-specific behavior;
- every substantial feature has purpose, input, output, state/rules, permission, exception/recovery, cross-role impact, source, and acceptance;
- repeated role views are consistent and role deltas are explicit;
- cross-role scenarios cover handoff, disclosure, confirmation, failure, retry, and audit where applicable;
- global states and operation results match feature-level rules;
- AI, simulator, and test surfaces have separate data and authorization boundaries;
- current implementation/demo evidence is labeled without overstating production capability;
- source PRD, unresolved decisions, companion technical documents, and change summary are linked.

This review supplements `scripts/prd_validate.py --strict`; it does not replace PRD validation when a PRD is also delivered.
