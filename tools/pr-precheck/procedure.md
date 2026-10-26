# Procedure: how this tool grades a PR package

## Read order

1. Repo facts first (eval) or the repo's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` (live). Note every PR template section, checklist item or reference the PR must carry, and any AI-use rule (disclose tool and extent, or own words). These feed the Template and disclosure check.
2. Issue and thread highlights. Note what the issue asks for and any maintainer statement of cause or direction.
3. Plan context (eval) or `plan.md` (live) before the diff. List, in writing, the plan's Files, its scope statement, its not-in-scope line, any deferral, any deviation note, and its test plan with the repro it names. Reading the plan first fixes the boundary the diff is judged against, so the diff cannot define its own scope.
4. The diff and commit list. For each changed file, note whether the plan or a deviation note names it, and list every added line that looks like debris.
5. The test evidence. Note the command or input, the before output, the after output, and any suite or check named.
6. The description last. Note each concrete claim about the change, any AI disclosure, and which template sections it fills.

In eval mode use only the bundle text. In live mode gather per the evidence guide and treat the drafts and diff as the whole package.

## Evidence gathering

- Plan fidelity: build a two-column list. Left: each changed file and each hunk. Right: the plan item or deviation note that covers it, or "none". Then list each deliverable the plan promised and mark it present in the diff, deferred in a note, or absent.
- Description claims: copy each factual claim from the description ("exactly as planned", "adds docs", "no other changes", "handles X") and find the diff lines or commit that back it, or mark it unbacked.
- Test evidence: record the plan's test plan and repro; record what the PR actually ran. Mark whether the before and the after both appear for that repro, whether it exercises the changed path or only a control, and whether a named suite or check has a visible result.
- Diff quality: scan only the added or changed lines for debug prints, commented-out code, added unused functions or imports, added TODO/FIXME, and re-indent or reorder hunks that do not touch the fix. Record each with the file.
- Template and disclosure: for each ask recorded in step 1, mark present with content, empty, or missing. Mark whether an AI disclosure appears when the policy requires one.
- Thread: record any maintainer direction and whether the description follows or explains it.

## Check execution

- Run the checks in rubric order, grading each from the evidence recorded above. Quote the deciding fact; do not re-read the whole package for each check, only the part the rubric names.
- Grade `pass` only when the pass condition is clearly met, and `fail` when the failure condition is met. Grade `unclear` only when the package lacks the evidence the check needs. A required element that is simply absent (no before/after, no disclosure when the policy demands one) is a `fail`, not `unclear`.
- A shortfall that the plan or description openly defers is not a fail on Diff matches the plan or Description matches the diff. Judge what the diff and the claims actually contain, not how polished the write-up is.
- If the procedure or rubric is silent on a case, note the gap in the summary and do not invent a step.

## Verdict assembly

- Apply the rubric's verdict rule: `accept` only if every required check is `pass`; any required `fail` or `unclear` gives `reject`. Preferred checks are reported but never change the verdict.
- Output a short readable summary (one line per check), then the JSON block with each check's grade, a one-line evidence quote or fact, and the verdict. When more than one required check failed, quote the first failing check in rubric order as the deciding one in the summary, and still list every grade in the JSON.
