# Status

**Intended repository name:** `grok-bot-ops-graph`  
**Playbook version:** v0.1  
**Freeze date:** 2026-09-10

If this checkout lives under a temporary project slug, keep using **`grok-bot-ops-graph`** in titles and citations.

## What v0.1 contains

- Default five-role Ops Graph: `chief`, `research`, `drafts`, `checker`, `distribution`.
- Charter: graph diagram, job loop, approval-by-reversibility, autonomy ladder, quiet-graph rule.
- Handoff packet JSON schema v0.1 with five fictional packets for “research topic X / draft changelog”.
- Standup recipe to create Bots, a group, and the first objective.
- Paste-ready agent profiles.
- Portable skill `ops-graph-team` for `chief`.
- Example job folder with empty artifact layout.
- Optional markets-desk extension (SCAN → chief, no tickers, no broker advice).
- Attribution for the community write-up, public product docs, and this operationalization.

## What v0.1 deliberately omits

- Hosted code, APIs, or a web app.
- Named third-party Bots or a marketplace roster.
- Broker integrations, order tickets, or symbol lists.
- Routine schedules (those come after a clean manual run).
- Product UI screenshots (they rot and often leak account chrome).
- Any real job artifacts.

## Iteration ideas (later versions)

- Packet `0.2`: `blocker_class`, `confidence`, checksum of artifacts.
- A `LADDER.md` template (still local-only).
- Checker rubric files per artifact type (changelog, patch, brief).
- Optional `infra` / `video` / `code` extension notes matching the markets split.
- A dry-run script that validates packet JSON against the schema (no network).
- Translations of the profile blurbs.
- After a public canonical URL exists for “Grok Bot: The AI Team That Never Sleeps”, add it to `ATTRIBUTION.md`.

## Scrub audit (v0.1)

Audit performed on the playbook files in this repository at freeze. **Fail the release if any row is “found”.**

| Class | Rule | Result |
| --- | --- | --- |
| Real usernames | Only placeholders `YOUR_NAME`, role names, and the requested source handle as a citation | pass — `0xwhrrari` only in ATTRIBUTION.md and this table |
| Emails | No `user@` addresses | pass |
| Hostnames / IPs / VMIDs | No machine names, IPs, VM IDs | pass |
| Employer names | None | pass |
| Ticker lists | None; markets extension uses `YOUR_WATCHLIST` | pass |
| Account numbers | None | pass |
| API keys / tokens | None | pass |
| Private URLs | Only `https://example.com/...` in examples; product docs are public `x.ai` / `cursor.com` / `docs.x.ai` | pass |
| Agent UUIDs | None | pass |
| Personal blog domains | Community piece cited by title/date (no URL found); no personal blogs linked | pass |
| Example objectives | Fictional: “research topic X”, “draft changelog” | pass |
| Lane specialists | Generic `infra`, `markets`, `video`, `code` only | pass |
| Job paths | `ops-graph/jobs/<slug>/` convention only | pass |

Re-run this table before publishing a fork. Search the tree for `@`, `http`, `0x`, `sk-`, `Bearer`, IPv4 patterns, and any proper names you added locally.

### Local search suggestions (do not paste hits back into the repo)

```
rg -n -i "@[a-z0-9._%+-]+\\.[a-z]{2,}" 
rg -n -i "api[_-]?key|bearer |sk-|token="
rg -n "[0-9]{1,3}(\\.[0-9]{1,3}){3}"
rg -n -i "ticker|broker|account number"
```

Public product URLs in `ATTRIBUTION.md` and `README.md` are allowed.

## Compatibility notes

- Written against **public, high-level** Grok Bot / Cursor patterns: named Bots, small group chats, skills, routines, shared files. UI steps in `STANDUP.md` are intent-level.
- Other multi-agent desktops can use the same charter if they have: named agents, a shared filesystem or equivalent artifact store, and a way to address one agent at a time.
