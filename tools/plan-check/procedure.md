# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->
## Read order

1. Read the issue context and thread highlights first. Record the requested behavior, any stated constraints, and any repository or communication conventions that apply to the plan.
2. Read the repository facts next. Record the relevant files, functions, tests, and technical constraints that are established by the package.
3. Read the reproduction evidence before judging the proposed plan. Record the reproduction steps, the observed failure or behavior, and what the evidence establishes about where and why the behavior occurs. Keep observations separate from causes that have not been demonstrated.
4. Read the proposed plan after establishing that evidence baseline. Record its diagnosis, scope and exclusions, files to touch, implementation approach, test plan, and risks or unknowns.
5. Read the draft plan comment last. Compare it with the detailed plan, issue thread, and applicable conventions so that the shorter comment is not treated as evidence for claims missing from the plan.

## Evidence gathering

1. For diagnosis, pair each material causal claim in the plan with the reproduction evidence or repository fact that supports it. Record any claim that contradicts the evidence or goes beyond what the evidence establishes.
2. For scope, list the changes and files the plan proposes to touch and compare each one with the issue request and diagnosis. Record any proposed work that does not have a necessary connection to the issue or its tests.
3. For executability, identify the concrete starting points supplied by the plan, including relevant files, functions, behavior, or logic to change. Record any material implementation decision a developer would still have to invent even though the available evidence permits the plan to make it.
4. For the test plan, record the reproduced input or action, the original observed result, the post-fix command or check, and the expected observable result. Verify that the planned check exercises the real changed behavior rather than a stand-in.
5. For uncertainty, list material risks, assumptions, and unknowns from the plan and compare them with the reproduction evidence and repository facts. Record unsupported claims that are presented as established facts.
6. For conventions, compare the draft plan comment with the issue thread, repository facts, and applicable contribution or communication rules. Record any missing requirement, contradiction, unsupported promise, or attempt to rely on another student's plan instead of presenting the student's own plan.

## Check execution

1. Grade diagnosis first using only the gathered diagnosis evidence. Mark it pass when the stated cause and approach satisfy the rubric condition, fail when they contradict or overstate the evidence or target only a symptom, and unclear when the available evidence cannot support the required judgment.
2. Grade scope next from the recorded proposed changes, exclusions, issue request, and diagnosis. Judge the scope of implementation changes separately from investigation or auditing. An audit for related risk is not scope creep when the plan explicitly keeps unrelated resulting fixes out of scope.
3. Grade executability from the recorded implementation starting points. Distinguish normal coding choices that can be made during implementation from material decisions the plan should already resolve from available evidence.
4. Grade test-plan from the recorded before-and-after behavior. Require an observable expected result that would demonstrate that the reported failure changed to the intended behavior.
5. Grade uncertainty from the recorded assumptions, risks, and unknowns. Do not fail a plan merely because it identifies an unresolved risk or unknown. Fail when a material unknown is presented as certainty, ignored, or must be resolved before the proposed implementation or expected test result can be justified.
6. Grade conventions last using the draft comment and applicable thread and repository rules.
7. If evidence required for any check is genuinely absent or conflicting, mark that check unclear rather than guessing. Do not reread unrelated package material to manufacture support for a missing fact.

## Verdict assembly

1. Collect the grade for every rubric check before deciding the overall verdict.
2. Apply the rubric's verdict rule exactly: accept only when every required check passes. A required fail or unclear produces reject. Preferred checks, if any are later added, do not change the verdict.
3. For each check, report the grade with a concise reason tied to the gathered evidence.
4. For a rejecting verdict, identify and quote or precisely reference the evidence responsible for the first decisive required fail or unclear grade. If several required checks fail, report them all while keeping the verdict binary.
