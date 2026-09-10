# PLAN — topic-x-changelog

Fictional example job. Copy this folder to `ops-graph/jobs/<slug>/` and rewrite the objective. Do not put real customer work in a public fork.

## Objective

Research topic X. Produce a cited pack, then a draft changelog for the notes page at `https://example.com/notes/changelog`. Stage a human packet. Do not publish.

## Out of scope

- Publishing or notifying anyone
- Adjacent topics unless they change the changelog
- Unofficial timelines (locked in packet 03 as D3)
- Contacting living people

## Slices

| ID | Owner | Input | Output | Independent? |
| --- | --- | --- | --- | --- |
| S1 | `research` | OBJECTIVE | `artifacts/research/pack.md` | n/a (first) |
| S2 | `drafts` | accepted pack | `artifacts/drafts/changelog.md` | **no** (needs S1) |
| S3 | `checker` | pack + draft | `artifacts/checks/findings.md` | **no** (needs S2) |
| S4 | `distribution` | accepted draft + findings | `artifacts/staging/human-packet.md` | **no** (needs S3 pass) |

No parallel slices in this job.

## Locked decisions

| ID | Statement | Locked by |
| --- | --- | --- |
| D1 | Topic is X only | `YOUR_NAME` |
| D2 | Destination is draft-only for `https://example.com/notes/changelog` | `YOUR_NAME` |
| D3 | Unofficial timeline out of scope | `chief` (after Q1) |

## Approval line

Reversible: files under this folder, including staging.

PARK for `YOUR_NAME`: send, publish, purchase, delete, production, legal.

`next_gate` after S4 is `human_approval`.

## Packets

Write JSON under `packets/` using [HANDOFFS.md](../../HANDOFFS.md). Do not store transcripts here.

## Close-out

- [ ] S1 pack attached
- [ ] S2 draft attached
- [ ] S3 verdict pass or pass-with-nits folded
- [ ] S4 staged
- [ ] `YOUR_NAME` published **or** explicitly closed as staged-only
- [ ] Group quieted
