---
title: Milestone 3 Staging UAT
description: Step-by-step staging verification for August 21 scheduling, home promos, countdowns, coin vouchers, artist reads, and authentication-log extras
sidebar_position: 3
---

# Milestone 3 — Staging UAT (August 21)

Use this guide to verify **Milestone 3: Scheduling and contract extras** on staging. Each section explains what was built, why it matters, and the exact clicks to confirm it works. Work through the scenarios in order, or jump to the [sign-off checklist](#sign-off-checklist) when you are ready to confirm completion.

**Staging site:** [https://snacktoons-development.zeekertech.com/](https://snacktoons-development.zeekertech.com/)

Related guides:

- [Managing Chapters](../content-management/managing-chapters.md) — scheduled publish
- [Managing Comics](../content-management/managing-comics.md) — upload cadence
- [Managing Home Banners](../content-management/managing-home-banners.md)
- [Managing Popups](../content-management/managing-popups.md)
- [Managing Countdowns](../content-management/managing-countdowns.md)
- [Managing Coin Vouchers](../monetization/managing-coin-vouchers.md)
- [Authentication Logs](../system/authentication-logs.md)
- [Monetization & purchases (reader)](../../reader/monetization-purchases.md)

---

## S2-006 / SA-035 — Scheduled chapter publish

**What this is:** After review, a chapter can wait for a **Publish at** time. Status becomes **Scheduled** until that moment.

**Why it matters:** Operators can lock a release time without leaving a chapter as a draft. Readers never see it early.

**What you're checking:** Future **Publish at** holds the chapter; when the time passes it goes live; drafts are not auto-published.

### 3A — Hold a published chapter

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Chapters** → edit a reviewed chapter |
| 2 | Set status **Published** and **Publish at** to a time a few minutes in the future → save |

**Pass:** Status becomes **Scheduled**. The chapter is not on the public comic page.

**Fail:** Chapter stays Published and is readable immediately.

### 3B — Automatic go-live

| Step | Action |
|------|--------|
| 1 | Wait until **Publish at** has passed (or use a chapter already due) |
| 2 | Refresh the public comic page |

**Pass:** Status is **Published** and readers can open the chapter.

**Fail:** Chapter remains Scheduled after the time has passed.

---

## S2-003 — Upload cadence / Today’s comics

**What this is:** Each comic can use a **weekday** or **every tenth** upload term. Home **Today’s comics** only lists matching published titles.

**Why it matters:** Daily rails should follow the editorial calendar, not “recently updated.”

**What you're checking:** Scheduled comics appear only on the right day; unscheduled comics stay out of the rail.

### 3C — Weekday match

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Comics** → edit a published comic with a published chapter |
| 2 | Set **Upload schedule** to **Weekday** and check today’s weekday → save |
| 3 | Open [site home](https://snacktoons-development.zeekertech.com/) |

**Pass:** Comic appears in **Today’s comics**.

**Fail:** Comic is missing despite matching today.

### 3D — No schedule

| Step | Action |
|------|--------|
| 1 | Clear the upload schedule on that comic → save |
| 2 | Refresh home |

**Pass:** Comic is gone from **Today’s comics**.

---

## Home promo banners

**What this is:** Settings-driven promo strip **above** the most-read carousel.

**Why it matters:** Marketing can time and localize home creatives without replacing discovery carousels.

### 3E — In-window banner

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → Home Page** → add an active banner for **All locales** with a start time in the past |
| 2 | Open home |

**Pass:** Promo strip shows the banner above most-read comics. **Full artwork** is image-only; **Series showcase** shows title beside art; **Marketing promo** shows a headline and footer bar.

**Fail:** Only the most-read carousel appears.

### 3F — Locale / window

| Step | Action |
|------|--------|
| 1 | Set the banner locale to **Español** only, or move **Starts at** to tomorrow |
| 2 | View English home |

**Pass:** That banner is hidden on English home.

---

## Site popups

**What this is:** One active popup overlay with optional show-once dismiss.

### 3G — Show and dismiss

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Popups** → create an active popup for all locales, in window, **Show once** on |
| 2 | Open any public page → close the popup → refresh |

**Pass:** **Notice** shows title and body. **Image** shows the creative. **Offer** adds a header bar above the image. After dismiss it stays gone.

---

## Countdown campaign

**What this is:** Site-wide clock plus a public countdown page. After expiry the clock hides; the CTA stays.

### 3H — Clock and landing

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Countdown Campaigns** → create an active campaign ending later today |
| 2 | Browse home and open `/countdown` (or the localized countdown URL) |

**Pass:** Clock ticks on the layout. Without a landing page, `/countdown` shows title, body, and CTA. With a published **Pages** design attached, `/countdown` shows that builder content plus a slim clock and CTA.

### 3I — After expiry

| Step | Action |
|------|--------|
| 1 | Use a campaign whose **Ends at** is in the past and still **Active** |
| 2 | Refresh any public page |

**Pass:** Clock is gone; CTA remains. Readers can hide the bar with **X**; it stays gone after refresh.

---

## Coin vouchers

**What this is:** Admin-issued codes that add coins on the reader **Billing** page.

### 3J — Redeem

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → Coin Vouchers** → create an active code with a coin amount |
| 2 | Sign in as a reader → **Billing** → enter the code → **Redeem** |

**Pass:** Balance increases; voucher **Redemptions** lists the reader. A second redeem by the same reader fails.

---

## Artist reads and payout detail

**What this is:** Artist dashboard bar chart of reads over time, plus payout explanation and timestamps.

### 3K — Artist dashboard

| Step | Action |
|------|--------|
| 1 | Sign in to the artist panel |
| 2 | Open the dashboard |

**Pass:** **Reads Over Time** chart is visible and scoped to that artist’s comics.

### 3L — Payout view

| Step | Action |
|------|--------|
| 1 | Artist → **Payouts** → view a payout that has an explanation |
| 2 | Confirm **Payout Explanation**, **Approved At**, and **Claimed At** |

**Pass:** Those fields appear (placeholders if empty).

---

## Authentication logs (city and device)

**What this is:** Login history with city (when available) and device type, plus filters.

### 3M — Review a login

| Step | Action |
|------|--------|
| 1 | Sign in to the admin panel (or any role) once |
| 2 | Admin → **Logs → Authentication Logs** |
| 3 | Filter by **Device** or **City** if values exist |

**Pass:** A new row shows device (desktop/mobile/tablet). City may be blank when no geo lookup is configured.

---

## Sign-off checklist

- [ ] Scheduled chapter holds until **Publish at**, then goes live
- [ ] Today’s comics follows weekday / every-tenth; unscheduled titles are excluded
- [ ] Home promo strip appears above most-read and respects locale/window
- [ ] Popup shows once when configured
- [ ] Countdown clock + landing page; CTA remains after expiry
- [ ] Reader redeems a coin voucher on Billing
- [ ] Artist sees reads chart and payout explanation / dates
- [ ] Authentication logs show device (and city when available)
