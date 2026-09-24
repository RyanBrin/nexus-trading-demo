# Architecture (high level)

> Sanitized overview only. No source, no strategies, no config, no real data.

## Components

- **Market data ingest** — read-only public market data by symbol (quotes,
  snapshots, market clock and calendar). No account-linked source.
- **Watchlists & research** — stock and crypto watchlists with research surfaces
  feeding a review step; nothing here decides anything on its own.
- **Instrument review** — instrument-scoped checklists that the user works
  through before committing to a plan. Stock and crypto paths stay separate.
- **Paper ledger & portfolio** — simulated fills reconciled into a portfolio
  view, structurally separated so a simulated fill can never carry the
  attestations of a real one.
- **Journal** — the record of what was planned, what was done, and why.
- **Risk floors** — minimum-confidence and risk gates as hardcoded constants, not
  tunable settings, checked in the deployment gate.
- **Legacy archive** — the retired autonomous engine, preserved verbatim and
  fenced off by archive-boundary tests.

## Flow

```
market data ──> watchlists / research ──> instrument review (user) ──> plan
                                                                        │
                                                      confirm (user) ───┤
                                                                        ▼
                                                        paper ledger ──> portfolio
                                                                        └──> journal
```

Every arrow after "review" is a person deciding. There is no automated path from
a signal to an order, and no order path at all.

## Principles

- **Paper-only by hard rule** — the live-trading flag stays off, and a deployment
  gate fails the build if its default or its sanitizer changes.
- **Separation** of crypto vs stock logic; neither can alter the other as a side
  effect.
- **The archive stays archived** — tests fail the build if live code imports from
  the legacy engine again.
- **No secrets in code** — market-data keys and account IDs in private config
  only.

## Boundaries

- No order path and no account endpoint reachable from the product; no brokerage
  credential in this repo.
- No real financial data. Real implementation and history remain private.
