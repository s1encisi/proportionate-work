# Working Agreement (For AGENTS.md or CLAUDE.md)

Documentation language: English. See the [Chinese version](minimal-rules.md).

- Match verification depth to the scope of the change: distinguish text, local, cross-module, and high-risk changes instead of defaulting to comprehensive checks.
- Do not repeat passed deterministic checks when the relevant code, inputs, and environment are unchanged. Reruns need a concrete reason.
- Report honestly: do not invent successful tests, hide or exaggerate problems, or describe an unstudied area as a defect.
- State evidence-supported conclusions clearly. Explain necessary scope qualifications once without accumulating repetitive disclaimers.
- Stop when acceptance criteria are met. Do not add unrelated checks, documentation, or artifacts.
