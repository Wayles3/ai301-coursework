# Rubric: is this a good first issue?

All recency thresholds are measured against the capture date in eval mode
and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer commits recent | Repo facts: dates of the last 5 default-branch commits | The newest default-branch commit is within 90 days of the capture date, and at least one of the last 5 commits is authored by a human (not a `[bot]` account) or is a bot merge of a human's PR | required |
| Maintainer responds | Repo facts: maintainer first-response sample, with each sampled issue's open date | Pass if at least 1 sampled issue has a first owner/member/collaborator reply within 60 days. If there are no replies, pass anyway when fewer than 3 sampled issues were opened more than 30 days before the capture date (too new to judge). Fail only when 3 or more sampled issues are older than 30 days and none has a maintainer reply, or the sample holds no replies and no issues at all | required |
| Repo not archived | Repo facts: `archived:` flag on the repo line | `archived: no` | required |
| Repo in use | Repo facts: latest release date, last push date, last 5 default-branch commit dates | A release within 12 months of the capture date, OR no recent release but the last push to any branch is within 90 days AND the newest default-branch commit is within 90 days and human-authored. A single-author small repo passes on commits alone | required |
| Scope is bounded | Issue title, body, labels and comment thread | None of: the issue is an umbrella or tracking issue (a list of sub-items meant to be split up), a maintainer says the fix touches core internals, the thread shows the design still being debated with no maintainer decision, or it is a pure usage/support question. A terse body alone does not fail this check | required |
| Work is wanted | Issue author, author_association, labels and comment thread | Fail if the opener is a bot account (name ends in `[bot]`). Fail if the issue is an unendorsed feature request (asks for new behavior, not a bug fix or docs change) AND has none of: opened by an Owner/Member/Collaborator, a maintainer comment in the thread, or a good first issue / help wanted label. Bug reports and docs tasks pass this check | required |
| No existing claim | Repo facts: `assignees` and `linked PRs`; comment thread | No assignee, no open linked PR, and no comment in the last 60 days before the capture date saying "I'll take this", "working on this", or naming a PR in progress that a maintainer did not reject. A closed unmerged PR does not fail this by itself | required |
| AI policy allows assisted work | Repo facts: contribution policy line | The policy does not outright ban AI-assisted or AI-generated contributions. Disclosure, understanding, testing and review conditions pass; silence passes. A ban on "fully AI-generated" contributions that explicitly allows assistive AI use passes | required |
| Maintainer authored or labeled | Issue author_association and labels | Opened by an Owner/Member/Collaborator, or labeled good first issue / help wanted | preferred |
| Acceptance criteria stated | Issue body | The body states a concrete expected result or checklist | preferred |
| Not a stale label | Label event lines vs issue open date | Issue is under 12 months old, or a maintainer commented in the last 6 months | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required` check
fails. `unclear` on a required check counts as fail. Preferred checks
never change the verdict; they only rank accepted issues.
