# Evidence guide: where proof lives in a reproduction package

In eval mode the package is one bundle with these parts: the issue
context (title, body, thread highlights), the repo-facts block (bug
report template asks, contribution policy, release info), the candidate
claim comment, and the candidate repro report. In live mode the issue
side is the issue page on GitHub plus the repo's CONTRIBUTING.md,
AI-policy files and issue template; the candidate side is the student's
draft comment files, and nothing else in their working directory.

## Environment

- Where it lives: the repro report's environment lines (OS, version of
  the tool or project under test, how it was installed or which commit,
  runtime versions). Compare them to the version the issue was filed
  against, found in the issue body or its template fields, and to the
  repo-facts "latest release" line.
- What good looks like: the report names the version actually tested,
  and that version either matches the issue's target or the report says
  how it differs (for example "issue filed on 4.53.2, I tested 4.53.3").
  A report that names no version, or only an OS, is not recorded.

## Steps

- Where it lives: the commands, inputs and actions in the repro report,
  in the order a reader would run them.
- What good looks like: a stranger with only the report could go from
  an empty starting state to the trigger. Every command is written out,
  every input file's content is shown or quoted, and no step depends on
  something unstated ("set up the project", "use the usual config").

## Behavior shown

- Where it lives: the output excerpts, logs, stack traces or
  screenshot descriptions inside the repro report, read against the
  symptom in the issue body (the error text, the wrong value, the
  crash location).
- What good looks like: the excerpt contains the same symptom the
  issue names: same error message or function, or same wrong output
  versus the same expected output. An excerpt that shows a different
  error, a neighboring feature, or no output at all is an adjacent
  behavior and does not show the issue. A control run that changes one
  variable and behaves differently is strong support.

## Honesty

- Where it lives: every factual claim in the repro report and the
  claim comment: "I ran it N times", "also fails on version X", "every
  machine", "always". Each is matched against the artifacts the report
  actually shows.
- What good looks like: each claim has an artifact next to it, or is
  stated as unverified. Sweeping words (everyone, always, constantly)
  with nothing shown fail. A report that says it could not reproduce,
  with its environment and the output it got, is honest and passes.
  Confidently reporting the issue's symptom when the shown output
  differs is not honest, however polished.

## Comms

- Where it lives: the claim comment, read against the issue; the repro
  report and claim comment read against the repo-facts block: the bug
  template's asks and the contribution policy, including any AI-use
  disclosure rule.
- What good looks like: the claim names specifics only this issue has
  (the symptom, the component, the version), and commits only to
  investigating, never to a fix or a date. If the repo-facts policy
  requires disclosing AI assistance, one of the two comments states
  that AI was used, with the tool and how much; silence fails. Any
  information the bug template asks for appears in the report.
  "+1", "me too", and "claiming this" with nothing else are boilerplate
  and carry no information.
