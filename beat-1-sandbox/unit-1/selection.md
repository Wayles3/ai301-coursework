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

Live-mode run of `issue-select` on 2026-10-07 over issues #56, #57 and #63 of
`codepath/pathreview-ai301-fa26-howard`. Path Review house rule applied: classmates' claim
comments do not block an issue.

**RANKED READ-OUT**

Accepted (fit order)
1. #56 Structural chunker silently drops documents that contain no headings
   Fit: a bounded product-code bug with a one-call repro and an existing failing test
   (test_document_with_no_headings); needs no architectural change and has zero
   comments or competing PRs, so it is a clean issue -> PR -> review loop.
   Preferred checks: maintainer-labeled PASS, acceptance criteria PASS, not stale PASS.
2. #57 Tech detector counts vendored and build-output files
   Fit: also a bounded bug with a repro and named failing tests, but one classmate
   (jjoiles) has already posted a claim comment and a reproduction; ignored per the
   house rule, though it makes this the more crowded of the two.
3. #63 README scorer test fixture is too short for its own word-count assertion
   Fit: bounded and safe, but it is a test-fixture fix rather than product code, so it
   gives the least practice shipping real behavior.

Rejected: none.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (human), 21 days before 2026-10-07"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "Sampled issues were opened 2026-09-14, 23 days ago, so fewer than 3 are older than 30 days: too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "Repo in use", "grade": "pass", "evidence": "No release, but last push 2026-09-16 and newest default-branch commit 2026-09-16 by human Aburke225, both within 90 days"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "One function (StructuralChunker.chunk) returns [] for heading-less docs; no umbrella list, no design debate, not a support question"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Bug report opened by Aburke225 (COLLABORATOR), labeled good first issue"},
      {"name": "No existing claim", "grade": "pass", "evidence": "assignees: none; no linked PR; 0 comments"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no statement on AI or generated contributions; silence passes"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Opened by COLLABORATOR; labeled good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "Expected: chunk as a single block or fall back to another strategy; failing test test_document_with_no_headings named"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened 2026-09-14, under 12 months old"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (human)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "Sampled issues opened 2026-09-14, under 30 days old: too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "Repo in use", "grade": "pass", "evidence": "Last push and newest human commit 2026-09-16, within 90 days"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Add node_modules/ and build/ exclusions in tech_detector.py; one file, one repro"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Bug opened by COLLABORATOR, labeled good first issue"},
      {"name": "No existing claim", "grade": "pass", "evidence": "No assignee or linked PR; comments by classmate jjoiles (2026-10-05) are claim comments, ignored under the Path Review house rule"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md silent on AI"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Opened by COLLABORATOR; good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "Expected primary_language 'Python'; tests test_node_modules_excluded, test_build_directory_excluded named"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened 2026-09-14"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63",
    "checks": [
      {"name": "Maintainer commits recent", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (human)"},
      {"name": "Maintainer responds", "grade": "pass", "evidence": "Sampled issues opened 2026-09-14, under 30 days old: too new to judge"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "Repo in use", "grade": "pass", "evidence": "Last push and newest human commit 2026-09-16, within 90 days"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Extend one test fixture (~51 words vs > 100 asserted) or correct the assertion"},
      {"name": "Work is wanted", "grade": "pass", "evidence": "Bug opened by COLLABORATOR, labeled good first issue"},
      {"name": "No existing claim", "grade": "pass", "evidence": "assignees: none; no linked PR; 0 comments"},
      {"name": "AI policy allows assisted work", "grade": "pass", "evidence": "docs/CONTRIBUTING.md silent on AI"},
      {"name": "Maintainer authored or labeled", "grade": "pass", "evidence": "Opened by COLLABORATOR; good first issue"},
      {"name": "Acceptance criteria stated", "grade": "pass", "evidence": "pytest tests/unit/test_readme_scorer.py -q should pass; 'assert 51 > 100' is the failure"},
      {"name": "Not a stale label", "grade": "pass", "evidence": "Opened 2026-09-14"}
    ],
    "verdict": "accept"
  }
]
```

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

1. **Fit.** I chose #56 because it is a bounded bug in real product code: `StructuralChunker.chunk()` returns an empty list for a document with no headings, so the whole document silently drops out of the RAG index. The issue gives a one-call reproduction and names the failing test, so I can see what "done" looks like. That is the kind of well-defined fix I want, since I'm a senior CS student who has shipped code at OneMain Financial and maintains my own iOS app, and I want practice with the issue, pull request and review workflow on someone else's codebase rather than open-ended design work. The fix is probably one function, so it fits the time I have for this course.

2. **What the verdict caught, and what I weighed myself.** The skill correctly confirmed that the repo is alive (human commits on 2026-09-16), the issue was opened by a Collaborator with a good first issue label, nobody is assigned, there is no linked PR, no comments, and the contributing doc says nothing banning AI-assisted work. It did not know that I wanted product code rather than a test-fixture change (#63), or that the time I'd have to spend might favor an issue where nobody else is working, which is why I ranked #56 above #57, where a classmate already posted a claim comment and repro. I also first looked at #68, #60 and #54 and set them aside after finding open classmate PRs on all three, even though the house rule says those claims do not block.

3. **Anticipated difficulty in claiming it.** The main risk is that the issue is a good-first-issue in a class repo, so a classmate may claim or open a PR on it before I do; the house rule says that is fine and I should claim anyway. The harder part is design: the issue allows either a single-block chunk or "another strategy", so I will need to pick one and justify it. Also the maintainer has not yet replied on anything in the sampled threads, so I may wait a while for review.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
