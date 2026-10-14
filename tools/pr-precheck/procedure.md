# Procedure: how this tool grades a PR package

## Read order

1. Identify the evaluation mode before reviewing the package.
   - In live mode, read `scope.md` and verify that the repository is authorized. Refuse to grade if the scope is invalid or the repository placeholder has not been replaced.
   - In eval mode, use only the supplied evaluation package. Do not fetch external information or apply live-mode scope restrictions.

2. Read `rubric.md`, `references/evidence-guide.md`, and this procedure to identify the required checks, evidence standards, and verdict rule. If the rubric or procedure is missing or contains no substantive instructions, refuse to grade.

3. Read the original issue and its discussion thread, or the Issue section of an evaluation package. Record:
   - The reported problem and affected behavior.
   - The expected outcome.
   - Any constraints or edge cases.
   - Relevant maintainer decisions or unresolved questions.

4. Read the accepted implementation plan before examining the diff. In live mode, use `plan.md`, including `## Deviations`. In eval mode, use Plan context. Record:
   - The intended implementation and scope boundaries.
   - Authorized files and directories.
   - Explicit exclusions.
   - Required tests and expected results.
   - Documented deviations and their explanations.

5. Read repository contribution requirements. In live mode, inspect `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. In eval mode, inspect Repo facts and any stated repository policies. Record mandatory checks, documentation requirements, disclosures, and submission standards.

6. Read the complete implementation diff. In live mode, run `git diff main...HEAD` from the repository working directory. In eval mode, use the package's Diff section. Record every changed file and the purpose of each substantive change.

7. Read the PR title and description. In live mode, use `pr_draft.md`; in eval mode, use Candidate PR. Record implementation claims, checklist statements, declared limitations, and reviewer notes.

8. Read the test evidence. In live mode, use `test_evidence.md`; in eval mode, use Test evidence. Record commands, actual printed output, before-and-after behavior, and disclosed failures or omissions.

9. In live mode only, read `voice-guide.md` and compare its requirements against the PR title and description. Record violations as advisory feedback.

Complete this read order before assigning grades. Reading the plan before the diff prevents the implementation from redefining its own approved scope.

## Evidence gathering

1. **Plan fidelity**
   - Extract the authorized files, implementation boundaries, exclusions, and deviations from the accepted plan.
   - Compare them against every changed file and substantive hunk in the diff.
   - Record unauthorized changes, omitted planned work, and deviations that are or are not disclosed.
   - Do not treat an honestly disclosed shortfall as an automatic failure.
   - Distinguish an undisclosed omission from a limitation explicitly identified in the PR description or plan deviations. Grade the accuracy of the disclosure and the actual scope of the diff rather than requiring every planned improvement to be completed.
   
2. **Description accuracy**
   - Extract each material claim from the PR title, description, and checklist.
   - Locate its supporting code change, test result, or documented limitation.
   - Record whether the claim is supported, contradicted, or unverifiable.
   - Pay particular attention to claims such as "all tests passed," "no unrelated changes," and "implemented exactly as planned."

3. **Test evidence**
   - Extract the required reproduction steps, regression cases, and expected outcomes from the plan's test plan.
   - Match each requirement to the submitted test evidence.
   - Record the command, actual printed output, observed result, and any disclosed limitation.
   - Distinguish actual command output from comments, summaries, and unsupported assertions.
   - Do not assume tests passed because a contributor says they passed.

4. **Repository checks**
   - Extract required test commands from the repository's PR template and contribution guide, or the eval package's Repo facts.
   - Match each command against the submitted test evidence.
   - Record whether it ran, its observed result, and any disclosed failure or omission.
   - Determine whether repository rules explicitly require successful execution or permit documented limitations.

5. **Diff reviewability**
   - Inspect all changed files and hunks.
   - Identify unrelated refactoring, debugging statements, temporary files, commented-out code, and changes unrelated to the issue.
   - Record the exact file and relevant hunk for each problem.
   - Distinguish necessary supporting changes from unrelated modifications.

6. **Repository standards**
   - Compare the PR description and submitted artifacts against the repository's stated requirements.
   - Check required sections, changelog entries, documentation updates, contribution policies, and AI-use disclosures where applicable.
   - Record each requirement and whether the submitted package satisfies it.
   - Accept a justified "N/A" only when the requirement permits it.

7. **Evidence traceability**
   - Match each significant implementation or testing claim to a specific diff hunk, command output, issue detail, or plan statement.
   - Record unsupported claims and evidence that a reviewer cannot independently locate.
   - Avoid treating the PR description as proof of its own claims.

8. **Review clarity**
   - Read the title, summary, change descriptions, and reviewer notes.
   - Determine whether a maintainer can understand the change's purpose, impact, and limitations.
   - Record material ambiguities separately from minor stylistic preferences.
   - In live mode, record voice-guide violations as advisory feedback.

Use `references/evidence-guide.md` to identify the correct location for each evidence type. Do not invent missing evidence or substitute assumptions for observed results.

## Check execution

1. Execute the checks in the exact order listed in `rubric.md`:
   - Plan fidelity
   - Description accuracy
   - Test evidence
   - Repository checks
   - Diff reviewability
   - Repository standards
   - Evidence traceability
   - Review clarity

2. For each check, read its Evidence, Pass condition, and Weight from the rubric.

3. Compare the gathered evidence directly against the pass condition. Use the recorded evidence rather than rereading the entire package unless a contradiction or missing detail requires verification.

4. Assign exactly one grade:
   - `pass`: The evidence satisfies the check's pass condition.
   - `fail`: The evidence demonstrates a violation or contradicts a material claim.
   - `unclear`: The evidence is insufficient to determine whether the condition is satisfied.

5. Assign fail when a required claim of completion or successful testing lacks observable supporting evidence, or when evidence contradicts the claim. Assign unclear when the available package genuinely cannot establish the outcome and no explicit requirement has been demonstrably violated. Never infer success from missing evidence.

6. Apply the honest-outcome rule. An accurately disclosed shortfall, failed test, or deviation does not automatically fail a check. Determine whether the remaining implementation is reviewable, whether the evidence supports the disclosed outcome, and whether any mandatory repository requirement is violated. Disclosure does not excuse unrelated changes or unsupported claims.

7. Evaluate every check independently. A failure in one check does not automatically cause another check to fail unless the same evidence independently violates both pass conditions.

8. For each check, record:
   - The exact rubric check name.
   - Its grade.
   - One concise evidence statement identifying the decisive fact, file, command, or missing proof.

9. Do not stop grading after the first failure. Complete every check so the contributor receives a full review.

10. Do not add, remove, or change rubric checks during execution. If a required procedure step is undefined, report the procedural gap instead of improvising a new grading method.

## Verdict assembly

1. Collect the final grade for every check in the order defined by `rubric.md`.

2. Apply the rubric's verdict rule:
   - Return `accept` only when every required check receives `pass`.
   - Return `reject` when at least one required check receives `fail` or `unclear`.
   - Preferred checks never change the verdict.

3. Treat `unclear` on a required check as blocking acceptance. Do not assume missing evidence establishes compliance.

4. Identify the deciding check:
   - If the verdict is `reject`, select the first required check graded `fail` or `unclear` in rubric order.
   - If several required checks fail, identify the first as the deciding check and summarize the remaining failures.
   - If the verdict is `accept`, identify the strongest evidence supporting readiness.

5. Produce a concise review summary that:
   - States whether the PR is ready to submit.
   - Identifies the deciding check and its supporting evidence.
   - Explains additional required failures or uncertainties.
   - Recommends specific corrective actions.
   - Separates preferred or voice-related suggestions from verdict-blocking problems.

6. End the response with the exact JSON structure required by `SKILL.md` and `CONTRACT.md`.

7. Populate the JSON fields:
   - `item`: The PR URL in live mode or package identifier in eval mode.
   - `checks`: Every rubric check, in rubric order, with its exact name, grade, and one-line evidence.
   - `verdict`: Exactly `accept` or `reject`.

8. Verify that the JSON is valid, that every required check is included, and that the verdict follows the recorded grades.

9. Place the fenced JSON block at the very end of the response, with no text afterward.