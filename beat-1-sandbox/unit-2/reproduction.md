# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`


Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Wayles3

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56#issuecomment-6207296464

Hi, I'd like to investigate this as a first contribution. I reproduced the empty result from `StructuralChunker.chunk()` on a ~1,000-character document with no headings (details in my next comment), so I plan to read `_extract_sections` to see why it returns nothing when there is no `#` line to start a section. I'll post what I find here, and I'm not promising a fix or a date yet.

(Disclosure: I'm using an AI assistant to help with this work. I re-ran the commands myself.)

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/56#issuecomment-6207437352

Reproduced on `main` at commit 99673c7.

**Environment:** macOS 26.6.2 (arm64), Python 3.13.7 in a fresh venv, tiktoken 0.14.0, pytest 9.1.1. I did not run the full `make setup` (Docker, DB); I only installed `tiktoken` and `pytest`, since the chunker doesn't use the services.

**Steps** (from a clean clone of this repo, repo root as working directory):

```
$ python -m venv venv && venv/bin/pip install tiktoken pytest
$ venv/bin/python - <<'PY'
from ingestion.chunking.structural_chunker import StructuralChunker
c = StructuralChunker()
plain = "This is plain text without any markdown headings. " * 20
print("plain text, len", len(plain), "->", len(c.chunk(plain, {"source": "test"})), "chunks")
with_heading = "# Title\n" + plain
r = c.chunk(with_heading, {"source": "test"})
print("same text with '# Title' heading ->", len(r), "chunks; heading_path:", r[0].metadata["heading_path"] if r else None)
PY
```

**Observed:**

```
plain text, len 1000 -> 0 chunks
same text with '# Title' heading -> 1 chunks; heading_path: Title
```

So the same text yields 0 chunks without a heading and 1 chunk once a heading line is added.

The xfail test also fails as the issue describes:

```
$ venv/bin/python -m pytest tests/unit/test_structural_chunker.py -q --runxfail
>       assert len(result) >= 1
E       assert 0 >= 1
FAILED ...::test_document_with_no_headings
1 failed, 14 passed
```

**Expected:** a document with no headings still produces at least one chunk. **Actual:** `[]`.

I only tested this one commit on macOS; I haven't looked at the cause yet.

(Disclosure: AI assistant used to help with this work; I ran the commands above myself and the output is what I got.)

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

2/3 (smoke run, `--limit 3`), then 15/20 (first full run), then 7/9 and 11/12 (partial `--only` re-grades after I revised checks, with canaries), then 20/20 (confirming full run with `--save-run`). The last score matches the agreement line in `eval-run.txt`: "agreement: 20/20 scored items  (bar: 18/20: PASS)". I also ran two small `--only` re-grades only to read the graders' evidence and did not record their scores.

**Package analysis**

pkg-05 (conda `EnvironmentSectionNotValid` message breaking JSON output). The gold label is accept. My rubric first rejected it on `steps-followable`, because the report only described the `env.yml` ("a valid `dependencies:` list plus a `category:` section") and never showed its contents. After I revised that check to accept inputs the issue text already names, pkg-05 still failed in two partial runs, and then passed in the confirming full run. I read it as an arguable call: the issue names the failing `category` section, so a stranger can build the file, but the report never wrote it out, so a strict grader reads it as a guess. It matters for my rubric because the same check is what keeps the unfollowable-comms packages rejected.

**Check rationale**

The `steps-followable` row of `tools/repro-check/rubric.md`, as it reads now:

> Every command is written out, and the input is fully determined by the report plus the issue text (shown, quoted, or pointed to exactly, such as "the two calls in the issue" or a file whose triggering contents are named), from an empty starting state to the trigger. Where the issue text states the input and options exactly (the strings, ranges, flags, or the construct that triggers the symptom), the report need not copy them: naming that source is enough, and a step that is a direct call of the issue's own inputs does not fail. Fails if a stranger would have to guess a command or an input the issue does not give, or would need something only the author has

It reads this way because my first version demanded that every input's content be shown, which rejected pkg-03 and pkg-12, both gold accepts whose inputs are written in the issue. I rewrote it to judge whether a stranger could follow the steps with the issue open, not whether the report copied the input again.

**Trade-offs**

Loosening `steps-followable` risked flipping packages that were correctly rejected. After the change I re-ran with `--only` on pkg-06, pkg-18 and pkg-19 (unfollowable-comms), pkg-13, pkg-14, pkg-15 and pkg-04 (no-evidence), pkg-02 and pkg-08 (wrong-target) and pkg-20 (disclosure). All still matched their gold reject labels, and the confirming full run agreed on all 20. What I accept it will miss: a report that points at an input the issue only half-describes, like pkg-05, can swing between runs.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
