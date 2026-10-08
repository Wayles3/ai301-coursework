# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56

**Verdict output**

Live-mode run on 2026-10-07 with `claude "issue-select: grade these candidate first issues: <URL> <URL> <URL>"` over issues #56, #57 and #63 of `codepath/pathreview-ai301-fa26-howard`, pasted verbatim. Issue #56 is my chosen issue; its verdict is `accept` in the final JSON block.

````text
I couldn't run `gh` here because those commands need approval, so I graded from the public GitHub pages. All three issues are accepted. Here is the ranking.

**Ranked read-out**
1. **#57, tech detector counts `node_modules/` and `build/` files.** It is a clear product-code bug with a repro. Two failing tests are named, `test_node_modules_excluded` and `test_build_directory_excluded`, and the expected result is stated (Python, not JavaScript). That makes it a bounded fix with an obvious "done", which matches your preference for well-defined tasks you can finish and have reviewed.
2. **#56, structural chunker drops documents with no headings.** It is also real product code with a failing test named (`test_document_with_no_headings`). It ranks lower because the issue offers two fixes ("single block or fall back to another strategy"), so there is a small design choice to settle in review.
3. **#63, README scorer test fixture is too short.** It is bounded and safe, but it only touches a test fixture, so it gives you the least product-code practice.

All three were opened by `Aburke225` on Sep 14, 2026. Each carries `bug`, `good first issue` and `tier-1` labels, has no assignee, and shows no linked PRs.

**Repo checks (same for all three)**
- **Maintainer commits recent:** pass. The newest commits are from Sep 16, 21 days ago, by `Aburke225`, a human account.
- **Maintainer responds:** pass. I couldn't see any maintainer replies, but all the sampled issues were opened on Sep 14, only 23 days ago. The rubric treats fewer than 3 issues older than 30 days as too new to judge.
- **Repo not archived:** pass. There is no archived banner.
- **Repo in use:** pass. There is no release, but the newest commit is from Sep 16, within 90 days and human-authored. I didn't confirm the last-push date directly. The Sep 16 commit puts it at least that recent.
- **AI policy allows assisted work:** pass. `docs/CONTRIBUTING.md` says nothing about AI, and silence passes.

