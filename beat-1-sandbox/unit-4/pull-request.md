# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-howard/pull/92

Opened from `Wayles3:fix/56-chunker-no-headings` against `main` on `codepath/pathreview-ai301-fa26-howard`, with every section of the repo's PR template filled in, an AI-use disclosure, the before/after repro, and the outcome of `ruff`, `mypy`, `black --check` and the unit suite. When I opened it, the CI-green and integration-test boxes were unchecked with a reason (CI had not been confirmed, and I did not set up Docker or the database). CI then reported success on commit 6040f31 for `lint`, `typecheck`, `test-unit`, `test-integration` and `frontend`, so I checked both boxes in the description and noted that the integration tests ran in CI, not locally.

My own `pr-precheck` verdict on the draft before I opened it (live mode): **accept**. All six checks passed: Diff matches the plan (two files, the two in `plan.md`), Description matches the diff, Decisive test evidence (repro 0 chunks before and 1 chunk after; test file 1 failed, 14 passed before and 15 passed after; unit suite 375 passed before and 376 passed after), Reviewable diff, Template and disclosure, and Engages maintainer direction. The one tension it noted: CONTRIBUTING wants green CI, which the draft reported as unconfirmed rather than claiming it. Its voice-guide note was to make sure I had read the code and output myself before posting.

**Branch**

fix/56-chunker-no-headings

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

20/20. This was the only full run that produced a score, and it is the one saved as `eval-run.txt`, whose agreement line reads: "agreement: 20/20 scored items  (bar: 18/20: PASS)". Two earlier launches crashed before grading anything (the harness needs Python 3.10 or newer and my system Python is 3.9, and the `claude` command was not on my shell's PATH), so they have no score. I did not re-grade anything with `--only`.

**Package analysis**

pkg-20 (ghostty#13604, a mode-2031 color-scheme fix). The gold label is reject, and my tool said reject, so it agrees. The gold note says the fix is excellent and well evidenced, and the only fault is that the description has no AI-use disclosure while ghostty's stated policy requires disclosing all AI use. My tool rejected it for that reason, quoting "AI_POLICY requires disclosure of tool and extent of AI use; the description contains no AI disclosure" on Template and disclosure. It also failed Decisive test evidence, which the gold note does not: it read the before/after as annotation comments on an identical command with no real output, and "zig build test passes" as a bare claim. So I got the right verdict with one reason the instructor did not give. I think my evidence rule is stricter than the gold label on that package, and the verdict only matched because the disclosure failure was enough on its own to hold it.

**Check rationale**

The `Template and disclosure` row of `tools/pr-precheck/rubric.md`, as it reads now:

> Every section, checklist item or reference the repo-facts block says the PR must carry (for example a linked issue, a filled checklist, a changelog or release-notes entry shown in the diff) is present with real content. If the policy states that AI use must be disclosed, the description discloses it (the tool and how it was used). Treat every package as AI-assisted work. FAIL if a stated ask is empty, skipped or left as boilerplate, or if a required disclosure is missing. A repo that states no AI policy and asks for nothing the description lacks passes.

It reads this way because this category is the one the set builds a floor around, so the check has to see two things: required template content, and a stated AI-disclosure policy. I wrote "Treat every package as AI-assisted work" so the tool never has to guess whether the author used AI, and I wrote "A repo that states no AI policy and asks for nothing the description lacks passes" so that packages whose repos state no AI policy (for example pkg-13) are not rejected for lacking a disclosure. I kept it to what the repo-facts block states, because a disclosure demanded by a repo that never asked for one would be an invented rule.

**Trade-offs**

I did not change the rubric after the run, so there are no canaries to report; the first full run agreed on all 20 with every category matched (`standards-wall 2/2`), and I left the components alone because loosening or tightening any check could flip a package that already agreed. What I accept the tool may miss: the strict reading of Decisive test evidence that pkg-20 shows (it failed a package on evidence the instructor called decisive) means a PR with real but loosely formatted output could be held for a reason a human reviewer would not give. The cost of that is a false reject, not a false accept, which is the safer way for a pre-submission check to err.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
