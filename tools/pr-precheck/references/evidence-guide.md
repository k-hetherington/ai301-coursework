
# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

### Where it lives

**Eval mode:**
- Read the package's Plan context section for the intended implementation, authorized files, scope boundaries, exclusions, and test plan.
- Read any documented deviations or explicitly permitted changes.
- Inspect the Candidate PR's Diff section for every changed file and substantive code change.
- Compare the Candidate PR title, description, and checklist claims against the diff and plan.
- Read the Issue section for the original problem and expected behavior.

**Live mode:**
- Read `plan.md`, including its scope, implementation steps, test plan, and `## Deviations` section.
- Run `git diff main...HEAD` from the Path Review repository to inspect every committed change on the branch.
- Read `pr_draft.md` for implementation claims, stated limitations, and explanations of deviations.
- Consult the GitHub issue thread for relevant requirements and maintainer decisions.

### What good looks like

Every substantive change in the diff falls within the plan's stated scope or is covered by a clearly documented, relevant deviation. The PR description accurately represents what the implementation accomplishes and identifies meaningful differences from the original plan.

An honestly disclosed shortfall or justified deviation does not automatically make the PR unacceptable. The actual implementation and its limitations must remain clear and consistent with the issue.

### Failure signals

- A changed file or behavior is outside the plan without an explanation.
- The implementation silently omits a planned requirement.
- The PR claims exact plan compliance despite an unauthorized change.
- The description claims functionality or tests not present in the submitted evidence.
- A deviation is disclosed but introduces unrelated work that is unnecessary for the issue.

## Test evidence (harness category: not-tested)

### Where it lives

**Eval mode:**
- Read the Plan context's test plan for required reproduction steps, regression cases, and expected outcomes.
- Read the Issue section for the original failure and desired behavior.
- Inspect the Candidate PR's Test evidence section for commands, actual printed output, and reported results.
- Read the Repo facts section for required test suites, validation commands, and any permitted exceptions.
- Compare test-related claims in the Candidate PR description against the submitted evidence.

**Live mode:**
- Read the testing requirements in `plan.md` and the original issue's reproduction steps.
- Inspect `test_evidence.md` for before-and-after reproduction results and captured command output.
- Compare results against `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
- Verify evidence for `make test-unit`, `make test-integration`, `make lint`, and `make typecheck`, where required by Path Review.

### What good looks like

Test evidence identifies the behavior being checked, shows the command or reproduction steps, and provides observable results that can be compared with the expected outcome.

Claims that tests passed are supported by actual printed output or another verifiable result. Failed, incomplete, or unavailable tests are reported accurately, with their limitations explained.

### Failure signals

- A command is shown without its actual output, followed by a claim that it passed.
- Comments beginning with `#` are presented as if they were command output.
- The PR claims a regression case was tested, but no corresponding evidence exists.
- Before-and-after behavior cannot be distinguished.
- Required repository checks are omitted without disclosure.
- Test failures are hidden or misrepresented.
- The description says "all tests passed" when the evidence shows otherwise.

An honestly disclosed test limitation is not automatically a failure. Determine whether the available evidence supports the claimed outcome and whether repository rules require the missing test to pass before submission.

## Diff quality (harness category: unreviewable)

### Where it lives

**Eval mode:**
- Inspect the Candidate PR's unified Diff section, including file paths, added and removed lines, and surrounding context.
- Inspect the package's commit list when provided.
- Compare the changed files against the Plan context and Issue section to determine whether each change serves the intended fix.

**Live mode:**
- Run `git diff main...HEAD` to inspect the complete committed implementation.
- Run `git diff main...HEAD --stat` to identify the files changed and the size of the diff.
- Use `git log main..HEAD --oneline` to review the branch's commits.
- Compare the implementation against `plan.md` and its documented deviations.

### What good looks like

The diff contains the intended fix and necessary supporting changes without unrelated modifications that obscure the implementation. A reviewer can identify what changed, why it changed, and how it addresses the issue.

Changes are reviewable based on their relevance and content, not the number of commits or the length of the diff.

### Failure signals

- Debugging statements or temporary instrumentation remain in the code.
- Commented-out code or unused experimental changes remain.
- Unrelated refactoring or formatting churn appears alongside the fix.
- Unnecessary files are added or modified.
- Large unrelated changes obscure the behavior being corrected.
- The diff contains changes that cannot be connected to the issue, plan, or justified deviations.

Do not reject a change solely because it is large or contains multiple commits. Evaluate whether the changes are necessary and reviewable.

## Standards and comms (harness category: standards-wall)

### Where it lives

**Eval mode:**
- Read the Repo facts section for required PR template sections, contribution guidelines, testing expectations, and stated policies.
- Inspect the Candidate PR title, description, checklist, and reviewer notes.
- Read the Issue section for explicit maintainer directions or requirements.
- Inspect any changelog or documentation changes in the Diff section when required by repository policy.

**Live mode:**
- Read `.github/PULL_REQUEST_TEMPLATE.md` for the required PR sections and checklist.
- Read `docs/CONTRIBUTING.md` for contribution standards, testing requirements, and policies.
- Read `pr_draft.md` for the proposed PR title, description, checklist, and reviewer notes.
- Check the GitHub issue thread for explicit maintainer requests.
- Read `voice-guide.md` for additional communication guidance. Apply voice feedback without independently changing the verdict.

### What good looks like

The PR satisfies the repository's mandatory submission requirements. Required sections contain relevant information, applicable policies are followed, and AI assistance is disclosed when required.

A section may be marked "N/A" when it genuinely does not apply and the repository permits that response. Optional formatting or stylistic preferences do not independently block submission.

### Failure signals

- A mandatory PR template section is missing or left as an unfilled placeholder.
- Required AI-use disclosure is absent.
- A mandatory changelog or documentation requirement is ignored.
- Repository contribution policies are violated.
- An explicit maintainer requirement is ignored without explanation.
- Required checklist items are falsely marked complete.
- Boilerplate replaces information that the repository specifically requires.

Evaluate compliance against the repository's stated requirements, not invented standards. Keep voice and stylistic recommendations separate from required submission conditions.

A description that misrepresents the diff belongs under Plan fidelity, even if it is also poorly written.