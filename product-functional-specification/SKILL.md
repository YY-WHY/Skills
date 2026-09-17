---
name: product-functional-specification
description: Apply the Di-Edu MVP V2.0 product contract when explaining, designing, reviewing, or updating Di-Edu workspaces, roles, permissions, workflows, data boundaries, Console and Backend capabilities, and AI-native behavior. Use only for Di-Edu product work, not for unrelated education products or generic UI design.
---

# Product Functional Specification

Use this Skill to keep Di-Edu MVP product decisions consistent with the approved V2.0 Functional Specification while allowing the user to revise that baseline explicitly.

## Authoritative reference

The current product baseline is [references/Di-Edu-Functional-Specification-V2.0-Four-Zone.md](references/Di-Edu-Functional-Specification-V2.0-Four-Zone.md). The bundled V1.1 role-module document remains a historical compatibility reference.

- For any Di-Edu task, first read `文档定位`, `共同原则`, `功能结构总览`, `核心业务对象`, and `角色层次与用户范围`.
- For a request limited to one portal, role, module, Console area, or Backend capability, also read the matching section before answering or editing.
- For cross-role design, four-zone topology changes, permission changes, MVP scope changes, or a full-document audit, read the complete V2.0 reference.
- Treat V2.0 as the current MVP product baseline. A direct user decision may revise it; identify the affected rules, role views, coverage matrix, unresolved requirements, and downstream sections instead of silently forcing the old wording.
- Preserve the V1.1 reference as historical evidence. Create a new versioned reference when a later revision changes product meaning; do not overwrite an earlier baseline without explicit instruction.

The bundled V2.0 reference is an exact copy of the Di-Edu MVP V2.0 source document, SHA-256 `fe7e4a63393e7490abddbe2788b124424219b72a21ca948fc745b661c537cc25`.

## Select the working mode

Choose the smallest mode that satisfies the request:

1. **Explain**: answer from the reference and distinguish confirmed rules from interpretation.
2. **Design**: derive a new function or workflow without contradicting the product model.
3. **Audit**: identify omissions, duplication, contradictions, ambiguous ownership, permission leaks, broken states, or incomplete business loops. Do not edit unless requested.
4. **Update**: revise the specification while preserving unaffected structure, numbering, scope, and language. State material changes and unresolved decisions.

## Product invariants

Apply these rules whenever relevant:

- Portal identity, position, system role, and organizational affiliation are separate dimensions.
- The four primary work zones are `今日动态`, `我的任务`, `沟通协作`, and `我的集体`; they are work views over shared business objects, not duplicated module databases.
- AI助手 is a cross-zone natural-language entry point and an independent working surface. It inherits the initiating user's exact permissions and pauses at confirmation points for high-impact actions.
- Student, parent, and Staff user subjects remain distinct. Staff work views vary by effective position and affiliation; a user may hold multiple active user subjects, positions, system roles, and organizational relationships.
- Positions include student, teacher, supervisor, principal, and vice-principal. System or management roles include academic/school administration, administration, HR/personnel, facilities, IT, attendance, super administrator, and configurable roles. Do not conflate position with system role.
- School, campus, stage, grade, Department, Class, course, and Team/Club relationships determine both visibility and executable scope. One person may hold several active relationships, each with effective dates and provenance.
- System roles govern Console administration. They do not replace portal positions or real organizational relationships. IT access to runtime metadata does not imply access to sensitive student records.
- Console is the human-facing administration and operations surface. Backend is the service and data layer that enforces identity, permission, rules, workflow, AI calls, notifications, audit, and recovery.
- A student may be a managed record without owning a login account.
- Permission checks happen before retrieval, comparison, export, AI processing, or write operations.
- AI inherits the initiating user's exact permissions. It may increase production capacity but cannot widen visibility, bypass confirmation, or gain independent override authority.
- AI actions are never silent. Low-risk actions may appear only in status, history, or activity records, but every action remains traceable.
- Source records, attachments, and original facts are retained before classification, generation, approval, or formal write-back. Generated conclusions cannot replace source facts.
- Workflow steps are configurable by organization and context. Every active step has an owner, status, deadline when applicable, and result.
- A state changes only after the corresponding business result exists. Preserve distinctions such as draft, pending confirmation, pending approval, submitted, partially completed, failed, closed, and needs resubmission.
- User settings include language, time zone, date format, notification and privacy preferences, default identity or organization, AI interaction preferences, and optional WeChat account association by confirmed QR-code flow. Association and unbinding are auditable.
- Initial development follows a microservice-oriented boundary model across identity/relationships, permissions, organization objects, teaching records, tasks/approvals, communication/notifications, files/knowledge, AI orchestration, audit, and data simulation. Deployment may temporarily combine services without collapsing ownership or authorization boundaries.
- Reserve file-object, directory-mapping, inherited-permission, version, provenance, and write interfaces for later cloud-drive integration. MVP may simulate or defer the external service but must not block the future contract.
- V2.0 is the MVP-stage baseline: distinguish MVP-required business verification, MVP-simulated external or AI behavior, later extensions, and unresolved rules. Complete capability coverage does not mean every external production service is live.

## Functional specification method

When defining or revising a function, cover the details needed for implementation without prescribing visual layout:

1. **功能目的**: what problem the function solves and why the target user needs it.
2. **Users and scope**: user subject, Portal/workspace, position, system role, affiliation, and object range.
3. **核心能力**: the user-visible capabilities and supported objects.
4. **输入与输出**: records, files, relationships, dates, statuses, sources, required fields, and produced results.
5. **状态与规则**: truthful state transitions, ownership, deadlines, conflicts, missing data, failure, partial completion, withdrawal, recovery, and idempotent retry.
6. **权限边界**: summary/detail/sensitive-field visibility and executable actions, including temporary authorization and audit requirements.
7. **四区归属**: primary zone, cross-zone entry, authoritative record location, and downstream task or communication effect.
8. **AI contribution**: retrieval, classification, drafting, suggestions, anomaly detection, workflow acceleration, source links, confirmation points, and stopping conditions.
9. **Console and Backend support**: include configuration, enforcement, integration, orchestration, audit, recovery, and service ownership where required.

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
- The full V1.1 capability set is mapped to V2.0 zones or explicitly listed as unresolved; no original requirement is silently dropped.
- MVP-required, MVP-simulated, later-extension, and unresolved items are distinguishable.
- Unaffected requirements and the V2.0 topology remain unchanged.

Do not publish, push, merge, or replace a baseline document merely because this Skill was invoked; perform external mutations only when the user requests them.
