# Evidence — 2026-08-08-slots-test-2-cdd1e66d

This folder holds the evidence behind every result in the test report. Each file is plain Markdown and independently checkable.

## This test run at a glance

| | |
|---|---|
| **Standard tested against** | GLI-19 v3.0 |
| **Game engine family** | `slots` |
| **Exact code tested** | `sha256:2457a837740120b17d5e5409…` over 62 files |
| **Random seed** | `gli-1786181394271` |
| **Run started / finished** | 2026-08-08T09:29:54.366Z → 2026-08-08T09:37:00.645Z |
| **Outcome** | 2 passed · 1 failed · 1 warnings · 9 manual |

## Files

| File | What it is |
|---|---|
| [3.2.2.md](./3.2.2.md) | What was tested for requirement 3.2.2, how it was tested, and the full measured result. |
| [3.2.3.md](./3.2.3.md) | What was tested for requirement 3.2.3, how it was tested, and the full measured result. |
| [3.2.4.md](./3.2.4.md) | What was tested for requirement 3.2.4, how it was tested, and the full measured result. |
| [4.7.1.md](./4.7.1.md) | What was tested for requirement 4.7.1, how it was tested, and the full measured result. |
| [4.7.3.md](./4.7.3.md) | What was tested for requirement 4.7.3, how it was tested, and the full measured result. |
| [custom-4.7.3.md](./custom-4.7.3.md) | What was tested for requirement custom:4.7.3, how it was tested, and the full measured result. |
| [custom-4.7.3-cdd1.md](./custom-4.7.3-cdd1.md) | What was tested for requirement custom:4.7.3, how it was tested, and the full measured result. |
| [custom-4.7.1.md](./custom-4.7.1.md) | What was tested for requirement custom:4.7.1, how it was tested, and the full measured result. |
| [custom-4.7.1-cdd1.md](./custom-4.7.1-cdd1.md) | What was tested for requirement custom:4.7.1, how it was tested, and the full measured result. |
| [custom-4.7.3-cdd1.md](./custom-4.7.3-cdd1.md) | What was tested for requirement custom:4.7.3, how it was tested, and the full measured result. |
| [custom-4.7.3-cdd1.md](./custom-4.7.3-cdd1.md) | What was tested for requirement custom:4.7.3, how it was tested, and the full measured result. |
| [custom-4.7.1-cdd1.md](./custom-4.7.1-cdd1.md) | What was tested for requirement custom:4.7.1, how it was tested, and the full measured result. |
| [custom-4.7.1-cdd1.md](./custom-4.7.1-cdd1.md) | What was tested for requirement custom:4.7.1, how it was tested, and the full measured result. |
| [adversarial-findings.md](./adversarial-findings.md) | Every "attempt to break the game" probe and what it found (empty if none). |
| [live-tests.md](./live-tests.md) | Runtime checks played against the live deployed game — double-spend, session/validation, and the deployed-vs-certified RTP cross-check. |
| [checksums.md](./checksums.md) | SHA-256 of each of the 62 tested source files, plus the aggregate fingerprint this report is bound to. |

## How to verify a result yourself

Every result carries the **random seed** that produced it. The test engine has no external dependencies and no AI in its numeric path, so re-running with the same seed reproduces the same numbers exactly. Because the source files are checksummed (`checksums.md`), you can also confirm the code that was tested is exactly the code that is deployed.
