---
title: Milestone 1 Staging UAT
description: Step-by-step staging verification for August 11 security and account controls on snacktoons-development.zeekertech.com
sidebar_position: 1
---

# Milestone 1 — Staging UAT (August 11)

Use this guide to verify **Milestone 1: Stabilization and security** on staging. Each section explains what was built, why it matters, and the exact clicks to confirm it works. Work through the scenarios in order, or jump to the [sign-off checklist](#sign-off-checklist) when you are ready to confirm completion.

**Staging site:** [https://snacktoons-development.zeekertech.com/](https://snacktoons-development.zeekertech.com/)

Related operator guides:

- [Authorization](../authorization.md) — admin 2FA
- [Managing Readers](../user-management/managing-readers.md) — account status and coin adjustments

---

## SA-002 — Reader profile updates

**What this is:** Readers manage their own identity on the site — display name, login email, and profile picture.

**Why it matters:** Profile edits should save reliably without support intervention. If this breaks, members cannot keep their account details up to date.

**What you're checking:** A reader can change their name and email, upload a photo that appears in the header, and optionally remove the photo again.

### 1A — Update name and email

| Step | Action |
|------|--------|
| 1 | Open [Reader login](https://snacktoons-development.zeekertech.com/login) |
| 2 | Log in as **Reader A** |
| 3 | Open **Profile** from the top-right user menu, or [Profile page](https://snacktoons-development.zeekertech.com/user/profile) (use the locale path in your browser if redirected, e.g. `/en/user/profile`) |
| 4 | Under **Profile Information**, change **Name** (e.g. `UAT Reader Aug11`) |
| 5 | Optionally change **Email** to a test address you control |
| 6 | Click **Save** |
| 7 | Hard-refresh the page (Ctrl+F5) |

**Pass:** Success message; name (and email if changed) persist after refresh; header shows updated name.

**Fail:** Save fails, errors remain, or values revert after refresh.

### 1B — Upload profile photo

| Step | Action |
|------|--------|
| 1 | On **Profile** as **Reader A**, confirm the **Photo** section is visible |
| 2 | Click **Select A New Photo** |
| 3 | Choose a JPG or PNG (max 1 MB) |
| 4 | Confirm preview appears |
| 5 | Click **Save** |
| 6 | Refresh the page |

**Pass:** Photo displays in the form and in the site header.

**Fail:** No photo section, upload error, or initials-only avatar after save.

### 1C — Remove photo (optional)

| Step | Action |
|------|--------|
| 1 | Click **Remove Photo** → refresh |

**Pass:** Photo removed; initials/default avatar returns.

---

## S2-005 — Admin two-factor authentication

**What this is:** An extra security step for anyone using the admin panel — after password, they enter a code from an authenticator app on their phone.

**Why it matters:** Admin accounts control payouts, user access, and platform settings. Requiring 2FA reduces the risk of unauthorized admin access.

**What you're checking:** A new admin must set up 2FA before using the panel; returning admins must enter a valid code each time they sign in.

### 2A — First-time MFA enrollment

| Step | Action |
|------|--------|
| 1 | Open a **private/incognito** window |
| 2 | Go to [Admin login](https://snacktoons-development.zeekertech.com/admin/login) |
| 3 | Log in as **Admin** |
| 4 | If redirected to set up two-factor authentication, follow the wizard. Otherwise: account menu (top-right) → **Profile** → **Two-factor authentication** / **App authentication** |
| 5 | Click **Set up** |
| 6 | Scan the **QR code** with Google Authenticator, Authy, or similar |
| 7 | Enter the **6-digit code** |
| 8 | Save **recovery codes** securely |
| 9 | Confirm you can reach the admin dashboard |

**Pass:** Full admin access only after MFA enrollment; sidebar shows **Readers**, **Payouts**, etc.

**Fail:** Full panel access without MFA setup, or enrollment fails with no recovery path.

### 2B — Login with MFA on return visit

| Step | Action |
|------|--------|
| 1 | Sign out of admin |
| 2 | [Admin login](https://snacktoons-development.zeekertech.com/admin/login) |
| 3 | Email + password → **Sign in** |
| 4 | Enter current **6-digit TOTP** when prompted |

**Pass:** Dashboard loads after valid code.

**Fail:** Password-only login succeeds, or valid codes always rejected.

### 2C — Recovery code (optional)

| Step | Action |
|------|--------|
| 1 | At MFA step, use **recovery code** if offered |
| 2 | Enter one saved code |

**Pass:** Login succeeds once (code may be consumed).

---

## S2-007 — Account status controls

**What this is:** Tools for staff to temporarily or permanently restrict a reader account — **Pause**, **Suspend**, or **Ban** — with a written reason, and **Reinstate** when access should return.

**Why it matters:** When policy or abuse issues come up, you need a clear way to stop someone from logging in while keeping a record of who changed what and why.

**What you're checking:** Status changes stick in the admin panel, blocked readers cannot sign in, reinstated readers can sign in again, and changes appear in the audit log.

Use **Reader B** for status tests so **Reader A** stays available for profile and coin checks.

### 3A — Suspend and block login

| Step | Action |
|------|--------|
| 1 | Admin → [Readers](https://snacktoons-development.zeekertech.com/admin/readers) |
| 2 | Find **Reader B**; confirm **Account status** is **Active** |
| 3 | Row action → **Suspend** |
| 4 | Reason: `UAT suspend test Aug 11` → confirm |
| 5 | Confirm status badge shows **Suspended** |
| 6 | New incognito window → [Reader login](https://snacktoons-development.zeekertech.com/login) |
| 7 | Log in as **Reader B** |

**Pass:** Login fails (error / not redirected to dashboard).

**Fail:** Suspended reader reaches dashboard or can browse.

### 3B — Reinstate

| Step | Action |
|------|--------|
| 1 | Admin → **Readers** → **Reinstate** on **Reader B** |
| 2 | Reason: `UAT reinstate after suspend` → confirm |
| 3 | Status **Active** |
| 4 | Incognito → log in as **Reader B** |

**Pass:** Login succeeds.

### 3C — Pause and Ban (spot-check)

Repeat 3A/3B with **Pause** and **Ban** instead of Suspend.

**Pass:** Same block and reinstate behavior.

### 3D — Audit trail

| Step | Action |
|------|--------|
| 1 | **Readers** → **View** (eye) on **Reader B** |
| 2 | Header → **Audit log** |

**Pass:** Status change entries with timestamps.

---

## SA-021 — Payout status alignment

**What this is:** A consistent way to track artist and platform payouts — each record is **Pending**, **Paid**, or **Failed**.

**Why it matters:** Finance and ops need one clear status language. Older **Sent** labels are gone so reports and the admin screen match what actually happened.

**What you're checking:** You can mark a pending payout as paid (or failed on a test record), the status saves correctly, and the list never shows outdated **Sent** values.

### 4A — Mark payout Paid

| Step | Action |
|------|--------|
| 1 | Admin → [Payouts](https://snacktoons-development.zeekertech.com/admin/payouts) |
| 2 | Find a **Pending** payout |
| 3 | **View** or **Edit** |
| 4 | Set **Payout status** to **Paid** |
| 5 | Set **Payout date** if required → **Save** |
| 6 | Refresh list |

**Pass:** Status **Paid** (green); no error; persists on refresh.

**Fail:** Save error, status reverts, or invalid status shown.

### 4B — Failed status (optional)

Edit a test **Pending** payout → set **Failed** → save.

**Pass:** **Failed** badge persists.

### 4C — No legacy Sent status

**Pass:** List shows only **Pending**, **Paid**, and **Failed** — never **Sent**.

---

## S2-009 — Manual coin adjustments

**What this is:** A way for admins to add or remove coins from a reader's wallet — for goodwill credits, corrections, or support resolutions — always with a required reason.

**Why it matters:** Coin balance affects what readers can unlock. Manual changes must update the balance correctly, leave an audit trail, and never allow removing more coins than the reader has.

**What you're checking:** Credit increases balance, debit decreases it, over-debit is rejected, and each action is logged.

### 5A — Credit coins

| Step | Action |
|------|--------|
| 1 | Admin → **Readers** → **Reader A** |
| 2 | Note coin balance (log in as Reader A → **Billing**, or note the success notification) |
| 3 | **Adjust coins** → **Credit** → amount **25** → reason `UAT credit test Aug 11` → confirm |
| 4 | As **Reader A** → **Billing** |

**Pass:** Balance increased by 25.

### 5B — Debit coins

| Step | Action |
|------|--------|
| 1 | **Adjust coins** → **Debit** → **10** → reason `UAT debit test Aug 11` → confirm |
| 2 | Check **Reader A** balance |

**Pass:** Balance decreased by 10.

### 5C — Over-debit rejected

| Step | Action |
|------|--------|
| 1 | **Debit** amount **99999** → reason `UAT insufficient balance test` → confirm |

**Pass:** Error notification; balance unchanged.

**Fail:** Negative balance or debit succeeds without funds.

### 5D — Audit log

| Step | Action |
|------|--------|
| 1 | **Readers** → **View** **Reader A** → **Audit log** |

**Pass:** Coin adjustment entries with amount, direction, reason.

---

## Quick URL reference

| Area | URL |
|------|-----|
| Site home | https://snacktoons-development.zeekertech.com/ |
| Reader login | https://snacktoons-development.zeekertech.com/login |
| Reader profile | https://snacktoons-development.zeekertech.com/user/profile |
| Admin login | https://snacktoons-development.zeekertech.com/admin/login |
| Admin Readers | https://snacktoons-development.zeekertech.com/admin/readers |
| Admin Payouts | https://snacktoons-development.zeekertech.com/admin/payouts |

---

## Sign-off checklist

- [ ] **SA-002** — Reader can save name and email; changes still there after refresh
- [ ] **SA-002** — Reader can upload a profile photo; it shows in the header
- [ ] **S2-005** — Admin completed authenticator app setup
- [ ] **S2-005** — Admin login asks for a 6-digit code after password
- [ ] **S2-007** — Suspended reader cannot log in
- [ ] **S2-007** — Reinstated reader can log in again
- [ ] **S2-007** — Audit log shows who changed account status and when
- [ ] **SA-021** — Pending payout can be marked **Paid** and stays saved
- [ ] **S2-009** — Admin credit adds coins to reader balance
- [ ] **S2-009** — Admin debit removes coins correctly
- [ ] **S2-009** — Debit above balance is blocked with an error
