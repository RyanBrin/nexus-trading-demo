# Nexus Trading Core — Project Overview (Demo)

> Public overview of a **private** project. This repository is documentation only:
> it contains **no source code, strategies, configuration, credentials, or real data**.

The Nexus trading core supports a multi-user, manual-execution workflow for research,
planning, confirmation, portfolio review, and journaling. It does not connect a plan to
broker execution and **never places an order**.

## Current workflow

```text
research -> opportunity -> review -> plan -> human execution outside Nexus -> recorded fill -> journal
                                           \-> simulated Paper fill ---------> Paper journal
```

- Plans and fills are distinct records; creating or approving a plan cannot create an order.
- Recorded fills require explicit human attestation that execution occurred elsewhere.
- Paper fills are simulated, cannot carry broker attestation, and remain in a separate ledger.
- Portfolio and journal views preserve the Recorded/Paper boundary.
- Stock and crypto paths remain separate so work on one cannot change the other's behavior
  as a side effect.

## Safety by construction

- There is no order-submission endpoint in the product.
- External market-data access is symbol-scoped and separated from account or order APIs.
- User-scoped storage prevents one account from reading or changing another account's data.
- Risk and workflow gates are tested invariants, not advisory UI text.
- Public copy and route-inventory tests guard against implying automated execution.

## Historical engine

An earlier autonomous paper-research engine covered crypto analysis and stock scanning.
It was retired non-destructively into an excluded legacy archive. Boundary tests prevent
the active manual product from importing that archived implementation.

## Technologies

- Python and FastAPI
- PostgreSQL with user-scoped persistence
- Symbol-level market-data adapters
- pytest-based safety and route-inventory checks
- Nexus web surfaces for planning, portfolio, and journal workflows

## Privacy and security posture

- No live-trading code or broker order path is published or active.
- No real balances, positions, fill history, account identifiers, or market-data credentials
  are included here.
- Secrets live only in private configuration and are never logged or committed.
- Any examples are sanitized or synthetic.

This project makes no financial-performance claim and is not financial advice.

See [`docs/architecture.md`](docs/architecture.md) for a high-level architecture summary.
