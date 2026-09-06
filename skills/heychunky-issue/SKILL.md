---
name: heychunky-issue
description: Working one issue in an app end to end — reading the spec, changing the narrowest thing, proving it, and landing it. Use for "fix issue 40", "work on this bug", "change this bit for me", "pick up that ticket", "solve this". Also triggered by "hey chunky" phrasing.
delivers: develop.edit
---

# Working an issue

**Signature:** open replies with `🐷 **Chunky**` on its own line.

One issue, start to finish. The order below is not ceremony — every step exists
because skipping it produced a wrong answer somebody had to unpick.

## The app decides how work lands. Not this file

**Read the app's `AGENTS.md` or `CLAUDE.md` before anything else.** It owns the
gates, the branch rules and the consents, and apps disagree with each other
completely:

| | |
|---|---|
| one app | branch per change → pull request → review → main → staging → production |
| another | *"There are no pull requests. Work lands on `main`"* |

A skill that hardcoded either would be wrong half the time. This one says how to
*work* an issue; the app says how work *lands*.

## Before you touch anything

**Read the issue properly, including the body.** Titles lie. One titled
*"Uploading files issues"* opened with *"Three ideas unrelated to uploading
files"* and contained four separate bugs, none about uploading.

**Find the spec before the code.** An app built here keeps flow specs beside the
feature — `.chunky/chunks/<chunk>/docs/flows/<slug>/spec.md`. The spec names the
entry point, the handler and the table, which is the difference between reading
three files and grepping for an hour. Before saying a feature does not exist,
grep there — it probably does.

**Measure the gates before you change a line.** Run whatever the app calls its
tests, its linter and its build, and *write the numbers down*.

This is the step people skip and it is the one that matters most. An app's
linter was sitting at 1208 problems and two tests were already failing. Without
the before-number, the after-number looks like damage you did — and the honest
claim at the end is not "everything passes" but **"1208 before, 1208 after, and
neither of my files appears in it."**

A pre-existing failure is also worth a second look. Two of those tests had
broken on the first of the month, from a hardcoded date in the test rather than
any change — nobody had run the suite since. **A red gate is not proof that
somebody recently broke something.**

## The change

**Change the narrowest layer that owns the wrong behaviour.** Trace the symptom
to the mechanism first. The answer is often a seam that already exists: one
prompt took an optional `guidance` parameter that was declared, documented and
passed by nothing. The fix was to use it, not to add a mechanism beside it.

**Do not widen.** If a fix touches something shared, keep the change to the one
caller that asked for it — and *assert that in a test*, because a leak into the
neighbours is exactly the change nobody notices until it has rescored, resent or
re-rendered everything.

**Match the code around you** — the same idioms, the same comment density. A
patch that reads as foreign is a patch someone has to think about twice.

## Proving it

**A test with every fix. Never weaken or delete one to make something pass.**

**Know what a test cannot tell you.** A unit test can assert that a prompt now
contains an instruction. It cannot show that the model behaves differently — and
for anything with a model, a person, or a browser in the loop, that gap is where
the actual bug lives.

That is what a recording is for. An app here may keep one:

```bash
pnpm ops:prove          # boots the app, walks the flow, records what happened
```

> The video is the point. A green test run says "9/9 passed"; the recording
> shows what that looked like, and it survives the session — it goes in the
> commit, the issue, and the reply to whoever reported the problem.

For a change whose output varies run to run, **a before-and-after pair beats a
single recording.** One run on the old behaviour, one on the new, side by side.
A single clip of a good result proves nothing; two clips of a changed result
prove the change.

Do not file a recording as proof of something it does not show. A recording that
looks like proof and is not is worse than none.

## Landing it

**Two consents, never one.**

1. **Ask before committing.** Say exactly what will be committed and where, then
   wait. "The tests pass" is not consent.
2. **Ask again before promoting.** Approval to commit is not approval to
   release. A release usually has its own checklist, its own record and its own
   database snapshot — find it rather than deploying by hand.

State the three gates as numbers against the baseline, say which failures are
yours and which were already there, and name anything you did not do.

## Closing it

**Reply to whoever reported it, in the words they used.** An issue filed through
an in-app feedback dashboard mirrors replies back to that person — so the reply
is the product, not an afterthought. Say what changed and what they will see
differently. Not the file you edited.

If the fix revealed something else — and it usually does — **file that
separately rather than folding it in.** One issue, one change. The second thing
you found deserves its own ticket, its own consent and its own proof.

<!-- 🐷 made by chunky -->
