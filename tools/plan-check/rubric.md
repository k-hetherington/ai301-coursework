# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated cause and proposed approach, read against the reproduced behavior and supporting evidence identified in `references/evidence-guide.md`. | Pass when the diagnosis is consistent with the reproduced evidence and the proposed change addresses the evidenced cause rather than only an observed symptom. If the evidence does not establish a single cause, the plan must preserve that uncertainty instead of presenting an unsupported cause as fact. | required |
| scope | The plan's stated scope, files to change, exclusions, and any investigation or audit work, read against the diagnosis, issue request, and repository facts identified in `references/evidence-guide.md`. | Pass when the implementation work is bounded to the issue and every planned change has a clear connection to the diagnosed problem or its necessary tests. Investigation or auditing for related risk does not count as scope creep when the plan keeps resulting unrelated fixes out of scope. Unrelated refactoring or behavior changes fail this check unless the evidence shows they are necessary to the fix. | required |
| executability | The plan's implementation approach and files to touch, read against the repository facts and reproduced evidence identified in `references/evidence-guide.md`. | Pass when a developer unfamiliar with the issue could identify where to begin and what behavior or logic to change without having to invent a material implementation decision that the available evidence already permits the plan to make. | required |
| test-plan | The plan's test plan read against the unit 2 reproduction steps, observed failure, proposed change, and expected post-fix behavior identified in `references/evidence-guide.md`. | Pass when the planned checks exercise the real changed behavior, include an observable expected result after the fix, and would distinguish the reported failure from the intended behavior. | required |
| uncertainty | The plan's risks, unknowns, diagnosis, and implementation claims read against the reproduced evidence and repository facts identified in `references/evidence-guide.md`. | Pass when uncertain or unverified claims are identified as such and the plan does not state assumptions as established facts. A stated risk or unknown may remain unresolved when it does not prevent the proposed bounded change from being executed or tested. An unresolved unknown fails this check only when it is material enough that the implementation or expected test result depends on resolving it first. | required |
| conventions | The draft plan comment read against the issue thread, issue request, repository facts, and applicable contribution or communication rules identified in `references/evidence-guide.md`. | Pass when the comment presents the student's own issue-specific plan, remains consistent with the reproduced evidence and planned work, and satisfies every applicable repository or thread convention without making unsupported claims or promises. | required |

## Verdict rule

Accept only if every required check passes. Reject if any required check fails or is unclear. An unclear grade counts as a failure because a plan is not ready to post or build from when a required judgment cannot be supported by the available evidence. Preferred checks, if added later, do not change the verdict.
