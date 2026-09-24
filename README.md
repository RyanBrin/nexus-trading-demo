# Hermes Trading — Project Overview (Demo)

> Public overview of a **private** project. This repository is documentation only —
> it contains **no source code, no strategies, no configuration, and no real data**.
> The real implementation is kept in a private repository.

Hermes is the **trading core inside [Nexus](https://github.com/RyanBrin/nexus-demo)** —
**manual-first and paper-only**. It powers the plan → confirm → journal workflow:
market data, watchlists, research surfaces, instrument-scoped review checklists,
a reconciled paper portfolio, and a trade journal. The platform **never places an
order**; every trading decision is the user's own.

## History: the autonomous era, retired properly

Hermes began as an autonomous **paper**-research engine — Elliott Wave and
Fibonacci analysis over a unified crypto engine (BTC/ETH/SOL) plus a stock
scanner, with decision logging and a hardcoded risk firewall. That engine was
**retired non-destructively** into a legacy archive: ~80 modules and their tests
moved intact, with **archive-boundary tests** that fail the build if live code
ever imports from the archive again. Retiring a system cleanly — instead of
deleting it or letting it rot — turned out to be one of the project's best
engineering lessons.

## What the core enforces today

- **Paper-only by hard rule** — live trading is disabled everywhere; the safety
  invariant is written down, tested, and binding on both humans and the AI
  coding agents that work on the codebase.
- **Risk floors as constants** — minimum-confidence and risk gates are hardcoded
  floors, not tunable settings.
- **Separation of concerns** — stock and crypto logic stay isolated; nothing can
  alter the core crypto path as a side effect.
- **A paper ledger with structural honesty** — simulated fills can never carry
  the attestations of real ones, so nothing simulated ever reaches holdings,
  analytics, or the journal disguised as real.

## Privacy & security posture

- **No live trading code and no order path.** Market data is read from a
  broker's data API through a client built so that misuse is structural rather
  than a matter of discipline: one HTTP verb, and a host-and-path allowlist
  checked before a socket is opened, so no account or trading endpoint is
  reachable from the product. The key is a paper-account key, lives only in
  private config, and is never committed or logged.
- Secrets live only in private local config and are never committed.
- No real financial data, balances, or order history is included here.

## Technologies

- Python (data layer, portfolio reconciliation, safety gating)
- Market data by symbol only — no account-linked data sources
- Served through the Nexus platform (FastAPI + vanilla JS)

## Notes

- The real source code and commit history are **private**.
- This is **not** financial advice and makes no performance claims. Any examples
  are **sanitized/mock**.

See [`docs/architecture.md`](docs/architecture.md) for a high-level architecture summary.
