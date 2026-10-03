---
sidebar_position: 10
title: Managing Rankings
description: Add extra homepage comic rails using featured, most-read, newest, editor pick, or today’s algorithms
---

# Managing Rankings

Ranking lists add extra comic rails on the public home page. They appear **after** the promo banner and most-read carousel, in the order you set. The existing featured, popular, today’s, genre, and other home sections stay in place.

## Accessing Rankings

1. Log in to the admin panel
2. Open **Content → Ranking Lists**
3. Create or edit a list

## Fields

- **Title**: Shown as the rail heading. The slug updates from this as you type
- **Slug**: Unique key for the list (for example `uat-ranking`). Filled from the title; you can still edit it
- **Algorithm**: Featured, Most read, Newest, Editor's pick, or Today's comics
- **Locale**: All locales, or one language
- **Limit**: How many comics to load (1–40)
- **Sort order**: Lower numbers appear first
- **Active**: Turn off to hide the rail

## What readers see

Each active list for their language (or **All locales**) becomes a home section after the promo/banner block. The rail **title always shows**. If that algorithm has no published comics (for example Featured when nothing is marked featured), the heading still appears with a short empty note. If a list uses the same algorithm as a built-in section, both can appear. Turn **Active** off when you do not want a duplicate.
