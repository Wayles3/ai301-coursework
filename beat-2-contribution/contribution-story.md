# Contribution: Filter audit log for a process

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Adewale Abodunde
**GitHub Username:** Wayles3
**Issue:** https://github.com/cabotage/cabotage-app/issues/375
**Pull Request:** https://github.com/cabotage/cabotage-app/pull/509

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: Built an issue-scout with my own search queries, then fixed three rubric gaps**

I replaced my unit 5 grader with the issue-scout skill and wrote a search strategy: three `gh search issues` queries (Swift good-first-issue bugs, Swift good-first-issue, TypeScript help-wanted bugs) plus ranking filters traced to my fit profile. My first scan graded five issues and accepted all five, but it let through flisk-sh/flisk#4426, which was blocked on an upstream release, and my "fewest comments first" order filled the top five with TypeScript and Go issues and no Swift. Grading my own picks exposed two more gaps: the rubric had no "issue is open" check (spotatui#822 was already fixed and closed), and a dependabot burst made it reject christianliebel/paint#1067 because its last five commits were all bot bumps. I added a "blocked on upstream" condition to "Scope is bounded", a required "Issue is open" check, and a rule to skip dependency-bot commits. Regrading #1067 then flipped it to accept, so that fix is tested. The upstream-blocked fix and the Swift-first ordering are untested because I never rescanned. Across seven graded issues, two were rejected for stale open PRs (ArduPilot #32090 and #31107) and I chose cabotage/cabotage-app#375, which passed every required check.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched with my own issue-scout: three `gh search issues` queries built from my fit profile (Swift good-first-issue bugs, Swift good-first-issue, TypeScript help-wanted bugs), ranked by fewest comments. The scan surfaced flisk and Lelu issues and no Swift ones, so I also graded issues I found on the Issue Selection site: ArduPilot #32090 and #31107 (rejected, stale open PRs), spotatui #822 (rejected, already closed), paint #1067 (rejected, then accepted after I fixed the rubric), Altinn dialogporten #2427 (accepted but vague, "Implementation: TBD") and cabotage-app #375 (accepted, every required check passed). I chose #375 because it is a bounded, well-specified feature on a Python/Flask codebase: the audit data already exists and the maintainer's thread names the two pieces (a filter on `/audit` and a small icon on the process cards). It fits my profile of bounded work I can finish and have reviewed, with no architectural change, and I want practice with the issue, PR and review workflow on a real team codebase. The scout's verdict on it was accept.

My claim comment link: https://github.com/cabotage/cabotage-app/issues/375#issuecomment-6958956958 (posted 2026-11-17). My tooling session could not post it for me, so I posted it myself.

Honest read of the scout: it held up on the repo-health checks (it correctly rejected the two ArduPilot issues for stale open PRs), but it fell short on real repos in four ways. It accepted an issue blocked on an upstream release, it had no "issue is open" check, a dependabot burst made it reject a live repo, and its ranking order buried every Swift result. I patched all four in the rubric and search strategy. The dependabot fix and the "issue is open" check were tested; the other two were not. One caveat it could not settle for #375: the repo looks single-maintainer, and the maintainer's fast replies were on his own issues, so I do not know how quickly he reviews outside PRs.

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric), run as a scan plus direct-URL grades of my picks.
- What it produced: a scan that accepted all five of its top picks, and a read-out per pick; for #375 an accept with every required check passing, a weak pass on acceptance criteria, and a note that maintainer responsiveness to outsiders was unproven.
- Difficulties: the blocked-upstream miss, no open-issue check, the dependabot misread, and the all-TypeScript ordering. The headless runs also needed tool permissions I had to grant narrowly (`gh`, `python3`).
- What changed: three rubric fixes (blocked on upstream, issue is open, skip dependency-bot commits) and a Swift-first ordering in search-strategy.md. I did not rescan, so the ordering and blocked-upstream fixes are untested.

---

## Understanding the Issue

**Problem Description**

Cabotage's audit log lists what happened to an application, but the only filters are verb and object type. There is no way to see the history of one Procfile process, such as `web` or `worker`, even though scale events already record changes per process name.

**Expected Behavior**

I should be able to filter the audit log to one process (for example `/audit?process=worker`), and each process card on the application page should link straight to that process's filtered history.

**Current Behavior**

