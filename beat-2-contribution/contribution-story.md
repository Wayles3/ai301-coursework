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

**Unit 10: Installed a voice guard and wrote a repo memory file for cabotage-app**

I extended my voice guide with an Upstream section (claims, questions, pings, each rule with a wrong/right pair), installed the voice-guard hook, and wrote a 29-line `CLAUDE.local.md` for cabotage-app (CONTRIBUTING rules, the audit subsystem files, test commands), excluded from my PR with `.git/info/exclude`. The wiring test blocked a body-less `gh issue comment --help` and logged the stop, so the hook fires. What fell short: I had already posted my claim by hand before installing the guard, and repro-check then failed it for promising "a PR up in the next day or two". The guard also stopped my revised draft three times, on rules about marking what I observed versus guessed, giving a concrete first step, and labelling unverified claims, and the draft passed on the fourth try. I revised the draft but have not yet edited the posted comment.

**Unit 11: Installed the ship-gate and wrote a manifest for cabotage-app**

I wrote a ship manifest with the project's own checks (`make lint`, `make type-check`, `make test`), tested that both my voice guard and the ship-gate stop `gh pr create --help`, and ran the gate on my branch. It said PASS after running all three checks and my pr-precheck. What fell short: I had opened PR #509 before installing the gate, so it never ran on opening. Building the manifest made me run `make type-check` and `make security-check`, which I had skipped and which CI runs. pr-precheck then pointed out an over-claiming test name and that my review request did not say what I had checked against the maintainer's direction, and I fixed both in a new commit and an updated description. I found the repo's PR template, which my first description had ignored, myself while writing the gate's description file; the gate only ever read the revised one.

**Unit 12: Installed the PR monitor and wrote a playbook from cabotage-app's real merge history**

I installed the PR monitor and wrote a four-section playbook, setting the nudge threshold from data: cabotage's CONTRIBUTING.md says review is "usually within a few weeks", and five merged PRs from outside contributors waited 0, 4, 4, 36 and 53 days to merge, so I chose one nudge after 14 quiet days and a walk-away at 45 days after that nudge. On my PR #509 (no comments or reviews yet) the monitor drafted "No nudge yet, write a wait note instead", with 2026-12-01 as the earliest date my threshold is met, and I agreed and posted nothing. It also flagged that no CI checks had reported, which I traced to both runs showing `action_required` (a maintainer has to approve first-time contributors' workflows), so there was nothing for me to fix. What fell short is that the monitor had nothing real to draft, since no maintainer has responded, so I have not tested its reply-to-reviewer path; I changed nothing in the playbook because of this run.

---

## Why I Chose This Issue

I searched with my own issue-scout: three `gh search issues` queries built from my fit profile (Swift good-first-issue bugs, Swift good-first-issue, TypeScript help-wanted bugs), ranked by fewest comments. The scan surfaced flisk and Lelu issues and no Swift ones, so I also graded issues I found on the Issue Selection site: ArduPilot #32090 and #31107 (rejected, stale open PRs), spotatui #822 (rejected, already closed), paint #1067 (rejected, then accepted after I fixed the rubric), Altinn dialogporten #2427 (accepted but vague, "Implementation: TBD") and cabotage-app #375 (accepted, every required check passed). I chose #375 because it is a bounded, well-specified feature on a Python/Flask codebase: the audit data already exists and the maintainer's thread names the two pieces (a filter on `/audit` and a small icon on the process cards). It fits my profile of bounded work I can finish and have reviewed, with no architectural change, and I want practice with the issue, PR and review workflow on a real team codebase. The scout's verdict on it was accept with every required check passing. After the unit 10 scope patch it also gives each accepted issue a difficulty note, and for #375 that note is moderate: the change is bounded, but I had to find the audit view and the process-card template myself, and the open question is whether "process" covers only scale events. I read the repo's CONTRIBUTING.md end to end before claiming: it asks you to comment on the issue first, to open a focused PR from an up-to-date branch, to push review fixes as new commits instead of force-pushing, and it says nothing about AI, so I disclose my AI assistance in what I post.

