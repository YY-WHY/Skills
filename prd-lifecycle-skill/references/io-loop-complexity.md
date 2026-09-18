# IO Loop Complexity Layers

Use this reference when a PRD contains one or more user/system entry points whose processing path changes with the requested output. The model is derived from the TopoGrow IO Flow pattern: classify within each entry point, then expand the ordered loop for that entry-and-layer combination.

## Three-level model

Classify by the output the user expects, then use data, reasoning, orchestration, latency, and persistence as supporting signals.

| Layer | Canonical name | Output boundary | Typical supporting signals |
|---|---|---|---|
| `L1` | Immediate Result | A direct answer, retrieval result, acknowledgement, extraction, classification, or stored record; no contextual insight or standalone artifact | One request or file; little/no history; short synchronous path |
| `L2` | Contextual Insight | An interpreted answer or insight shown in the interaction; no standalone report, plan, or downloadable artifact | History or multiple records; comparison, trend, pattern, or personalized analysis |
| `L3` | Orchestrated Artifact | A structured report, plan, recommendation package, export, or other durable artifact | Multi-source reasoning; planning/orchestration; long-running or queued work; archive/versioning may apply |

Legacy source labels such as Type A/B/C may be retained as aliases (`A → L1`, `B → L2`, `C → L3`) only when the source supports that mapping. Use the canonical `L1/L2/L3` IDs in new output so the layer communicates output complexity rather than an unexplained letter.

### Classification precedence

1. The requested output is the primary classifier.
2. A single file can still be `L3` when the requested output is a substantial plan or report.
3. Multiple sources do not automatically make a request `L3`; if the result is an in-context insight without an artifact, use `L2`.
4. Slow execution alone does not determine the layer. Record latency or queueing separately.
5. Recording or archiving without analysis remains `L1`, even when extraction and validation contain several technical steps.
6. When one request asks for several outputs, route to the highest required layer or split it into independently traceable loops when the outputs can complete separately.

## Required hierarchy

Model the flow in this order:

```text
Entry Point (EP-*)
  └─ Output Complexity Layer (L1 / L2 / L3)
       └─ Ordered Loop (LOOP-<EP>-L*)
            ├─ synchronous main path
            └─ supported asynchronous side effects
```

Do not define one global L1/L2/L3 loop and reuse it across every entry point. The layer meaning is shared; the service path is entry-specific. A text request may begin with interpretation and retrieval, while a file request may begin with upload validation and content extraction.

## Required PRD representation

Create an IO Loop Matrix under the User Journey section.

| Loop ID | Entry ID | Entry Point | Layer | Output | Decision Rule | Main Path | Side Effects | Evidence Class |
|---|---|---|---|---|---|---|---|---|
| LOOP-EP-01-L1 | EP-01 | Main interaction | L1 | Direct answer | No contextual analysis or artifact | Input → Route → Execute → Verify → Output | Persist interaction | `[确认]` |

Rules:

- Give every entry point a stable `EP-*` ID and every represented path a stable `LOOP-<EP>-L*` ID.
- Include only layers that the source or product scope supports. Do not manufacture all three for symmetry.
- Write a positive, routing-grade decision rule. Avoid labels such as “simple” or “complex” without an output boundary.
- Keep the main path ordered. Name product/service responsibilities when known; use capability labels rather than invented service names when implementation is not established.
- When normalizing an existing IO Flow, retain its node order verbatim unless the user explicitly authorizes a redesign. If persistence or archive placement looks questionable, record the issue as a decision instead of silently moving the node.
- Show database writes, queues, notifications, analytics, archives, and other side effects separately when they are not required before the user receives the result.
- Mark each row `[确认]`, `[推断]`, `[建议]`, or `待决策 Q-*`. Source-backed flow intent is not proof of implementation.
- Link each loop to its governing `UC-*`, `FR-*`, `AC-*`, dependencies, and relevant `NFR-*` in the detailed subsection or traceability table.

## Detailed loop expansion

For each matrix row, add a short subsection when the main path, branches, or verification cannot be understood from the table alone:

```markdown
#### LOOP-EP-01-L2 — Main interaction / Contextual Insight

- Entry / trigger: ...
- Expected output: ...
- Classification rule: ...
- Main path: Input → Interpret → Retrieve context → Analyze → Verify → Present insight
- Async side effects: Persist interaction; refresh derived index
- Failure / recovery: ...
- Maps to: UC-CORE-002; FR-CORE-002; AC-CORE-006; NFR-PERF-002
- Evidence class / implementation status: `[确认]`; delivery status tracked separately
```

The Loop is a product behavior contract. Technical implementation details belong in a companion specification when they make the PRD difficult to scan.

## TopoGrow pattern captured by this model

The source demonstrates why the Loop must stay entry-specific even when both entries use A/B/C.

| Source path | New layer | Source-ordered Loop |
|---|---|---|
| Text Type A | `L1` | IR Service → Task Distribution Service → Execution Service → Verification Service → Output → Database Update |
| Text Type B | `L2` | IR Service → Pre-Analysis → Task Distribution Service → Execution Service → Database → Data Cleaning & Structuring → Analysis / Insight Generation → Verification Service → Output → Database Update |
| Text Type C | `L3` | IR Service → Pre-Analysis → Task Planning Service → Execution Service → Database → Data Cleaning & Structuring → Multi-Source Analysis / Insight Generation → Artifact Generation Service → Verification Service → Output → Archive Service → Database Update |
| File Type A | `L1` | File Upload → File Validation Service → Content Extraction Service → Classification Service → Memory Atom Generation → Verification Service → Evidence Storage Service → Output → Database Update |
| File Type B | `L2` | File Upload → File Validation Service → Content Extraction Service → Classification Service → Context Retrieval Service → Task Distribution Service → Execution Service → Database → Data Cleaning & Structuring → Cross-Source Analysis → Insight Generation → Verification Service → Output → Database Update |
| File Type C | `L3` | File Upload → File Validation Service → Content Extraction Service → Knowledge Structuring Service → Context Retrieval Service → Task Planning Service → Workflow Orchestration Service → Execution Service → Database → Multi-Source Analysis → Artifact Generation Service → Verification Service → Archive Service → Output → Database Update |

TopoGrow Entry 03 (Structured Form) supplies only a location. Its function, classification, examples, and Loop remain unresolved and must not be generated as confirmed content.

These are reference patterns, not universal service chains. Preserve the source's actual node order and label unsupported nodes as decisions instead of silently adding them.
