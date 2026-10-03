---
title: Milestone 2 Staging UAT
description: Step-by-step staging verification for August 16 reader UX, billing history, admin view history, and payout workflow on snacktoons-development.zeekertech.com
sidebar_position: 2
---

# Milestone 2 — Staging UAT (August 16)

Use this guide to verify **Milestone 2: Reader, history, and reporting** on staging. Each section explains what was built, why it matters, and the exact clicks to confirm it works. Work through the scenarios in order, or jump to the [sign-off checklist](#sign-off-checklist) when you are ready to confirm completion.

**Staging site:** [https://snacktoons-development.zeekertech.com/](https://snacktoons-development.zeekertech.com/)

Related guides:

- [Comic discovery (reader)](../../reader/comic-discovery.md) — search and home sections
- [Reading experience (reader)](../../reader/reading-experience.md) — page/scroll modes and resume
- [Monetization & purchases (reader)](../../reader/monetization-purchases.md) — billing and coin history
- [Analytics & tracking](../analytics-tracking.md) — view history export
- [Testing subscription payouts](../monetization/testing-subscription-payouts.md) — payout approve/claim workflow

---

## SA-003 — Homepage featured and genre sections

**What this is:** The home page highlights **featured** comics and groups comics by **genre/category** so readers can browse curated rails.

**Why it matters:** Discovery should not rely on search alone. Featured and genre sections make new and returning content easier to find.

**What you're checking:** A featured rail appears when comics are marked featured in admin; genre sections show category-driven carousels.

### 3A — Featured rail

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Comics** → open a published comic |
| 2 | Enable **Featured** (or equivalent toggle) → save |
| 3 | Open [site home](https://snacktoons-development.zeekertech.com/) |

**Pass:** Featured comic appears in the featured section on home.

**Fail:** Toggle saves but comic never appears on home.

### 3B — Genre sections

| Step | Action |
|------|--------|
| 1 | Confirm comics exist in at least two categories |
| 2 | Refresh home |

**Pass:** Genre/category sections list comics under their categories.

**Fail:** Home shows only a single generic list with no genre grouping.

---

## SA-004 — Advanced search

**What this is:** Readers can filter comics by text, **paid/free**, **tags**, genre, country, and date range.

**Why it matters:** Power users need to narrow large catalogs without scrolling every title.

**What you're checking:** Filters change results; paid/free and tag filters work together with search text.

### 4A — Open advanced search

| Step | Action |
|------|--------|
| 1 | Open [Advanced search](https://snacktoons-development.zeekertech.com/en/search/advanced) (adjust locale prefix if needed) |
| 2 | Enter a known comic title fragment |
| 3 | Apply **Free only** or **Paid only** filter |

**Pass:** Results respect the access filter.

### 4B — Tag filter

| Step | Action |
|------|--------|
| 1 | Admin → tag a comic with a unique tag in **Content → Comics** |
| 2 | Advanced search → filter by that tag |

**Pass:** Tagged comic appears; untagged comics drop out when tag is required.

---

## SA-005 — Page view and scroll view

**What this is:** Readers toggle **Page view** vs **Scroll view** in the chapter reader. Choice is remembered on the device.

**Why it matters:** Webtoon readers prefer continuous scroll; others prefer panel-by-panel navigation.

**What you're checking:** Both modes render full-width panels; page mode uses bottom-bar **Previous page** / **Next page**; scroll mode shows **Page X of Y** while scrolling.

### 5A — Scroll view

| Step | Action |
|------|--------|
| 1 | Log in → open any multi-panel chapter |
| 2 | Confirm default **Scroll view** (all panels stacked) |
| 3 | Scroll mid-chapter — bottom bar shows **Page X of Y** updating |

**Pass:** Full vertical scroll; page counter updates.

### 5B — Page view

| Step | Action |
|------|--------|
| 1 | Top bar → switch to **Page view** |
| 2 | Confirm one panel at a time, full height (scroll within tall panel) |
| 3 | Use bottom **Previous page** / **Next page** or keyboard arrows |
| 4 | Refresh — mode preference persists |

**Pass:** Panel changes reset scroll to top; mode persists after refresh.

---

## SA-009 — Mid-chapter resume

**What this is:** Reading **progress** and **page index** save while you read; reopening the chapter restores your last panel when possible.

**Why it matters:** Long chapters should not force readers to find their place manually.

**What you're checking:** Leave mid-chapter, return later, and land near the previous panel.

### 9A — Resume after leave

| Step | Action |
|------|--------|
| 1 | Open a multi-panel chapter in **Page view** or **Scroll view** |
| 2 | Advance to panel 3+ (or scroll past first panel) |
| 3 | Navigate away (comic page or home) |
| 4 | Re-open the same chapter |

**Pass:** Reader opens on or near the saved panel (not always panel 1).

**Fail:** Always starts at panel 1 despite prior progress.

---

## S2-004 — Capture deterrence (honest limits)

**What this is:** The reader disables right-click/drag on panels and shows a subtle **account watermark**. This deters casual copying; it is **not** full DRM.

**Why it matters:** Sets expectations for content protection without claiming impossible screenshot blocking.

**What you're checking:** Watermark visible when logged in; context menu blocked on reader area.

### 4A — Watermark and context menu

| Step | Action |
|------|--------|
| 1 | Log in → open a chapter |
| 2 | Look for faint repeated text on panels (email or account id) |
| 3 | Right-click on a panel |

**Pass:** Watermark visible; context menu does not appear on reader content.

**Fail:** No watermark for logged-in users, or panels can be dragged/saved trivially without any deterrence.

---

## S2-008 / SA-008 — Billing, coin history, filters, export

**What this is:** The reader **Billing** page shows **coin wallet activity** (unlocks, top-ups, admin adjustments) and **purchase history** with filters and **CSV export**.

**Why it matters:** Members and support need a clear financial paper trail without admin panel access.

**What you're checking:** Coin ledger rows appear; invoice filters work; export downloads a CSV.

### 8A — Coin history

| Step | Action |
|------|--------|
| 1 | Log in as a reader who unlocked a paid chapter or received an admin coin credit |
| 2 | Open **Billing** from profile menu |
| 3 | Review **coin transaction** / wallet activity section |

**Pass:** Unlock or adjustment appears with amount and description.

### 8B — Purchase filters and export

| Step | Action |
|------|--------|
| 1 | On **Billing**, apply **type** and/or **date** filters on purchase history |
| 2 | Click **Export** (CSV) |

**Pass:** List narrows correctly; CSV downloads with filtered rows.

---

## Gated next chapter — Upgrade redirect

**What this is:** When **Next chapter** is locked, the reader is sent to **sign in**, **auto-unlock with coins** (if balance allows), or the **membership & coins** page — not a dead-end error.

**Why it matters:** Conversion path should be obvious at the end of a free stretch.

### NG-A — Locked next chapter

| Step | Action |
|------|--------|
| 1 | Read through to the last free chapter of a series |
| 2 | Click **Next** for a locked chapter as a logged-in reader **without** enough coins |

**Pass:** Redirect to membership/coins page (or login if guest); optional message explains why.

**Fail:** Toast only — “unlock from series page” with no redirect.

---

## SA-029 — Admin view history

**What this is:** Operators review **all readers' chapter views** in one place with filters and CSV export.

**Why it matters:** Support and analytics need cross-reader activity, not only per-reader tabs.

**What you're checking:** **Analytics → View history** lists reads; date/comic filters work; export succeeds.

### 29A — View history list and export

| Step | Action |
|------|--------|
| 1 | Admin → **Analytics → View history** |
| 2 | Filter by **date range** and/or **comic** |
| 3 | **Export reading history** |

**Pass:** Rows match filters; CSV download completes.

---

## S2-011 / SA-023 — Payout workflow and monthly vs yearly share

**What this is:** Subscription payouts move **Pending → Approved → Paid**; artists **Acknowledge** approved payouts (unclaimed until acknowledged). Global settings support **separate monthly and yearly** artist share percentages.

**Why it matters:** Finance needs a clear approval chain; yearly subscribers can use a different rev-share than monthly.

**What you're checking:** Admin can approve and mark paid; artist can acknowledge; settings show monthly/yearly percentages.

### 11A — Approve and pay

| Step | Action |
|------|--------|
| 1 | Admin → **General Settings → Artist Payout Settings** — note **monthly** and **yearly** subscription % fields |
| 2 | Admin → **Payouts** → find **Pending** artist payout |
| 3 | Row action → **Approve** |
| 4 | Log in to **Artist panel → Payouts** → **Acknowledge payout** on that row |
| 5 | Admin → **Mark paid** |

**Pass:** Status progresses; **Claimed** timestamp set after artist acknowledge; **Paid** after admin marks paid.

### 11B — Force-run (non-production only)

| Step | Action |
|------|--------|
| 1 | On staging, use **Run subscription payout calculation** per [testing subscription payouts](../monetization/testing-subscription-payouts.md) |

**Pass:** New **Pending** rows created with explanation mentioning monthly/yearly pools when mixed plans exist.

---

## Quick URL reference

| Area | URL |
|------|-----|
| Site home | https://snacktoons-development.zeekertech.com/ |
| Advanced search | https://snacktoons-development.zeekertech.com/en/search/advanced |
| Reader billing | https://snacktoons-development.zeekertech.com/en/billing |
| Admin view history | https://snacktoons-development.zeekertech.com/admin/reading-histories |
| Admin payouts | https://snacktoons-development.zeekertech.com/admin/payouts |
| Artist payouts | https://snacktoons-development.zeekertech.com/artist/payouts |

---

## Sign-off checklist

- [ ] **SA-003** — Featured rail and genre sections visible on home
- [ ] **SA-004** — Advanced search paid/free and tag filters work
- [ ] **SA-005** — Page view and scroll view toggle; page counter in scroll mode
- [ ] **SA-009** — Mid-chapter resume restores last panel
- [ ] **S2-004** — Watermark + context-menu deterrence (limits understood)
- [ ] **S2-008** — Coin wallet history visible on Billing
- [ ] **SA-008/030** — Purchase filters and CSV export work
- [ ] **Gated next** — Locked next chapter redirects to upgrade path
- [ ] **SA-029** — View history filters and export work
- [ ] **S2-011** — Payout pending → approved → acknowledged → paid
- [ ] **SA-023** — Monthly vs yearly payout % visible in settings