My claim comment link: https://github.com/cabotage/cabotage-app/issues/375#issuecomment-6958956958 (posted 2026-11-17). I posted it by hand before my voice guard was installed, so the guard never checked it. When I ran repro-check on that text afterwards it failed my own rule: it says "I expect to have a PR up in the next day or two", which promises a date. I have a revised claim that passes the guard and repro-check, but I have not edited the posted comment.

Honest read of the scout: after the unit 10 patch, regrading #375 returned reject, but only because "No existing claim" counted my own claim and my own open PR #509 as a stranger's, a gap I have not patched. I am keeping this issue anyway for that reason. Otherwise it held up on the repo-health checks (it correctly rejected the two ArduPilot issues for stale open PRs), but it fell short on real repos in four ways. It accepted an issue blocked on an upstream release, it had no "issue is open" check, a dependabot burst made it reject a live repo, and its ranking order buried every Swift result. I patched all four in the rubric and search strategy. The dependabot fix and the "issue is open" check were tested; the other two were not. One caveat it could not settle for #375: the repo looks single-maintainer, and the maintainer's fast replies were on his own issues, so I do not know how quickly he reviews outside PRs.

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric), run as a scan plus direct-URL grades of my picks.
- What it produced: a scan that accepted all five of its top picks, and a read-out per pick; for #375 an accept with every required check passing, a weak pass on acceptance criteria, and a note that maintainer responsiveness to outsiders was unproven.
- Difficulties: the blocked-upstream miss, no open-issue check, the dependabot misread, and the all-TypeScript ordering. The headless runs also needed tool permissions I had to grant narrowly (`gh`, `python3`).
- What changed: three rubric fixes (blocked on upstream, issue is open, skip dependency-bot commits) and a Swift-first ordering in search-strategy.md. In unit 10 I replaced my "Scope is bounded" check with the staff `scope-feasible` row plus a difficulty note, and kept my blocked-upstream condition as its own "Not blocked upstream" row so that fix survived. #375 came out moderate and Altinn #2427 ambitious. I did not rescan, so the Swift-first ordering is untested.

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

- Tool: the maintainer's thread on issue #375 and Claude Code reading the code, to turn the two-line request into the four fields above.
- What it produced: the problem statement and the list of affected files, including the finding that process names live in `raw_data["changes"]` of scale events.
- Difficulties: the issue body is one line and the maintainer's comment only says "the UI bits of showing a little icon on the process cards", so the expected behavior had to be inferred.
- What changed: I stated the inferred scope explicitly (scale events only) and put it in my claim comment so the maintainer could correct it.

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

- Tool: repro-check, with the wild scope installed, run on my claim comment and repro report together.
- What it produced: reject on the first run because my posted claim promised "a PR up in the next day or two"; the repro report passed. A later run also rejected the report because the symptom was only in prose and step 1 had no command. After I added the real `assert 2 == 1` output and concrete steps, and rewrote the claim to promise only investigation, it accepted.
- Difficulties: repro-check graded the same text differently on two runs, so its first pass did not mean I was done. It also needed real output, not my description of it.
- What changed: I captured the actual baseline failure by running the test on unmodified `main`, and I rewrote the claim draft so it passes my voice guard and repro-check.

---

## Solution Approach

**Analysis**

`_render_audit_log` in `cabotage/server/user/views.py` reads only `verb`, `type`, `before` and `after` from the query string, so `process` is never looked at. Scale activities are stored against the Application with `raw_data["changes"]` keyed by process name (written by the scale handler around line 6580), so a process filter can be expressed as "the entry's `changes` object has this key".

**Proposed Solution**

Read `?process=<name>` in `_render_audit_log` and filter with `AuditLog.raw_data["changes"].has_key(name)`, applying it to the entries query and to the verb and type option queries. Show it as a removable pill, keep it in the pagination links and the filter script, and add a History link on each process card that opens the application audit log with `process=<name>`. I am deliberately NOT changing the SQL view or adding a process column, not adding a process filter to deploy or config entries (unverified: from reading the SQL view I believe they carry no process name, but I have not run those entry types), and not adding a dropdown of processes.

**Implementation Plan**

