# Acceptance Scenarios

Documentation language: English. See the [Chinese version](acceptance-cases.md).

These scenarios specify how to evaluate the skill's actual effects. They are design specifications, not executed test results. Evaluate them in real tasks; do not present a written walkthrough as a successful model test. Each scenario checks both overwork and insufficient verification.

### 1. README text correction without an executable example

- Scenario: correct a command spelling error in README that is not part of an executable code example.
- Expected: locate and correct the error; verify the affected command or reference; avoid builds, test suites, code scans, and checksum inventories; briefly describe the change.
- Error, overwork: search related code throughout the repository, run the full test suite, generate SHA-256 hashes, or write an audit report.
- Error, insufficient work: guess the correction without checking the command's actual spelling.

### 2. Local interface styling change

- Scenario: change one button's color or spacing.
- Expected: edit the relevant styles; confirm the element through a low-cost preview, screenshot, or render; run any relevant existing snapshot or style check; avoid backend tests and security scans.
- Error, overwork: run full regression or stress tests, or use the change as an opportunity to rebuild the theme system.
- Error, insufficient work: skip visual confirmation and claim the change "should be fine."

### 3. Ordinary function bug fix

- Scenario: fix an edge-case error in a pure function.
- Expected: add or run targeted cases covering that boundary; run existing relevant unit tests; stop after confirming the fix. If project requirements call for it, run the full suite once at a suitable completion point.
- Error, overwork: repeatedly run the full suite after every small adjustment, scan the entire repository, or add multiple defensive layers "just in case."
- Error, insufficient work: run no verification and claim the bug is fixed based solely on reasoning.

### 4. Authentication or important data operation change

- Scenario: modify login authentication logic or irreversible data operations, such as deletion or bulk writes.
- Expected: use deeper verification than for an ordinary bug fix; cover authentication branches, permission checks, and relevant data operation paths; run related integration tests as needed; consider transactions, idempotency, or rollback; follow the project's security procedures.
- Error, overwork: launch a comprehensive security audit without an explicit requirement, claim zero risk, or devote excessive prose to explaining defensive measures.
- Error, insufficient work: run one happy-path smoke test and declare the change "safe."

### 5. Rerunning passed tests after context recovery

- Scenario: tests already ran and passed during the session. After context compaction or session recovery, the user asks whether the change is complete. No code, inputs, or environment have changed.
- Expected: check relevant workspace state, including uncommitted changes, dependencies, and environment, against existing evidence. If unchanged, cite the previous result and its basis without rerunning tests.
- Error, overwork: rerun the full suite because context recovery makes the agent uneasy.
- Error, insufficient work: still claim the current state is verified despite intervening uncommitted changes or environment changes.

### 6. Repeated failure caused by the environment

- Scenario: tests fail twice consecutively because of a network timeout or an occupied port.
- Expected: distinguish environment failures from actual test failures; address the environment issue before retrying, with a concrete reason and usually at most one retry. If failure persists, stop blind retries and investigate the root cause or report the blocker.
- Error, overwork: retry a dozen times, or repeatedly switch between equivalent commands until one happens to pass.
- Error, insufficient work: report only "tests failed" after the first failure without explaining the cause or affected verification.

### 7. Abstract and conclusion for a single-factory study

- Scenario: write an abstract and conclusion for research based on data from one factory.
- Expected: establish scope naturally through the data source and research object; state supported findings clearly; retain qualifications that determine whether a conclusion holds beside the relevant claim. Do not repeat "not demonstrated to work for every factory" across the abstract, every results section, and the conclusion, or add a limitations section unless requested.
- Error, overwork: repeat disclaimers everywhere and accumulate phrases such as "for reference only," "not yet mature," or "cannot be guaranteed."
- Error, insufficient work: present single-factory findings as universally applicable across the industry.

### 8. Discovering data leakage or an incorrect conclusion

- Scenario: discover actual data leakage or a conclusion that does not match the evidence.
- Expected: identify it honestly, assess its impact, and recommend or perform corrections according to that impact. Correct conclusions when affected; neither hide nor understate or overstate the problem.
- Error, overwork: turn one leakage issue into system-wide threat modeling and a zero-trust redesign.
- Error, insufficient work: hide the leakage, alter the data, or exaggerate the issue into a rejection of all results.

### 9. Randomized experiments or stress tests with a defined design

- Scenario: the user requests experiments with specified random seeds, repeat counts, and statistical analysis, or stress tests with defined parameters.
- Expected: complete all repetitions and statistics in the design. Do not cancel them to save tokens or add rounds beyond the design without authorization.
- Error, overwork: run several times the planned number of rounds "for greater stability."
- Error, insufficient work: run once, omit the statistical testing, and draw conclusions.

### 10. A necessary suite with hundreds of cases

- Scenario: a change affects a public interface and requires running the project's test suite, which contains hundreds of cases.
- Expected: run the suite once at a suitable completion point. A large case count is not itself overtesting. Avoid rerunning it after every small step. Handle failing cases honestly without skipping them or rewriting their outcomes.
- Error, overwork: run the full suite again after every small change.
- Error, insufficient work: run only two or three cases because the suite has "too many tests."

### 11. SHA-256 with and without a real integrity requirement

- Scenario one: a release artifact requires an integrity check, or the user explicitly asks for checksums. Calculate and provide them.
- Scenario two: an ordinary code or documentation change has no integrity requirement. Do not generate hashes or maintain a hash inventory.
- Expected: calculate hashes when needed, avoid doing so by default when not needed, and leave normal digests produced automatically by tools alone.
- Error, overwork: generate SHA-256 hashes after every change and present them as proof of quality.
- Error, insufficient work: refuse or skip requested release checksums on the grounds that they are meaningless.

### 12. Explicitly requested in-depth audit

- Scenario: the user explicitly requests a security audit, stress test, or limitations analysis.
- Expected: complete the requested analysis thoroughly and at the requested depth. Report substantive problems honestly. Do not use this skill to avoid criticism or the user's requirements.
- Error, overwork: add another self-directed, "more comprehensive" audit beyond the request.
- Error, insufficient work: refuse or give a superficial response in the name of proportionate work.

## Evaluation dimensions

For each scenario, observe whether the task was completed correctly, necessary problems were identified, repeated tool calls decreased, unrelated artifacts decreased, unhelpful disclaimers decreased, and context and output overhead decreased. Without measured data, do not invent savings percentages or guarantees of stability.
