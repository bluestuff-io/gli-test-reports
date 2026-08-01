<div align="center">

<img src="https://raw.githubusercontent.com/bluestuff-io/gli-test-reports/main/assets/bluestuff-logo.svg" alt="BlueStuff Game Studio" height="44" />

# Game Test Report

### Dangrondropa Mines

**BlueStuff Game Studio — Automated Pre-Certification Testing**

**🟡 PASSED WITH NOTES**

</div>

| | |
|---|---|
| **Report Number** | `BS-SPINNY-20260801-70EC6CF5` |
| **Date of Report** | 2026-08-01 |
| **Issued By** | BlueStuff Game Studio · Automated Test Engine |
| **Report Recipient** | 6a43beed9eae7b49adcdc60e |
| **Engine Under Test** | `spinny` |
| **Standard Tested Against** | GLI-19 v3.0 — Interactive Gaming Systems |
| **Classification** | Pre-certification self-assessment (Non-Jurisdictional) |
| **Software Fingerprint** | `sha256:c28f83af68b4d184d4210e86e52d5357…` (30 files) |
| **Result Summary** | 3 passed · 0 failed · 0 warnings · 1 manual · 0 source findings |

> **Disclaimer.** This is an automated **pre-certification self-assessment** produced by BlueStuff Game Studio's own test engine, published unmodified — including any failures. It is tested **against** the GLI-19 v3.0 technical standard but is **not** an accredited-laboratory certification and does not imply affiliation with, or endorsement by, Gaming Laboratories International. Final certification requires an independent accredited testing laboratory.

## 1. Executive Summary

Every hard requirement that ran passed. Some results are provisional or need human review — see the notes below.

### Evaluator's Assessment

_The following assessment is the reasoned opinion of the automated evaluator, based strictly on the measured results in this report._

## GLI-19 Compliance Evaluation — Spinny
**Game ID:** ea4b051c-ca04-410d-98d5-fc52a59a4872 | **Engine:** spinny | **Run:** 70ec6cf5 | **Date:** 2026-08-01

---

### Overall Determination: **Inconclusive — Not Fully Tested**

The RNG subsystem is statistically sound, but the game's payout math has not been verified. Spinny **cannot be certified for real-money operation** at this time. This is not a marginal result — it is a fundamental gap: the engine produced zero payouts across 200,000 simulated spins, leaving the single most player-critical requirement (§4.7.1 RTP) unresolvable by any statistical method.

---

### What Passed

The shared crypto-backed RNG clears all three applicable GLI-19 RNG clauses at the 99% family-wise confidence level:

| Clause | Verdict | Key Statistic |
|--------|---------|---------------|
| §3.2.2 — Statistical quality (7 tests) | **PASS** | Fisher combined p = 0.416; 0 of 7 tests rejected (Holm–Bonferroni) |
| §3.2.3 — Uniform distribution | **PASS** | Float 32-bin p = 0.093; int 64-range p = 0.816 |
| §3.2.4 — Independence | **PASS** | Fisher combined p = 0.664; 0 of 3 tests rejected |

These results are based on 600,000 samples across 5 independent replicates. The RNG is fit for purpose and would not require re-testing if only the game-math layer changes.

---

### The Blocking Issue: §4.7.1 — Return to Player (MANUAL)

The audit engine drove 200,000 spins against the registered backend and observed **no payouts**. The engine is either a stub, an integration placeholder, or is missing the payout-resolution logic entirely. The §4.7.1 verdict is MANUAL — not a borderline fail, but an untestable state. Concretely:

- **For players:** An operator cannot lawfully represent this game as having a certified RTP. Any displayed RTP figure (e.g. "96%") would be unsubstantiated.
- **For operators:** Deploying this build to real-money wallets exposes the operator to regulatory enforcement. Any jurisdiction that requires pre-certification would not accept a MANUAL verdict here.
- **For certification:** §4.7.1 is not waivable. The RTP measurement must be repeatable and deterministic before the audit can close.

---

### Adversarial Findings

No adversarial findings were returned. This is reported as measured — it does not imply the backend was fully exercised. Runtime probes (concurrent-bet race conditions, cash-out after settlement, session fixation) require a running containerised backend; those classes were **not tested** in this run and remain open.

---

### Recommendations (prioritised)

1. **[Blocking]** Implement and connect the payout resolver in the spinny backend engine. The `play()` path must return multiplier outcomes that the audit engine can observe. Re-run §4.7.1 with `--spins=200000` (minimum); 1,000,000+ spins is recommended for a target RTP above 95% to achieve statistical power.
2. **[Blocking before live]** Once a containerised backend exists, re-run adversarial probes to cover the runtime attack surface (double-spend, cash-out timing, session fixation). The current clean adversarial result reflects an untested scope, not a confirmed clean state.
3. **[No action needed]** RNG clauses §3.2.2, §3.2.3, §3.2.4 are clear. Do not re-test these unless the RNG implementation changes.

This report should **not** be staged for public certification publication until §4.7.1 returns a measurable verdict. The current state is suitable only as an internal development checkpoint confirming RNG readiness.

## 2. Scope & Evaluation Elements

