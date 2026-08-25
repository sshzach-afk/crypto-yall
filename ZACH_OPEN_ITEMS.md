# ZACH_OPEN_ITEMS

> **NOT IN THE ORIGINAL REPO.** Added by Zach (`sshzach-afk`). See `ZACH_CHANGELOG.md`.

### Open
1. **Ask Discord about the $10 minimum before messaging Josh.** Members run 100–1500 capital; he may have already told people. Draft written, unsent.
2. **Analysis layer unbuilt.** `crypto-automation-lab` has only a read-only client — no round trips, attribution, or MFE/MAE.

### Watch
3. **Funding dominates.** First 23h: realized **+$0.012**, funding **−$0.795** (66×). The strategy never reads funding rates. Testnet rates are inflated, but the blind spot is real.
4. **ETH mispriced on testnet: +3.91%** vs mainnet (BTC +0.89%, SOL/AVAX/SUI within 0.2%). Testnet ETH results are not transferable.
5. **5 of 7 assets only.** LINK and XRP aren't listed on testnet.
6. **Public fork leaks config.** Variables print in plaintext in Actions logs; secrets stay masked. Accepted for unlimited minutes.
7. **Mid-cap pyramids stay rounding-sensitive** if capital is ever lowered.

### Known
8. Kill switches block new orders only — closing positions is manual, no flatten-all.
9. Upstream has zero tests.
10. Actions cron drifts 30–60 min.

### Undecided
- Mainnet timing.
- R-multiple method (needs ATR-at-entry from candles).
- Modifying upstream Python — default **no**, `ZACH_*` additions only.
