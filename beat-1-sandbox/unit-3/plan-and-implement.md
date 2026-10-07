# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

k-hetherington

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-6030838729

I reproduced issue #69 at `f89c06f`. A top-level JSON array is successfully decoded to a Python list, but the raw-JSON path passes it to `_parse_json_output()`, which assumes a dictionary and calls `.items()`, raising `AttributeError`.

My plan is to keep `_parse_json_output()` limited to dictionary-shaped JSON and route successfully decoded non-dictionary JSON through `_parse_plaintext_output()`. I’ll apply the handling consistently to the code-fenced and raw JSON paths, preserve the existing JSON-object behavior, and remove the `xfail` marker from `test_json_array_fallback` once it passes normally.

I’ll verify the change with the existing issue-specific test, the output-parser unit tests, the repository's PR-time checks, and my Unit 2 top-level-array reproduction.

---

## Your branch

**Branch**

fix/69-json-array-fallback

**Evidence**

Before:

```bash
$ python -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback XFAIL [100%]
============================== 1 xfailed in 1.06s ==============================
```

The direct reproduction showed the reported failure:

```bash
$ python -c "import json; from rag.generator.output_parser import parse_review_output; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"
Traceback (most recent call last):
  File "...rag\generator\output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
  File "...rag\generator\output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
                      ^^^^^^^^^^
AttributeError: 'list' object has no attribute 'items'
```

After:

```bash
$ python -c "import json; from rag.generator.output_parser import parse_review_output; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"
2026-10-06 21:36:23 [info     ] plaintext_output_parsed        content_length=47
[FeedbackSection(section_name='general_feedback', content='["First feedback item", "Second feedback item"]', confidence=0.7, suggestions=[])]
```

The issue-specific test now passes normally:

```bash
$ python -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED [100%]
============================== 1 passed in 0.30s ===============================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Initial 3-package smoke run: 2/3 agreement.
- Targeted 3-package rerun after rubric/procedure revisions: 3/3 agreement.
- Final full evaluation: 18/20 agreement.

Final saved run:

`agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

I analyzed `pkg-02`, a `clear-accept` package. The gold label was `accept`, but my rubric decided `reject`. The evaluation output identified the failed checks as `scope` and `uncertainty`:

`pkg-02  clear-accept       accept  reject   NO     failed: scope, uncertainty`

My rubric read the package as a rejection because both checks are required, and my verdict rule states that a package is accepted only when every required check passes. The `scope` check asks whether the implementation is bounded to the issue and whether every planned change is connected to the diagnosed problem or its necessary tests. The `uncertainty` check requires uncertain claims to remain identified as uncertain and treats an unresolved unknown as a failure when the implementation or expected test result depends on resolving it first. For `pkg-02`, the evaluator determined that the plan did not satisfy those two required checks, so the rubric produced `reject` even though the gold label was `accept`.

**Check rationale**

I chose the `scope` check. Its final pass condition is:

> Pass when the implementation work is bounded to the issue and every planned change has a clear connection to the diagnosed problem or its necessary tests. Investigation or auditing for related risk does not count as scope creep when the plan keeps resulting unrelated fixes out of scope. Unrelated refactoring or behavior changes fail this check unless the evidence shows they are necessary to the fix.

I revised this check to distinguish between investigation and actual implementation scope. A developer may need to investigate or audit related behavior to understand the risk of a proposed change, but that does not necessarily mean the plan proposes fixing everything discovered during that investigation. I therefore chose to judge scope based on the changes the plan actually proposes to implement. At the same time, the check still rejects unrelated refactoring or behavior changes unless the evidence establishes that they are necessary to the issue being fixed.

**Trade-offs**

The trade-off in my `scope` check is that it allows investigation or auditing beyond the immediate implementation area as long as unrelated fixes remain out of scope. This makes the rubric less likely to reject a good plan simply because the developer investigates related behavior, but it also means the check must distinguish carefully between investigation and proposed implementation.

I accepted that trade-off because the final evaluation still correctly rejected all four `scope-creep` packages:

`scope-creep 4/4`

This showed that allowing bounded investigation did not prevent the rubric from identifying the evaluated plans that actually proposed out-of-scope changes.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