The following elements were evaluated to the extent applicable to automated testing of this software:

| Element | Status |
|---|---|
| Software & System Version Control | ✅ Performed |
| Source Code Review | ✅ Performed |
| Game Accounting (RTP / payout) | ⚪ Not applicable / manual |
| RNG & Statistical Analysis (GLI-19 §3.2) | ✅ Performed |
| Functionality Testing | 🔵 Partial — see Requirement Results |

## 3. Requirement Results

Each row is a numbered requirement from GLI-19 v3.0. Every automated verdict carries the statistic, the p-value, the sample size and a seed that reproduces the exact run.

| Requirement | Result | Sample | Evidence |
|---|---|---|---|
| **3.2.2** | 🟢 PASS | 600,000 | p = 9.33e-2 |
| **3.2.3** | 🟢 PASS | 600,000 | p = 9.33e-2 |
| **3.2.4** | 🟢 PASS | 120,000 | p = 4.43e-1 |
| **4.7.1** | 🔵 MANUAL REVIEW | 200,000 | — |

## 4. Requirement Detail

### 3.2.2 — 🟢 PASS

Shared RNG source (crypto-backed, used by every engine on this template). float() scaled to 32 bins, 5 independent draws combined by Fisher's method. 7 of the 7 tests named in §3.2.2 applied. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 4.156e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 4.156e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 16.229 | 9.326e-2 | yes |
| overlaps | (b) | 9.966 | 4.435e-1 | yes |
| coupon-collector | (c) | 14.487 | 1.519e-1 | yes |
| runs | (d) | 10.412 | 4.051e-1 | yes |
| interplay-correlation | (e) | 8.309 | 5.987e-1 | yes |
| serial-correlation | (f) | 9.493 | 4.860e-1 | yes |
| duplicates | (g) | 3.244 | 9.751e-1 | yes |

</details>

### 3.2.3 — 🟢 PASS

RNG output is uniformly distributed (float 32-bin: Fisher chi-square = 16.23, p = 0.0933; int 64-range: p = 0.8155).

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 16.229 | 9.326e-2 | yes |
| chi-square | (a) | 52.845 | 8.155e-1 | yes |

</details>

### 3.2.4 — 🟢 PASS

Independence of the shared RNG (serial, overlaps, interplay) and of each engine's per-round outcomes (none playable). 3 of the 7 tests named in §3.2.2 applied. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 6.638e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 6.638e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| overlaps | (b) | 9.966 | 4.435e-1 | yes |
| interplay-correlation | (e) | 8.309 | 5.987e-1 | yes |
| serial-correlation | (f) | 9.493 | 4.860e-1 | yes |

</details>

### 4.7.1 — 🔵 MANUAL REVIEW

Return-to-player measured per registered engine by driving play() with the template RNG:
  • example: no payouts observed over 200,000 spins — stub or non-payout engine; nothing to certify.
No registered engine produced payouts — this backend has no certifiable game math yet. (1 non-payout/stub engine(s) noted above.)

## 5. Source Code Review — attempts to break the game

No adversarial findings. The probes that were run (see reproduction section) did not surface an exploitable issue.

## 6. Software & System Version Control

A SHA-256 checksum was generated for each of the 30 source files in the engine under test. The aggregate fingerprint below is a single hash over all of them — any change to any tested file changes it, so this report is bound to exactly the code that was tested.

**Aggregate fingerprint:** `sha256:c28f83af68b4d184d4210e86e52d53577f2b4c7a7bea72bdd86f66a41b8dc8f7`

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
| `src/engines/index.js` | 1,419 | `e3b360a4589c591a637805d2…` |
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

</details>

## 7. Verification & Reproduction

The test engine has no dependencies and no LLM in its numeric path — every statistic is computed by reviewable in-tree code. Anyone can reproduce this run:

```bash
node src/cli.ts --engine=spinny --repo=D:\Projects\Devops\MCP\mcp-server\.repo-cache\games\bluestuff-io__smokestack-original-games\BackendEngines\spinny --samples=100000 --spins=200000 --replicates=5 --seed=gli-1785584499864
```

_The seven statistical tests are the ones GLI-19 §3.2.2 names explicitly (chi-square, overlaps, coupon collector, runs, interplay correlation, serial correlation, duplicates), evaluated collectively at 99% family-wise confidence and combined across independent replicate seeds._

## 8. Test Environment

| | |
|---|---|
| Test engine | SportsITDev/gli-audit-engine |
| Runtime | Node v24.14.0 |
| Seed | `gli-1785584499864` |
| Started | 2026-08-01T11:41:40.006Z |
| Finished | 2026-08-01T11:41:44.064Z |
| Generated by | gli-audit-engine game-tester agent |

---

<div align="center">

<img src="https://raw.githubusercontent.com/bluestuff-io/gli-test-reports/main/assets/bluestuff-logo.svg" alt="BlueStuff Game Studio" height="28" />

**BlueStuff Game Studio** · Automated Game Test Engine

Report `BS-SPINNY-20260801-70EC6CF5` · Generated 2026-08-01T11:41:44.064Z

</div>
