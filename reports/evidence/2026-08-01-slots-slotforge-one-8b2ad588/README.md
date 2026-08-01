# Evidence — 2026-08-01-slots-slotforge-one-8b2ad588

This folder holds the evidence behind every result in the test report. Each file is plain Markdown and independently checkable.

| File | What it is |
|---|---|
| [3.2.2.md](./3.2.2.md) | The result, statistics and seed behind requirement 3.2.2. |
| [3.2.3.md](./3.2.3.md) | The result, statistics and seed behind requirement 3.2.3. |
| [3.2.4.md](./3.2.4.md) | The result, statistics and seed behind requirement 3.2.4. |
| [4.7.1.md](./4.7.1.md) | The result, statistics and seed behind requirement 4.7.1. |
| [adversarial-findings.md](./adversarial-findings.md) | Every "attempt to break the game" probe and what it found (empty if none). |
| [live-tests.md](./live-tests.md) | Runtime checks played against the live deployed game — double-spend, session/validation, and the deployed-vs-certified RTP cross-check. |
| [checksums.md](./checksums.md) | SHA-256 of each of the 34 tested source files, plus the aggregate fingerprint this report is bound to. |

## How to verify a result yourself

Every result carries the **random seed** that produced it. The test engine has no external dependencies and no AI in its numeric path, so re-running with the same seed reproduces the same numbers exactly. Because the source files are checksummed (`checksums.md`), you can also confirm the code that was tested is exactly the code that is deployed.
