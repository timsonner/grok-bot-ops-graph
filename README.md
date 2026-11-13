# Ops Graph Playbook (`grok-bot-ops-graph`)

A public template for standing up a **chief of staff + specialists** team on Grok Bot (or a similar multi-agent desktop assistant) and running work as an **Ops Graph**.

This repository is documentation and copy-pasteable profiles. It is not a hosted service, API, or web app. If the clone you are looking at was minted under a temporary slug, treat **`grok-bot-ops-graph`** as the intended name. Playbook version: **v0.1** ([STATUS.md](STATUS.md)).

## What it is and why

You, the human (`YOUR_NAME`), give **one OBJECTIVE** to **one Bot**: `chief`.

`chief` decomposes that objective, routes **compact handoff packets** (not chat transcripts), and keeps irreversible actions parked for you. Specialists do one job each:

| Role | Job |
| --- | --- |
| `research` | Cited packs. Sources, claims, gaps. |
| `drafts` | Turns packs into prose, diffs, or copy. |
| `checker` | Independent review. Never builds what it checks. |
| `distribution` | Stages the final packet. Never publishes alone. |

Optional lane specialists (`infra`, `markets`, `video`, `code`, …) stay in their own chats. Pull them only when you ask, or when the specialty is unambiguous. One worked split is in [OPTIONAL/markets-desk-extension.md](OPTIONAL/markets-desk-extension.md). It is not part of the default group.

A persistent multi-agent desktop can keep working while you are away. The Ops Graph is a small operating model on top of that:

1. One objective in, not a task list.
2. Packets, not transcripts.
3. Parallelize only independent work.
4. Finish reversible work; park send / publish / purchase / delete / production / legal.
5. Promote autonomy only after clean runs.
6. One specialist message by default.

The diagram, job loop, approval line, and autonomy ladder are in [CHARTER.md](CHARTER.md). Packet JSON schema v0.1 is in [HANDOFFS.md](HANDOFFS.md). Conceptual inspiration and public product patterns are in [ATTRIBUTION.md](ATTRIBUTION.md).

## Prerequisites

- A product where you can create multiple named Bots, put five of them in one group chat, and share files on one computer. Job folders are the artifact bus. Public product entry points are listed in [ATTRIBUTION.md](ATTRIBUTION.md).
- A shell that can run `mkdir` and `cp`. The optional scrub checks use `rg` (ripgrep).
- No language runtime, package manager, compiler, or network service. v0.1 has no `package.json`, `Makefile`, `pyproject.toml`, or test runner ([STATUS.md](STATUS.md)).

Examples in this repo are fictional. When you copy them, keep the same shape and fill your own values later.

| Use this | Not this |
| --- | --- |
| `YOUR_NAME` | a real name or handle |
| `chief`, `research`, `drafts`, `checker`, `distribution` | a specific person's Bot names |
| `ops-graph/jobs/<slug>/` | host paths, VMIDs, home directories |
| `example.com` | private or personal domains |
| "research topic X", "draft changelog" | live customer work |

## Install, build, run, and test

There is nothing to install, build, or unit-test in this checkout. v0.1 deliberately omits hosted code. A packet JSON validator is listed in [STATUS.md](STATUS.md) as a later idea; this tree does not contain that script.

From the repository root, seed a local working tree and the fictional first job. `ops-graph/` is a working directory on the shared computer. It is not part of the template and is not committed here.

```bash
mkdir -p ops-graph/jobs
cp -R AGENT_PROFILES skills jobs/_example ops-graph/
cp -R jobs/_example ops-graph/jobs/topic-x-changelog
find ops-graph -print | sort
```

`topic-x-changelog` is the slug for the first fictional run only. Later jobs get a new slug. Do not pile objectives into `jobs/_example/`.

Optional read-only scrub searches, copied from [STATUS.md](STATUS.md). Do not paste hits back into a public fork. These commands match words in the audit itself (and the filename `markets-desk-extension`, which contains the letters `sk-`). They are not a test suite.

```bash
rg -n -i "@[a-z0-9._%+-]+\\.[a-z]{2,}"
rg -n -i "api[_-]?key|bearer |sk-|token="
rg -n "[0-9]{1,3}(\\.[0-9]{1,3}){3}"
rg -n -i "ticker|broker|account number"
```

## Usage

