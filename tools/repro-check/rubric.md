# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | Repro report's environment lines, read against the version in the issue body and the repo-facts release line | The report names the OS and the exact version or commit of the software under test, and that version matches the issue's target or the report states how it differs | required |
| steps-followable | Repro report's commands and inputs, in order, read together with the issue text | Every command is written out, and the input is fully determined by the report plus the issue text (shown, quoted, or pointed to exactly, such as "the two calls in the issue" or a file whose triggering contents are named), from an empty starting state to the trigger. Where the issue text states the input and options exactly (the strings, ranges, flags, or the construct that triggers the symptom), the report need not copy them: naming that source is enough, and a step that is a direct call of the issue's own inputs does not fail. Fails if a stranger would have to guess a command or an input the issue does not give, or would need something only the author has | required |
| behavior-matches-issue | Output excerpt in the repro report, read against the symptom in the issue body | If the report says it reproduced: the excerpt contains the same symptom the issue names (same error text or function, or same wrong-versus-expected output); a different error, an adjacent feature, or no output fails. If the report says it could not reproduce: it passes when it shows the output actually obtained for the issue's own scenario and compares it to the issue's expected and actual behavior | required |
| claims-backed-by-artifacts | The report's conclusions (reproduced, could not reproduce, also fails on another version) and any popularity claim, matched to the output the report shows | Each conclusion is supported by output shown or by concrete values named (for example "the control run reports lines 1, 4, 7, 10"), or is labeled unverified. Fails when a conclusion has nothing shown or named ("confirmed on version X" with no output, "fails on every machine") or the report makes sweeping claims (everyone, always, constantly). Incidental details such as how many times a shown command was run do not fail it. An honest could-not-reproduce with environment and the output obtained passes | required |
| claim-specific | Claim comment read against the issue | The claim names at least one fact only this issue has (its symptom, error, component or version) and would not fit a different issue unchanged | required |
| claim-promises-investigation-only | Claim comment's forward-looking sentences | Commits at most to investigating, testing or reporting back. Fails if it commits to delivering a fix or PR, or gives a date or "shortly/soon" | required |
| repo-conventions-met | Repo-facts block: bug template asks and contribution policy, read against both comments | The substantive data the template asks for (versions, platform, input, runnable steps, actual and expected behavior) appears in the report or is covered by equivalent environment lines. Reporter confirmation boxes (searched duplicates, read the docs) and bulk diagnostic dumps are not required. If the policy requires disclosing AI assistance in issue comments or reports, one comment states AI was used with the tool and extent, and silence fails; a disclosure rule that covers only pull requests does not apply. A stated policy is not otherwise violated | required |
| no-filler | Both comments | Neither comment is mainly "+1", "me too" or "claiming this" with no new information; each sentence adds a fact, a step or an observation | preferred |

## Verdict rule

Accept (ready to post) only if every `required` check passes. Reject if
any `required` check fails. `unclear` on a required check counts as
fail. Preferred checks never change the verdict. In live mode with a
claim-only draft, leave out the checks that need the repro report, as
SKILL.md says.
