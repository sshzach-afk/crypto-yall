# ZACH_CHANGELOG

> **⚠️ NOT PART OF THE ORIGINAL REPOSITORY.**
> This file was added by Zach (`sshzach-afk`) and does not exist in
> upstream `aicodepathways/crypto-yall`. Every `ZACH_*` file in this repo is
> local-only. Nothing here came from Josh Rhodes or Crypto Y'all.

## Baseline
Forked from `aicodepathways/crypto-yall` @ `43a163b` on 2026-08-24.

**No upstream Python has been modified.** Verify at any time:

```bash
git fetch upstream && git diff --stat upstream/main HEAD
```

Only `ZACH_*` files should appear. If any of Josh's files show up, something
was changed that shouldn't have been.

---

## 2026-08-24 — Initial setup
Followed `docs/AI_ASSISTED_SETUP.md`, Phases 1–8.

| Item | Value |
|---|---|
| Fork | `sshzach-afk/crypto-yall`, public |
| Network | testnet (`HL_TESTNET=true`) |
| Funding | 999 mock USDC (faucet) |
| Secrets / variables | 12 / 13, per the setup prompt |
| Capital | 1000 / 500 / 300 (as documented) |
| Test trade | passed — BTC round trip, −$0.0096 slippage |

### Deviation from the guide: Hyperliquid account type
Hyperliquid defaults new accounts to **Unified**, where balances consolidate
into the *spot* clearinghouse. The executors read `clearinghouseState` (perps),
which returns `accountValue: 0.0` under Unified regardless of actual balance.

Fix applied: **Account Type → Manual**, then **Transfer to Perps**.

Not covered in the setup guide; the troubleshooting table attributes an
equity of $0.00 to an unclaimed faucet.

---

## 2026-08-25 — Capital raised (deviation from documented values)

| Variable | Documented | Now |
|---|---|---|
| `SEGREGATED_CAPITAL` | 1000 | 1000 (unchanged) |
| `INTRADAY_CAPITAL` | 500 | **1000** |
| `AGGRESSIVE_CAPITAL` | 300 | **1500** |

**Reason.** Hyperliquid rejects *opening* orders below **$10 notional**
(reduce-only closes are exempt). Order size is
`notional = capital × POSITION_SIZE_PCT × leverage`, and the percentages are
hardcoded in the executors. At the documented capital values:

| Path | Notional | Result |
|---|---|---|
| Intraday, all assets | $10.00 | rejected after ROUND_DOWN |
| Aggressive SOL/AVAX/SUI | $8.98 | rejected |
| Aggressive pyramid, large cap | $5.99 | rejected |
| Aggressive pyramid, mid cap | $2.99 | rejected |

Observed: ~40 consecutive `open_long: error` results across Intraday and
Aggressive in the first 24 hours. Workflow runs still report **success**.

`round_size()` uses `ROUND_DOWN`, so a SOL pyramid (szDecimals=2, ~$100) can
lose up to ~$1 to truncation. Capital of 1050–1100 clears $10 only at some
prices; 1200+ clears at all tested prices. 1500 chosen for margin.

**Resulting smallest order:** Daily $15 · Intraday $20 · Aggressive $44.89 ·
pyramids $14.96–29.93.

**No code change was required or made for this.** GitHub repository variables only.
