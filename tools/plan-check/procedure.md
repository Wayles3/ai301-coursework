# Procedure: how this skill grades a plan package

## Read order

1. Repo facts block first. Note the bug-report template asks and the contribution policy, specifically any AI-use rule (disclosure of tool and extent, or own-words requirement). These feed the conventions check.
2. Issue and Thread highlights. Note what the issue asks for (the single reported behavior), any maintainer or owner statement of cause or direction, and any open PRs or prior art.
3. Repro evidence block, before the plan. Note the observed behavior, every control run, any debug output, and which component the evidence implicates or rules out. Reading it before the plan means the plan is judged against the evidence and cannot frame it.
4. Candidate plan: Diagnosis, Scope, Files, Approach, Test plan, in that order. Note the stated cause, the in-scope and not-in-scope lines, files named, and the test outcome.
5. Candidate plan comment last. Note its approach, scope promises, whether it mentions thread direction and prior art, and any AI disclosure or own-words statement.

In eval mode use only the bundle text. In live mode, gather per the evidence guide and treat the drafts as the whole package.

## Evidence gathering

- Diagnosis and grounding: copy the plan's stated cause. List the repro evidence's controls and debug lines. Record whether any of them rules the stated cause out.
- Scope: list every Approach step and Files entry. Mark each as needed for the issue's ask or extra. Record any not-in-scope line.
- Executability: record the files and the single chosen approach, and any decisions left to build time.
- Test plan: record the command or test named and the expected observable result.
- Honesty: record unknowns named and any claim stronger than the evidence.
- Comms: record maintainer direction and open PRs from the thread, whether the comment engages each, the repo's AI-policy requirement, and whether the comment satisfies it.

## Check execution

- Execute the checks in rubric order. Grade each from the evidence recorded above, quoting the deciding fact; do not re-read the whole package for each check, only the part the rubric names.
- Grade `pass` only when the pass condition is clearly met. Grade `fail` when the failure condition is met. Grade `unclear` only when the package genuinely lacks the evidence the check needs; absence of a required element (no files named, no test outcome, no disclosure when the policy demands one) is a `fail`, not `unclear`.
- Grade the plan itself, not its polish. A short plan with the file, change and test is ready; a long confident plan can fail. Apply the rubric's stated condition even when the result feels wrong.
- If the procedure or rubric is silent on a case, note the gap in the summary; do not invent a step.

## Verdict assembly

- Apply the rubric's verdict rule: `accept` only if every required check is `pass`; any required `fail` or `unclear` gives `reject`. Preferred checks are reported but never change the verdict.
- Output a short readable summary (one line per check), then the JSON block with each check's grade and a one-line evidence quote or fact, and the verdict. For a reject, the evidence line of the failing check quotes the specific text or evidence that decided it.
