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

## Things I never post

- A promised fix, PR, or date ("by Friday", "tomorrow", "shortly", "soon").
- "+1", "same here", or "can confirm" with no output of my own.
- A claim about something I did not run.
- A comment that hides AI assistance when the repo's policy asks for it to be stated.
