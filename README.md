# Ops Graph Playbook (`grok-bot-ops-graph`)

A public template for standing up a **chief of staff + specialists** team on Grok Bot (or a similar multi-agent desktop assistant) and running work as an **Ops Graph**.

This repository is documentation and copy-pasteable profiles. It is not a hosted service. If the clone you are looking at was minted under a temporary slug, treat **`grok-bot-ops-graph`** as the intended name.

## What you get

You, the human (`YOUR_NAME`), give **one OBJECTIVE** to **one Bot**: `chief`.

`chief` decomposes that objective, routes **compact handoff packets** (not chat transcripts), and keeps irreversible actions parked for you. Specialists do one job each:

| Role | Job |
| --- | --- |
| `research` | Cited packs. Sources, claims, gaps. |
| `drafts` | Turns packs into prose, diffs, or copy. |
| `checker` | Independent review. Never builds what it checks. |
| `distribution` | Stages the final packet. Never publishes alone. |

Optional lane specialists (`infra`, `markets`, `video`, `code`, …) stay in their own chats. Pull them only when you ask, or when the specialty is unambiguous.

## Why this shape

A persistent multi-agent desktop can keep working while you are away. Without a graph, that becomes a noisy group chat: everyone replies, nobody owns the gate, and irreversible actions leak.

The Ops Graph is a small operating system on top of that product capability:

1. One objective in, not a task list.
2. Packets, not transcripts.
3. Parallelize only independent work.
4. Finish reversible work; park send / publish / purchase / delete / production / legal.
5. Promote autonomy only after clean runs.
6. One specialist message by default.

Conceptual inspiration and product patterns are listed in [ATTRIBUTION.md](ATTRIBUTION.md). The handoff packets, approval-by-reversibility rule, and autonomy ladder are this playbook’s operationalization.

## Placeholders (keep them)

Examples in this repo are fictional. When you copy them, keep the same *shape* and fill your own values later — do not paste real identifiers into a public fork.

| Use this | Not this |
| --- | --- |
| `YOUR_NAME` | real name or handle |
| `chief`, `research`, `drafts`, `checker`, `distribution` | a specific person’s Bot names |
| `ops-graph/jobs/<slug>/` | host paths, VMIDs, home directories |
| `example.com` | private or personal domains |
| “research topic X”, “draft changelog” | live customer work |

## Quick start

1. Read [CHARTER.md](CHARTER.md) once (diagram, job loop, approval line, ladder).
2. Create five Bots from [AGENT_PROFILES/](AGENT_PROFILES/).
3. Follow [STANDUP.md](STANDUP.md) to make the group and run the first objective.
4. Install [skills/ops-graph-team/SKILL.md](skills/ops-graph-team/SKILL.md) on `chief` (and optionally on you as a reminder).
5. Copy [jobs/_example/](jobs/_example/) to `ops-graph/jobs/<slug>/` for each new objective.

A new user should be able to recreate the graph from `STANDUP.md` alone. A new `chief` should be able to run the loop from the skill + [HANDOFFS.md](HANDOFFS.md).

## Repo map

```
README.md                 this file
ATTRIBUTION.md            sources
CHARTER.md                graph, roles, loop, gates, ladder
HANDOFFS.md               packet schema + scrubbed examples
STANDUP.md                create Bots, group, first objective
AGENT_PROFILES/           paste-ready profile blurbs
skills/ops-graph-team/    portable skill for chief
jobs/_example/            sample PLAN.md + empty artifact dirs
OPTIONAL/                 extra desks (not required for v0.1)
STATUS.md                 v0.1 scope, iteration ideas, scrub audit
```

## Default roster

Keep the default group at five Bots: `chief` + the four specialists. That stays inside a typical small group-chat size and avoids fan-out.

- You talk to `chief`.
- `chief` talks to one specialist per message.
- You do not @-mention the whole group except for job-open, job-close, or “human needed”.

## Core rules (print this)

1. **One OBJECTIVE.** You do not dump a task list on the group.
2. **Packets.** Every route carries artifacts, decisions, constraints, open_questions, next_gate.
3. **Lane discipline.** Research cites. Drafts write. Checker never authors the artifact it reviews. Distribution stages only.
4. **Independence test.** Two workstreams run in parallel only if neither needs the other’s output.
5. **Reversibility.** If it cannot be undone locally, it parks for `YOUR_NAME`.
6. **Ladder.** observe → prepare → approve → schedule/trigger → coordinate. Promote a Bot one rung after clean runs, not after a good speech.
7. **Specialty pull.** Existing lane Bots stay put. `chief` does not recruit them into the ops-graph group.
8. **Quiet graph.** Default is one specialist ping. No status storms.

## First objective (fictional)

Use this until the graph has completed one clean loop:

> Research topic X. Produce a cited pack, then a draft changelog for the notes page at `https://example.com/notes/changelog`. Stage it. Do not publish.

Copy the rest of the kickoff from [STANDUP.md](STANDUP.md).

## What this is not

- Not financial, legal, or medical advice.
- Not a prompt pack that grants extra product features.
- Not permission to bypass the host product’s approval, secret, or sharing controls.
- Not a marketplace of named third-party Bots.

## License-shaped use

Copy the profiles, skill, and packet schema into your own Grok Bot (or similar) workspace. Keep attribution if you republish the playbook. Do not publish other people’s transcripts, identifiers, or job artifacts.
