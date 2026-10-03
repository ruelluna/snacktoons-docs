---
title: Milestone 4 Staging UAT
description: Step-by-step staging verification for SEO, GTM, Meta CAPI, site menus, ranking rails, and coin currency rates
sidebar_position: 4
---

# Milestone 4 — Staging UAT (August 26)

Use this guide to verify **Milestone 4: Integrations and SEO** on staging. Each section explains what was built, why it matters, and the clicks to confirm it works. Work through the scenarios in order, or jump to the [sign-off checklist](#sign-off-checklist).

**Staging site:** [https://snacktoons-development.zeekertech.com/](https://snacktoons-development.zeekertech.com/)

Related guides:

- [Analytics and Tracking](../analytics-tracking.md) — SEO tab, GTM, Meta CAPI
- [Managing Menus](../content-management/managing-menus.md)
- [Managing Rankings](../content-management/managing-rankings.md)
- [Managing Coin Packages](../monetization/managing-coin-packages.md)
- [Comic discovery (reader)](../../reader/comic-discovery.md)

**Not in this milestone:** Braze (no account yet), Duo (admin already uses authenticator-app codes), and automatic artist bank payouts (operators still mark payouts paid).

---

## SA-015 — SEO tab

**What this is:** **Settings → General Settings** opens a read-only view. Click **Edit**, then use the **SEO** tab for the default title, keywords, and extra metadata. Saving SEO does not require filling payout or other tabs.

**Why it matters:** Search results and social previews can be set from the admin panel on this single domain.

**What you're checking:** Saved SEO values appear in the public page source.

### 4A — Default title and description

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → General Settings** (read-only view) → **Edit** → **SEO** |
| 2 | Set **SEO Title** and **SEO Keywords** → save |
| 3 | Open the public home page and view page source |

**Pass:** The browser tab / `<title>` on the public home page matches the SEO Title you saved (not “Welcome - Snacktoons”). Keywords (and other metadata) match as well.

**Fail:** The title stays **Welcome - Snacktoons** after a refresh, or keywords do not update.

---

## SA-028 — Google Tag Manager

**What this is:** A GTM container ID field on **General Settings → Analytics**. When set, the official GTM snippet loads in the head.

**Why it matters:** Marketing can add tags in GTM without a code deploy. GA4 Measurement ID still works if you keep it filled.

### 4B — Container present

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → General Settings → Edit → Analytics** → enter a **GTM-** container ID → save |
| 2 | Open public home and view page source |

**Pass:** You see the GTM script and the noscript iframe with that container ID. The dataLayer array is present.

**Fail:** No GTM snippet appears.

### 4C — Container empty

| Step | Action |
|------|--------|
| 1 | Clear the GTM field → save |
| 2 | Refresh public home |

**Pass:** GTM snippet is gone. Existing GA4 / Meta Pixel snippets still load if those IDs are set.

---

## SA-027 — Meta Conversions API

**What this is:** Server-side Purchase and CompleteRegistration events, using the Pixel ID plus an access token. Browser Pixel and GTM `event_id` values can match for dedupe.

**Why it matters:** Purchases still count when the browser blocks the Pixel.

### 4D — Token saved

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → General Settings → Edit → Analytics** → paste the CAPI access token (and optional test event code) → save |
| 2 | Register a new reader or complete a coin purchase on staging |

**Pass:** Meta Test Events (or Events Manager) shows CompleteRegistration or Purchase. The token is not visible on the public site.

**Fail:** No server event arrives after a successful register or purchase when token and Pixel are both set.

---

## Site menus

**What this is:** Extra header and footer links managed under **Content → Site Menus**.

**Why it matters:** Operators can add campaign or category links without replacing subscribe, search, or account navigation.

### 4E — Header extras

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Site Menus** → create an **Active** header menu for **All locales** with a Home or Categories item |
| 2 | Open public home on desktop and mobile |

**Pass:** The extra label appears beside subscribe/coins (desktop) and in the mobile menu. Logo, subscribe, categories, search, and the user menu remain.

**Fail:** Built-in links disappear, or the extra link never shows.

### 4F — Empty menus

| Step | Action |
|------|--------|
| 1 | Turn the menu **Active** off, or delete it |
| 2 | Refresh home |

**Pass:** Extra links are gone. Terms, Privacy, and Artist login in the footer stay.

---

## Ranking lists

**What this is:** Extra home rails from **Content → Ranking Lists**.

**Why it matters:** Editorial can add a titled carousel without removing featured / today’s / genre sections.

### 4G — Extra rail

| Step | Action |
|------|--------|
| 1 | Admin → **Content → Ranking Lists** → create an active list (Featured or **Newest**, limit 8) |
| 2 | Open home and look **under the Top Comics banner** for that rail title |

**Pass:** A rail with that title appears after the promo/banner block. If Featured has no comics, you still see the heading (and “No comics match this list yet.”). Switch the list to **Newest** or **Most read** to see covers. Existing home sections stay.

**Fail:** Home is blank except for the new rail, or the new title never appears under the banner.

---

## Currency → coins

**What this is:** **Settings → Coin Currency Rates** sets coins per 1.00 of a currency. Package save and checkout use that rate.

**Why it matters:** USD and EUR packages stay consistent with Stripe amounts. Artist cash-out rate is unchanged.

### 4H — Rate and storefront

| Step | Action |
|------|--------|
| 1 | Admin → **Settings → Coin Currency Rates** → confirm **usd** is active (for example 30 coins per 1.00) |
| 2 | Admin → **Settings → Coin Packages** → edit a USD package and note the computed cents helper |
| 3 | Open the public plans page as a reader |

**Pass:** Only **Active** packages show. Checkout charges the computed amount for that currency.

**Fail:** Inactive packages still list, or Stripe charges the old stored price when a rate exists.

---

## Review results (2 September 2026)

Local walkthrough on the development site. Staging can use the same steps to confirm.

| ID | Item | Result |
|----|------|--------|
| 4A | SEO title, keywords, and extra metadata on public home | Pass |
| 4B | GTM snippet present when a container ID is saved | Pass |
| 4C | GTM snippet gone when the container ID is cleared | Pass |
| 4D | CAPI token saves and is not shown on the public site | Pass |
| 4E | Header extra links appear without replacing built-in nav | Pass |
| 4F | Extra links gone when the menu is inactive | Pass |
| 4G | Extra ranking rail title on home; built-in sections remain | Pass |
| 4H | Coin currency rate; only active packages on the plans page | Pass |

Braze, Duo, and automatic artist bank payouts stay out of scope.

## Sign-off checklist

- [x] SEO title and description appear in public page source
- [x] GTM snippet loads only when a container ID is saved
- [x] CAPI token can be saved (Events Manager on staging when Pixel + token are set)
- [x] Header/footer extras appear without replacing built-in nav
- [x] Extra ranking rail appears; built-in home sections remain
- [x] Coin currency rate drives package cents and checkout currency
- [x] Braze, Duo, and auto bank payouts are out of scope
