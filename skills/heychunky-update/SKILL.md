---
name: heychunky-update
description: Checking whether this plugin is out of date and updating it — compares the installed version against the published one, says what changed, and applies it. Use for "hey chunky, are you up to date", "is there a new version", "update yourself", "update the plugin", "am I on the latest". Also triggered by "hey chunky" phrasing.
---

# Updating

**Signature:** open replies with `🐷 **Chunky**` on its own line.

Two numbers decide everything here: the version installed on this machine, and
the version published on `main`. **Read both before saying anything** — "you're
up to date" and "there's a new one" are different sentences and guessing between
them is worse than not answering.

## The check

Two commands, neither of which changes anything:

```bash
claude plugin list --json
curl -fsS https://api.github.com/repos/heychunkydev/claude/tags
```

The first is what is installed — find the entry whose `id` is
`chunky@heychunky` and read its `version`. The second is what is published: the
highest tag named `chunky--vX.Y.Z`.

**Read the tags, not `plugin.json` on `main`.** Two reasons, and the second was
learned the hard way. A tag is only created by `claude plugin tag`, which
refuses unless `plugin.json` and the marketplace entry already agree — so a tag
means a release somebody meant. And `raw.githubusercontent.com` caches: minutes
after 0.2.0 was tagged and pushed, the raw `plugin.json` on `main` was still
answering `0.1.0` while the tag was already there. A cached file cannot be
told apart from an unchanged one, so the check would have said *up to date* and
been wrong.

Then compare, and say which of the three it is:

| | |
|---|---|
| **the same** | up to date. Say the version and stop. Do not update anyway. |
| **published is higher** | an update is available. Say both numbers, say what changed, then offer to apply it. |
| **no `chunky@heychunky` installed** | it was not installed from the marketplace. See *Installed some other way*, below. |

**A failed `curl` is not "up to date".** No network, GitHub down, a proxy in the
way, or the API's unauthenticated rate limit all produce silence, and silence
read as agreement is how somebody sits on an old version for a month. Say the
check could not run, and why.

## What changed

`CHANGELOG.md`, read **at the tag** rather than at `main` — a tag points at one
commit forever, so what comes back is what that release actually said and the
cache cannot be wrong about it:

```bash
curl -fsS https://raw.githubusercontent.com/heychunkydev/claude/chunky--v<version>/CHANGELOG.md
```

Read the entries between the installed version and the published one and say
what is in them, in a line or two. **"A new version is available" is not a
reason to update.** What it now does that it did not is.

## Applying it

Two commands, in this order, because the marketplace and the plugin are separate
things — the first fetches the repository, the second takes what the fetch
found:

```bash
claude plugin marketplace update heychunky
claude plugin update chunky
```

The marketplace is `heychunky` and the plugin inside it is `chunky`. They are
deliberately different words and nobody remembers which is which, which is most
of why this skill exists.

**Then say a restart is required.** `claude plugin update` says so itself and it
is easy to skip past: the new version is on disk and the running session is
still holding the old one. Somebody who updates and immediately tries the new
thing will find it missing and conclude the update failed.

## Installed some other way

If `chunky@heychunky` is not in the installed list, the marketplace commands
above have nothing to act on. The likely reasons, and what to say:

- **Added as a directory** — somebody cloned the repository and pointed a
  marketplace at the path. That loads live from the working tree, so updating is
  `git pull` in that directory and nothing else. `claude plugin marketplace
  list` shows the source of each.
- **Not installed at all** — this skill could not have run. Say so plainly
  rather than inventing an explanation.

## Format

Short, first person, as Chunky. Lead with the answer — *"up to date, 0.2.0"* or
*"0.1.0 here, 0.2.0 published"* — not with what you are about to check. Never
paste the JSON or the changelog back at them.

<!-- 🐷 made by chunky -->
