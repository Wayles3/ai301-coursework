# Plan: issue #56, StructuralChunker drops documents with no headings

Repo: codepath/pathreview-ai301-fa26-howard. Built from my Unit 2 repro on `main` at 99673c7.

## Diagnosis

`StructuralChunker.chunk()` returns `[]` for any non-empty text with no markdown heading line. My repro: a 1,000-character plain paragraph gives 0 chunks, and the same text with `# Title\n` in front gives 1 chunk with `heading_path: Title`. The only thing I changed between those runs was the heading line, so the heading is what matters.

From reading `_extract_sections` in `ingestion/chunking/structural_chunker.py`: a content line is only appended when `heading_stack or current_section_lines` is truthy, and the final section is only saved when `heading_stack` is truthy. With no heading, both stay empty, so `sections` is `[]` and `chunk()` has nothing to loop over. I have not stepped through it in a debugger; this comes from reading the code plus the two repro runs, which agree with it.

## Scope

In scope: a document with no heading lines at all should come back as one section, so `chunk()` returns at least one chunk.

Not in scope: text that appears before the first heading in a document that does have headings (my reading is that it is dropped too, but that is a separate behavior and I have not reproduced it); the unused `current_level` variable and its `# noqa: F841` line; any change to `SemanticChunker`, `SECTION_TOKEN_LIMIT`, or other chunkers.

## Files

- `ingestion/chunking/structural_chunker.py`: `_extract_sections` only.
- `tests/unit/test_structural_chunker.py`: remove the `@pytest.mark.xfail(strict=True, ...)` marker from `test_document_with_no_headings` (the repo's CONTRIBUTING says to, since the strict marker fails CI once the test passes).

## Approach

1. In `_extract_sections`, after the line loop, if `sections` is empty and no heading was ever seen, return one section: `content` is `text.strip()`, `path` is `[]`, `level` is 0.
2. Leave the heading-present code path unchanged, so documents with headings produce the same output as before.
3. Remove the xfail marker from `test_document_with_no_headings`.

The one thing I have not checked is that `chunk()` handles `path == []` cleanly: it would set `heading_path` to the empty string `""`. I will confirm that in my run, and by grepping for readers of `heading_path`. In the non-test code I looked at, only a docstring in `base.py` mentions it ("if applicable").

## Test plan

- Re-run my Unit 2 snippet from the repro comment. Before: `plain text, len 1000 -> 0 chunks`. After: `plain text, len 1000 -> 1 chunks`, and the `# Title` case still prints `1 chunks; heading_path: Title`.
- Run `python -m pytest tests/unit/test_structural_chunker.py -q` with the marker removed. Before the fix it is `1 failed, 14 passed` under `--runxfail`. After the fix I expect `15 passed`.
- Check that the single chunk's text is the whole document and that its `heading_path` is `""`.

## Deviations

Nothing changed; the plan held. The build was the single fallback in `_extract_sections` plus removing the xfail marker, the same two files I named. The one unknown I had listed, whether an empty `heading_path` causes trouble, turned out fine: the chunk comes back with `heading_path` `""` and the existing tests still pass (15 passed). Because nothing changed, the posted plan did not need an update.
