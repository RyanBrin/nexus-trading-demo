# Architecture (high level)

> Sanitized overview only. No source, no strategies, no config, no real data.

## Components

- **Market data ingest** — pulls public market data for monitoring.
- **Strategy/research engine** — evaluates strategy ideas in **paper mode**;
  BTC/crypto and stock logic are kept separate.
- **Risk controls** — safety floors and limits applied to simulated activity.
- **Options research lab** — isolated, **research/paper-only**, no execution.
- **Reporting/notifier** — summaries; dry-run by default.
- **Dashboard** — private local research view.

## Flow

```
market data ──> research/strategy engine (paper mode) ──> risk controls
                                                              │
                                            ┌─────────────────┴───────────────┐
                                            ▼                                 ▼
                                      private dashboard                 reports / (opt-in) notifier
```

## Principles

- **Paper/research first** — no live execution in scope for the public overview.
- **Separation** of crypto vs stock strategy logic; options lab isolated.
- **No secrets in code** — exchange/broker keys and account IDs in private config
  only.

## Boundaries

- No live trading code, broker/exchange identifiers, or API keys exposed.
- No real financial data. Real implementation and history remain private.
