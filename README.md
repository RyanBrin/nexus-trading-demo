# Hermes Trading — Project Overview (Demo)

> Public overview of a **private** project. This repository is documentation only —
> it contains **no source code, no strategies, no configuration, and no real data**.
> The real implementation is kept in a private repository.

Hermes is a **private market-research and paper-trading system** — a personal
research dashboard for monitoring markets and exercising strategy ideas in
**paper mode**.

## What it does

- Monitors market data and presents it on a private research dashboard.
- Runs strategies in **paper mode** (simulated) — research/education focused.
- Applies risk controls and safety limits to any simulated activity.

## Key features

- Paper-trading by default; safety floors and risk controls.
- Clear separation between BTC/crypto and stock strategy logic.
- An isolated options-research lab that is **research/paper-only** (no execution).
- Reporting and notifications that are dry-run by default.

## Privacy & security posture

- **No live trading code, broker/exchange details, or API keys are exposed** in
  this overview.
- Paper/research mode by default; real-money execution is out of scope for the
  public overview.
- Secrets (exchange/broker keys, tokens, account IDs) live only in private local
  config and are never committed.
- No real financial data, balances, or order history is included here.

## Technologies

- Python (data processing, strategy/research engine)
- Local dashboards and reporting; private configuration

## Notes

- The real source code and commit history are **private**.
- This is **not** financial advice and makes no performance claims. Any examples
  are **sanitized/mock**.

See [`docs/architecture.md`](docs/architecture.md) for a high-level architecture summary.
