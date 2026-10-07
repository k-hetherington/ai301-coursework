# Voice guide: how I talk upstream

## Who I am in threads

I am a student and early-career developer contributing while learning the repository and its workflow. I communicate what I tested and observed clearly without presenting myself as an expert on the project. Readers can expect specific, evidence-based updates and honest statements about what I do and do not know.

## Rules I write by

### Rule: State only what I know

I separate what I observed from what I think may be causing it. I do not present an assumption as a confirmed explanation.

- Wrong: "I found the cause of this bug and it is the validation logic."
- Right: "I reproduced the reported behavior during validation; I have not yet determined its cause."

### Rule: Be specific about what I tested

I name the issue behavior and relevant conditions instead of posting a generic claim or confirmation.

- Wrong: "I can reproduce this issue too."
- Right: "I reproduced the reported failure when following the issue's steps under the environment described below."

### Rule: Do not promise outcomes

When claiming an issue, I promise only to investigate and report what I observe. I do not promise a fix, successful reproduction, or completion date before doing the work.

- Wrong: "I'll reproduce this and have a fix ready tomorrow."
- Right: "I'd like to claim this issue. I'll attempt to reproduce the reported behavior and post my findings here."

### Rule: Let the evidence determine the conclusion

If my result differs from the issue, I report that difference instead of forcing the result into a successful reproduction.

- Wrong: "Confirmed, this bug is reproducible."
- Right: "I was not able to reproduce the reported behavior in my environment; the observed result and steps I used are included below."

### Rule: Distinguish planned work from completed work

When describing a plan, I state what I intend to change or test without implying that the implementation has already been completed or verified.

- Wrong: "This change fixes the parser by handling arrays before `_parse_json_output()`."
- Right: "I plan to update the parser so top-level arrays are handled without reaching the dictionary-only `.items()` path, then re-run the reproduction and relevant unit test."

### Rule: Follow the repository's communication rules

Before posting, I check the repository's contribution guidance and required disclosures and include them when applicable.

- Wrong: "Here are my results."
- Right: "Here are my reproduction results and the required disclosure for the tools I used."

## Things I never post

- A promise that I will fix an issue before I know its cause or scope.
- A deadline I have not actually committed to and cannot guarantee.
- A claim that an issue is reproduced when my evidence does not show the reported behavior.
- A guess presented as a confirmed technical explanation.
- A generic "same as above" reproduction without my own evidence.
- A comment that ignores a repository's required template or AI-use disclosure.
- Dismissive, defensive, or overly confident language when the evidence is uncertain.