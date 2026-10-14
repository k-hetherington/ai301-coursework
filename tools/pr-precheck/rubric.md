# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan fidelity | Compare the plan's scope, named files, and documented deviations against every changed file and behavior in the diff. | Every substantive change is authorized by the plan or explicitly documented as a justified deviation. No unexplained scope expansion, omission, or contradiction exists. An honestly disclosed shortfall does not automatically fail this check. | required |
| Description accuracy | Compare the PR title, description, implementation claims, and checklist against the actual diff and documented limitations. | Every material claim accurately reflects the implementation. Completed work is not overstated, missing work is disclosed, and no claim of exact plan compliance contradicts the diff. | required |
| Test evidence | Compare the plan's test plan with the test commands, printed output, reproduction results, and limitations in the package's Test evidence section or live `test_evidence.md`. | The evidence identifies what was tested and reports concrete outcomes supporting the material testing claims. Valid evidence includes before-and-after reproduction output, regression test assertions, or named test commands with specific reported results (such as pass, fail, or skip counts). Complete raw terminal output is not required unless repository rules explicitly demand it. Missing or failing tests must be accurately disclosed; unsupported claims of successful execution do not pass. | required |
| Repository checks | Compare the repository's required test commands from its PR template or contribution guide against the submitted test evidence. In eval mode, use the package's repo-facts block. |Applicable repository checks have sufficiently specific reported outcomes, including named test commands, concrete test summaries, or explicit results for standard repository checks such as formatting and linting. A statement such as "fmt and clippy clean" is acceptable when consistent with the supplied evidence and no repository rule requires full command transcripts. Unrun or failing checks must be disclosed, and mandatory submission requirements must be satisfied. | required |
| Diff reviewability | Inspect all changed files and hunks in the diff against the issue, plan, and stated implementation purpose. | The diff is focused and reviewable, without unrelated refactoring, debugging artifacts, temporary code, or unnecessary changes that obscure the fix. | required |
| Repository standards | Compare the PR description and submitted artifacts against the repository's PR template, contribution requirements, and applicable policies. In eval mode, use the repo-facts block. | All mandatory submission requirements are satisfied, including required sections, disclosures, and policy obligations. An explicitly permitted N/A explanation satisfies a nonapplicable requirement. | required |
| Evidence traceability | Compare significant PR claims with the corresponding diff hunks, test results, issue context, and plan. | Each material implementation or testing claim is supported by identifiable evidence in the supplied package, such as relevant diff hunks, regression test assertions, reproduction results, or concrete test summaries. A claim may be supported by multiple forms of evidence collectively. Do not require a separate printed result for every behavior when the diff and tests substantiate it. Contradicted claims and material assertions without meaningful support do not pass. | required |
| Review clarity | Read the PR title, description, and reviewer notes against the issue and implementation. | The PR communicates its purpose, impact, and relevant limitations clearly enough for a maintainer to review efficiently. Minor stylistic preferences do not constitute failure. | preferred |

## Verdict rule

Grade every check as `pass`, `fail`, or `unclear`.

- `pass`: The available evidence satisfies the check's pass condition.
- `fail`: The evidence demonstrates a violation, contradiction, or unsupported material claim.
- `unclear`: The evidence is missing or insufficient to establish whether the condition is satisfied.

Return `accept` only when every required check receives `pass`.

Return `reject` when any required check receives `fail` or `unclear`. Treat material claims without meaningful supporting evidence as insufficient. In eval mode, assess the evidence supplied in the bundle; do not require independent execution, external verification, or full raw transcripts when concrete results already support the claim.

Preferred checks provide feedback but never change the verdict, regardless of whether they receive `pass`, `fail`, or `unclear`.

Apply the honest-outcome rule: a disclosed limitation, incomplete test, or deviation does not independently require rejection when the PR accurately describes the situation, the remaining evidence is reviewable, and no mandatory repository requirement is violated.

Do not reward polished descriptions that contradict the diff or test evidence. Base every grade on observable evidence and the specific pass condition.

The final verdict must be exactly `accept` or `reject`.