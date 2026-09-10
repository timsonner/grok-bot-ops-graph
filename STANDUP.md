# Stand up the Ops Graph

Goal: a new user (or a newly created `chief`) can recreate the default team and finish one fictional objective without reading the rest of the repo first. Read this in order. Product UI labels change; the *intent* of each step does not.

Public product patterns (groups, skills, routines, shared computer) are summarized in [ATTRIBUTION.md](ATTRIBUTION.md). This page is the playbook’s recipe, not a vendor tutorial.

## Before you start

- You can create multiple named Bots and put several of them in one group chat.
- Bots on one account typically share a computer and files. That is why job folders work as the artifact bus.
- You will **not** paste real emails, hostnames, account numbers, or API keys into profiles.
- Optional lane Bots you already have (`infra`, `markets`, `video`, `code`, …) stay where they are. Do not add them to this group.

Working directory on the shared computer (create it once):

```
ops-graph/
  jobs/
  LADDER.md          # local, do not publish; autonomy promotions
```

Copy this repository’s `AGENT_PROFILES/`, `skills/`, and `jobs/_example/` into that tree, or keep this git checkout as the source of templates.

## Step 1 — Create five Bots

Create Bots in this order. Name, title, and description matter; they are the operating contract.

| Name | Title | Profile file |
| --- | --- | --- |
| `chief` | Chief of staff | [AGENT_PROFILES/chief.md](AGENT_PROFILES/chief.md) |
| `research` | Research | [AGENT_PROFILES/research.md](AGENT_PROFILES/research.md) |
| `drafts` | Drafts | [AGENT_PROFILES/drafts.md](AGENT_PROFILES/drafts.md) |
| `checker` | Checker | [AGENT_PROFILES/checker.md](AGENT_PROFILES/checker.md) |
| `distribution` | Distribution | [AGENT_PROFILES/distribution.md](AGENT_PROFILES/distribution.md) |

For each Bot:

1. Create a new Bot.
2. Set **name** exactly to the left column (lowercase).
3. Set **title** to the middle column.
4. Paste the **profile blurb** from the matching file (the fenced block under “Paste this”).
5. Do not add secrets, private URLs, or employer names to the profile.
6. Attach or install the skill on `chief` only for v0.1: [skills/ops-graph-team/SKILL.md](skills/ops-graph-team/SKILL.md). Other Bots get lane rules from their profile; they do not need the full skill.

If the product asks for an avatar: pick a color, not a photo of a person.

## Step 2 — Create the group channel

1. New group chat.
2. Add exactly these five: `chief`, `research`, `drafts`, `checker`, `distribution`.
3. Name the group `ops-graph`.
4. In the group topic / first pin (if you have one), paste:

```
Ops Graph. YOUR_NAME talks to @chief.
@chief routes packets to one specialist at a time.
Reversible work finishes in ops-graph/jobs/<slug>/.
send / publish / purchase / delete / production / legal PARK for YOUR_NAME.
```

You may DM `chief` instead of using the group. The group exists so handoffs are visible. Do **not** work the objective in five separate DMs.

## Step 3 — Seed the job folder

On the shared computer:

```
cp -R jobs/_example ops-graph/jobs/topic-x-changelog
```

Or create by hand:

```
ops-graph/jobs/topic-x-changelog/
  PLAN.md
  packets/
  artifacts/
    research/
    drafts/
    checks/
    staging/
```

Replace `PLAN.md` with the example in this repo, or copy its headings. Slug is `topic-x-changelog` for the first run only.

## Step 4 — First objective (you → `chief`)

In the `ops-graph` group, mention only `chief`. Paste:

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

That is the whole kickoff. Do not add a task list.

## Step 5 — What you should see

A clean first run looks like this. Times vary; sequence should not.

1. `chief` fills `PLAN.md` (slices, owners, independent? no for research→drafts).
2. `chief` @-mentions **only** `research` with packet `topic-x-changelog-01`.
3. `research` writes `artifacts/research/pack.md` and returns a packet to `chief`.
4. `chief` @-mentions **only** `drafts` with the accepted pack.
5. `drafts` writes `artifacts/drafts/changelog.md`.
6. `chief` @-mentions **only** `checker`. `checker` writes `artifacts/checks/findings.md` and does not patch the draft.
7. If findings fail: `chief` routes `drafts` again, then `checker` again. No shortcut.
8. `chief` @-mentions **only** `distribution`. Staging file appears. Live page is untouched.
9. `chief` parks a short note to you: path to `artifacts/staging/human-packet.md`, what you would paste, and that publish is yours.

If anyone @-mentions the whole group, if `checker` rewrites the changelog, or if someone opens `https://example.com/notes/changelog` to paste, stop the job and reset from the charter.

## Step 6 — Your human gate

Open `artifacts/staging/human-packet.md`. You either:

- publish it yourself, or
- tell `chief` to close the job as staged-only, or
- send one new OBJECTIVE if you want a revision (not a side-thread of nits to four Bots).

Write the close-out into `PLAN.md`.

## Step 7 — Only after a clean run

- Promote reversible job-folder edits on `chief` from **prepare** toward **approve** (see the ladder in [CHARTER.md](CHARTER.md)).
- Then, if you want overnight prep, add a **routine** that fires the skill on `chief` with a *new* objective you already wrote — still parking irreversible actions.
- Do not put routines on `distribution`.
- Do not add lane Bots to this group. To pull `code` (for example), `chief` sends one DM packet after you ask, or after the specialty is clear.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Four Bots reply to your kickoff | You addressed the group, not `@chief` | Restate: “only chief replies; others wait for a packet” |
| `drafts` starts during research | Parallelized a dependent slice | `chief` cancels drafts until pack status is `accepted` |
| `checker` commits a rewrite | Role bleed | Discard the rewrite; `drafts` owns the next patch |
| Packet is a screenshot of chat | Transcript-forwarding | Rewrite as JSON in `packets/` |
| Job folder missing | Shared computer path not created | Create `ops-graph/jobs/<slug>/` before routing |
| Secret in a profile or packet | Scrub failure | Delete the message/file; rotate the secret outside this playbook |

## Done

You have an Ops Graph when:

- five named Bots exist with the paste-ready profiles,
- one group `ops-graph` contains only those five,
- one job folder completed research → drafts → checker → staging,
- you were the only publisher.

Iterate with a new slug, not by piling objectives into the example folder.
