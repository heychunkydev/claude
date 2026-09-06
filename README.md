# chunky

Claude Code skills for thinking an app through **before** you build it.

Nothing here needs an account, a key or an invite. It is a conversation and some
markdown files in your own home directory. Nothing is uploaded and nothing talks
to a server.

```bash
claude plugin marketplace add heychunkydev/claude
claude plugin install chunky@heychunky
```

Then start Claude Code and say `hey chunky`.

**Both lines.** Adding a marketplace installs nothing — after the first command
on its own, `claude plugin list` reports no plugins and `hey chunky` does
nothing. A marketplace is where plugins are found; the install is what puts one
on your machine.

---

## What it does

You say:

> **hey chunky, help me think through my idea**

Chunky takes a name for the app so there is somewhere to put the answers, then
asks three questions — one at a time, waiting for each answer — and writes each
one down as you settle it.

| | |
|---|---|
| **What is wrong today, and for whom?** | Not what the app does. What somebody does *now*, badly, and what it costs them. A problem nobody has a workaround for usually is not a problem yet. |
| **Who arrives?** | One person, described specifically enough to disagree with. "Small business owners" is a category, and a category cannot tell you what the first screen should say. |
| **What is it, and what does the first screen do?** | Written last, from the other two — including the part people skip: what is deliberately *not* in it. |

If you have not got a name yet, Chunky offers five and searches the web for each
one first — whether it is already somebody's product, whether it collides with a
trademark worth avoiding, whether it is distinctive enough to find later. A
working name is enough to start; renaming a folder costs nothing.

## What it leaves on your machine

```
~/.heychunky/apps/<name>/
  README.md          what this is, in one line, and when it started
  plan/
    problem.md       what is wrong today, and for whom
    people.md        who arrives, and what they already know
    brief.md         the one page everything later is checked against
    decisions.md     what was decided and why, appended as it changes
```

Plain markdown. Yours. Open it, edit it, put it in your own git repository,
delete it — none of that needs Chunky.

`decisions.md` is the one people underrate. Any file can say the app is for
freelancers; only that one says it was for agencies until somebody worked out
that agencies buy in committees. The reasoning is the part that evaporates.

## The rule it will not break

**It will not write an answer you did not give.**

The failure of every planning tool is a plausible persona nobody recognises, and
a plan built on invented answers is worse than no plan because it reads like
agreement. If you do not know who it is for, the file says so — *"not settled,
two candidates, neither tested"* is a true and useful line. An invented one is
neither.

Chunky suggests freely, and marks a suggestion as his until you take it.

## What it does not do

**It does not build the app.** A repository, a database, somewhere to run and an
address are things Chunky does on his own infrastructure, and those need an
account. This plugin will never pretend otherwise — if a skill in here ever has
to say *"this needs a key"*, it is in the wrong repository.

One thing that *is* free and worth doing straight after the plan:

```
npx getdesign list              seventy-six design languages
npx getdesign add raycast       writes a real DESIGN.md into your project
```

Tokens, type scale, spacing and the reasoning behind them — a design system
rather than a colour palette. No account, no plugin, nothing to sign up for.

## Skills

| | |
|---|---|
| `heychunky-plan` | the problem, the people, the brief |
| `heychunky-update` | whether you are on the latest version, and getting there |

That table is the whole list. A skill missing from it is a skill nobody knows to
reach for, so anything added goes in here in the same commit.

## Why this is a separate repository

There is a second plugin, private, that drives the factory — provisioning apps,
reading databases, our vault, our conventions. Those skills describe our own
infrastructure and belong in nobody else's context, and no "this needs an
account" preamble fixes that. So the split is by **audience**, in two
repositories, rather than one repository with a filter on it.

One public plugin, not one per tier: skills are prose, not permission. A key
decides what may run. Gating by plugin would be fake security, real friction,
and would make upgrading mean reinstalling.

The marketplace here is named `heychunky` rather than `heychunkydev` because the
private plugin's marketplace already answers to that name, and two marketplaces
with one name collide for anybody holding both.

<!-- 🐷 made by chunky -->
