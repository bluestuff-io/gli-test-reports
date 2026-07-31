# GLI-19 Test Report — Publish Pipeline Healthcheck

**🟡 PASSED WITH NOTES**

Every hard requirement that ran passed. Some results are provisional or need human review — see the notes below.

| | |
|---|---|
| Brand | smokestack |
| Engine | `slots` |
| Standard | GLI-19 v3.0 |
| Date | 2026-07-31 |
| Run ID | `a057d738-5c69-4766-9996-18a416268246` |
| Config fingerprint | `sha256:unknown` |
| Result | 3 passed · 0 failed · 1 warnings · 1 manual · 0 security findings |

> This report is generated automatically by an independent, open test engine and published unmodified — including any failures. It is a pre-certification quality check, not a substitute for certification by an accredited testing laboratory.

## What was tested

Each row is a numbered requirement from GLI-19 v3.0. Every automated verdict carries the statistic, the p-value, the sample size and a seed that reproduces the exact run.

| Requirement | Result | Sample | Evidence |
|---|---|---|---|
| **3.2.2** | 🟢 PASS | 60,000 | p = 1.11e-1 |
| **3.2.3** | 🟢 PASS | 60,000 | p = 9.61e-1 |
| **3.2.4** | 🟢 PASS | 90,000 | p = 9.37e-2 |
| **4.7.1** | 🟡 WARN | 30,000 | stat = 1.013 |
| **4.7.3** | 🔵 MANUAL REVIEW | 30,000 | — |

## Requirement detail

### 3.2.2 — 🟢 PASS

Usage "uniform scaling" (rng.int(0, 15)), 2 independent seeds combined by Fisher's method. 6 of the 7 tests named in §3.2.2 applied, 1 not applicable. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 7.725e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 7.725e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 7.506 | 1.115e-1 | yes |
| overlaps | (b) | 0.404 | 9.821e-1 | yes |
| coupon-collector | (c) | 4.044 | 4.001e-1 | yes |
| runs | (d) | 2.450 | 6.536e-1 | yes |
| interplay-correlation | (e) | — | — | no — no multi-value draws supplied; engine emits a single value per draw |
| serial-correlation | (f) | 0.000 | 1.000e+0 | yes |
| duplicates | (g) | 2.807 | 5.906e-1 | yes |

</details>

### 3.2.3 — 🟢 PASS

Final outcome output over 11 symbols conforms to the declared weight profile "high" across 2 independent seeds (Fisher combined chi-square = 0.62, df = 4, p = 0.9609; worst single seed p = 0.8365). Symbols: chalice, crown, gem_blue, gem_green, gem_purple, gem_red, gem_yellow, hourglass, multiplier, ring, scatter.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| chi-square | (a) | 0.619 | 9.609e-1 | yes |

</details>

### 3.2.4 — 🟢 PASS

Independence between successive draws (serial correlation, lag-1 contingency) and within a single draw across 5 reels (interplay correlation), over 2 independent seeds. 3 of the 7 tests named in §3.2.2 applied. None rejected at the 99% family-wise confidence level (Holm–Bonferroni; Fisher combined p = 5.168e-1).

Evaluated collectively at 99% family-wise confidence (holm-bonferroni). Fisher combined p = 5.168e-1.

<details><summary>Per-test results</summary>

| Test | GLI §3.2.2 | Statistic | p-value | Applied |
|---|---|---|---|---|
| serial-correlation | (f) | 0.000 | 1.000e+0 | yes |
| overlaps | (b) | 1.716 | 7.879e-1 | yes |
| interplay-correlation | (e) | 7.944 | 9.365e-2 | yes |

</details>

### 4.7.1 — 🟡 WARN

Measured RTP 101.328% over 30,000 rounds (3-sigma interval 85.606%–117.050%, SE 5.2407pp). Declared target 96.50%. GLI-19 §4.7.1 floor is 75%: met. UNDERPOWERED: the 3-sigma interval spans 31.44pp, wider than the 0.50pp tolerance, so this run cannot confirm the declared target — it only fails to contradict it. Roughly 29,661,813 rounds are needed to resolve RTP to +/-0.50pp at this volatility. Treat as provisional. Hit rate 25.76%, feature rate 0.417%, max observed win 443.3x against a 5000x cap (cap reached 0 times).

### 4.7.3 — 🔵 MANUAL REVIEW

§4.7.3 requires the highest advertised award to occur at least once in 100,000,000 games unless prominently disclosed. The max-win cap is 5000x and was reached 0 times in 30,000 rounds. Establishing the cap frequency to the precision this clause needs requires a run several orders of magnitude larger; escalate to a dedicated long-run simulation.

## Adversarial testing — attempts to break the game

No adversarial findings. The probes that were run (see reproduction section) did not surface an exploitable issue.

## Method & reproduction

The test engine has no dependencies and no LLM in its numeric path — every statistic is computed by reviewable in-tree code. Anyone can reproduce this run:

```bash
node src/cli.ts --engine=slots --repo=D:\Projects\Devops\MCP\mcp-server\.repo-cache\games\bluestuff-io__smokestack-original-games\BackendEngines\slots --samples=30000 --spins=30000 --replicates=2 --seed=pub-e2e
```

| | |
|---|---|
| Engine source | SportsITDev/gli-audit-engine |
| Node | v24.14.0 |
| Seed | `pub-e2e` |
| Started | 2026-07-31T08:37:52.595Z |
| Finished | 2026-07-31T08:37:53.911Z |
| Generated by | gli-audit-engine game-tester agent |

_The seven statistical tests are the ones GLI-19 §3.2.2 names explicitly (chi-square, overlaps, coupon collector, runs, interplay correlation, serial correlation, duplicates), evaluated collectively at 99% family-wise confidence and combined across independent replicate seeds._