1. Add the `process` query parameter and filter in `views.py`, and pass `process_filter` to the template.
2. Update `audit_log.html`: pill, clear button, filter script, and pagination links.
3. Add the History link to the process cards in `project_application.html`.
4. Add four route tests in `tests/test_audit_process_filter.py`, each requesting the application audit page after recording two scale events (`web` 1 to 2, `worker` 0 to 3): no filter shows 2 entries; `?process=worker` shows 1 entry and the text `process: worker`; `?process=web` shows 1 entry and a `data-filter-type="process"` pill; `?process=nope` shows 0 entries. Before the fix 3 of them must fail; after it all 4 must pass. Then run `make test` (full suite), `make lint` and `make type-check`.

No deviations from this plan during the build.

**Toolkit**

- Tool: plan-check, with the wild scope installed, run on `plan.md` (this section) and a draft plan comment.
- What it produced: reject on the first run. My test plan said only "add tests and run the suite" with no cases or expected outcome, and I stated that deploy and config entries "carry no process" as fact when I had not run them. After I named the four test cases with before and after outcomes and labelled the deploy and config claim unverified, it accepted.
- Difficulties: the plan was written after I had already built the fix, so plan-check graded a plan that had not been used to steer anything.
- What changed: I rewrote the Implementation Plan's test step and the Proposed Solution wording, and copied both back into this section. I did not post the plan comment.

---

## Testing Strategy

Before and after, with the same four route tests in `tests/test_audit_process_filter.py`: they create two scale events (`web`, `worker`) and request the application audit page. Observable checks: with no filter there are 2 `audit-row` entries; with `?process=worker` there is 1 entry and the text `process: worker`; with `?process=web` there is 1 entry and a `data-filter-type="process"` pill; with `?process=nope` there are 0 entries. Before the change 3 of the 4 failed; after it all 4 pass. I then ran the repo's full suite with `make test ARGS='--no-cov'`: 1213 passed in 8 minutes 31 seconds, and `make lint` and `make fmt` came back clean. I have not looked at the rendered page in a browser, so the History link layout on the process cards is verified by template rendering only.

**Toolkit**

- Tool: pytest through `make test`, ruff through `make lint`, ty and pyrefly through `make type-check`, and my own `test_evidence.md` to keep the before and after output together.
- What it produced: the before output (`assert 2 == 1`, 3 of 4 failing), the after output (4 passing, 57 audit tests, 1213 in the full suite), and clean lint, type-check and security-check runs.
- Difficulties: I had only run lint and tests; the CI file also runs type-check and bandit, so I added `make type-check` and ran `make security-check` once the manifest made me list the project's real checks. Both passed.
- What changed: the manifest now lists lint, type-check and tests, and the first two assertions I wrote earlier (with `or True`) were replaced with row counts.

---

## Implementation Notes

**2026-11-17**

Chose #375 after grading seven candidates. Forked and cloned cabotage-app, read CONTRIBUTING.md (it asks contributors to comment on the issue and tag the author before starting). Traced the audit page to `_render_audit_log` and found scale events carry process names in `raw_data["changes"]`.

**2026-11-17**

Wrong turn: ran `make start` expecting the whole stack, but image pulls failed. Switched to starting only Postgres and Redis, and hit a port clash with another project's Redis, so ran a separate Redis container. Wrote the tests first and confirmed 3 of 4 failed on unmodified code, then implemented the filter. Full suite 1213 passed; lint and format clean. Committed locally as "Add process filter to the audit log". Posting upstream was blocked in my tooling session, so I posted the claim comment myself (https://github.com/cabotage/cabotage-app/issues/375#issuecomment-6958956958); I opened the PR the same day (https://github.com/cabotage/cabotage-app/pull/509).

**2026-11-17 (later)**

Installed the ship-gate and listed the project's real checks in a manifest. That made me run `make type-check` and `make security-check`, which I had skipped; both passed. plan-check rejected my first plan (no named test cases, an unverified claim stated as fact), so I fixed the plan. The ship-gate passed my branch. Wrong turn: my PR description had ignored the repo's PR template, so I rewrote it and renamed an over-claiming test in a new commit.

**2026-11-17 (unit 12)**

Installed the PR monitor and filled in a playbook using the repo's real merge history. The monitor read PR #509 (no comments, no reviews) and drafted a wait note, not a nudge, so I posted nothing. CI showed `action_required` on both runs: GitHub holds first-time contributors' workflows until a maintainer approves them. Nothing to change on the branch.

**Toolkit**

