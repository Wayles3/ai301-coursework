---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this ready to submit? A PR package is a candidate pull request (its title, description, commit list, diff, and test evidence) read against the plan it claims to implement and the issue that plan belongs to. Grade one package per run. Never answer a different question, such as whether the fix is a good idea or whether the code is elegant, and never answer from gut feel: execute `procedure.md`, which applies `rubric.md` to evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

Run in exactly one of two modes.

- **Live mode:** the student's own submission, checked before it goes out. Inputs: their `plan.md` including its Deviations section, the branch diff (run `git diff main...HEAD`, three dots, in the working copy, and `git log main..HEAD --oneline` for the commits), the draft PR title and description, the test evidence they captured, and their issue read from the real repo (the thread, `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`). A student on the house issue reads the house plan and the house repro pack instead, and the same checks grade the same things. Gather issue-side evidence live with `gh`, the GitHub API, or the web.
- **Eval mode:** a package bundle is the whole world. Take every fact from the bundle text. Fetch nothing and read nothing else. Always grade a complete package: every check, the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo the pull request must target and the house rules there; apply those rules when reading evidence. Refuse to grade a PR for any other repo. If the scope's `Repo:` line is still an unfilled placeholder (it contains `<ORG>` or `<PATH-REVIEW-REPO>`), stop without grading and tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after the checks, read `voice-guide.md` and hold the outgoing PR title and description against its rules. Report each rule the text breaks in the summary, quoting the rule. The voice guide never changes the verdict on its own, because only a check in the rubric can do that. In eval mode, ignore `voice-guide.md` entirely: voice carries no gold labels, and the communication checks that apply to every package live in the rubric.

## Component reads

`rubric.md` defines the checks and the verdict rule. `references/evidence-guide.md` maps where each kind of evidence lives, in a bundle and live. `procedure.md` is the operating procedure: execute it exactly as written, in its read order. When the procedure is silent on a step, say so in the summary as a gap and do not improvise around it. If `rubric.md` has no checks, or `procedure.md` has no steps, refuse to grade and say which file is empty: a tool without a rubric and a procedure produces noise that looks like judgment.

## Verdict and output

The verdict is binary: `accept` means ready to submit, `reject` means hold. There is no third verdict and no score. Reservations belong in a check's evidence line, not in the verdict. A short readable summary (one line per check, plus voice-guide notes in live mode) may come first. End the reply with the fenced JSON block below, valid and last, with nothing after it. The eval harness parses the last fenced JSON block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: grade no check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: read the diff, the evidence, and the claims themselves against the plan and the stated standards. A terse complete PR can be ready, and a long confident description can hide drift.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary and leave the fix to the rubric.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. Where it is silent, treat an unverifiable claim as a failing one, because a PR you cannot verify from the package is not ready to submit.
