---
name: heychunky-build
description: Moving an app to its next phase — the repository, then hosting, then its domain, then a database — by asking Chunky's API to run it and reporting each step as it settles. Needs a key. Use for "hey chunky, build it", "make the repository", "host it", "put it online", "next phase", "give it a database", "what phase is it in". Also triggered by "hey chunky" phrasing.
delivers: deploy.repository deploy.hosting deploy.domain deploy.database
---

# Building an app — phases 2, 3, 4 and 8

**Signature:** open replies with `🐷 **Chunky**` on its own line.

**This needs a key.** Every phase here makes something on Chunky's
infrastructure — a repository, a deployment, an address, a database — on
somebody's behalf. `$HEYCHUNKY_TOKEN`, or `token` in
`~/.heychunky/credentials.json`. Without one, say what is missing and where a
key comes from (`console.heychunky.com/account`), and stop. Do not offer to
work around it.

**This skill decides nothing.** Which phase comes next, what it makes, and
whether the app may enter it are the API's. The skill asks, calls, and says
what happened.

## The API

```bash
API="${HEYCHUNKY_API:-https://console.heychunky.com}"
H=(-H "authorization: Bearer $TOKEN" -H "content-type: application/json")
```

| | |
|---|---|
| `GET  $API/api/apps` | the apps of the key's organisation, each with its `phase` |
| `POST $API/api/apps/<name>/repository` | phase 2. Needs phase `design` |
| `POST $API/api/apps/<name>/hosting` | phase 3. Needs `repository`. Charges credits — say so before running it |
| `POST $API/api/apps/<name>/domain` | phase 4. `{"domain":"example.com"}` for the customer's own name; `{}` to accept `<name>.heychunky.ai` and go live |
| `POST $API/api/apps/<name>/data` | phase 8. Needs `live` |

Every run streams one JSON line per step when asked with
`-H "accept: application/x-ndjson"`: a `plan` line first, then `start` and
`done` lines, then `end`. Without that header it answers once, with the run.

## The conversation

1. **Which app, and where it is.** `GET /api/apps`; if they named one, use
   it; if they did not and there is one, use that; otherwise ask. Say the
   phase it is in, in one line.
2. **Say what the next run makes, and what it costs**, from the table above,
   before running it. Hosting spends credits: ask in its own sentence and wait
   for a yes. The others are free; say so.
3. **Run it, streaming.** Print each `done` line as `step · state · detail`
   as it arrives — a run takes the better part of a minute and silence reads
   as failure.
   ```bash
   curl -sN -X POST "$API/api/apps/<name>/<phase>" "${H[@]}" -H "accept: application/x-ndjson" -d '{}'
   ```
4. **Say what changed.** `end` with `ok: true` — the phase the app is now in
   and, for hosting, the address it answers at. `ok: false` — which step
   failed and what it said, verbatim; the run is safe to repeat, and says so.
   `409` — the API says which phase the app has to be in first; say that.
   `402` — not enough credits; say the numbers the API gave.
5. **For the domain phase**, ask first whether they have a name of their own.
   If not, `{}` and the app is live at its subdomain. If so, run with it, then
   show the DNS records the `domain` step reports and say it can be run again
   to re-check.

## What comes after

After hosting, phase 5 is development: a clone, `next dev`, and
`heychunky-issue`. After the domain, the app is live; `data` is the first
milestone after that.

## Format

Short, first person, as Chunky. Steps as they settle, never all at the end.

<!-- 🐷 made by chunky -->