- Tool: Claude Code for tracing and drafting; the Makefile for tests.
- What it produced: the working change and this log.
- Difficulties: environment setup and the blocked upstream post.
- What changed: I will post the claim comment myself and update the claim and PR fields here.

---

## Pull Request

**PR Link:** https://github.com/cabotage/cabotage-app/pull/509

**PR Description:** I answered every section of the repo's own PR template (Description, Reference to issue, Review request, Breaking changes). Description: adds a `?process=<name>` filter to the audit log in `_render_audit_log` (all four scopes), a removable pill, pagination and clear-button support in `audit_log.html`, a History link on each process card in `project_application.html`, and four route tests. It names the scope limit (only scale events carry a process name; the deploy and config claim is labelled unverified) and the unchecked browser rendering. Reference: `Fixes #375`. Evidence: before, `assert 2 == 1` and `3 failed, 1 passed` on unmodified main; after, 4 passing, 1213 in the full suite, and clean lint, type-check and security-check. It also carries an AI-assistance disclosure in my own words.

**Maintainer Feedback:**

- 2026-11-17: none yet. No comments or reviews from anyone but me. CI shows `action_required` on both runs because GitHub holds a first-time contributor's workflows until a maintainer approves them, so no checks have reported; I cannot change that.
- 2026-11-17: no reviewer feedback to address, but the ship-gate's pr-precheck pointed out a test name that overstated what it checks, so I renamed it in a new commit (not a force-push, as CONTRIBUTING asks) and updated the PR description.

**Status:** Awaiting review (opened 2026-11-17; waiting on the maintainer).

**Toolkit**

- Tool: the ship-gate (my `ship-manifest.md` plus pr-precheck), run by hand on my branch with `check_gate.py --branch`.
- What it produced: PASS. It ran `make lint` (2s), `make type-check` (3s) and `make test` (522s), then pr-precheck, which passed diff-matches-plan, description-matches-diff, decisive test evidence, reviewable diff and template-and-disclosure. It also noted that a test name overstated its assertion and that my review request did not say what I had checked against the maintainer's direction.
- Difficulties: I opened PR #509 by hand before the ship-gate existed, so the gate never ran on opening. It also showed me that the repo has a `pull_request_template.md` that my first PR description ignored.
- What changed: I rewrote the description to answer every template section and added the direction-check line. I renamed the test in a new commit and pushed it, without rebasing.

---

## Learnings and Reflections

**Technical Skills Gained**

Reading a SQL-view-backed audit log and filtering a JSONB column by key (`raw_data["changes"].has_key`), writing Flask route tests with a logged-in session and `Activity` rows, running a Docker Compose Makefile workflow with only the services the tests need, and using `gh` to read a repo's merge history and CI state.

**Challenges Overcome**

The full stack would not start (image pulls failed) and port 6379 was taken by another project's Redis, so I ran only Postgres and a separate Redis container. My scout also misjudged real repos several times (a blocked-upstream issue, no "issue is open" check, a dependabot burst, and my own claim read as a stranger's), and fixing the rubric from those misses was the most useful part of the term. In the PR stage, pr-precheck and plan-check each caught something real: an over-claiming test name, and a test plan with no cases. I also found on my own that my first PR description ignored the repo's PR template.

**What I'd Do Differently Next Time**

Post the claim comment as soon as I commit to the issue, run my voice guard on it first (my posted claim promised "a PR up in the next day or two", which my own guide forbids), and install the ship-gate before opening the PR instead of after, so it runs on opening. I would also read the repo's `.github/` folder for a PR template before writing the first description.

---

## Resources Used

- cabotage-app `CONTRIBUTING.md`: the setup and test commands, the rule to comment on the issue first, the commit message style, and the "usually within a few weeks" review wait that set my nudge threshold.
- cabotage-app issue #375: the maintainer thread (ewdurbin and JacobCoffee) that defined the scope, a filter on `/audit` plus icons on the process cards.
- The repo's `.github/pull_request_template.md` and `.github/workflows/ci.yml`: the PR template I had to answer, and the checks (lint, type-check, tests, bandit) behind my ship manifest.
- The repo's `Makefile` targets `make test`, `make lint`, `make type-check` and `make fmt`.
- The repo's merged-PR history (via `gh pr list`): five outside-contributor merges that set my playbook's staleness number.
