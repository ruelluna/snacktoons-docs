---
sidebar_position: 9
title: Managing Menus
description: Add extra header and footer links without replacing account, search, or legal navigation
---

# Managing Menus

Site menus add extra links to the public header and footer. They sit **next to** the existing logo, subscribe/coins, category browse, search, account menu, and legal/language links. They do not replace those built-in items.

## Accessing Menus

1. Log in to the admin panel
2. Open **Content → Site Menus**
3. Create or edit a header or footer menu

## Fields

- **Slug**: Header or Footer
- **Locale**: All locales, or one language. A language-specific menu wins over the all-locales menu
- **Active**: Turn off to hide the extra links and keep the built-in navigation only
- **Items** (repeater, drag to reorder):
  - **Label**
  - **Link type**: Route, Category, or External URL
  - **Route**: Home, Advanced search, Plans and coins, Categories, or Library
  - **Category**: A site category page
  - **URL**: Full `https://` address
  - **Open in new tab**
  - **Active**

Only one active menu is used per location. Prefer a locale match; otherwise the **All locales** menu is used.

## What readers see

- Header extras appear beside subscribe/coins on desktop and in the mobile menu
- Footer extras appear next to Terms, Privacy, and Artist login
- If no active menu exists, the current hardcoded links stay as they are
