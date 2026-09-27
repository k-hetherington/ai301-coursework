# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Repo facts: last 5 default-branch commit dates and maintainer first-response sample; issue Comments section for Owner, Member, or Collaborator activity | Pass if at least one default-branch commit was made within 90 days of the capture date OR the maintainer first-response sample shows at least one maintainer response within 30 days. Bot-only commits do not count unless the bot merged a human pull request. | required |
| Repository active | Repo facts: archived status, latest release, and last push to any branch | Pass if the repository is not archived AND either the latest release or last push occurred within 180 days of the capture date. | required |
| Newcomer-sized scope | Issue body, labels, opener association, linked PR history, and Comments section | Pass if the requested work has one clearly defined objective with enough direction to identify the intended outcome. Multiple related files, steps, suspected causes, or acceptance criteria may still constitute one contribution when they serve the same objective. Distinguish required work from ideas explicitly presented as optional, lower-priority, additional suggestions, possible approaches, or future improvements; optional suggestions do not by themselves expand the required scope or create an unresolved design decision. A terse description or incomplete implementation detail does not by itself make the scope unclear; maintainer/collaborator authorship or a `good first issue` label is supporting evidence that a terse issue is intentionally scoped for a newcomer. Fail if the issue is an umbrella/tracking issue coordinating separate required contributions, a pure usage/support question, contains an unresolved design decision that must be settled before the stated objective can be implemented, or a maintainer states that the work requires changes to core internals. Also fail when the issue history shows multiple distinct contributors made substantive implementation attempts that were abandoned or closed without resolution, because repeated unsuccessful attempts are evidence that the apparent scope is not reliably newcomer-sized. A single abandoned attempt alone is not sufficient to fail. | required |
| Issue available | Repo facts: this issue's assignees and linked PRs; Comments section for current claim or work-in-progress statements | Pass if the issue has no assignee, no open linked PR, and no comment indicating that another contributor is currently working on it. Closed unmerged PRs or abandoned attempts do not count as active claims. | required |
| AI contribution policy | Repo facts: contribution policy, including CONTRIBUTING.md, dedicated AI policy files, and relevant contributor or PR-template requirements | Pass unless the contribution policy explicitly bans AI-generated or AI-assisted contributions. Disclosure, testing, personal-understanding, or human-review requirements pass. If no AI policy is stated, pass. | required |

## Verdict rule

Accept the issue only if every required check passes. Reject the issue if any required check fails. Treat unclear evidence for a required check as a fail. Preferred checks, if added later, do not change the accept/reject verdict and are used only to rank accepted issues.
