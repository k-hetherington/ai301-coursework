# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
┌──────────────────┬───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────┐
│      Check       │ Grade │                                               Evidence                                               │
├──────────────────┼───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Maintainer       │ pass  │ Newest main commit 2026-09-16 by human Aburke225 (COLLABORATOR) — 11 days, inside 90                 │
│ activity         │       │                                                                                                      │
├──────────────────┼───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Repository       │ pass  │ archived: false, pushed_at: 2026-09-16 — 11 days, inside 180 (no releases, but the push arm          │
│ active           │       │ satisfies the OR)                                                                                    │
├──────────────────┼───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Newcomer-sized   │       │ One objective: guard the .items() call on a list in output_parser.py and drop the xfail; two named   │
│ scope            │ pass  │ files, good first issue + tier-1, COLLABORATOR-authored, 2–4h estimate. No umbrella, no unresolved   │
│                  │       │ design decision, no maintainer "core internals" warning                                              │
├──────────────────┼───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                  │       │ assignees: []; repo's only PRs are #74–#78, none touching #69 (PR search for "69" → 0); the one      │
│ Issue available  │ pass  │ cross-reference is a merged PR in charancherry0/ai301-coursework — a classmate's write-up, not an    │
│                  │       │ attempt here. jacho15's three comments are a classmate (NONE) claim, ignored by house rule           │
├──────────────────┼───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ AI contribution  │ pass  │ Only policy surfaces are docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md; neither mentions │
│ policy           │       │  AI/LLM/generated code. No AI_POLICY.md/AGENTS.md. Silence passes                                    │
└──────────────────┴───────┴──────────────────────────────────────────────────────────────────────────────────────────────────────┘

All five required checks pass → accept.

Fit notes (ranking only, no verdict effect): this is a strong match for the profile — Python, a RAG subsystem, a concrete AttributeError reproduction, and a pre-written strict=True xfail at tests/unit/test_output_parser.py:141 that turns the fix into a failing-test-driven change in real application logic. No frontend or infra work.

One tension worth flagging (rubric change, not a run override): jacho15 has already reproduced the bug and posted a full fix plan. The house rule correctly says that doesn't block you, but you'll be implementing alongside them.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass",
     "evidence": "Latest main commit 2026-09-16 by human collaborator Aburke225, 11 days before capture date 2026-09-27 (within 90)"},
    {"name": "Repository active", "grade": "pass",
     "evidence": "archived: false and pushed_at 2026-09-16T21:48:27Z, 11 days before capture (within 180); no releases exist"},
    {"name": "Newcomer-sized scope", "grade": "pass",
     "evidence": "Single objective with two named files, 'good first issue'/'tier-1' labels, COLLABORATOR opener, 2-4 hour estimate, and a pre-existing xfail test defining the outcome"},
    {"name": "Issue available", "grade": "pass",
     "evidence": "assignees: []; no PR in the repo references #69; the sole cross-reference is a merged coursework PR in charancherry0/ai301-coursework, and jacho15's claim comments are author_association NONE (classmate, ignored by house rule)"},
    {"name": "AI contribution policy", "grade": "pass",
     "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI/LLM/generated-code restriction; no AI_POLICY.md or AGENTS.md exists"}
  ],
  "verdict": "accept"
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

- `2/3`
- `5/6`
- `9/10`
- `17/20`
- `19/20`
  
**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

`issue-15` — My rubric's final decision was `reject`, which matched the gold label of `reject`. The issue initially appeared available because it had no current assignee or open linked pull request, and the requested work appeared bounded. However, its history showed that multiple distinct contributors had made substantive implementation attempts that were later abandoned or closed without resolving the issue. My earlier rubric did not account for that history and incorrectly accepted the issue. I revised the Newcomer-sized scope check so that repeated unsuccessful implementation attempts are evidence that an apparently bounded issue may not actually be reliably newcomer-sized. With that evidence included, the rubric correctly rejected `issue-15`.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Quoted check — Newcomer-sized scope**

> **Evidence:** Issue body, labels, opener association, linked PR history, and Comments section
>
> **Pass condition:** Pass if the requested work has one clearly defined objective with enough direction to identify the intended outcome. Multiple related files, steps, suspected causes, or acceptance criteria may still constitute one contribution when they serve the same objective. Distinguish required work from ideas explicitly presented as optional, lower-priority, additional suggestions, possible approaches, or future improvements; optional suggestions do not by themselves expand the required scope or create an unresolved design decision. A terse description or incomplete implementation detail does not by itself make the scope unclear; maintainer/collaborator authorship or a `good first issue` label is supporting evidence that a terse issue is intentionally scoped for a newcomer. Fail if the issue is an umbrella/tracking issue coordinating separate required contributions, a pure usage/support question, contains an unresolved design decision that must be settled before the stated objective can be implemented, or a maintainer states that the work requires changes to core internals. Also fail when the issue history shows multiple distinct contributors made substantive implementation attempts that were abandoned or closed without resolution, because repeated unsuccessful attempts are evidence that the apparent scope is not reliably newcomer-sized. A single abandoned attempt alone is not sufficient to fail.
>
> **Weight:** `required`

I chose this form because my earlier versions treated scope too mechanically. Some legitimate newcomer issues involved multiple files, steps, or possible causes even though they still had one bounded objective, while other issues looked simple from the description but had a history of repeated unsuccessful implementation attempts. The current check therefore focuses on whether the required work has one clear objective while using labels, maintainer context, optional-versus-required work, unresolved design questions, and prior implementation history as supporting evidence.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check gives up some simplicity and may reject an issue that is technically manageable for a newcomer when its history contains multiple abandoned substantive attempts. I accepted that trade-off because `issue-15` initially passed my rubric even though its history showed repeated unsuccessful attempts by different contributors. After adding that history criterion, I re-ran `issue-15` with `--only` and it changed from `accept` to `reject`, matching the gold label. I also re-ran `issue-19` after refining the check so that optional suggestions would not automatically expand the required scope; it returned `accept`, matching its gold label.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

**1. Fit to my interests and time:** This issue fits my interests because I have experience with Python and RAG systems, and I want to continue improving my debugging and AI engineering skills. I also liked that the issue has a clear reproduction and an existing failing test, which makes the scope feel manageable within the time available.

**2. Verdict and other considerations:** The verdict correctly identified that the issue is active, available, and appropriately scoped for a newcomer. It also recognized that the existing xfail test provides a clear definition of what a successful fix should accomplish. Beyond the rubric, I considered which accepted issue would give me the most useful learning experience. I chose #69 over the other accepted issues because it involves debugging real application logic in a RAG component rather than making a narrower regex change.

**3. Anticipated difficulty:** I anticipate some difficulty because another student has already reproduced the bug and posted a fix plan. The Path Review house rule means this does not prevent me from working on the issue, but I may be working on the same problem at the same time as another contributor. Technically, I also expect that I will need to understand the parser's control flow before making the change rather than simply changing the line where the error occurs.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
