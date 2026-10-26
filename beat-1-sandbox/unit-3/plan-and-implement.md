# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Wayles3

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56#issuecomment-6406678902

Here's what I plan to do for this, built on my repro above (`main` at 99673c7).

**What I think is going on:** in `_extract_sections` (`ingestion/chunking/structural_chunker.py`), a content line is only added when `heading_stack or current_section_lines` is non-empty, and the last section is only saved when `heading_stack` is non-empty. With no `#` line, neither ever happens, so `sections` stays `[]` and `chunk()` returns `[]`. That matches my runs: 0 chunks for the plain text, 1 chunk once I add `# Title`. I got this from reading the code and my two runs; I haven't stepped through it in a debugger.

**Change:** if the document has no heading lines at all, `_extract_sections` returns the whole text as one section (empty path, level 0). Documents that have headings go through the same code as before. I'll also remove the `xfail` marker from `test_document_with_no_headings`, since CONTRIBUTING says the strict marker has to go with the fix.

**Files:** `ingestion/chunking/structural_chunker.py` and `tests/unit/test_structural_chunker.py`, nothing else.

**Not in scope:** text that comes before the first heading in a document that does have headings (it looks dropped to me too, but I haven't reproduced that), the unused `current_level` line, `SemanticChunker`, and the token limit.

**How I'll check it:** re-run my repro snippet (I expect `plain text, len 1000 -> 1 chunks` and the `# Title` case unchanged), and run `tests/unit/test_structural_chunker.py` with the marker removed (I expect 15 passed).

**One thing I wasn't sure about:** an empty `heading_path` for that one chunk. I looked for readers of `heading_path` and only found a docstring in `base.py`; I'll confirm in my run that it comes back as `""` and nothing breaks, and post what I see.

I don't see another PR open for #56. I can't promise a date for a PR yet.

(Disclosure: I'm using an AI assistant to help with this work. I ran the commands myself.)

---

## Your branch

**Branch**

fix/56-chunker-no-headings

**Evidence**

Repro steps from my Unit 2 comment on issue #56, run in a fresh Python 3.13.7 venv (tiktoken 0.14.0, pytest 9.1.1) from the repo root, on `main` at 99673c7 (before) and on the branch (after).

Before:

```
$ PYTHONPATH=. venv/bin/python repro.py
plain text, len 1000 -> 0 chunks
same text with '# Title' heading -> 1 chunks; heading_path: Title

$ venv/bin/python -m pytest tests/unit/test_structural_chunker.py -q --runxfail
FAILED tests/unit/test_structural_chunker.py::TestStructuralChunker::test_document_with_no_headings
1 failed, 14 passed
```

After (the change adds a no-headings fallback in `_extract_sections` and removes the xfail marker):

```
$ PYTHONPATH=. venv/bin/python repro.py
plain text, len 1000 -> 1 chunks
same text with '# Title' heading -> 1 chunks; heading_path: Title

$ venv/bin/python -m pytest tests/unit/test_structural_chunker.py -q
...............                                                          [100%]
15 passed

$ PYTHONPATH=. venv/bin/python -c "<chunk the plain text, print len, heading_path, text == whole document>"
1 '' True
```

The documents with headings behave as before. The no-heading document now gives one chunk containing the whole text, with an empty `heading_path`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20. This is the only full run that produced a score, and it is the one saved as `eval-run.txt`, whose agreement line reads: "agreement: 19/20 scored items  (bar: 18/20: PASS)". My first attempt crashed before grading anything because the `claude` command was not on my shell's PATH, so it has no score. After fixing that I ran the full eval once, it passed the bar, and the category tally was "clear-accept 6/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4". Afterwards I re-graded only pkg-14 with `--only` to read why it failed; that partial run is not a scored run, so the last scored run is still the 19/20 one.

**Package analysis**

pkg-14 (zellij#5174, OSC color responses leaking on session reattach). The gold label is accept. In the saved run my rubric said reject, failing it on "Stranger could start". The plan's diagnosis is well grounded (reattach is the only place it leaks, 0.44.1 is clean) and its test plan is concrete, but its Files section says "exact functions to be pinned in the PR after tracing the query issuance with debug logs", and my check fails a plan that "defers the real decisions to build time". That plan names the area (the attach path in `zellij-server` and the query issuance in `zellij-client`) and one approach, but no function. When I re-graded pkg-14 alone, the same rubric passed it, with the evidence line "only exact functions deferred to tracing", and the verdict was accept. So the check sits right on the edge for this package: whether naming an area but not a function counts as "deferring the real decision" depends on how the grader reads that clause, and the saved run read it strictly. I read pkg-14 as an arguable call and did not loosen the check to chase it.

**Check rationale**

The `Stranger could start` row of `tools/plan-check/rubric.md`, as it reads now:

> A stranger could begin work without asking the author: the plan names the concrete files or areas, and the chosen approach (one approach, not a menu). FAIL if the plan defers the real decisions to build time ("somewhere", "whichever is easier", "investigate first", "not sure which layer"), names no files, or is only intent. Terse is fine if the file, the change, and the approach are all named.

It reads this way because the failure I want to catch is a plan that cannot be started without asking the author, such as "somewhere" or a menu of approaches. It accepts "files or areas" so that a plan which names the right area but not the exact function can still pass, and pkg-14 shows the edge of that: the wording "exact functions to be pinned in the PR" still tripped the "defers to build time" clause.

**Trade-offs**

Keeping "defers the real decisions to build time" as a failure is what rejects the three unbuildable packages (pkg-10, pkg-17, pkg-18), which all matched their reject labels. The price is pkg-14: a correct plan that honestly says "I will pin the exact function after tracing" can be rejected, and the saved run did reject it, though the single re-grade accepted it. I did not change the rubric after the run, so there are no canaries to report. I left it because loosening it risks the unbuildable category, and 19/20 clears the bar with every category matched.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