`/audit?process=worker` is ignored and shows every entry, and the process cards have no link to the audit log. I confirmed this by running new tests against the unmodified code: the filter tests failed and the unfiltered test passed.

**Affected Components**

`cabotage/server/user/views.py` (`_render_audit_log`, shared by all four audit scopes), `cabotage/client/templates/user/audit_log.html` (filter pills, script and pagination links), `cabotage/client/templates/user/project_application.html` (the process cards), and the `audit_log` SQL view in `cabotage/server/models/audit.py`, whose `raw_data` column holds the per-process changes.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

macOS (Darwin 25.6, Apple Silicon) with Docker. I forked cabotage/cabotage-app to Wayles3/cabotage-app, cloned it, and added the upstream remote. The project runs in Docker Compose: the `base` image installs Python dependencies with uv, with Postgres 16 and Redis 7 as services. I ran the project's own `make test` and `make lint`. Challenges: `make start` failed because pulling the extra service images (consul, vault, minio, registry and others) did not complete, but tests only need Postgres and Redis, so I started just `db`. Port 6379 was already used by another project's Redis on my machine, so I ran a separate Redis container on the project's Compose network with the alias `redis` instead of touching the other one. I created the `cabotage_test` database with the extensions the Makefile uses.

**Steps to Reproduce**

1. Create an org, project, application and environment, and record two scale events on the application: `web` 1 to 2 and `worker` 0 to 3.
2. Load the application audit page `/projects/<org>/<project>/applications/<app>/audit`: two entries show, as expected.
3. Load the same page with `?process=worker`: both entries still show (expected one), and no process pill appears.
4. Open the process cards on the application page: there is no link to the audit log.

**Reproduction Evidence**

- **Commit showing reproduction:** I did not make a separate reproduction commit. I wrote the tests first and ran them against the unmodified code by stashing my source change, so the reproduction lives in the test file `tests/test_audit_process_filter.py` in my commit https://github.com/Wayles3/cabotage-app/commit/773aba764ab1c405edc7ef526a0779ec61681fe3 on branch `add-process-filter-to-audit-log` (pushed to my fork and opened as the PR above).
- **Screenshots/logs:** `make test ARGS='-k process_filter --no-cov'` on the unmodified code: `3 failed, 1 passed, 1209 deselected`. The failures were `test_process_filter_keeps_only_that_process`, `test_process_filter_pill_and_pagination_carry_the_filter` and `test_unknown_process_shows_no_entries`; the passing one was the unfiltered baseline.
- **My findings:** the filter parameter is silently ignored, as the issue says. The data is there: scale events store changes keyed by process name in the `raw_data` column of the `audit_log` view. Other entry types (deploys, config changes) carry no process name.

**Toolkit**

- Tool: the repo's own Docker/Make test setup, and Claude Code to read the code and run it.
- What it produced: a failing-then-passing test as the reproduction.
- Difficulties: the full stack would not start (image pulls), and a Redis port conflict with another project.
- What changed: ran only the services the tests need, and used a separate Redis container.

---

## Solution Approach

**Analysis**

`_render_audit_log` in `cabotage/server/user/views.py` reads only `verb`, `type`, `before` and `after` from the query string, so `process` is never looked at. Scale activities are stored against the Application with `raw_data["changes"]` keyed by process name (written by the scale handler around line 6580), so a process filter can be expressed as "the entry's `changes` object has this key".

**Proposed Solution**

Read `?process=<name>` in `_render_audit_log` and filter with `AuditLog.raw_data["changes"].has_key(name)`, applying it to the entries query and to the verb and type option queries. Show it as a removable pill, keep it in the pagination links and the filter script, and add a History link on each process card that opens the application audit log with `process=<name>`. I am deliberately NOT changing the SQL view or adding a process column, not adding a process filter to deploy or config entries (they carry no process), and not adding a dropdown of processes.

**Implementation Plan**

1. Add the `process` query parameter and filter in `views.py`, and pass `process_filter` to the template.
2. Update `audit_log.html`: pill, clear button, filter script, and pagination links.
3. Add the History link to the process cards in `project_application.html`.
4. Add tests in `tests/test_audit_process_filter.py` and run the full suite, lint and format.

No deviations from this plan during the build.

**Toolkit**

- Tool: Claude Code, used to trace the audit view and draft the change; I reviewed the diff.
- What it produced: the plan above and the change itself.
- Difficulties: the issue does not say what counts as an audit entry for a process, so I had to infer it from scale events and ask in the claim comment.
- What changed: I narrowed the scope to scale events and said so in the claim comment.

