# ZACH_CHANGELOG

> **NOT IN THE ORIGINAL REPO.** Added by Zach (`sshzach-afk`). All `ZACH_*` files
> are local-only and came from no one at Crypto Y'all.

**Baseline:** forked from `aicodepathways/crypto-yall` @ `43a163b`, 2026-08-24.
**No upstream file has been modified.** Check: `git fetch upstream && git diff --stat upstream/main HEAD`
— only `ZACH_*` should appear.

---

### 2026-08-24 — Setup
Followed `docs/AI_ASSISTED_SETUP.md` Phases 1–8. Testnet, 999 mock USDC,
12 secrets / 13 variables, capital 1000/500/300 as documented. Test trade passed.

**Deviation:** Hyperliquid defaults to **Unified** account type, which reports
`clearinghouseState.accountValue = 0` no matter the balance. The bots read that
field. Fixed via Account Type → **Manual** → Transfer to Perps. Not in the guide.

### 2026-08-25 — Capital raised

| Variable | Was | Now |
|---|---|---|
| `SEGREGATED_CAPITAL` | 1000 | 1000 |
| `INTRADAY_CAPITAL` | 500 | **1000** |
| `AGGRESSIVE_CAPITAL` | 300 | **1500** |

Hyperliquid rejects opening orders under **$10 notional** (closes exempt).
Size is `capital × POSITION_SIZE_PCT × leverage`; the percentages are hardcoded.
At the documented capital: intraday $10.00, aggressive mid-caps $8.98,
pyramids $2.99–$5.99 — all rejected. ~40 failed orders in 24h, while runs
still reported success.

`round_size()` truncates, so a SOL pyramid can lose ~$1 to rounding. 1200+
clears at all tested prices; 1500 chosen for margin.

**Variables only — no code changed.**
