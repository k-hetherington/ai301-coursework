# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives:** In eval packages, read the Candidate plan's cause and proposed change against the Repro evidence, Issue, and relevant Repo facts. The reproduction establishes the observed behavior and may provide evidence about where the failure occurs; repository facts provide only the technical or contribution facts explicitly included in the package. In live mode, use the diagnosis in `plan.md`, the student's posted Unit 2 reproduction comment, the issue thread, and relevant repository files or documentation.

**What good looks like:** The diagnosis explains the reproduced behavior without contradicting it or claiming a cause the available evidence does not establish. The proposed change addresses the evidenced cause rather than merely hiding the visible symptom. When the evidence supports behavior but not a definite cause, the plan states that uncertainty instead of converting it into certainty.

## Scope

**Where it lives:** In eval packages, use the Candidate plan's change, in-scope and out-of-scope statements, and named files or areas. Read them against the Issue, diagnosis, Repro evidence, and relevant Repo facts. In live mode, use the scope, files-to-touch, and exclusions in `plan.md` together with the issue and repository context.

**What good looks like:** Every proposed change is necessary to address the issue or verify the fix, and the plan identifies meaningful boundaries on the work. Unrelated cleanup, broad refactoring, or changes to behavior outside the issue are not part of the plan unless the evidence shows they are required.

## Executability

**Where it lives:** In eval packages, use the Candidate plan's change description, named files or areas, and implementation approach, read against the Repo facts and Repro evidence. In live mode, use the files-to-touch and approach in `plan.md` together with the actual repository locations established while investigating the reproduced issue.

**What good looks like:** A developer unfamiliar with the issue can identify a concrete place to begin and the behavior or logic that needs to change. The plan resolves material implementation decisions that the available evidence permits it to resolve, while leaving ordinary coding details to the build.

## Test plan

**Where it lives:** In eval packages, use the Candidate plan's test section and compare it directly with the Repro evidence's inputs, steps, observed result, and expected result. Also use Repo facts when they identify relevant existing tests. In live mode, use the test plan in `plan.md`, the Unit 2 reproduction commands and output, and relevant repository tests.

**What good looks like:** The test plan exercises the real behavior being changed and states an observable post-fix result that distinguishes the bug from the intended behavior. It reuses or meaningfully adapts the reproduction where possible and includes relevant regression coverage when the repository evidence identifies it.

## Honesty

**Where it lives:** In eval packages, compare causal and implementation claims in the Candidate plan with its risks or unknowns, the Repro evidence, Issue, and Repo facts. In live mode, use the diagnosis, risks and unknowns, and `## Deviations` section of `plan.md`, together with the reproduction and repository evidence.

**What good looks like:** Facts supported by evidence are stated as facts, while assumptions and unresolved questions remain identified as assumptions or unknowns. A material unknown that could alter the implementation or result is not hidden behind confident wording. During the build, any departure from the posted plan is recorded accurately under `## Deviations`.

## Comms

**Where it lives:** In eval packages, read the Candidate plan comment against the Candidate plan, Issue, Thread highlights, and Repo facts, especially contribution guidance, templates, maintainer requests, and any AI-use disclosure requirement. In live mode, read `comment.md` against the GitHub issue thread, the student's own reproduction, `plan.md`, repository contribution guidance, and the Path Review house rules in `scope.md`.

**What good looks like:** The comment is specific to the issue, represents the student's own plan, stays consistent with the evidence and detailed plan, and responds to applicable maintainer or repository requirements. It does not piggyback on another student's plan, make unsupported promises, or omit a required contribution or disclosure convention.
