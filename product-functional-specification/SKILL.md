---
name: product-functional-specification
description: Apply the Di-Edu v1.1 product contract when explaining, designing, reviewing, or updating Di-Edu portal modules, permissions, Console and Backend capabilities, workflows, data boundaries, and AI-native behavior. Use only for Di-Edu product work, not for unrelated education products or generic UI design.
---

# Product Functional Specification

Use this Skill to keep Di-Edu product decisions consistent with the approved Functional Specification while allowing the user to revise that baseline explicitly.

## Authoritative reference

The product baseline is [references/Di-Edu-Functional-Specification-Role-Modules-v1.1.md](references/Di-Edu-Functional-Specification-Role-Modules-v1.1.md).

- For any Di-Edu task, first read `0 共同原则` and `功能结构总览`.
- For a request limited to one portal, role, module, Console area, or Backend capability, also read the matching section before answering or editing.
- For cross-role design, permission changes, topology changes, or a full-document audit, read the complete reference.
- Treat the reference as the current product baseline. A direct user decision may revise it; identify the affected rules and downstream sections instead of silently forcing the old wording.
- Preserve the reference snapshot unless the user explicitly asks to update the Skill baseline. Create a new versioned reference when a revision changes product meaning.

The bundled reference is an exact copy of `Di-Edu-Functional-Specification-Role-Modules-v1.1.md`, SHA-256 `c53fc84779096452bc7b6527bbd0784025914003a22d740c252d0d5f95fd571f`.

## Select the working mode

Choose the smallest mode that satisfies the request:

1. **Explain**: answer from the reference and distinguish confirmed rules from interpretation.
2. **Design**: derive a new function or workflow without contradicting the product model.
3. **Audit**: identify omissions, duplication, contradictions, ambiguous ownership, permission leaks, broken states, or incomplete business loops. Do not edit unless requested.
4. **Update**: revise the specification while preserving unaffected structure, numbering, scope, and language. State material changes and unresolved decisions.

## Product invariants

Apply these rules whenever relevant:

- Portal identity, position, system role, and organizational affiliation are separate dimensions.
- Student, parent, and Staff portals remain independent. Staff job views share one Staff Portal and vary by effective position and affiliation.
- Class, Team/Club, Department, grade, and Campus relationships determine both visibility and executable scope. One person may hold several active relationships.
- System roles govern Console administration. They do not replace portal positions or real organizational relationships.
- Console is the human-facing administration and operations surface. Backend is the service and data layer that enforces identity, permission, rules, workflow, AI calls, notifications, audit, and recovery.
- A student may be a managed record without owning a login account.
- Permission checks happen before retrieval, comparison, export, AI processing, or write operations.
- AI inherits the initiating user's exact permissions. It may increase production capacity but cannot widen visibility, bypass confirmation, or gain independent override authority.
- AI actions are never silent. Low-risk actions may appear only in status, history, or activity records, but every action remains traceable.
- Source records, attachments, and original facts are retained before classification, generation, approval, or formal write-back. Generated conclusions cannot replace source facts.
- Workflow steps are configurable by organization and context. Every active step has an owner, status, deadline when applicable, and result.
- A state changes only after the corresponding business result exists. Preserve distinctions such as draft, pending confirmation, pending approval, submitted, partially completed, failed, closed, and needs resubmission.
- The reference is a complete product capability library, not an MVP selection. Do not label functions as MVP unless the user explicitly defines the MVP scope.

## Functional specification method

When defining or revising a function, cover the details needed for implementation without prescribing visual layout:

1. **Purpose and necessity**: what problem the function solves and why the target user needs it.
2. **Users and scope**: eligible portal, position, system role, affiliation, and object range.
3. **Core information or inputs**: records, files, relationships, dates, statuses, sources, and required fields.
4. **User capabilities**: what the user can view, create, submit, approve, communicate, compare, configure, or delegate.
5. **Outputs and state changes**: persisted results, notifications, reports, assignments, audit records, and truthful status transitions.
6. **Business rules and exceptions**: permission checks, ownership, deadlines, conflicts, missing data, failure, partial completion, withdrawal, and recovery.
7. **AI contribution**: retrieval, classification, drafting, suggestions, anomaly detection, workflow acceleration, source links, confirmation points, and stopping conditions.
8. **Console and Backend support**: include these only where configuration, enforcement, integration, orchestration, audit, or operational control is required.

Keep each section concise but complete enough that an experienced developer can identify actors, data, actions, states, permissions, failure behavior, and acceptance boundaries.

## Structure and writing rules

- Preserve the approved hierarchy and numbering unless the user explicitly changes the topology.
- Organize portal functions by the user's relationship space, moving from personal scope toward class, team, grade, department, and Campus scope.
- Keep secondary and tertiary modules coherent; merge duplicated capabilities and describe the authoritative location plus any cross-module entry or result.
- Do not design navigation placement, buttons, sidebars, dialogs, screen coordinates, or component implementations unless the user asks for UI design.
- Avoid unnecessary implementation names and technology choices. Include a technology only when it changes a functional requirement or acceptance boundary.
- Write clear, natural Chinese. Retain established product terms such as Portal, Console, Backend, AI, Class, Team/Club, Department, and Campus when they carry defined meanings.
- Separate confirmed requirements, proposed additions, assumptions, and unresolved decisions. Do not present an inference as an approved rule.

## Consistency check

Before delivering substantial Di-Edu work, verify:

- The requested module exists in the correct portal or administration layer.
- Position, role, and affiliation are not conflated.
- Object visibility and executable scope are both defined.
- AI sees and acts only within the initiating user's authority.
- Every multi-step process has explicit ownership and truthful states.
- Console controls and Backend enforcement are distinguished.
- Cross-role effects, notifications, audit evidence, and failure paths form a complete loop.
- Unaffected requirements and the reference topology remain unchanged.

Do not publish, push, merge, or replace a baseline document merely because this Skill was invoked; perform external mutations only when the user requests them.
