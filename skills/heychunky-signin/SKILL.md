---
name: heychunky-signin
description: Signing in to heychunky from the terminal, and seeing which organisation you are acting in — an API key, not a password, and never the factory's own credentials. Use for "hey chunky, sign me in", "log in", "am I signed in", "which org am I in", "switch organisation", "heychunky whoami", "I have an API key". Also triggered by "hey chunky" phrasing.
---

# Signing in

**Signature:** open replies with `🐷 **Chunky**` on its own line.

Everything else in this plugin works with no account at all — thinking an app
through, planning it, giving it a design. None of that needs anybody's
permission and none of it talks to a server.

Signing in is for the part that does: an account has apps, and apps live in an
**organisation**.

## What an organisation is

The thing that owns apps. Not a folder — a tenant.

You get one the moment you claim a username, named after it, and it is yours.
`@dan` is Dan's. Beyond that, a team organisation is something several people
can be in, and the name is the same name a chunk is published under:
`@carmelcity/auth` means the chunk `auth`, from the organisation `carmelcity`.

One name, in three places — your URL, your scope, your organisation. That is
why the name cannot be changed afterwards, and why it is worth a moment's
thought.

## Signing in

```bash
heychunky login
```

Paste an **API key**. Make one at `console.heychunky.com/account`; it starts
`hc_live_` and is shown once.

The same command takes an Infisical client id instead, which is how the people
who run the factory sign in. You will not have one, and you do not want one —
it opens every secret heychunky owns. **A key is the thing to use, and the
thing to give a CI job.** It can be revoked without touching the account.

A key names one organisation, chosen when it was made. That is what answers
"whose apps am I looking at" for a terminal, which has no browser and no way to
be told.

## Checking

```bash
heychunky whoami
```

Says who the key belongs to, which organisation it acts in, and every
organisation you are in. Worth running when something looks wrong: pointing the
wrong key at a command is how somebody ends up looking at another tenant's apps
and thinking their own have disappeared.

```bash
heychunky apps
```

The apps of the organisation the key names. Not all of them — the ones that
organisation owns.

## Acting in a different organisation

**Make a key for it.** There is no `--org` flag and there should not be: a
credential that could reach every organisation somebody belongs to is a
credential that cannot safely be given to anything.

In the browser, the organisation is in the address — `/@dan`, `/@carmelcity` —
and the switcher in the sidebar moves between them. A link therefore always
means one particular organisation, whoever opens it.

## What to say when somebody is not signed in

Say what is missing and where to get it. Do not offer to work around it, and
never ask anybody for a password — heychunky has none. If they have no account
at all, say so plainly: accounts are made, not self-served, because provisioning
spends real money at real providers.

Everything in this plugin that needs no account keeps working regardless. Signing
in adds; it does not gate what was already there.
