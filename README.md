# chunky — the public plugin

Skills for Claude Code that need **no account, no key and no invite**.

```
/plugin marketplace add heychunkydev/claude
```

Then say `hey chunky` and ask for something. The plugin installs as
`chunky@heychunky`.

The marketplace is named `heychunky` rather than `heychunkydev` on purpose: the
private plugin's marketplace already carries that name, and two marketplaces
answering to one name collide for anybody holding both — which is us.

## What is in here

| Skill | |
|---|---|
| `heychunky-plan` | thinking an app through before it is built — the problem, the people, the brief |

More is coming, and this table is the whole list. A skill missing from it is a
skill nobody knows to reach for.

## Why this repository is separate

There is a second plugin, private, that drives the factory: provisioning apps,
reading databases, our vault, our conventions. Those skills describe our
infrastructure and belong in nobody else's context, and no "this needs an
account" preamble fixes that — so the split is by audience, in two repositories,
rather than one repository with a filter on it.

**One public plugin, not one per tier.** Skills are prose, not permission. A key
decides what you may run; gating by plugin would be fake security, real
friction, and would make upgrading mean reinstalling.

## What belongs here

Only capabilities that need no account. That is a real line, not a marketing
one: everything in this plugin runs on your own machine, and nothing in it
reaches anything of ours.

Anything that provisions, spends, or authenticates goes in the private plugin
instead. If a skill here ever has to say *"this needs a key"*, it is in the
wrong repository.

<!-- 🐷 made by chunky -->
