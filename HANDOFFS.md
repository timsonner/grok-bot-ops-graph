# Handoff packets

Specialists do not need the chat history. They need a **packet**: pointers to artifacts, locked decisions, constraints, open questions, and the next gate.

If a Bot cannot fill these fields, it is not ready to route.

## Schema (v0.1)

Copy-paste this object. Unknown fields are allowed but must not replace these.

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/<slug>/",
  "packet_id": "<slug>-<nn>",
  "from_role": "chief",
  "to_role": "research",
  "objective": "one sentence copied from PLAN.md",
  "context_for_this_slice": "what this recipient is being asked to do now",
  "artifacts": [
    {
      "path": "ops-graph/jobs/<slug>/artifacts/research/pack.md",
      "status": "needed | attached | accepted | blocked",
      "notes": "optional one-liner"
    }
  ],
  "decisions": [
    {
      "id": "D1",
      "statement": "locked choice",
      "locked_by": "YOUR_NAME | chief"
    }
  ],
  "constraints": [
    "do not publish",
    "cite every non-obvious claim",
    "stay inside the job folder"
  ],
  "open_questions": [
    {
      "id": "Q1",
      "ask": "what is still unknown",
      "blocks": "research | drafts | checker | distribution | none",
      "owner": "YOUR_NAME | chief | research"
    }
  ],
  "next_gate": {
    "type": "reversible_complete | specialist_handoff | human_approval",
    "owner": "chief | research | drafts | checker | distribution | YOUR_NAME",
    "done_when": "observable condition",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

### Field rules

| Field | Rule |
| --- | --- |
| `job_id` | Always the folder path convention `ops-graph/jobs/<slug>/`. Never a hostname, VMID, or home directory. |
| `from_role` / `to_role` | One of `YOUR_NAME`, `chief`, `research`, `drafts`, `checker`, `distribution`, or a generic lane (`infra`, `markets`, `video`, `code`). |
| `artifacts[].path` | Paths inside the job folder. No `file://`, no IPs, no private URLs. Public citations belong *inside* the research pack, not as packet destinations. |
| `decisions` | Only locked choices. Debates stay in `open_questions`. |
| `constraints` | Hard stops. Include the reversibility line every time. |
| `open_questions` | Empty array if none. Do not omit the key. |
| `next_gate.park_if` | Repeat the irreversible verbs so a specialist cannot miss them. |

### Allowed `next_gate.type` values

- `reversible_complete` — slice can finish in the job folder; `chief` may close it.
- `specialist_handoff` — output is an input to another role; `chief` routes the next packet.
- `human_approval` — irreversible, ambiguous, or budgeted; park for `YOUR_NAME`.

## How to send a packet

1. Write the JSON to `ops-graph/jobs/<slug>/packets/<packet_id>.json`.
2. In the group, @-mention **one** `to_role`.
3. Paste or attach the JSON (or a three-line summary plus the path).
4. Do not include prior messages, tool logs, or screenshots unless they are artifacts with paths.

Three-line summary (optional, above the JSON):

```
@research packet <slug>-01
objective: research topic X into a cited pack
next_gate: specialist_handoff → chief (then drafts)
```

## Anti-patterns

| Do not | Do |
| --- | --- |
| Forward the whole thread | Write a packet |
| @everyone “please read this” | @ one role |
| “see above” | Put a path in `artifacts` |
| Hide a publish step in a footnote | `next_gate.type = human_approval` |
| Ask `checker` to “also rewrite it” | Bounce findings to `chief` → `drafts` |
| Put secrets in the packet | Write `secret needed at gate` in `open_questions` and park |

## Example 1 — `chief` → `research`

Fictional objective: research topic X.

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/topic-x-changelog/",
  "packet_id": "topic-x-changelog-01",
  "from_role": "chief",
  "to_role": "research",
  "objective": "Research topic X and stage a draft changelog. Do not publish.",
  "context_for_this_slice": "Build a cited pack on topic X for a notes-page changelog. Audience is internal notes, not a press release.",
  "artifacts": [
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/research/pack.md",
      "status": "needed",
      "notes": "create this file; include claims table + source list"
    }
  ],
  "decisions": [
    {
      "id": "D1",
      "statement": "Topic is X. No adjacent topics unless they change the changelog.",
      "locked_by": "YOUR_NAME"
    },
    {
      "id": "D2",
      "statement": "Destination is a draft only, for https://example.com/notes/changelog",
      "locked_by": "YOUR_NAME"
    }
  ],
  "constraints": [
    "cite every non-obvious claim",
    "do not contact living people",
    "do not publish",
    "stay inside the job folder"
  ],
  "open_questions": [],
  "next_gate": {
    "type": "specialist_handoff",
    "owner": "chief",
    "done_when": "pack.md exists with claims, sources, gaps, and confidence",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

## Example 2 — `research` → `chief` (pack ready)

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/topic-x-changelog/",
  "packet_id": "topic-x-changelog-02",
  "from_role": "research",
  "to_role": "chief",
  "objective": "Research topic X and stage a draft changelog. Do not publish.",
  "context_for_this_slice": "Cited pack is ready for drafts. One gap remains; it does not block a conservative changelog.",
  "artifacts": [
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/research/pack.md",
      "status": "attached",
      "notes": "claims table + sources"
    }
  ],
  "decisions": [],
  "constraints": [
    "do not treat gaps as facts",
    "do not publish"
  ],
  "open_questions": [
    {
      "id": "Q1",
      "ask": "Is the unofficial timeline for topic X in scope, or only dated public notes?",
      "blocks": "none",
      "owner": "chief"
    }
  ],
  "next_gate": {
    "type": "specialist_handoff",
    "owner": "chief",
    "done_when": "chief accepts the pack and routes drafts",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

## Example 3 — `chief` → `drafts`

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/topic-x-changelog/",
  "packet_id": "topic-x-changelog-03",
  "from_role": "chief",
  "to_role": "drafts",
  "objective": "Research topic X and stage a draft changelog. Do not publish.",
  "context_for_this_slice": "Write changelog draft from the accepted pack. Ignore unofficial timeline (Q1 closed: out of scope).",
  "artifacts": [
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/research/pack.md",
      "status": "accepted",
      "notes": "input"
    },
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/drafts/changelog.md",
      "status": "needed",
      "notes": "output; short bullets, dated if the pack dates them"
    }
  ],
  "decisions": [
    {
      "id": "D3",
      "statement": "Unofficial timeline is out of scope.",
      "locked_by": "chief"
    }
  ],
  "constraints": [
    "no claim without a pack citation",
    "no marketing voice",
    "do not publish"
  ],
  "open_questions": [],
  "next_gate": {
    "type": "specialist_handoff",
    "owner": "chief",
    "done_when": "changelog.md exists and only uses pack-backed claims",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

## Example 4 — `chief` → `checker`

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/topic-x-changelog/",
  "packet_id": "topic-x-changelog-04",
  "from_role": "chief",
  "to_role": "checker",
  "objective": "Research topic X and stage a draft changelog. Do not publish.",
  "context_for_this_slice": "Independent review. Do not edit changelog.md. Write findings only.",
  "artifacts": [
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/research/pack.md",
      "status": "accepted"
    },
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/drafts/changelog.md",
      "status": "attached"
    },
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/checks/findings.md",
      "status": "needed"
    }
  ],
  "decisions": [
    {
      "id": "D3",
      "statement": "Unofficial timeline is out of scope.",
      "locked_by": "chief"
    }
  ],
  "constraints": [
    "never build or patch the draft you check",
    "flag overclaiming and missing citations",
    "flag any step that would publish",
    "do not publish"
  ],
  "open_questions": [],
  "next_gate": {
    "type": "specialist_handoff",
    "owner": "chief",
    "done_when": "findings.md lists pass/fail plus defects",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

## Example 5 — `chief` → `distribution` (stage, then park)

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/topic-x-changelog/",
  "packet_id": "topic-x-changelog-05",
  "from_role": "chief",
  "to_role": "distribution",
  "objective": "Research topic X and stage a draft changelog. Do not publish.",
  "context_for_this_slice": "Stage the approved draft for YOUR_NAME. Prepare the suggested paste and rollback note. Do not touch the live notes page.",
  "artifacts": [
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/drafts/changelog.md",
      "status": "accepted"
    },
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/checks/findings.md",
      "status": "accepted",
      "notes": "pass with nits already folded by drafts"
    },
    {
      "path": "ops-graph/jobs/topic-x-changelog/artifacts/staging/human-packet.md",
      "status": "needed"
    }
  ],
  "decisions": [
    {
      "id": "D2",
      "statement": "Destination is a draft only, for https://example.com/notes/changelog",
      "locked_by": "YOUR_NAME"
    }
  ],
  "constraints": [
    "never publish alone",
    "never log into the live notes page to paste",
    "do not send notifications"
  ],
  "open_questions": [],
  "next_gate": {
    "type": "human_approval",
    "owner": "YOUR_NAME",
    "done_when": "staging/human-packet.md contains paste body, destination URL, and rollback",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

## Parallel packets

Only if neither slice needs the other’s artifact. Example: `research` on topic X **and** `infra` gathering a local dry-run checklist for a different, already-locked decision.

Send two messages. Two packet files. No `@everyone`.

If `drafts` needs `research`, they are **not** independent. Sequence them.

## Minimal `PLAN.md` keys

Packets assume a plan exists. See [jobs/_example/PLAN.md](jobs/_example/PLAN.md). Required headings:

- Objective
- Out of scope
- Slices (owner, input artifact, output artifact, independent?)
- Locked decisions
- Approval line
- Close-out
