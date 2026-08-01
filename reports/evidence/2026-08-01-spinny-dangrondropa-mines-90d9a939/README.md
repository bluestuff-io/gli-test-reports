# Evidence — 2026-08-01-spinny-dangrondropa-mines-90d9a939

This folder holds the raw evidence behind every result in the test report. 
Each file is machine-readable and independently checkable.

| File | What it is |
|---|---|
| [`3.2.2.json`](./3.2.2.json) | Full statistics, seed and reproduction command behind the 3.2.2 result. |
| [`3.2.3.json`](./3.2.3.json) | Full statistics, seed and reproduction command behind the 3.2.3 result. |
| [`3.2.4.json`](./3.2.4.json) | Full statistics, seed and reproduction command behind the 3.2.4 result. |
| [`4.7.1.json`](./4.7.1.json) | Full statistics, seed and reproduction command behind the 4.7.1 result. |
| [`adversarial-findings.json`](./adversarial-findings.json) | Every "attempt to break the game" probe and what it found (empty if none). |
| [`audit.full.json`](./audit.full.json) | The entire machine-readable audit: every verdict, every per-test statistic, the collective evaluation, seeds and commands. |
| [`live-tests.json`](./live-tests.json) | Runtime checks run against the live deployed container — double-spend, session/validation, and the deployed-vs-certified RTP cross-check, with the real rounds played. |
| [`checksums.json`](./checksums.json) | SHA-256 of each of the 30 tested source files, plus the aggregate fingerprint this report is bound to. |

## How to verify a result yourself

Every result carries a **seed** and the exact **command** that produced it. 
The test engine has no external dependencies and no AI in its numeric path — 
re-running the command with the same seed reproduces the same numbers, bit for bit. 
Because the source files are checksummed (`checksums.json`), you can also confirm 
the code that was tested is exactly the code that is deployed.
