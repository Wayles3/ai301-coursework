# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives: the plan's cause is under "Diagnosis" in the Candidate plan (live: the draft plan.md). The behavior it must explain is in the "Repro evidence" block: numbered steps, control runs (same input with one thing changed), `--debug`/log/trace output, and the Expected/Actual summary. The Issue body and Thread highlights are secondary.
- What good looks like: every named component in the diagnosis is one the repro evidence implicates, and no control run or debug output in the evidence contradicts it. Controls are the strongest evidence: if the failure persists with the blamed component absent, or the blamed component works in a control, the diagnosis is wrong however confident it sounds. A diagnosis that never cites the evidence and names a different component than the repro isolates is ungrounded.

## Scope

- Where it lives: the plan's "Scope" statement (in scope / not in scope), the "Files" list, and the numbered "Approach". Compare them with what the Issue actually asks for.
- What good looks like: a few named files, one fix, an explicit not-in-scope line, and any adjacent work deferred rather than done. A drive-by rewrite shows up as Approach steps or Files that the issue never asked for: refactors, migrations, new options or settings, new subsystems, test-harness changes, or several fixes bundled into one plan.

## Executability

- Where it lives: "Files", "Approach", and the Diagnosis in the Candidate plan.
- What good looks like: concrete file paths or named functions, one chosen approach, steps in order. A stranger can open the named file and know what to change. Unbuildable plans use words like "somewhere", "whichever is easier", "investigate", "maybe", or leave the layer or file undecided.

## Test plan

- Where it lives: "Test plan" in the Candidate plan, to be matched against the numbered steps and artifacts in the Repro evidence block.
- What good looks like: re-runs a named repro step or adds a named regression test and states the expected observable result (output, exit code, color, a failing-then-passing test). A vague test plan states a feeling or a blanket suite run without an outcome for this fix.

## Honesty

- Where it lives: the plan's Approach and Test plan (stated unknowns, "will verify", "open question", deferrals with reasons) and the plan comment.
- What good looks like: unverified items are labelled and given a way to be checked; deferrals give reasons; claims of verification match what the repro evidence shows. False confidence asserts untested results or a certain root cause the evidence does not establish. Live mode: honest mid-build deviations are recorded in the plan.md deviations section.

## Comms

- Where it lives: the "Candidate plan comment", read against "Thread highlights" (maintainer/owner direction, prior PRs, prior art) and the "Repo facts" block (bug-report template asks, contribution policy and any AI-use policy).
- What good looks like: the comment follows the maintainer's stated culprit or direction, acknowledges open PRs and prior art, matches the plan it summarizes, and includes whatever the repo-facts contribution policy requires: an AI-use disclosure (tool and extent) where the policy demands it, and the contributor's own voice where the policy demands that. Boilerplate that ignores the thread, or a comment that omits a stated policy requirement, is a comms fail even when the plan itself is excellent.
