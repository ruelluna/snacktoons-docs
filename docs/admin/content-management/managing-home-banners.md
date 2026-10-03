---
sidebar_position: 6
title: Managing Home Banners
description: Schedule locale-specific promo banners that appear above the most-read carousel on the public home page
---

# Managing Home Banners

Promo banners are a settings-driven strip on the public home page. They appear **above** the most-read comic carousel. Each banner has a **Style** that controls how the artwork and copy appear. The comic carousels are unchanged.

## Accessing Home Banners

1. Log in to the admin panel
2. Open **Settings → Home Page**
3. Edit the **Home Banners** repeater

## Styles

Pick one **Style** per banner:

- **Full artwork** — The uploaded image is the whole banner. Title is alt text only. Use this when the offer is already designed into the art.
- **Series showcase** — Artwork on one side, title and description on a dark panel (Manga Plus title-card look). Optional **Badge** pill (for example `New Series!`).
- **Marketing promo** — Headline and description beside the art, with the CTA text on a dark footer bar.

Existing banners without a style use **Full artwork**.

## Banner fields

For each banner, set:

- **Style**
- **Badge** (optional; used on Series showcase and Marketing promo)
- **Title** and **Description**
- **Image** (required), plus optional tablet and mobile images
- **Call to Action** link and text
- **Locale**: all locales, or English, Español, 日本語, or 한국어
- **Starts at** and **Ends at** (optional window, shown in the admin timezone)
- **Active**: turn off to hide without deleting

## What readers see

A banner appears on home when all of these are true:

- **Active** is on
- The current site language matches **Locale**, or locale is **All locales**
- The current time is inside the start/end window (empty dates mean no limit)

Inactive, future, expired, or other-locale banners stay hidden. Readers can have more than one matching banner; they rotate in the promo strip.

## Best practices

- Use **Full artwork** when the file already contains the headline and offer
- Use **Series showcase** for a single title launch (cover + name + short line)
- Use **Marketing promo** for platform offers (sale, launch, languages)
- Prefer **All locales** only when the artwork and copy have no language-specific text
- Set an end date so seasonal art does not linger
