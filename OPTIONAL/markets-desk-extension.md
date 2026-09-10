# Optional: markets desk (SCAN → chief)

**Not required for v0.1.** Do not add this Bot to the `ops-graph` group. Do not treat this file as trading advice, a broker guide, or a recommendation to buy or sell anything.

Use it only if `YOUR_NAME` already maintains a watch universe and wants a **scan packet** that `chief` can file, route to `research`, or park.

## Split

```
YOUR_WATCHLIST (names you already chose; not listed here)
        │
        v
   ┌─────────┐     one packet      ┌─────────┐
   │  SCAN   │ ─────────────────▶  │  chief  │
   │  (lane) │                     └────┬────┘
   └─────────┘                          │
                                  observe / prepare
                                          │
                          ┌───────────────┼───────────────┐
                          v               v               v
                     file only        research         PARK
                     (notes)        (cited pack     purchase /
                                     if asked)      order / advice
```

- `SCAN` lives in its own chat (or routine), not in `ops-graph`.
- `chief` is the only Ops Graph Bot that receives SCAN output.
- Default autonomy: **observe** (notes) or **prepare** (a packet). Never **approve** an order.
- `distribution` is not in this path. Nothing is published or sent to a broker.

## What SCAN may do

- Read a universe `YOUR_NAME` already named as `YOUR_WATCHLIST` (file on disk you maintain; this playbook does not include symbols).
- Write `ops-graph/jobs/<slug>/artifacts/research/scan-notes.md` *or* return a packet to `chief` with observations and confidence.
- Flag that a human should look. Flags are not orders.

## What SCAN must not do

- Name tickers, CUSIPs, or account numbers in any public copy of this repo (and avoid them in packets you might screenshot).
- Recommend a broker, venue, or product.
- Place, preview, or “arm” an order.
- Size a position, set a stop, or talk in share counts.
- Bypass `chief` to ping `drafts` / `distribution`.
- Present a scan as research. Research is a cited pack; a scan is a pointer.

## Packet extras (still schema v0.1)

Use the standard object. Put market-specific material in `context_for_this_slice` and `open_questions`, for example:

```json
{
  "packet_version": "0.1",
  "job_id": "ops-graph/jobs/watchlist-brief/",
  "packet_id": "watchlist-brief-01",
  "from_role": "markets",
  "to_role": "chief",
  "objective": "Prepare an observe-only briefing from YOUR_WATCHLIST. No orders.",
  "context_for_this_slice": "SCAN notes only. No symbols in this packet. Chief decides file vs research vs park.",
  "artifacts": [
    {
      "path": "ops-graph/jobs/watchlist-brief/artifacts/research/scan-notes.md",
      "status": "attached",
      "notes": "observe-only; no order language"
    }
  ],
  "decisions": [
    {
      "id": "D1",
      "statement": "Universe is YOUR_WATCHLIST as maintained by YOUR_NAME. Playbook contains no list.",
      "locked_by": "YOUR_NAME"
    }
  ],
  "constraints": [
    "not financial advice",
    "no broker recommendations",
    "no orders, previews, or arming of trades",
    "do not publish",
    "PARK purchase"
  ],
  "open_questions": [
    {
      "id": "Q1",
      "ask": "Should chief file these notes, ask research for a cited pack on the theme (not the symbols), or drop?",
      "blocks": "none",
      "owner": "chief"
    }
  ],
  "next_gate": {
    "type": "human_approval",
    "owner": "YOUR_NAME",
    "done_when": "chief has filed, routed research, or dropped — and no order exists",
    "park_if": ["send", "publish", "purchase", "delete", "production", "legal"]
  }
}
```

`purchase` here includes any order, conversion, or paid data upgrade you did not already authorize.

## Profile blurb for a generic `markets` lane Bot

Paste only if `YOUR_NAME` creates this lane. Keep it out of the default five.

```
You are markets, an optional lane Bot. You are not in the ops-graph group.

You SCAN a universe YOUR_NAME already maintains as YOUR_WATCHLIST.
You produce observe/prepare notes and one packet to chief.
You do not give financial advice. You do not recommend brokers.
You do not place, preview, or arm orders. You do not list symbols in
public documents. You do not talk to drafts, checker, or distribution.

Autonomy: observe by default. prepare packets only. PARK purchase.
```

## When `chief` should ignore a scan

- Packet contains order language or a broker name.
- Packet lists instruments (treat as a scrub failure; ask SCAN to rewrite).
- `YOUR_NAME` did not ask for markets work and the specialty is not clear.
- A routine fired without a job slug.

## Disclaimer

This extension is an **ops split** (who talks to whom). It is not research on any instrument, not a strategy, and not an invitation to automate trading.
