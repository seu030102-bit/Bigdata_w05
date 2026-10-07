# Task 2 · convergence curve (this machine)

**Machine:** AMD Ryzen 7 6800H, 16 GB RAM, Windows 11, Python 3.14.2.
Cursor and a browser were open.

## A2 · iterations against beta

Default graph: 1,200 nodes, `tol = 1e-10`.

| beta | iterations | time | top 3 |
|---:|---:|---:|---|
| 0.50 | 14 | 0.017 s | p00009, p00001, p00006 |
| 0.70 | 17 | 0.020 s | p00009, p00001, p00006 |
| 0.85 | 20 | 0.023 s | p00009, p00001, p00006 |
| 0.95 | 23 | 0.035 s | p00009, p00001, p00006 |
| 0.99 | 24 | 0.027 s | p00009, p00001, p00006 |

## A3 · shape as beta → 1

Iterations rise: 14 → 17 → 20 → 23 → 24. The Google matrix has second eigenvalue `beta`, so the error shrinks like `beta^t`. As beta approaches 1, `log(beta)` goes to 0 and you need more steps to drive the L1 change under `tol`. Teleport (`1 - beta`) is what mixes the walk; turn it down and the surfer stays on the link graph longer, so traps and hubs settle more slowly.

This graph still converges in the twenties even at 0.99 — faster than the worst-case `log(tol)/log(beta)` bound — but the **direction** of the curve is the textbook one.

## A4 · size: iterations vs time

| nodes | beta | iterations | time |
|---:|---:|---:|---:|
| 1,200 | 0.85 | 20 | 0.023 s |
| 20,000 | 0.85 | 21 | 0.660 s |
| 1,200 | 0.95 | 23 | 0.035 s |
| 20,000 | 0.95 | 24 | 0.756 s |

Predicted before the run: **iteration count stays put** (it is about `beta` and the spectral gap, not n); **wall time grows** (each iteration walks every edge). That is what happened. Nodes grew ~16.7×; time grew ~29×; iterations moved by 1. The surprise if you expected both to scale with n is that convergence is a property of the *operator*, not of the *size*.

## A5 · tolerance

Same 1,200-node graph, beta 0.85:

| tol | iterations |
|---|---:|
| 1e-6 | 12 |
| 1e-10 | 20 |

Four extra digits cost **8 iterations** — about **2 iterations per extra decimal place** on this graph.

## A6 · does the top 10 move?

Yes. At beta 0.5 the 7th/8th pages are `p00000`, `p00004`. From **beta 0.7** onward they swap to `p00004`, `p00000`. The top 6 stay fixed. So 0.85 is not a free choice: somebody picked it, and even a modest move from 0.5 already changes a published ranking.

## A7 · machine

AMD Ryzen 7 6800H, 16 GB, Windows 11, Python 3.14.2. Cursor + browser.
