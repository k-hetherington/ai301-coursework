# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:** In an eval bundle, look at the repro report's environment section and compare it with the issue context and repo-facts block. In live mode, look at the student's draft repro comment and the issue or repository documentation for any stated environment requirements.

**What good looks like:** The report identifies the software, versions, platform, configuration, or other conditions materially needed to interpret and rerun the reproduction. Compare these against environment requirements explicitly stated by the issue or repository. If a required condition differs, the report should identify that difference; do not require agreement on conditions the issue never specifies.

## Steps

**Where it lives:** In an eval bundle, look at the reproduction steps in the repro report together with any setup or starting-state information. In live mode, look at the steps in the student's draft repro comment and compare them with setup instructions in the repository documentation when relevant.

**What good looks like:** A stranger can start from the stated setup, perform the actions in the order given, and reach the point where the behavior is triggered without having to infer a material command, configuration, input, or action.

## Behavior shown

**Where it lives:** In an eval bundle, look at the repro report's observed behavior and its supporting artifacts, including output excerpts, logs, screenshots, error messages, or other recorded results. Compare these directly with the behavior described in the issue context. In live mode, use the student's captured artifacts and the original GitHub issue.

**What good looks like:** The artifacts visibly support the reported outcome and correspond to the specific behavior described by the issue rather than merely showing a related error or adjacent problem. If the issue cannot be reproduced, the evidence should instead show the actual differing result observed.

## Honesty

**Where it lives:** Compare the conclusion or stated outcome in the repro report with its steps, environment record, and supporting artifacts. In live mode, compare what the student's draft says happened with the evidence the student actually collected.

**What good looks like:** The wording stays within what the evidence demonstrates. A successful reproduction is claimed only when the target behavior is shown. A failed or differing reproduction is reported as such, including an honest cannot-reproduce when that is what the evidence supports.

## Comms

**Where it lives:** In an eval bundle, look at the claim comment and repro comment together with the issue context, repo-facts block, repository contribution policy, required comment templates, and any stated AI-use disclosure requirements. In live mode, check the issue thread and repository documentation before evaluating the student's draft comment.

**What good looks like:** The claim identifies the specific issue and proposed investigation without promising a fix, result, or deadline. The repro comment describes the observed result specifically and accurately. Both comments satisfy every applicable repository convention or required template. When the repository requires AI-use disclosure, look for the disclosure in the candidate comments themselves and verify that it includes whatever details the policy requires, such as the tool used and extent of assistance. If a required disclosure is absent or incomplete, the communication check does not pass.
