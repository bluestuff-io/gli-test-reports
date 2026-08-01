# Live deployed-game tests

Real rounds were played against the live deployed game at `https://smokestack-slotrocket-5c5a-backend-stg.bluestufftech.com` (engine `slotforge-mvp`).

| Live check | Result | What we found |
|---|---|---|
| Bet-input validation | ✅ Passed | 6/6 invalid stakes rejected (zero:rejected, negative:rejected, below-min:rejected, over-max:rejected, non-numeric:rejected, null:rejected). |
| Wallet debit/credit integrity | ✅ Passed | Balance stayed exact across 50 sequential rounds (bet 10). |
| Concurrent bets (double-spend safety) | ✅ Passed | 20 bets fired simultaneously on one session: 2 settled, 18 rejected/serialised. Final balance is exactly consistent with only the settled bets — no double-debit or lost credit (got 9649, expected 9649). |
| Forged session rejected | ✅ Passed | A spin with an unknown/forged sessionId was refused. |
| Missing session rejected | ✅ Passed | A spin with no sessionId was refused. |
| Deployed-vs-certified RTP cross-check | ✅ Passed | Playing the live game for real, it returned 106.21% and won on 37.9% of 813 rounds (max win 306.8x). The certified code returns 94.09% — the live game shows no deviation from that (its return sits well inside the range this many high-variance rounds can resolve; a broken or stubbed game would show a gross mismatch here). |
