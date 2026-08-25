# ZACH_OPEN_ITEMS

> **⚠️ NOT PART OF THE ORIGINAL REPOSITORY.**
> Added by Zach (`sshzach-afk`). Does not exist upstream in
> `aicodepathways/crypto-yall`. See `ZACH_CHANGELOG.md`.

Status key: 🔴 blocking · 🟡 watch · 🟢 informational

---

## 🔴 Open

**1. Raise the $10 minimum with the group before messaging Josh**
Members run capital from 100 to 1500 — no two alike. Some may already have been
told to raise it. Ask in Discord first; the docs may simply be stale rather
than wrong-and-unknown. Draft message prepared, not sent.

**2. Mid-cap pyramids remain price-sensitive**
`round_size()` truncates (ROUND_DOWN). At `AGGRESSIVE_CAPITAL=1500` all tested
SOL prices ($85–120) clear $10, but this is a floor that does not scale with
capital. Re-check if capital is ever lowered.

**3. Analysis layer not built**
`crypto-automation-lab` (separate project) is scaffolded but only has a
read-only Hyperliquid client. No round-trip reconstruction, no attribution,
no MFE/MAE yet.

---

## 🟡 Watch

**4. Funding cost is untracked and dominant**
First 23h: realized P&L **+$0.012**, funding paid **−$0.795**. Funding was 66×
the realized P&L. The strategy has no funding awareness — it does not read
funding rates when selecting entries. Testnet rates are unrealistic
(ETH ~0.4%/hr vs ~0.01%/hr typical mainnet), so the magnitude will not carry
over, but the structural blind spot will.

**5. ETH is mispriced on testnet**
Testnet vs mainnet, measured 2026-08-24: BTC +0.89%, **ETH +3.91%**,
SOL +0.15%, AVAX +0.02%, SUI −0.14%. A z-score oscillator on a book that
dislocated will produce genuinely different entries. **Treat testnet ETH
results as non-transferable.**

**6. Only 5 of 7 assets trade on testnet**
LINK and XRP return `None` from the testnet info API — not listed. 29% of the
documented universe is untested.

**7. Public fork exposes configuration**
Repository *variables* print in plaintext in Actions logs, and public repos
have public logs. Capital settings, DD thresholds and equity are world-readable.
Secrets are masked (`***`), including the account address. Accepted trade-off
for unlimited Actions minutes.

---

## 🟢 Informational

**8. Kill switches do not close positions**
They block new orders only. A full stop is all three switches OFF **plus**
closing by hand in the Hyperliquid UI. No flatten-all exists.

**9. Upstream has no tests**
Zero test files in `aicodepathways/crypto-yall`.

**10. Cron drift**
GitHub Actions free tier is best-effort; 30–60 min delays expected. The
30-minute Aggressive bot is not reliably a 30-minute bot.

---

## Decisions not yet made

- **Mainnet timing.** Currently testnet. No date set.
- **R-multiple methodology.** Needs ATR-at-entry reconstructed from candles.
- **Whether to ever modify upstream Python.** Default: no. See the rule in
  `ZACH_CHANGELOG.md` — only `ZACH_*` files are added, nothing of Josh's is edited.
