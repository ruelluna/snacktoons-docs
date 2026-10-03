---
sidebar_position: 4
title: Managing Coin Vouchers
description: Issue redeemable coin voucher codes with limits, expiry, and a redemption audit trail
---

# Managing Coin Vouchers

Coin vouchers grant coins to a reader’s wallet when they redeem a code on **Billing**. They are not discount coupons.

## Accessing Coin Vouchers

1. Log in to the admin panel
2. Open **Settings → Coin Vouchers**
3. Create, view, or edit a voucher

## Creating a voucher

Set:

- **Code** (stored in uppercase)
- **Coin amount**
- **Max uses** (total redemptions across all readers)
- **Expires at** (optional)
- **Purpose** (why the code exists)
- **Active**

The creating admin is stored as the voucher owner.

## Redemptions

Open a voucher’s **Redemptions** relation to see who redeemed it, how many coins were granted, and when.

A reader can redeem a given code only once. Redemption stops when the code is inactive, expired, already used by that reader, or at the max-use limit.

## What readers do

On **Billing**, members enter the code and choose **Redeem**. Coins appear in the wallet history with a voucher source.
