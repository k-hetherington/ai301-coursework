# Plan: Issue #69 — Output parser crashes on a top-level JSON array fallback

## Diagnosis

I reproduced the failure at commit `f89c06fc3ff292df2a04a39ac51319d32a76b779`.

When `parse_review_output()` receives a top-level JSON array such as:

`["First feedback item", "Second feedback item"]`

`json.loads()` succeeds and returns a Python `list`. The raw-JSON path then passes that value to `_parse_json_output()`. `_parse_json_output()` currently expects a dictionary and iterates with `data.items()`, so the list raises:

`AttributeError: 'list' object has no attribute 'items'`

The existing `test_json_array_fallback` covers this case and is currently marked `xfail` for issue #69.

## Scope

In scope:
- Prevent top-level JSON arrays from reaching the dictionary-only `.items()` path.
- Handle a successfully decoded non-dictionary JSON value without crashing.
- Preserve the existing JSON-object parsing behavior.
- Update the existing regression test for issue #69 by removing its `xfail` marker once the behavior passes normally.

Out of scope:
- Redesigning the structure of parsed feedback.
- Changing how valid JSON objects are converted into `FeedbackSection` objects.
- Unrelated cleanup or the separately documented seeded defect in `parse_review_output()`.

## Files to change

- `rag/generator/output_parser.py`
  - Add handling so successfully decoded JSON that is not a dictionary does not reach `_parse_json_output()`'s `.items()` loop.

- `tests/unit/test_output_parser.py`
  - Remove the `xfail` marker from `test_json_array_fallback` after the parser handles the input without crashing.
  - Keep the regression focused on the behavior required by issue #69.

## Approach

1. Add a type check around the JSON parsing path so `_parse_json_output()` is only used for dictionary-shaped JSON.
2. Route a successfully decoded non-dictionary value through `_parse_plaintext_output(raw)` rather than calling the dictionary-only `.items()` logic.
3. Apply the same handling consistently to the code-fenced JSON and raw JSON paths so either form cannot trigger the same type mismatch.
4. Remove the issue #69 `xfail` marker from the existing regression test once the behavior passes normally.
5. Avoid changing the existing dictionary-to-`FeedbackSection` behavior.

## Test plan

1. Re-run the existing issue-specific test:

   `pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v`

   Expected after the fix: the test passes normally rather than xfails or raising `AttributeError`.

2. Re-run the output parser unit tests:

   `pytest tests/unit/test_output_parser.py -v`

   Expected: existing JSON-object and plaintext parsing tests continue to pass.

3. Run the repository's PR-time checks:

   `make check && make test-unit`

   Expected: linting, type checks, and unit tests complete successfully without introducing a regression.

## Risks and unknowns

The issue and existing test require graceful handling of a top-level JSON array but do not prescribe a new structured representation for array elements. I will therefore avoid inventing a new array-specific `FeedbackSection` format and use the parser's existing safe fallback behavior.

The same type assumption exists after both code-fenced JSON decoding and raw JSON decoding, so the implementation needs to cover both paths even though the Unit 2 reproduction exercised the raw JSON path.

## Deviations

None — implementation matched the posted plan.