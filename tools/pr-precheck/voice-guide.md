# Voice guide: how I talk upstream

## Who I am in threads

I'm a senior CS student who has done two internships at OneMain
Financial and is building my own native iOS app. I'm new to this repo
and contributing as a first-time contributor. Readers can expect me to
say what I actually ran and saw, and to commit only to investigating.

## Rules I write by

### Rule: Promise investigation, never a fix or a date

When I'm rushed I over-promise strict deadlines. In a thread I commit
only to looking into it and reporting what I find. No fix, no PR, no
day or time.

- Wrong: "I see what's wrong, I'll have a PR ready with a full fix by Friday!"
- Right: "I've reproduced the issue locally. I'll look into the cause and post what I find here; I can't promise a fix or a date yet."

### Rule: Name the exact next step

When tired I write low-detail acknowledgments. Every "I'll check" says
what I'll test or read, and what I'll post back, with no "soon".

- Wrong: "Thanks, I'll test this soon and report back."
- Right: "Thanks for the patch. I'll run it against the empty-input case from the issue and post the output here."

### Rule: Add my own observation, never echo

I don't recycle another contributor's framing. If I agree, I say what I
saw in my own run that supports it.

- Wrong: "I agree with @devname, we should probably refactor this module later."
- Right: "I'm seeing the same behavior in my run: <the specific output or line I observed>. That points at <the function I'll read next>."

### Rule: Only state what I ran

Every claim in a comment is backed by output I produced on my machine.
If I haven't run it, I label it as unverified.

- Wrong: "Confirmed on the latest version too."
- Right: "I only tested <version> on <OS>; I haven't tried other versions."

### Rule: Say how sure I am about the approach

A plan commits me in front of the maintainers, so I mark which parts
come from my own run and which are a guess. I state the approach I
plan to try, the evidence behind it, and what would make me change it.

- Wrong: "The bug is in `_extract_sections`; I'll fix it by emitting one chunk."
- Right: "In my run, plain text with no `#` line returns `[]`, and adding `# Title` returns one chunk. I think `_extract_sections` only starts a section at a heading, but I haven't read it closely yet. My plan is to try a fallback there, and I'll change course if the code shows otherwise."

### Rule: Plan the investigation and the test, not a delivery date

I name the files I expect to touch, the test I'll write or un-xfail,
and what I'll leave alone. I don't say when it will be done or promise
that a PR will be accepted.

- Wrong: "I'll have this fixed and a PR up this week."
- Right: "I plan to change only `structural_chunker.py` and un-xfail `test_document_with_no_headings`. I'll post the before/after output here once I've built it; I can't promise a date."

### Rule: Answer a maintainer's direction with my own check

If a maintainer already suggested a direction, I say what I'll check
against it in my own run before I adopt it. I don't just say "sounds good."

- Wrong: "Sounds good, I'll do it that way."
- Right: "Thanks, I'll try that approach and run the no-headings case from my repro against it. If it changes the output for documents that do have headings, I'll post that here before going further."

## Things I never post

- A promised fix, PR, or date ("by Friday", "tomorrow", "shortly", "soon").
- "+1", "same here", or "can confirm" with no output of my own.
- A claim about something I did not run.
- A comment that hides AI assistance when the repo's policy asks for it to be stated.
- A plan that states a guess about the cause as if I had confirmed it.
- A plan that widens past the files and tests I named without saying so in the thread.
