<div align="center">

<img src="https://raw.githubusercontent.com/bluestuff-io/gli-test-reports/main/assets/bluestuff-logo.svg" alt="BlueStuff Game Studio" height="44" />

# Game Test Report

### SlotForge One

**BlueStuff Game Studio — Automated Pre-Certification Testing**

**🟡 PASSED WITH NOTES**

</div>

| | |
|---|---|
| **Report Number** | `BS-SLOTFORGE-20260731-7E5B5696` |
| **Date of Report** | 2026-07-31 |
| **Issued By** | BlueStuff Game Studio · Automated Test Engine |
| **Report Recipient** | Smokestack |
| **Engine Under Test** | `slotforge` |
| **Standard Tested Against** | GLI-19 v3.0 — Interactive Gaming Systems |
| **Classification** | Pre-certification self-assessment (Non-Jurisdictional) |
| **Software Fingerprint** | `sha256:b7861063fdb9bc4fb98a0a18c7253564…` (34 files) |
| **Result Summary** | 3 passed · 0 failed · 1 warnings · 0 manual · 0 source findings |

> **Disclaimer.** This is an automated **pre-certification self-assessment** produced by BlueStuff Game Studio's own test engine, published unmodified — including any failures. It is tested **against** the GLI-19 v3.0 technical standard but is **not** an accredited-laboratory certification and does not imply affiliation with, or endorsement by, Gaming Laboratories International. Final certification requires an independent accredited testing laboratory.

## 1. Executive Summary

Every hard requirement that ran passed. Some results are provisional or need human review — see the notes below.

## 2. Scope & Evaluation Elements

The following elements were evaluated to the extent applicable to automated testing of this software:

| Element | Status |
|---|---|
| Software & System Version Control | ✅ Performed |
| Source Code Review | ✅ Performed |
| Game Accounting (RTP / payout) | ✅ Performed |
| RNG & Statistical Analysis (GLI-19 §3.2) | ✅ Performed |
| Functionality Testing | 🔵 Partial — see Requirement Results |

## 3. Requirement Results

Each row is a numbered requirement from GLI-19 v3.0. Every automated verdict carries the statistic, the p-value, the sample size and a seed that reproduces the exact run.

| Requirement | Result | Sample | Evidence |
|---|---|---|---|
| **3.2.2** | 🟢 PASS | 240,000 | p = 1.89e-2 |
| **3.2.3** | 🟢 PASS | 240,000 | p = 4.84e-1 |
| **3.2.4** | 🟢 PASS | 220,000 | p = 5.61e-1 |
| **4.7.1** | 🟡 WARN | 200,000 | — |

## 4. Requirement Detail

### 3.2.2 — 🟢 PASS

Shared RNG source (crypto-backed, used by every engine on this template). float() scaled to 32 bins, 2 independent draws combined by Fisher's method. 7 of the 7 tests named in §3.2.2 applied. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 3.584e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 3.584e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 3.460 | 4.840e-1 | yes |
| overlaps | (b) | 2.979 | 5.613e-1 | yes |
| coupon-collector | (c) | 7.618 | 1.066e-1 | yes |
| runs | (d) | 0.359 | 9.857e-1 | yes |
| interplay-correlation | (e) | 1.024 | 9.062e-1 | yes |
| serial-correlation | (f) | 0.451 | 9.781e-1 | yes |
| duplicates | (g) | 11.804 | 1.887e-2 | yes |

</details>

### 3.2.3 — 🟢 PASS

RNG output is uniformly distributed (float 32-bin: Fisher chi-square = 3.46, p = 0.4840; int 64-range: p = 0.3395).

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 3.460 | 4.840e-1 | yes |
| chi-square | (a) | 67.066 | 3.395e-1 | yes |

</details>

### 3.2.4 — 🟢 PASS

Independence of the shared RNG (serial, overlaps, interplay) and of each engine's per-round outcomes (slotforge-mvp). 4 of the 7 tests named in §3.2.2 applied. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 9.909e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 9.909e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| overlaps | (b) | 2.979 | 5.613e-1 | yes |
| interplay-correlation | (e) | 1.024 | 9.062e-1 | yes |
| serial-correlation | (f) | 0.451 | 9.781e-1 | yes |
| outcome-independence:slotforge-mvp | (f) | 1.693 | 9.037e-1 | yes |

</details>

### 4.7.1 — 🟡 WARN

Return-to-player measured per registered engine by driving play() with the template RNG:
  • example: no payouts observed over 100,000 spins — stub or non-payout engine; nothing to certify.
  • slotforge-mvp: RTP 94.148% ±7.792pp over 100,000 spins (hit 35.10%, max 1010.0x) — provisional (widen sample).
GLI-19 §4.7.1 requires a theoretical payout of at least 75%. (1 non-payout/stub engine(s) noted above.)

## 5. Source Code Review — attempts to break the game

No adversarial findings. The probes that were run (see reproduction section) did not surface an exploitable issue.

## 6. Software & System Version Control

A SHA-256 checksum was generated for each of the 34 source files in the engine under test. The aggregate fingerprint below is a single hash over all of them — any change to any tested file changes it, so this report is bound to exactly the code that was tested.