---

## Testing Strategy

Before and after, with the same four route tests in `tests/test_audit_process_filter.py`: they create two scale events (`web`, `worker`) and request the application audit page. Observable checks: with no filter there are 2 `audit-row` entries; with `?process=worker` there is 1 entry and the text `process: worker`; with `?process=web` there is 1 entry and a `data-filter-type="process"` pill; with `?process=nope` there are 0 entries. Before the change 3 of the 4 failed; after it all 4 pass. I then ran the repo's full suite with `make test ARGS='--no-cov'`: 1213 passed in 8 minutes 31 seconds, and `make lint` and `make fmt` came back clean. I have not looked at the rendered page in a browser, so the History link layout on the process cards is verified by template rendering only.

**Toolkit**

- Tool: pytest through `make test`, plus ruff through `make lint` and `make fmt`.
- What it produced: 3 failing then all passing tests, and 1213 passing in the full run.
- Difficulties: the first draft of two assertions was meaningless (`or True`); I replaced them with row counts. `make lint` flagged formatting, fixed by `make fmt`.
- What changed: tightened the tests and applied the formatter.

---

## Implementation Notes

**2026-11-17**

Chose #375 after grading seven candidates. Forked and cloned cabotage-app, read CONTRIBUTING.md (it asks contributors to comment on the issue and tag the author before starting). Traced the audit page to `_render_audit_log` and found scale events carry process names in `raw_data["changes"]`.

**2026-11-17**

Wrong turn: ran `make start` expecting the whole stack, but image pulls failed. Switched to starting only Postgres and Redis, and hit a port clash with another project's Redis, so ran a separate Redis container. Wrote the tests first and confirmed 3 of 4 failed on unmodified code, then implemented the filter. Full suite 1213 passed; lint and format clean. Committed locally as "Add process filter to the audit log". Posting upstream was blocked in my tooling session, so I posted the claim comment myself (https://github.com/cabotage/cabotage-app/issues/375#issuecomment-6958956958); I opened the PR the same day (https://github.com/cabotage/cabotage-app/pull/509).

**Toolkit**

- Tool: Claude Code for tracing and drafting; the Makefile for tests.
- What it produced: the working change and this log.
- Difficulties: environment setup and the blocked upstream post.
- What changed: I will post the claim comment myself and update the claim and PR fields here.

---

## Pull Request

**PR Link:** https://github.com/cabotage/cabotage-app/pull/509

**PR Description:** Adds a `?process=<name>` filter to the audit log (removable pill, kept through pagination) and a History link on each process card on the application page. Only scale events carry a process name, so the filter covers scaling history for a process. Four route tests added; full suite, lint and format pass. AI assistance disclosure: I used Claude Code to help trace the code and draft the change, and I reviewed and tested it.

**Maintainer Feedback:**

- 2026-11-17: none yet; PR opened and awaiting review.

**Status:** Awaiting review (opened 2026-11-17).

**Toolkit**

- Tool: gh CLI for the issue, and git.
- What it produced: a fork, a committed branch, and PR #509.
- Difficulties: posting upstream was blocked in my tooling session.
- What changed: I posted the claim comment and opened the PR myself from my terminal.

---

## Learnings and Reflections

**Technical Skills Gained**

Reading a SQL-view-backed audit log and filtering it by a key inside a JSONB column (`raw_data["changes"].has_key`), writing Flask route tests with a logged-in session and Activity rows, and running a Docker Compose Makefile workflow without the full stack.

**Challenges Overcome**

The full stack would not start, so I ran only Postgres and Redis and resolved a port clash with another project's Redis. My own scout also misjudged real repos four times (see the Toolkit blocks above), and fixing the rubric from those misses was the most useful part of the week.

**What I'd Do Differently Next Time**

Post the claim comment on the issue as soon as I commit to it, before writing any code, and check what I can and cannot do from my tooling before relying on it for the PR.

---

## Resources Used

- cabotage-app CONTRIBUTING.md: the setup, test and commit-message conventions, and the instruction to comment on the issue first.
- cabotage/cabotage-app issue #375: the maintainer thread that defined the scope (a filter on `/audit` plus icons on the process cards).
- The repo's `Makefile` targets `make test`, `make lint` and `make fmt`.
