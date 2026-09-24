# Engineering Rules (Read as Needed)

Documentation language: English. See the [Chinese version](engineering.md).

Applies to code changes, debugging, test execution, builds and releases, and infrastructure changes.

## 1. Assess scope and risk

Determine the scope and impact of a change before choosing verification depth. Consider the actual reach of the change, data sensitivity, reversibility, external side effects, existing tests, and evidence of failure.

- A small change is not necessarily low risk, and missing information is not necessarily high risk. First resolve uncertainty with a low-cost check relevant to the problem, such as inspecting callers or running a targeted test.
- Text, formatting, and explanatory changes: check wording, facts, formatting, and relevant references. Do not run builds, test suites, or code scans.
- Local code or interface changes: test the affected behavior using relevant unit tests or direct execution. For styling changes, a preview or screenshot can provide confirmation.
- Changes spanning modules, interfaces, dependencies, or data processing logic: expand verification to affected paths and callers, running relevant integration tests according to project requirements.
- Changes involving permissions, authentication, irreversible data operations, real-world control, or major conclusions: expand verification as needed to authentication branches, permission checks, and data operation paths; consider rollback and idempotency. Follow the project's security procedures. Do not automatically launch a comprehensive security audit without an explicit requirement.
- Explicitly requested in-depth audits, stress tests, or large-scale experiments: follow the user's requirements and the predetermined design, without reducing or expanding the scope unilaterally.

## 2. Read the smallest relevant scope

Start with applicable project instructions, such as AGENTS.md, CLAUDE.md, and relevant README sections, followed by directly relevant files and necessary context.

For code tasks, also inspect relevant configuration, calling relationships, and version control state.

Expand as needed rather than scanning the entire repository by default.

## 3. Distinguish case count from execution rounds

- Running an existing suite with hundreds of different test cases once is normal execution, not excessive testing.
- Repeating the same deterministic smoke test when code, inputs, and environment are unchanged usually adds no value.
- Do not impose arbitrary limits such as "at most N test cases." The scope of the change determines the required coverage.

## 4. Do not repeat passed deterministic checks by default

Reuse conditions: the relevant code, tests, inputs, dependencies, configuration, and runtime environment are unchanged, and results have traceable support such as execution output.

- Context switches, session recovery, or a desire for reassurance before replying do not automatically require rerunning checks.
- Do not assume the current state is unchanged merely because someone previously reported success or the commit identifier is the same. Consider uncommitted changes, data changes, and environment changes.
- Invalidate only evidence affected by relevant changes. Unrelated file changes do not require rerunning everything.

## 5. Allow justified reruns

- Confirming that a change fixes the problem.
- Recovering from an identifiable transient environment failure, such as a network, port, or temporary file issue.
- Investigating evidence of an intermittent problem.
- Repeating runs according to a predetermined statistical or experimental design.

Have a concrete reason before rerunning a check, rather than appealing to general caution.

## 6. Default repeat budget

These are engineering defaults that can be adjusted to project requirements:

- Unchanged deterministic check that already passed: zero extra runs.
- Transient failure supported by a reasonable explanation: usually at most one retry.
- The same failure twice consecutively without new evidence: stop blind retries on that path and investigate the root cause or report the blocker.
- Necessary full test suite: run once at a suitable completion point, rather than after every small step.

Renaming commands, splitting subtasks, starting another agent, or reloading this skill does not reset the budget. The budget must not excuse hiding failures or ending prematurely.

## 7. Repeated research experiments

Use multiple seeds, resampling, stability evaluation, and statistical analysis as required by the research design and conclusions. Do not cancel repetitions necessary to support scientific conclusions to save tokens. Do not expand ordinary code changes into large-scale training or experiments without need and authorization.

## 8. SHA-256 and other hashes

- Calculate and publish hashes when an explicit need exists for integrity verification, release checks, or artifact identification.
- Hashes do not prove functional correctness. Without a corresponding need, do not calculate them by default, maintain hash inventories, or present checksums as proof of quality.
- Normal digests produced automatically by tools need not be removed.

## 9. Do not reduce testing quality to save effort

Do not delete valid tests, weaken assertions, swallow exceptions, fabricate logs, or relabel failure as success.

If tests cannot run, accurately explain the affected verification and its cause. Do not list every untested area unrelated to the task.

## 10. Necessary safeguards and unnecessary complexity

Preserve validation proportionate to actual input boundaries; clear, useful error handling; necessary permission controls; transactions, idempotency, or rollback appropriate to side effects; and tests needed to cover the affected behavior.

Do not add these by default: abstractions without an actual need; frameworks for hypothetical future scenarios; multiple layers of duplicate validation; unsupported retry, degradation, or fallback chains; dependencies added merely to appear robust; or unrelated configuration systems, monitoring platforms, and audit infrastructure.

When fixing a local problem, prefer the existing design and interfaces, making only necessary changes. Avoiding excessive defensive work does not justify empty exception handlers, silent failure, or default success in place of correct handling.

## 11. Unrelated problems

When you identify a real problem outside the current task, decide whether to mention it briefly based on its impact. Do not automatically turn it into another remediation project.

## 12. Conflicting project requirements

Follow the project's explicit verification requirements. Briefly explain conflicting rules when encountered, without overriding them unilaterally or independently adding a second process of similar size.

## 13. Context, memory, and multiple agents

- For long tasks, retain only enough concise state to resume work: the current goal, completed work, remaining blockers, necessary verification results and evidence locations, remaining budget, and stopping conditions. Prefer the environment's existing task state or summary mechanism.
- Do not create memory databases, audit logs, checkpoint directories, or state management systems for ordinary tasks.
- When reusing results across sessions, check whether relevant state has changed. Neither assume verification still applies without evidence nor automatically redo everything.
- Do not start multiple agents for duplicate reviews by default. When parallel work is necessary, assign non-overlapping responsibilities and share the budget, preventing each agent from independently rerunning the full set of checks.
- Do not expose lengthy internal reasoning. Show only necessary decisions, evidence, and results.
