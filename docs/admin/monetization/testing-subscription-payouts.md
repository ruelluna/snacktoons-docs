---
title: Testing Subscription Artist Payouts
description: How admins can force-run subscription payout calculation on non-production environments to verify artist earnings from subscriber reads
sidebar_position: 5
---

# Testing Subscription Artist Payouts

This guide is for **admin testers** verifying that artists receive **monthly USD subscription payouts** when subscribed readers open paid chapters.

Subscription reads do **not** add coins to the artist earnings wallet. They are paid through **subscription payout records** after the monthly calculation runs.

## Before you test

1. An **artist** has a published comic with at least one **paid chapter** (not free).
2. A **reader** has an **active subscription**.
3. That reader **opens the paid chapter** on the member site (a read is recorded when the chapter page loads).
4. In the admin panel, confirm the read under **Users → Readers → [reader] → Reading History**.

## Force-run the calculation (non-production only)

On **local**, **staging**, and **development**, admins can trigger subscription payout calculation without waiting for the monthly schedule.

This button **does not appear in production**. Production payouts always follow the configured monthly payout schedule.

### Steps

1. Sign in to the **admin panel**.
2. Go to **Payments → Payouts**.
3. Click **Run subscription payout calculation** (warning-colored button in the page header).
4. Read the modal carefully:
   - Available only on non-production environments
   - Creates **pending USD** subscription payout rows
   - Does **not** change artist coin wallets
   - Running twice for the **same period** creates **duplicate** payout rows
5. Set **Period start** and **Period end** to cover the dates when your test reads occurred (defaults are the previous calendar month).
6. Confirm and run.

### After running

| Where | What to check |
|-------|----------------|
| **Admin → Payments → Payouts** | New rows with type **Subscription** for artists and the platform |
| **Artist panel → Payouts** | Artist sees a **Subscription** payout for the period (USD, pending) |
| **Artist coin earnings** | Unchanged — subscription reads are not coin credits |

## What should and should not happen

**Should**

- Subscribed reader can open paid chapters without spending coins
- Reading history shows the chapter after the reader opens it
- Force-run creates subscription payout records for the selected period

**Should not**

- Artist coin wallet increases from subscription reads alone
- Button appears on production
- Same period run twice without cleanup (duplicates payout rows)

## Payout status values

Artist and platform payout records use this workflow:

| Status | Meaning |
|--------|---------|
| **Pending** | Calculated; awaiting admin review |
| **Approved** | Admin approved; artist may **Acknowledge payout** in the artist panel |
| **Paid** | Admin confirmed funds sent |
| **Failed** | Payment attempt failed or was rejected |

**Unclaimed:** An **Approved** payout with no **Claimed** timestamp — the artist has not acknowledged yet.

On **Admin → Payouts**, use **Approve** then **Mark paid**. Artists acknowledge from **Artist panel → Payouts**.

When marking a payout **Paid**, set the **Payout date** if the form requires it. Legacy **Sent** values are no longer used in the admin panel.

## Monthly vs yearly artist share

In **Settings → General Settings → Edit → Artist Payout Settings**, configure:

- **Subscription payout percentage (default)** — used when monthly/yearly overrides are blank
- **Monthly plans** and **Yearly plans** — separate percentages applied to each subscription revenue pool during calculation

Payout explanation text on new rows references both pools when mixed plan types exist in the period.

## Related revenue stream

**Coin unlocks** are separate: when a reader spends coins to unlock a chapter, the artist receives coins in the earnings wallet immediately. That path is not what this testing button calculates.

For artist-facing payout concepts, see the artist payout guide on the documentation site.
