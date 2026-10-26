# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Where it lives: eval bundle: "Plan context" gives the plan's Files, scope statement, not-in-scope line and any deviation note; "Candidate PR" gives the diff (file headers and hunks), the commit list, and the description. Live: `plan.md` (including its Deviations section) in the course repo, the branch diff from `git diff main...HEAD` run in the working copy, the draft title and description, and `git log main..HEAD --oneline`.
- What good looks like: every changed file and hunk in the diff is named by the plan or by a deviation note, and every promised deliverable (a fix, a test, a docs change) shows up in the diff or is deferred in writing. The description's claims about what the PR contains ("exactly as planned", "adds docs", "nothing else changed") are checked against the diff itself. Silent drift is more than the plan (a new flag or setting, a refactor or rename, an unrelated edit) or less than the plan (a promised piece missing) with no note. A shortfall that the plan or description names with a reason is honest and not drift.

## Test evidence (harness category: not-tested)

- Where it lives: eval bundle: "Test evidence" under the Candidate PR, read against the "Plan context" repro evidence and test plan. Live: the "Testing" section of the draft description and the output you captured (before and after of the plan's repro, and the repo's check run such as `make test-unit`, `make lint`, `make typecheck`).
- What good looks like: the plan's own repro or named test appears with a command or input and its output before the change and after it, on the path the change touches, and the expected-after from the plan is met. If the plan names a suite or lint check, its result is visible. Not decisive: "tested locally", "tests pass", "works on my machine", output from the unchanged path (a control run or a different input than the repro), or a repro that is never re-run.

## Diff quality (harness category: unreviewable)

- Where it lives: eval bundle: the unified diff under "Candidate PR" (look at added `+` lines and changed hunks) and the commit list. Live: `git diff main...HEAD` and `git log main..HEAD --oneline`.
- What good looks like: the added lines are the fix and its test. Debris tells: debug prints or logging added for debugging, commented-out code, functions or imports added and never used, added TODO/FIXME notes, and hunks that only re-indent, reorder, or reformat lines the fix does not touch. Mechanical churn counts even when the underlying fix is right. A comment that explains why the fix works is not debris.

## Standards and comms (harness category: standards-wall)

- Where it lives: eval bundle: the "Repo facts" block (PR template asks, contribution policy, AI-use policy) read against the description under "Candidate PR", and the diff for any file the template requires (such as a changelog or release-notes entry). Live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the repo, read against the draft description.
- What good looks like: every section or checklist item the repo requires is present with real content (a linked issue such as `Closes #N`, a filled checklist, a required changelog entry present in the diff), and the description discloses AI assistance (tool and extent) where the policy requires it. Treat every package as AI-assisted. Not compliant: a section left as its placeholder comment or empty, a required checklist or issue reference omitted, a stated changelog entry missing from the diff, or a required disclosure absent. A repo that states no AI policy does not require a disclosure. Maintainer direction in the thread highlights (a stated cause or approach) is engaged or explained, which feeds only the preferred check.