**Issue checks**
- **Scope is bounded:** pass for all three. None is an umbrella issue, a support question or a design debate, and no maintainer says it touches core internals.
- **Work is wanted:** pass for all three. Each is a bug with a `good first issue` label, and none was opened by a bot.
- **No existing claim:** pass for all three. There are no assignees or linked PRs, and none of the 6 open PRs (#73–#79) targets these issues. Under the Path Review house rule, classmates' claim comments don't block an issue anyway.
- **Preferred checks:** all three pass. They carry the `good first issue` label, state an expected result, and are under 12 months old.

**Caveats**
- **Missing evidence:** the pages didn't show author association badges or comment bodies. The issue list showed 2 comments on #57, but the issue page itself showed none. This doesn't change any verdict.
- **PR link not verified:** the PR list didn't reveal which issues PRs #73–#79 link to. I'm treating the "no linked PRs" panels on the issue pages as authoritative.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit Sep 16, 2026 (21 days ago), authored by Aburke225 (human)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "All sampled issues opened Sep 14, 2026 (<30 days old), so too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "No archived banner on repo page"},
      {"name": "Repo in use", "grade": "pass", "evidence": "No release, but newest commit Sep 16, 2026 is within 90 days and human-authored"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Single bug in tech_detector.py excluding node_modules/ and build/; two named failing tests; no debate"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Labeled bug + good first issue; opener Aburke225 is not a bot"},
      {"name": "No existing claim", "grade": "pass", "evidence": "No assignees; Development: 'No branches or pull requests'; house rule ignores classmate claim comments"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI language; silence passes"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Labeled good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "Expected primary_language Python vs observed JavaScript, plus named tests"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened Sep 14, 2026, under 12 months old"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit Sep 16, 2026 (21 days ago), authored by Aburke225 (human)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "All sampled issues opened Sep 14, 2026 (<30 days old), so too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "No archived banner on repo page"},
      {"name": "Repo in use", "grade": "pass", "evidence": "No release, but newest commit Sep 16, 2026 is within 90 days and human-authored"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "StructuralChunker.chunk() returns [] for heading-less docs; one bug, failing test test_document_with_no_headings named"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Labeled bug + good first issue; opener Aburke225 is not a bot"},
      {"name": "No existing claim", "grade": "pass", "evidence": "No assignees; Development: 'No branches or pull requests'; no comments; house rule ignores classmate claims"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI language; silence passes"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Labeled good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "Expected: chunk as single block or fall back to another strategy; repro gives 0 chunks"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened Sep 14, 2026, under 12 months old"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit Sep 16, 2026 (21 days ago), authored by Aburke225 (human)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "All sampled issues opened Sep 14, 2026 (<30 days old), so too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "No archived banner on repo page"},
      {"name": "Repo in use", "grade": "pass", "evidence": "No release, but newest commit Sep 16, 2026 is within 90 days and human-authored"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Fixture has ~51 words but test asserts >100; extend fixture or fix assertion in one test"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Labeled bug + tests + good first issue; opener Aburke225 is not a bot"},
      {"name": "No existing claim", "grade": "pass", "evidence": "No assignees; Development: 'No branches or pull requests'; no comments; house rule ignores classmate claims"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI language; silence passes"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Labeled good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "Repro: pytest tests/unit/test_readme_scorer.py -q fails 'assert 51 > 100'; fix must make test validate intent"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened Sep 14, 2026, under 12 months old"}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

I did one full run: `19/20 scored items (bar: 18/20: PASS)`, with categories `claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 4/4`. That is the agreement line in the `eval-run.txt` I committed. I also did one partial re-run, `--only issue-19`, to read the per-check reasoning; it graded `issue-19: reject` again and, being partial, wrote no file. So my scores in order are: 19/20 (full, saved), then 0/1 on the single issue-19 re-run.

**Issue analysis**

`issue-19` (zxcalc/zxlive#517, "Selecting large subgraphs in proof mode freezes the UI"). My rubric said **reject**; the gold label is **accept** (note: "maintainer-diagnosed performance bug with named causes, unclaimed"). The harness reported `failed: Scope is bounded, Acceptance criteria stated (preferred)`. The grader's own evidence on the scope check was: "Body lists two separate causes plus three additional suggestions (multiprocessing, collapsed-category matching, threaded apply): a list of sub-items meant to be split up." So my umbrella clause, "the issue is an umbrella or tracking issue (a list of sub-items meant to be split up)", fired on the shape of the body: two numbered lists. But the issue is a single titled bug with one symptom (the UI freezes), opened by a Collaborator, labeled `Type: bug` and `Priority: High`. The two "potential causes" are diagnosis of that one bug, and the "additional suggestions" are optional ideas, not separate work items. My rubric read the list formatting as an umbrella instead of asking whether the title and symptom describe one piece of work. The other 19 issues agreed, and every other umbrella issue (issue-05, issue-10) was rejected correctly.

**Check rationale**

The check is **Scope is bounded**. Its current wording in `rubric.md`: "None of: the issue is an umbrella or tracking issue (a list of sub-items meant to be split up), a maintainer says the fix touches core internals, the thread shows the design still being debated with no maintainer decision, or it is a pure usage/support question. A terse body alone does not fail this check". I wrote it as a list of four disqualifiers taken from the evidence guide's description of the scope family, because those are the four things that actually made issues in the eval set unsuitable for a newcomer (issue-05 and issue-10 are umbrellas, issue-15 is a long design debate, issue-20 hides a product decision). The last sentence is there so a short but well-aimed issue, like the maintainer-filed bugs in zxlive, is not rejected just for being brief.

**Trade-offs**

This check gives up precision on issues that contain lists. Because the umbrella clause keys on "a list of sub-items", it over-fires on a real single bug whose body numbers its causes, which is exactly what happened on issue-19 (gold accept, my rubric reject), the one disagreement in my final run. I accepted that: a rubric that is too strict only costs me a good issue, while one that is too loose sends a newcomer into a tracking issue like issue-05 or issue-10, and tightening the clause to fix issue-19 would risk letting those through. I chose not to change it after the 19/20 run since I was already above the bar of 18 and the other 19 issues, including all four scope-category issues (`scope 4/4`), agreed; a rewrite would have needed another full ~$4 run to prove nothing else moved. Nothing else changed because I did not edit the rubric after the full run.

---

## Selection rationale

**Selection rationale**

1. **Fit.** I picked #56 because it hits a critical edge case in core product code: `StructuralChunker.chunk()` returns an empty list whenever a document lacks headings, causing the document to silently drop out of the RAG index. The issue provides a single-call reproduction script alongside the specific failing test, making the scope and definition of "done" clear upfront. As a senior CS student who maintains my own iOS app and ships production code, I wanted a well-defined fix that lets me practice the full open-source workflow, from issue triage to pull request submission, rather than getting bogged down in open-ended system design. Since the fix is isolated to a single function, it comfortably fits the timeframe I have for this assignment.

2. **What the verdict caught vs. my personal trade-offs.** The evaluation skill accurately verified that the repository is active (recent human commits as of mid-September 2026), the issue was tagged good first issue by a core collaborator, no PR or assignee is attached, and the contributing doc does not restrict AI-assisted contributions. However, my manual review factored in additional context the automated check missed:
   - I preferred fixing actual pipeline logic over updating test fixtures (which ruled out #63).
   - I prioritised unclaimed issues to avoid redundant effort. I chose #56 over #57, which the skill ranked first, because a classmate had already posted a reproduction and claimed #57.
   - I screened out #68, #60, and #54 after identifying open pull requests from classmates on each, even though course rules technically permit overlapping attempts.

3. **Anticipated risk and difficulty.**
   - *Collision risk:* because it carries the good first issue label, another classmate might submit a PR or claim it while I'm working. Per course guidelines, I plan to post my claim immediately and proceed regardless.
   - *Design ambiguity:* the issue leaves the fallback behavior open, either returning a single top-level chunk or applying an alternative chunking strategy. I'll need to make a reasoned design choice and justify it in the PR notes.
   - *Maintainer latency:* maintainer activity on open threads has been quiet, so I anticipate a potential wait for final code review after opening the PR.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
