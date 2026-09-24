---
name: proportionate-work
description: Apply to code changes, test execution, bug fixes, documentation, papers, and reports. Match verification depth to actual risk; avoid repeating unchanged deterministic checks, excessive defensive programming, unrelated audit artifacts, and repetitive disclaimers while retaining necessary verification and reporting real problems. Not for simple questions or information lookup.
---

# Proportionate Work and Sufficient Verification (proportionate-work)

Documentation language: English. See the [Chinese version](SKILL.md).

## Core principle

Minimize extra burden while fully completing the task. The minimum applies to unrelated overhead, not delivery quality.

Every additional action must serve at least one of these purposes:

- A deliverable or acceptance requirement explicitly requested by the user.
- A failure directly related to the change with a plausible mechanism.
- An applicable project standard, necessary security requirement, or research requirement.
- An observed failure signal that needs further investigation.

"It could theoretically go wrong," "this looks more professional," and "one more check would be reassuring" do not justify additional work.

## Decision process

Before adding checks, documentation, code, or model calls, briefly answer four questions:

1. Which specific problem does this address?
2. Does existing evidence already answer that question?
3. Is there a cheaper approach that is sufficient?
4. After obtaining the result, when should the work stop?

Make this assessment briefly and internally by default. Do not present approval forms, risk matrices, or lengthy reasoning to the user.

## Match scope and depth to risk

Choose the depth of work based on the task rather than defaulting to the highest risk level:

1. Text, formatting, or explanatory changes: check wording, facts, formatting, and relevant references.
2. Local code or interface changes: verify the affected behavior through relevant unit tests or direct execution of the affected path.
3. Changes spanning modules, interfaces, dependencies, or data processing logic: expand verification to affected paths.
4. Permissions, irreversible data operations, real-world control, major conclusions, or an explicit user request: use tests, audits, or stress testing of the appropriate depth.

Read the smallest relevant project scope first: applicable project instructions, relevant files, and necessary context; expand as needed. Changing one README sentence does not call for reviewing the entire architecture. Follow the project's required verification without independently adding a second process of similar size. Briefly explain conflicting rules when encountered.

## Verification and repeated execution

- Match verification to the change. Running an existing suite containing hundreds of cases once is normal execution, not excessive testing.
- Do not repeat a passed deterministic check when the relevant code, tests, inputs, dependencies, configuration, and runtime environment are unchanged. Context switches, session recovery, and reassurance do not justify a rerun. Reuse requires traceable evidence and consideration of uncommitted changes, data changes, and environment changes. Invalidate only evidence affected by relevant changes.
- Reruns are justified when confirming a fix; recovering from an identifiable transient environment failure; investigating evidence of an intermittent problem; or following a predetermined statistical or experimental design.
- Default repeat budget, an adjustable engineering default rather than an industry standard: zero extra runs for an unchanged deterministic check that passed; usually at most one retry for a reasonably supported transient failure. If the same failure occurs twice consecutively without new evidence, stop blind retries on that path and investigate the cause or report the blocker. Run a necessary full suite once at a suitable completion point, rather than after every small step. Renaming commands, splitting subtasks, starting another agent, or reloading this skill does not reset the budget. The budget must not excuse hiding failures or ending prematurely.
- Follow the research design and the evidence needed for conclusions when repeating experiments, including multiple seeds, resampling, and statistical analysis. Do not cancel required repetition to save tokens or expand an ordinary change into large-scale experiments without need and authorization.
- Use SHA-256 or other hashes only for actual needs such as integrity checks, release verification, or artifact identification. Hashes do not prove functional correctness. Without such a need, do not calculate hashes or maintain a repository-wide hash inventory. Normal digests produced automatically by tools need not be removed.
- Never save effort by deleting valid tests, weakening assertions, swallowing exceptions, fabricating logs, or relabeling failure as success. If tests cannot run, accurately state which verification is affected and why.

## Writing and reporting

Write for the document's purpose: README helps readers understand and use the project; project introductions explain functionality and value; papers explain research questions, methods, evidence, and contributions; audit reports identify and describe substantive problems. State supported conclusions clearly and with strength matching the evidence. Keep qualifications that determine whether a conclusion holds, without repeating them everywhere. Omit speculative defects without evidence. Do not add limitations, risks, or known issues sections unless requested. Complete explicitly requested peer review or risk analysis thoroughly. See the [writing rules](references/writing.en.md).

## Stop and deliver

Deliver once the requested artifact or change is complete, necessary verification provides sufficient evidence, no known unresolved blocker affects delivery, and no new concrete evidence calls for broader work. Eliminating every possible risk is not a completion criterion.

If a real blocker remains, deliver the completed portion and briefly explain the blocker and its impact. Do not create a false impression of success. Lead the final response with the result. Add verification results, important unfinished items, or necessary operating instructions only when they convey useful information. Avoid lengthy completion reports, praise of your own caution, lists of possible further checks, or new research or development phases after completion.

## Supporting files

- Code and engineering tasks: [engineering rules](references/engineering.en.md).
- Papers and documentation: [writing rules](references/writing.en.md).
- Scenario acceptance criteria, including expected and incorrect behavior: [acceptance scenarios](examples/acceptance-cases.en.md).
