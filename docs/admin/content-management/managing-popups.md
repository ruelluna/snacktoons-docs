---
sidebar_position: 7
title: Managing Popups
description: Create scheduled site popups as an image, an image with a header bar, or a text notice
---

# Managing Popups

Popups appear over the public site for readers on matching locales and date windows. Use them for announcements, launches, or limited offers. Most campaigns should use an image.

## Accessing Popups

1. Log in to the admin panel
2. Open **Content → Popups**
3. Create, view, or edit a popup

## Styles

Pick one **Style** per popup:

- **Image** — Campaign art only. Title is alt text.
- **Offer** — Campaign art plus a header bar (for example `LIMITED TIME OFFER`). Fill **Header**.
- **Notice** — Title, body, Close, and optional CTA button. No image.

If Image or Offer has no file, readers see Notice instead.

## Fields

- **Style**
- **Header** (required for Offer)
- **Title** (always required — admin list and image alt text)
- **Image** (required for Image and Offer)
- **Body** (required for Notice)
- **Locale**: all locales, or a single language
- **CTA label** (Notice) and **CTA URL** (optional)
- **Starts at** / **Ends at**
- **Active**
- **Show once**: if on, dismissing the popup sets a cookie so that reader does not see the same popup again

## What readers see

The newest matching **active** popup is shown. It must be in window and match the current locale (or **All locales**).

If a **CTA URL** is set on Image or Offer, the image is the link.

**Close**, the **X** on an image popup, or a click outside the modal dismisses it. If **Show once** is on, the cookie `popup_{id}` keeps it hidden on later visits.

Only one popup is shown at a time.
