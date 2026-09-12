# Changelog

Newest first. `heychunky-update` reads this file to say what changed between
the version somebody has and the one that is published, so an entry is written
for a person deciding whether to update — not for us.

## 0.4.0

**`heychunky-release`** — phases 6 and 7. A release takes `dev` to next
and writes a version down with its changelog; a promotion takes next to
production, and is asked for in its own sentence, never offered.

**`heychunky-build`** — phases 2, 3, 4 and 8. With a key, Chunky makes
the repository, then hosts it, then attaches a domain, then gives it a
database, one phase per ask, each step reported as it settles. The first
skill in this plugin that needs a key, and it says so before doing anything.

**`heychunky-design`** — phase 1. Three questions, then two or three
directions Chunky picks from the seventy-six design languages against your
brief, each with a reason; `DESIGN.md` next to `APP.md`, and the choice
recorded on the app if you are signed in.

**`heychunky-plan` is phase 0, and it is thin.** Five questions now — who it
is for, what is wrong today, why they would switch, what to call it, and what
it is — written to one `APP.md` rather than three files under `plan/`. The
questions come from Chunky's API, so the console asks exactly the same ones;
the skill holds none of its own. The name is checked against an open endpoint
before it is accepted, and if you are signed in the app is registered at the
end. Signed out, nothing changes: the file is the whole record.

## 0.2.2

**The install instructions were one command short.** Adding a marketplace
installs nothing — run against a clean `HOME`, `claude plugin list` reports no
plugins after the add, so anybody following the old README ended up with a
marketplace, no plugin, and a `hey chunky` that did nothing. Two commands now,
and the README says why the second is not optional.

## 0.2.1

**The version check reads git tags, not `plugin.json` on `main`.** Minutes after
0.2.0 was published, `raw.githubusercontent.com` was still serving the previous
version number from cache — so the check would have said *up to date* and been
wrong, which is the one answer it must never get wrong. Tags are immutable and
are only created by a command that validates the release first.

## 0.2.0

**`heychunky-update`** — ask *"hey chunky, are you up to date?"* and Chunky
compares the version installed on your machine against the one published, says
what changed, and applies it if you want. The marketplace is `heychunky` and
the plugin inside it is `chunky`; nobody remembers which is which, and now
nobody has to.

The README says what the plugin does before it says why the repository exists.

## 0.1.0

First release. **`heychunky-plan`** — three questions about what you are
building, asked one at a time, written into `~/.heychunky/apps/<name>/plan/`.
What is wrong today and for whom, who arrives, and what the first screen has to
do. It will not write an answer you did not give.
