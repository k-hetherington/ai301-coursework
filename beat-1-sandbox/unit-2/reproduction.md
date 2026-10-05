# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

k-hetherington

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-5987943696

Hi! I'd like to claim this issue. I'll work on reproducing the AttributeError that occurs when the output parser receives a top-level JSON array instead of an object. I'll document my environment, reproduction steps, and observed behavior here once I've completed the reproduction.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-5988222094

I reproduced this issue on the current `main` branch.

**Environment**

- Windows 10.0.19045.6466
- Git Bash
- Commit: `f89c06f`
- Python 3.14.6
- pytest 9.1.1
- structlog 26.1.0

**Setup**

From Git Bash:

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-s1.git
cd pathreview-ai301-fa26-s1
git checkout f89c06f
python -m venv .venv
source .venv/Scripts/activate
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
```

All reproduction commands below were run from the repository root with the virtual environment active.

**Reproduction**

First, I ran the existing test associated with issue #69:

```bash
python -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
```

The test was collected and reported:

```text
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback XFAIL
```

This is consistent with the test's current `xfail` marker for issue #69.

I then called `parse_review_output()` directly with a top-level JSON array:

```bash
python -c "import json; from rag.generator.output_parser import parse_review_output; raw=json.dumps(['First feedback item','Second feedback item']); print(parse_review_output(raw))"
```

The call produced:

```text
File "...rag/generator/output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
File "...rag/generator/output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
AttributeError: 'list' object has no attribute 'items'
```

The top-level JSON array is parsed into a list and passed to `_parse_json_output()`, where the call to `.items()` raises the reported `AttributeError`. This matches the behavior described in #69.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Initial smoke run (`--limit 3`): `2/3` scored items agreed.
- Targeted `pkg-01` rerun: `1/1` scored items agreed.
- First full-run attempt: `16/17` scored items agreed; `pkg-04`, `pkg-07`, and `pkg-11` errored because the Windows subprocess encoding could not encode characters in the package input.
- Targeted rerun of `pkg-04,pkg-07,pkg-11` after correcting the subprocess encoding: `3/3` scored items agreed.
- Targeted `pkg-20,pkg-02` rerun after revising the conventions check: `2/2` scored items agreed.
- Final full confirming run: `20/20` scored items agreed (`PASS`).

**Package analysis**

I analyzed `pkg-20`. The gold label was `reject`. Before I revised my conventions check, my rubric graded the package `accept`. The reproduction itself was strong: it recorded the environment and steps and showed the Ghostty mode-2031 behavior described by the issue. However, the repo facts stated that Ghostty requires all AI usage to be disclosed, including the tool and extent of assistance, while the candidate comments contained no AI-use disclosure. My original conventions check did not make that requirement explicit enough for the grader to reliably reject the package. I revised the check so repository communication and AI-disclosure requirements are part of the required evidence. After that revision, `pkg-20` was graded `reject`, matching the gold label.

**Check rationale**

I revised the `conventions` check. Its final form is:

> | conventions | The claim comment and repro comment read against the issue context, repo-facts block, repository contribution guidance, comment templates, and any AI-use disclosure requirements identified in `references/evidence-guide.md`. | Pass when the comments are specific to the issue, make no unsupported promises or claims, and satisfy every applicable repository communication requirement. If the repository requires disclosure of AI assistance, the candidate comments must contain the required disclosure, including any required tool or extent information; absence of a required disclosure fails this check. | required |

I revised this check after `pkg-20` was incorrectly accepted. The package had strong reproduction evidence, but Ghostty's repository policy required disclosure of all AI assistance, including the tool used and extent of assistance, and the candidate comments did not contain that disclosure. My earlier wording referenced repository conventions but did not make the consequence of a missing required AI disclosure explicit enough. I changed the pass condition so that a repository-required AI disclosure is part of the decision rule and its absence explicitly fails the check.

**Trade-offs**

After revising the conventions check to reject `pkg-20`, I re-ran `pkg-20` together with `pkg-02` as a canary using `--only pkg-20,pkg-02`. The result was `2/2` agreement: `pkg-20` changed to `reject`, matching its gold label, while `pkg-02` remained `reject`, also matching its gold label. This gave me evidence that making the disclosure requirement explicit fixed the case I intended to fix without changing the already-correct result for the wrong-target canary.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