Full recipe: [STANDUP.md](STANDUP.md). A new `chief` runs the loop from [skills/ops-graph-team/SKILL.md](skills/ops-graph-team/SKILL.md) plus [HANDOFFS.md](HANDOFFS.md).

1. Read [CHARTER.md](CHARTER.md) once.
2. Create five Bots from [AGENT_PROFILES/](AGENT_PROFILES/). Set each **name** exactly as below and paste the fenced blurb under "Paste this" in that file. Attach the skill to `chief` only for v0.1.

   | Name | Title | Profile |
   | --- | --- | --- |
   | `chief` | Chief of staff | [AGENT_PROFILES/chief.md](AGENT_PROFILES/chief.md) |
   | `research` | Research | [AGENT_PROFILES/research.md](AGENT_PROFILES/research.md) |
   | `drafts` | Drafts | [AGENT_PROFILES/drafts.md](AGENT_PROFILES/drafts.md) |
   | `checker` | Checker | [AGENT_PROFILES/checker.md](AGENT_PROFILES/checker.md) |
   | `distribution` | Distribution | [AGENT_PROFILES/distribution.md](AGENT_PROFILES/distribution.md) |

3. Create a group named `ops-graph` with exactly those five Bots. You talk to `chief`. `chief` talks to one specialist per message.
4. Run the seed commands above so `ops-graph/jobs/topic-x-changelog/PLAN.md` exists.
5. In the group, mention only `chief` and paste:

```
@chief OBJECTIVE

Research topic X. Produce a cited pack, then a draft changelog
for the notes page at https://example.com/notes/changelog.
Stage a human packet. Do not publish.

Constraints:
- one specialist message per route
- packets, not transcripts (schema in HANDOFFS.md)
- checker never edits the draft
- distribution never publishes
- park send / publish / purchase / delete / production / legal for me (YOUR_NAME)

Start from ops-graph/jobs/topic-x-changelog/PLAN.md
Return to me only at next_gate or if blocked on a decision I must make.
```

A clean loop is research pack, then draft, then checker findings (no rewrite of the draft), then a staging file. Publish stays with you. Sequence and troubleshooting are in [STANDUP.md](STANDUP.md).

Core rules:

1. **One OBJECTIVE.** You do not dump a task list on the group.
2. **Packets.** Every route carries artifacts, decisions, constraints, open_questions, next_gate.
3. **Lane discipline.** Research cites. Drafts write. Checker never authors the artifact it reviews. Distribution stages only.
4. **Independence test.** Two workstreams run in parallel only if neither needs the other's output.
5. **Reversibility.** If it cannot be undone locally, it parks for `YOUR_NAME`.
6. **Ladder.** observe, prepare, approve, schedule/trigger, coordinate. Promote a Bot one rung after clean runs.
7. **Specialty pull.** Existing lane Bots stay put. `chief` does not recruit them into the ops-graph group.
8. **Quiet graph.** Default is one specialist ping.

Boundaries recorded in [STATUS.md](STATUS.md) and [CHARTER.md](CHARTER.md): this playbook is not financial, legal, or medical advice; it does not grant extra product features; it does not bypass the host product's approval, secret, or sharing controls; it is not a marketplace of named third-party Bots.

## Layout

```
README.md                 this file
ATTRIBUTION.md            sources
CHARTER.md                graph, roles, loop, gates, ladder
HANDOFFS.md               packet schema v0.1 and scrubbed examples
STANDUP.md                create Bots, group, first objective
STATUS.md                 v0.1 scope, later ideas, scrub audit
AGENT_PROFILES/           paste-ready profile blurbs
skills/ops-graph-team/    portable skill for chief (SKILL.md)
jobs/_example/            sample PLAN.md, packets/, artifacts/
OPTIONAL/                 markets desk note (not required for v0.1)
```

Example job after you copy `jobs/_example/`:

```
ops-graph/jobs/<slug>/
  PLAN.md
  packets/            handoff JSON (empty in the template)
  artifacts/
    research/         pack.md
    drafts/           changelog.md or other requested artifact
    checks/           findings.md
    staging/          human-packet.md
```

`checker` writes only under `checks/`. `distribution` writes only under `staging/`.

## License

This repository has no `LICENSE` file. The playbook's own terms are: copy the profiles, skill, and packet schema into your own Grok Bot (or similar) workspace; keep attribution if you republish the playbook ([ATTRIBUTION.md](ATTRIBUTION.md)); do not publish other people's transcripts, identifiers, or job artifacts.