**Aggregate fingerprint:** `sha256:b7861063fdb9bc4fb98a0a18c7253564f1fd967bcd25db790cdfd7d17235caf6`

<details><summary>Per-file checksums</summary>

| File | Bytes | SHA-256 |
|---|---|---|
| `mock-rgs/server.js` | 6,941 | `efd3b571471ff87150983964…` |
| `package-lock.json` | 39,470 | `80396a8b9dc627a8b7bbf0e2…` |
| `package.json` | 650 | `dbe06c33c237788398400047…` |
| `src/adapters/InlineWallet.js` | 3,591 | `0f3d448ea065d1965b13372e…` |
| `src/adapters/RgsAdapter.js` | 11,741 | `bf249f586850cb72fe3d8be8…` |
| `src/adapters/WalletAdapter.js` | 1,827 | `96abb0fa90468bbcb94ab167…` |
| `src/app.js` | 2,960 | `4853c5de79c0d57c1eb9236d…` |
| `src/config/index.js` | 2,048 | `70ca00b00159577b15f39770…` |
| `src/engines/GameEngine.js` | 3,261 | `83d6fff9314cb1845d45e9e6…` |
| `src/engines/example/ExampleEngine.js` | 2,827 | `b146f8322209c3764e3ccb44…` |
| `src/engines/index.js` | 1,548 | `0b61a5e98c81add4284cc32b…` |
| `src/engines/slotforge-mvp/SlotForgeEngine.js` | 19,265 | `d1e0ebee4f7d106838d105f8…` |
| `src/engines/slotforge-mvp/analytics.js` | 7,427 | `b709c62a10f07eee7b5b7818…` |
| `src/engines/slotforge-mvp/defaultMath.js` | 17,834 | `6873b7255c0b10641b26508d…` |
| `src/middleware/errorHandler.js` | 936 | `e3c1912b7fe62a86a9cd2101…` |
| `src/models/index.js` | 4,175 | `763a60ca94e6cec820e5a643…` |
| `src/routes/config.js` | 957 | `a4c5adc3cd5cceaabe52e338…` |
| `src/routes/game.js` | 1,742 | `07682a3da73b014775f1f849…` |
| `src/routes/session.js` | 1,309 | `f3d8ea81cc657ab654454dce…` |
| `src/server.js` | 1,010 | `cda1ea92956411d4dd947b9b…` |
| `src/services/AuditService.js` | 1,205 | `2887a68af4ba2500ecb7253f…` |
| `src/services/GameService.js` | 13,281 | `2111fc9a04afb7c075079053…` |
| `src/services/SessionManager.js` | 3,501 | `9a133289e6702199ceb7f634…` |
| `src/store/index.js` | 554 | `90e0279b64368867bc0597d7…` |
| `src/store/memoryStore.js` | 1,524 | `33fcc249eed7130402f9feaa…` |
| `src/store/mongoStore.js` | 1,177 | `89d67140ee3156976ce56174…` |
| `src/utils/errors.js` | 1,710 | `0d4ee388580860da1abad1cb…` |
| `src/utils/ids.js` | 1,036 | `19816c83e246299f080e62fb…` |
| `src/utils/logger.js` | 1,938 | `6ab4fc4d1af74e62a7a47b58…` |
| `src/utils/money.js` | 996 | `6b633695f0ace232e6cdbf28…` |
| `src/utils/rng.js` | 1,106 | `6a75832219a1d9540812f8aa…` |
| `tests/lifecycle.test.js` | 11,972 | `e4c304aebdb95a95b6f146c1…` |
| `tests/rgs-adapter.test.js` | 8,944 | `d75b50b824c88f8ab9e776de…` |
| `tests/slotforge-mvp.test.js` | 44,552 | `e352794f8295f43f63be0eaa…` |

</details>

## 7. Verification & Reproduction

The test engine has no dependencies and no LLM in its numeric path — every statistic is computed by reviewable in-tree code. Anyone can reproduce this run:

```bash
node src/cli.ts --engine=slotforge --repo=D:\Projects\smokestack-original-games\BackendEngines\slotrocket-5c5a --samples=60000 --spins=100000 --replicates=2 --seed=branded
```

_The seven statistical tests are the ones GLI-19 §3.2.2 names explicitly (chi-square, overlaps, coupon collector, runs, interplay correlation, serial correlation, duplicates), evaluated collectively at 99% family-wise confidence and combined across independent replicate seeds._

## 8. Test Environment

| | |
|---|---|
| Test engine | SportsITDev/gli-audit-engine |
| Runtime | Node v24.14.0 |
| Seed | `branded` |
| Started | 2026-07-31T09:27:43.674Z |
| Finished | 2026-07-31T09:27:45.870Z |
| Generated by | gli-audit-engine game-tester agent |

---

<div align="center">

<img src="https://raw.githubusercontent.com/bluestuff-io/gli-test-reports/main/assets/bluestuff-logo.svg" alt="BlueStuff Game Studio" height="28" />

**BlueStuff Game Studio** · Automated Game Test Engine

Report `BS-SLOTFORGE-20260731-7E5B5696` · Generated 2026-07-31T09:27:45.870Z

</div>
