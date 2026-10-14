---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Determine whether a candidate pull request is ready to submit based on its implementation plan, issue requirements, code changes, description, and test evidence.

Treat a PR package as the collection of materials needed to review the proposed change: the original issue, accepted plan, code diff, PR title and description, and test results.

Evaluate whether the implementation follows the plan, whether every claim is supported by evidence, and whether the PR meets the repository's contribution requirements. Do not grade the quality of the original issue or create a new implementation plan.

## Inputs and modes

Identify whether the request is in live mode or eval mode before beginning the review.

**Live mode**

Read the following materials:

1. The issue URL and its discussion thread to understand the reported problem and expected behavior.
2. `plan.md`, including any `## Deviations` section, to identify the approved implementation scope and test plan.
3. The branch's committed changes relative to `main`, using `git diff main...HEAD` from the repository's working directory.
4. `pr_draft.md` for the proposed PR title, description, checklist, and implementation claims.
5. `test_evidence.md` for reproduction steps, test commands, and actual printed results.
6. `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` for repository-specific requirements and contribution standards.

For a house-chain assignment, use the provided house issue, reproduction evidence, accepted plan, and working implementation branch instead of the student's original issue and branch. Apply the same checks.

**Eval mode**

Read the complete evaluation package supplied by the harness. Treat the package as the only available evidence.

Use the issue, plan context, candidate PR description, diff, and test evidence contained in that package.

Do not fetch external issues, repository files, or additional test results. Do not execute commands or assume that unprovided evidence exists.

Apply every rubric check and the complete verdict rule. Do not relax requirements because the package is a practice submission.

## The scope seam (live mode only)

Read `scope.md` before grading a live PR.

Verify that the repository and proposed work satisfy the scope rules. If the repository is outside the allowed scope, refuse to grade and explain the mismatch.

If the `Repo:` line contains an unfilled placeholder, refuse to grade and instruct the user to replace it with the correct Path Review repository.

Do not treat a scope refusal as an ordinary rubric failure. Explain the reason without issuing an unsupported PR verdict.

Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

Read `voice-guide.md` when evaluating a live PR.

Apply its communication requirements to the proposed PR title and description. Identify wording that is vague, unsupported, unnecessarily confident, or inconsistent with the required contributor voice.

Report violations with specific examples and suggested revisions.

Voice violations alone must not change an `accept` verdict to `reject`. Determine the verdict using the rubric's required checks.

Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read the skill components and use each for its assigned purpose:

- `rubric.md`: Defines the checks, evidence requirements, pass conditions, weights, and final verdict rule.
- `procedure.md`: Defines the review sequence, evidence gathering, check execution, and verdict assembly.
- `references/evidence-guide.md`: Explains where evidence is located in live and evaluation packages and what qualifies as sufficient proof.

Execute the steps in `procedure.md` in order. Evaluate each check using the requirements in `rubric.md` and the evidence standards in the evidence guide.

If the procedure does not explain how to perform a necessary step, report the procedural gap rather than inventing a replacement process.

If `rubric.md` or `procedure.md` is missing or contains no substantive instructions, refuse to grade. Identify the missing component and request that it be completed before evaluation.

Do not invent additional checks, weights, or exceptions beyond those defined in the rubric.

## Verdict and output

Return exactly one final verdict:

- `accept`: The PR satisfies the rubric's requirements and is ready to submit.
- `reject`: The PR does not satisfy the rubric's requirements and should be held for revision.

Provide a concise review summary identifying the strongest evidence, failed checks, and necessary corrections.

For each rubric check, assign one grade:

- `pass`: The available evidence satisfies the pass condition.
- `fail`: The available evidence contradicts the pass condition or demonstrates a violation.
- `unclear`: The evidence is insufficient to establish either a pass or a fail.

Include specific supporting evidence for every grade. Do not report that a command passed unless its actual output is provided.

Apply the verdict rule defined in `rubric.md`.

End every completed grading response with the following fenced JSON block. Keep it valid, use the required keys, and place nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Grade the submitted evidence rather than the confidence or polish of the PR description.

Compare every changed file against the accepted plan and its documented deviations. Flag unrelated changes, unexpected refactoring, and unexplained scope expansion.

Verify that implementation claims correspond to actual code changes. Do not treat a statement in the PR description as proof of its own accuracy.

Compare the test evidence against the plan's test requirements. Require actual commands and printed output when evaluating claims that tests passed.

Check repository-specific requirements, including the PR template, contribution guidelines, and any applicable AI disclosure requirements.

Use the rubric to determine what passes and fails. Use the procedure to determine how evidence is collected and evaluated.

Do not infer missing evidence, fabricate test results, or silently excuse unsupported claims.

If the rubric does not explicitly explain how an `unclear` grade affects the verdict, treat `unclear` on a required check as blocking acceptance. Preferred checks may be reported as unclear without independently forcing rejection.

Keep review comments specific, concise, and actionable. Explain what evidence supports each finding and what the contributor must change before submitting.
