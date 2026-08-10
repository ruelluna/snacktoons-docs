---
sidebar_position: 1
title: Authorization
description: Understanding the authorization system for administrators
---

# Administrator Authorization

This document explains how the authorization system works for administrators in the Snacktoons platform.

## Overview

The Snacktoons admin panel uses a secure authorization system that requires explicit user creation by existing administrators. This approach ensures that only authorized personnel can access administrative functions.

## Key Authorization Points

- **No Self-Registration**: Administrators cannot register themselves through a public registration form
- **System User Creation**: New administrators must be added as system users by existing administrators
- **Role-Based Access**: All admin users are assigned the 'admin' role automatically
- **Secure Authentication**: Email and password login, then **required authenticator-app two-factor authentication**

## How to Gain Admin Access

To gain administrative access to the Snacktoons platform:

1. An existing administrator must create a system user account for you
2. You will receive login credentials or a password reset link via email
3. Use these credentials to log in at the admin login page

For detailed instructions on creating system users, please refer to the [Managing System Users](./managing-system-users.md) documentation.

## Login Process

1. Navigate to the admin login page at [https://snacktoons.com/admin/login](https://snacktoons.com/admin/login)
2. Enter your email address and password
3. Click **Login**
4. Enter the six-digit code from your authenticator app when prompted (after first-time enrollment)

If this is your first login since two-factor authentication was enabled, complete **Profile → Two-factor authentication** setup before using the panel.

If you've forgotten your password, use the "Forgot Password" link on the login page to request a password reset.

## Two-factor authentication (admin)

Every administrator must enroll in **authenticator app two-factor authentication** before using the admin panel after sign-in.

1. Log in at the admin login page with email and password
2. When prompted, open **Profile** (account menu) and complete **Two-factor authentication** setup
3. Scan the QR code with an authenticator app (Google Authenticator, Authy, or similar)
4. Save the **recovery codes** in a secure location
5. On future logins, enter the six-digit code from your app after your password

If you lose your device, use a recovery code once, then set up 2FA again from your profile. Contact another system administrator if you cannot sign in.

For a full staging walkthrough, see [Milestone 1 Staging UAT](./delivery/milestone-1-staging-uat.md).

## Security Best Practices

- Use a strong, unique password for your admin account
- Do not share your login credentials with others
- Log out when you're finished using the admin panel
- Request your own account rather than using someone else's credentials
- Report any suspicious activity to the system administrator
