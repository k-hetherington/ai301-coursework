# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment | The repro report's environment record, read against any environment requirements explicitly stated in the issue context or repo-facts block, as described in `references/evidence-guide.md`. | Pass when the report identifies the software, versions, platform, configuration, or other conditions materially needed to interpret and rerun the reproduction. If the issue or repository explicitly requires a particular environment condition, the report must satisfy it or clearly identify the difference. Do not require a match for conditions the issue does not specify. | required |
| steps | The reproduction steps in the repro report, read with any starting-state or setup information identified in `references/evidence-guide.md`. | Pass when a stranger could follow the described setup and actions from the stated starting condition through the action that triggers the observed result without having to infer a material missing step. | required |
| behavior | The repro report's observed behavior and supporting artifacts, such as output excerpts, logs, or screenshots, read against the behavior described in the issue context. | Pass when the evidence demonstrates the same behavior the issue describes, rather than merely a related or adjacent failure. An evidenced failure to reproduce also passes when the artifacts clearly show what occurred instead. | required |
| honesty | The report's stated outcome read against its reproduction steps, observed behavior, and supporting artifacts. | Pass when the conclusion does not claim more than the evidence supports: a reproduced issue is backed by evidence of the target behavior, and a cannot-reproduce or differing result is stated as such rather than presented as a successful reproduction. | required |
| conventions | The claim comment and repro comment read against the issue context, repo-facts block, repository contribution guidance, comment templates, and any AI-use disclosure requirements identified in `references/evidence-guide.md`. | Pass when the comments are specific to the issue, make no unsupported promises or claims, and satisfy every applicable repository communication requirement. If the repository requires disclosure of AI assistance, the candidate comments must contain the required disclosure, including any required tool or extent information; absence of a required disclosure fails this check. | required |

## Verdict rule

Accept only if every required check passes. Reject if any required check fails or is unclear. Preferred checks, if added later, do not change the verdict.