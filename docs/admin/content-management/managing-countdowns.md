---
sidebar_position: 8
title: Managing Countdowns
description: Run a locale-scoped countdown campaign with a public landing page and site-wide clock
---

# Managing Countdowns

Countdown campaigns show a clock on every public page and a dedicated landing page. After the end time, the clock hides and the call to action stays.

## Accessing Countdowns

1. Log in to the admin panel
2. Open **Content → Countdown Campaigns**
3. Create or edit a campaign

## Fields

- **Title** and optional **Body**
- **Landing page** (optional)
- **Locale**
- **CTA label** and **CTA URL** (required)
- **Ends at** (required)
- **Active**

## Landing page

The site clock bar always uses **Title**, **Ends at**, and the CTA fields. You can also attach a designed landing page:

1. Open **Pages** in the admin sidebar
2. Create a page. Under **Content**, use the visual editor (blocks on the left, canvas in the middle)
3. Turn **Published** on, then save
4. Open **Content → Countdown Campaigns** and choose that page under **Landing page**

When a published page is attached, `/countdown` shows that design plus a slim clock and CTA at the top. Leave **Landing page** empty to keep the simple title, body, and CTA page. **Body** is only used on that simple page, not on the site clock bar.

**Open Pages** next to the field jumps to the page list so you can create or publish a design first.

## What readers see

- A bar near the top of the site while the campaign is **Active** and matches the locale
- A live clock until **Ends at**
- After expiry: title and CTA remain; the clock is gone
- Readers can hide the bar with the **X**. That sets a cookie (`countdown_{id}`) so it stays hidden on later visits
- A public countdown page (for example `/countdown` on English): the attached published design when one is linked, otherwise the same title, body, and CTA

If several campaigns are active, the one with the latest **Ends at** is shown.
