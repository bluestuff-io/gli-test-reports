# Requirement custom:4.7.3 — 🔵 MANUAL REVIEW

> [Custom] Buy-bonus max win does not exceed declared 5000× stake cap — custom cases run against the game-engine-template contract, but this backend is not a template backend, so it was not executed here.

## What was tested

| | |
|---|---|
| **Requirement** | GLI-19 custom:4.7.3 (GLI-19 v3.0) |
| **Game engine family** | `slots` |
| **Rounds / outcomes used** | 0 |
| **Exact code tested** | `sha256:2457a837740120b17d5e5409…` over 62 source files |
| **Random seed** | `—` |
| **Measured at** | 2026-08-08T09:37:00.755Z |

## How it was tested

This is an **operator-defined check** added on top of the standard GLI-19 suite. It was evaluated by the test engine against the live engine code, using the same measured play-through as the standard payout tests.

## The result

**🔵 MANUAL REVIEW**

[Custom] Buy-bonus max win does not exceed declared 5000× stake cap — custom cases run against the game-engine-template contract, but this backend is not a template backend, so it was not executed here.

---

_Reproducible from the random seed `—`. The test engine has no external dependencies and no AI anywhere in its numeric path — every figure above is computed by reviewable, in-tree code, so re-running against the same engine with this seed reproduces these numbers exactly._
