# Attribution

This playbook is an **operating model** you overlay on a multi-agent desktop assistant. It is not an official product manual.

## 1. Community write-up (conceptual inspiration)

**0xwhrrari**, “Grok Bot: The AI Team That Never Sleeps” (2026-09-03).

- Role in this repo: the idea that a persistent multi-agent desktop can run as a team that keeps working while the human sleeps — roster, parallel work, handoffs across a shared computer.
- URL: no stable public URL was verified at playbook freeze. Cite by **title + date** as a **community write-up**.
- What we took: the *shape* (named teammates, overnight progress, human as exception handler).
- What we did not take: any private setup, personal Bot roster, or unstated internals.

If you later find a canonical public URL, add it here. Do not add mirrors that are personal blogs, private shares, or login-gated dumps.

## 2. Product patterns (high-level, public)

Grok Bot and Cursor document persistent named Bots, a shared cloud computer, group chats, skills, and routines. Use the **current** public docs; UI labels drift.

Verified public entry points (high-level only):

- Grok Bot product overview — <https://x.ai/bot>
- Designing Grok Bot for persistent agents — <https://x.ai/news/designing-grok-bot>
- Cursor: getting started — <https://cursor.com/help/grok-bot/getting-started>
- Cursor: working with Bots (groups, skills, routines) — <https://cursor.com/docs/grok-bot/work>
- xAI: create and manage Bots / organize a team — <https://docs.x.ai/grok-bot/bots>
- xAI: FAQ (shared computer, skills vs routines, parallel work) — <https://docs.x.ai/grok-bot/faq>

**Patterns referenced, not internals:**

| Pattern | How this playbook uses it |
| --- | --- |
| Named Bots with a profile | Five default roles with paste-ready descriptions |
| Group chat for a shared outcome | One `ops-graph` group; you speak to `chief` |
| @-mention a teammate | One specialist per routing message |
| Shared files / computer | Job folders at `ops-graph/jobs/<slug>/` |
| Skills (`/` recipes) | `skills/ops-graph-team` encodes the loop |
| Routines (schedule / event) | Only after the skill has clean manual runs |
| Human approval for sensitive actions | Mapped onto the reversibility line |

Do not copy proprietary system prompts, unpublished tool schemas, or private screenshots into a public fork.

## 3. This playbook (operationalization)

**Ops Graph Playbook** (`grok-bot-ops-graph`) — the files in this repository.

This is the layer that turns “several Bots in a group” into a repeatable desk:

- Compact **handoff packets** instead of transcript-forwarding ([HANDOFFS.md](HANDOFFS.md)).
- **Approval-by-reversibility**: reversible work finishes; send / publish / purchase / delete / production / legal park for the human ([CHARTER.md](CHARTER.md)).
- **Autonomy ladder**: observe → prepare → approve → schedule/trigger → coordinate, with promotion only after clean runs ([CHARTER.md](CHARTER.md)).
- Lane rules: `checker` never builds what it checks; `distribution` never publishes alone; optional specialists stay out of the default group.

## How to cite

```
Ops Graph Playbook (grok-bot-ops-graph), v0.1.
Inspired by the community write-up 0xwhrrari,
“Grok Bot: The AI Team That Never Sleeps” (2026-09-03).
Product patterns from public Grok Bot / Cursor documentation
(x.ai/bot, cursor.com/docs/grok-bot/work, docs.x.ai/grok-bot).
Handoff packets, approval-by-reversibility, and the autonomy
ladder are specified by this playbook.
```
