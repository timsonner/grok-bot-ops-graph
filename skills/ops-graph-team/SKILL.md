---
name: ops-graph-team
description: Run or stand up an Ops Graph (chief of staff + specialists). Use when YOUR_NAME gives one OBJECTIVE, when routing research/drafts/checker/distribution with handoff packets, when parking irreversible actions, or when a group chat is getting noisy.
---

# Ops Graph team

## When to use

Use this skill when any of the following is true:

- You are `chief` (or acting as chief) and received **one OBJECTIVE**.
- You need to route work to `research`, `drafts`, `checker`, or `distribution`.
- You are about to paste a transcript instead of a packet.
- You are considering send / publish / purchase / delete / production / legal.
- Optional lane work (`infra`, `markets`, `video`, `code`) appeared.
- The group is talking without packets.

Do **not** use this skill to bypass product approvals, to publish, or to recruit extra Bots into the `ops-graph` group.

## Recipe

### 0. Identity

If you are not `chief`, do your lane only and return a packet to `chief`. Do not run the whole graph.

### 1. Take the OBJECTIVE

- One paragraph outcome + constraints. If you received a task list, rewrite it as a single outcome in `PLAN.md` and confirm with `YOUR_NAME` only if the outcome is ambiguous.
- Allocate `ops-graph/jobs/<slug>/` (slug from the outcome, lowercase, hyphenated).
- Copy headings from `jobs/_example/PLAN.md`.

### 2. Slice

For each slice record: owner, input artifact, output artifact, **independent? yes/no**.

Default sequence (dependent):

1. `research` → cited pack
2. `drafts` → artifact
3. `checker` → findings (never authors the artifact)
4. `distribution` → staging (never publishes)

Parallelize only slices with `independent? yes`. Send **separate** messages, one @-mention each.

### 3. Packet every hop

Write JSON to `ops-graph/jobs/<slug>/packets/<packet_id>.json` using schema v0.1:

- `artifacts`, `decisions`, `constraints`, `open_questions`, `next_gate`
- `next_gate.park_if` always includes send, publish, purchase, delete, production, legal
- `from_role` / `to_role` are placeholders, never a person’s handle

@-mention **exactly one** `to_role`. No `@everyone` except job opened, job closed, or human needed.

### 4. Approval-by-reversibility

Finish if it can be undone from the job folder. Otherwise PARK for `YOUR_NAME`.

| Finish | PARK |
| --- | --- |
| Read, cite, write job files, draft, check, stage | Send, publish, purchase, delete, production, legal |

If unsure, PARK.

### 5. Lane pull (optional)

Existing specialty Bots stay in their chats. Pull only when `YOUR_NAME` asked or the specialty is clear. One packet. Do not add them to the group.

### 6. Close

- Fold checker fails back through `drafts`, then `checker` again.
- `distribution` writes `artifacts/staging/human-packet.md` and stops.
- Tell `YOUR_NAME` once: path, suggested action, what was *not* done.
- Update PLAN.md close-out. Quiet.

### 7. Autonomy

observe → prepare → approve → schedule/trigger → coordinate.

Promote only after clean runs, and only if `YOUR_NAME` says so. Routines come after the skill has worked manually. Never put a publish routine on `distribution`.

## Anti-patterns (stop)

- Transcript-forwarding
- Fan-out / status storms
- `checker` rewriting the draft
- `distribution` “test publish”
- Starting `drafts` before the pack is accepted
- Secrets or private URLs in packets
- Naming a specific person’s Bots

## Copy

Kickoff, profiles, and packet examples live with this playbook: `STANDUP.md`, `AGENT_PROFILES/`, `HANDOFFS.md`, `CHARTER.md`.
