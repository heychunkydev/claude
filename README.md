# chunky

Claude Code skills for thinking an app through **before** you build it.

Thinking an app through needs no account, no key and no invite. It is a
conversation and some markdown files in your own home directory — nothing is
uploaded and nothing talks to a server.

If you do have an account, `heychunky login` takes an API key and Chunky can
then see the apps your organisation owns. That is an addition, not a gate:
everything above keeps working signed out.

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

Chunky asks for a name, checks that nobody has it, and then asks four more
questions — one at a time, waiting for each answer — and writes them down.

| | |
|---|---|
| **Who is it for?** | One person, described specifically enough to disagree with. "Small business owners" is a category, and a category cannot tell you what the first screen should say. |
| **What is the problem?** | Not what the app does. What somebody does *now*, badly, and what it costs them. |
| **What is the value proposition?** | Why they would switch from the workaround. |
| **What is the solution, at the highest level?** | What the thing is in a sentence — and what it deliberately is not. |

The questions are Chunky's, not the plugin's: they come from the same API the
console uses, so the two never disagree about what is asked.

## What it leaves on your machine

```
~/.heychunky/apps/<name>/
  APP.md             the answers, under one heading each, and the date
  decisions.md       what was decided and why, appended as it changes
```

Plain markdown. Yours. Open it, edit it, put it in your own git repository,
delete it — none of that needs Chunky.

If you are signed in, the app is also registered in your organisation at the
end, which is where the next phases pick it up. If you are not, nothing is
missing: the file is the whole record.

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
| `heychunky-plan` | phase 0: who, the problem, the value, the name, the solution |
| `heychunky-design` | phase 1: what kind of thing, what vibe, what look — and a direction chosen from seventy-six |
| `heychunky-build` | phases 2, 3, 4 and 8: the repository, hosting, a domain, a database — needs a key |
| `heychunky-issue` | working one issue end to end, and proving it |
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
