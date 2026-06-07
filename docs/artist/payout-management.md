---
sidebar_position: 7
---

# Payout Management

## Overview

Payout management is essential for monetizing your comic content effectively. This guide covers setting up your payment information, understanding revenue streams, tracking earnings, and receiving payments.

## How Earnings and Payouts Work

Snacktoons uses **two separate surfaces** for monetization. Understanding the difference prevents confusion when testing or reviewing your dashboard.

| Surface | Location | What it shows | When it updates |
|-------|----------|---------------|-----------------|
| **Coins Earned** | Artist Dashboard | Total **coins** spent on unlocks of your paid chapters | Immediately after a reader unlocks with coins |
| **Payouts** | Artist panel → Payouts | **USD** payout records for a billing period | After the monthly payout batch runs |

**Coins Earned is not the same as money in your bank account.** Coins are converted to USD using the platform coin value and your payout percentage when monthly payouts are calculated.

### Coin unlock flow (paid chapters)

Coins are charged only when a reader explicitly unlocks a chapter:

1. Reader visits your comic page on the public site
2. Reader clicks **Purchase with Coins** on a paid chapter
3. Coins are deducted from the reader's wallet
4. A chapter unlock record is created
5. Your dashboard **Coins Earned** increases by that chapter's coin price

**Opening or reading a chapter does not charge coins.** If the reader never clicks **Purchase with Coins**, no coin revenue is recorded for that chapter.

### Subscriber reads (separate from coin unlocks)

Readers with an **active subscription** can access paid chapters without spending coins. For those reads:

- **No** coin unlock is created
- **Coins Earned does not increase**
- The read is tracked for **subscription revenue** sharing, which is calculated during the monthly payout batch

If you test payouts with a subscribed account, you will not see coin earnings on your dashboard. That is expected behavior.

## Understanding Revenue Streams

### Types of Revenue

#### Coin Purchases
- **Source**: Readers spending coins to unlock paid chapters (via **Purchase with Coins**)
- **Calculation**: Coins spent × coin value × your coin payout percentage
- **Dashboard tracking**: **Coins Earned** updates immediately (raw coin total)
- **USD payout**: Calculated monthly from unlocks in the payout period
- **Example**: 100 coins spent × $0.01 per coin × 5% platform rate = $0.05 USD (if your rate is 5%)

#### Subscription Revenue
- **Source**: Platform subscription fees shared with artists
- **Calculation**: Your share of paid subscriber reads relative to all paid subscriber reads on the platform, applied to active subscription revenue in the period
- **Dashboard tracking**: Not shown as coins on the dashboard
- **USD payout**: Calculated and recorded monthly in the Payouts section
- **Basis**: Paid chapter reads by subscribers (reads that did not use a coin unlock)

### Revenue Calculation

#### Coin Revenue Formula
```
Your Earnings = (Coins Spent on Your Chapters × Coin Value) × Your Payout Percentage
```

#### Subscription Revenue Formula
```
Your Earnings = (Total Subscription Revenue × Platform Share) × Your Readership Percentage
```

#### Example Calculation

Using platform defaults (coin and subscription payout percentages are configured by administrators; commonly **5%** unless your account has custom rates):

- **Coin USD payout**: 1,000 coins × $0.01 × 5% = **$0.50**
- **Subscription share**: Depends on your proportion of subscriber paid reads in the period × active subscription revenue × your subscription payout percentage

Your **Coins Earned** dashboard stat would show **1,000** (coins), while the **Payouts** page shows the USD amount after the monthly batch runs.

## Setting Up Payout Information

### Accessing Payout Settings

1. **Navigate to Payouts**: Go to Payouts section in main menu
2. **Settings Tab**: Click on "Payout Settings"
3. **Complete Information**: Fill out all required payment details

### Required Information

#### Personal Information
- **Legal Name**: Must match government-issued ID
- **Tax ID/SSN**: Required for tax reporting
- **Address**: Current mailing address for tax purposes

#### Payment Methods

##### Bank Transfer
- **Bank Name**: Your bank's full name
- **Account Name**: Name on the bank account
- **Account Number**: Your account number
- **Routing Number**: Bank routing number (US)
- **SWIFT Code**: International bank code (if applicable)

##### PayPal
- **PayPal Email**: Email associated with your PayPal account
- **Account Verification**: Ensure account is verified and active
- **Currency**: Confirm preferred currency

### Payout Percentages

#### Understanding Percentages
- **Coin Payout Percentage**: Your share of coin revenue after coin value conversion
- **Subscription Payout Percentage**: Your share of subscription revenue allocated to artists
- **Platform defaults**: Set by administrators in global settings (not 80% by default)
- **Per-artist overrides**: Administrators can set custom percentages on your artist account
- **Artist Payout Settings**: When you first open Payout Settings, defaults are taken from the platform configuration

#### Setting Your Percentages
1. **Review your rates**: Check Payout Settings and confirm with support if unsure
2. **Do not assume 80%**: Published examples may use illustrative rates; your live percentages are what matter
3. **Negotiate if needed**: Contact support for rate discussions
4. **Monitor changes**: Track how percentage changes affect monthly payout amounts

## Tracking Your Earnings

### Dashboard Overview

#### Key Metrics
- **Coins Earned** (dashboard): All-time total **coins** from paid chapter unlocks on your comics
- **Payouts** (Payouts menu): USD records per period with status (`pending`, `paid`, etc.)
- **Pending payouts**: USD amounts created by the monthly batch, awaiting admin payment
- **Payment history**: Past payout records in the Payouts section

#### What Updates in Real Time
- **Coins Earned** on the dashboard after a reader uses **Purchase with Coins**
- **Reads and unique readers** as readers consume your content

#### What Updates Monthly
- **USD payout rows** in the Payouts section (coin and subscription types)
- Subscription revenue attribution for subscriber reads (not shown as coins on the dashboard)

### Detailed Analytics

#### Revenue Breakdown
- **By Comic**: Earnings per comic series
- **By Chapter**: Individual chapter performance
- **By Time Period**: Daily, weekly, monthly trends
- **By Reader Type**: New vs. returning reader revenue

#### Performance Insights
- **Conversion Rates**: Free to paid reader ratios
- **Reader Lifetime Value**: Average revenue per reader
- **Peak Earning Times**: When readers spend most
- **Content Optimization**: Which content types earn best

## Payout Schedule and Process

### Monthly Payout Cycle

#### Cut-off Date
- **End of Month**: All earnings through month-end included
- **Processing Time**: 3-5 business days after cut-off
- **Payment Date**: Usually 5th of following month
- **Minimum Threshold**: $10 minimum for payout

#### Payout Timeline
1. **Throughout the month**: Readers unlock chapters (coins) or read as subscribers
2. **Cut-off date**: Earnings through the configured period end are included (see admin General Settings)
3. **Payout day**: The platform runs the monthly payout batch (`artist:payouts`) when payouts are active
4. **Pending records**: USD payout rows appear in your Payouts section
5. **Admin payment**: Administrators review and mark payouts as paid
6. **Confirmation**: You receive notification when a payout is marked paid

### Payment Methods

#### Bank Transfer
- **Processing Time**: 3-5 business days
- **Fees**: Usually free for domestic transfers
- **International**: May incur additional fees
- **Requirements**: Valid bank account information

#### PayPal
- **Processing Time**: 1-2 business days
- **Fees**: PayPal's standard transaction fees
- **Currency**: Automatic conversion if needed
- **Requirements**: Verified PayPal account

### Payout Status Tracking

#### Status Types
- **Pending**: Earnings accumulating for next payout
- **Processing**: Payment being prepared and sent
- **Paid**: Payment successfully completed
- **Failed**: Payment failed (requires attention)

#### Troubleshooting Failed Payouts
1. **Check Information**: Verify payment details are correct
2. **Account Status**: Ensure account is active and verified
3. **Contact Support**: Reach out for assistance
4. **Update Details**: Correct any invalid information

## Tax and Legal Considerations

### Tax Reporting

#### 1099 Forms
- **Annual Reporting**: Platform provides 1099-K forms
- **Threshold**: $600+ in earnings triggers reporting
- **Deadline**: Forms sent by January 31st
- **Requirements**: Keep accurate records of all earnings

#### Self-Employment Taxes
- **Responsibility**: Artists are responsible for their own taxes
- **Quarterly Payments**: May need to pay estimated taxes
- **Deductions**: Track business expenses for deductions
- **Professional Advice**: Consult tax professional for guidance

### Legal Compliance

#### Content Rights
- **Ownership**: Ensure you own or have rights to all content
- **Licensing**: Properly license any third-party content
- **Model Releases**: Get releases for any recognizable people
- **Copyright**: Protect your own intellectual property

#### Platform Policies
- **Terms of Service**: Comply with platform terms
- **Content Guidelines**: Follow content policies
- **Payment Policies**: Understand payment terms
- **Dispute Resolution**: Know how to handle conflicts

## Optimizing Your Earnings

### Content Strategy

#### High-Earning Content Types
- **Popular Genres**: Focus on trending categories
- **Engaging Stories**: Create compelling narratives
- **Quality Art**: Invest in professional artwork
- **Regular Updates**: Maintain consistent publishing schedule

#### Pricing Optimization
- **Market Research**: Study competitor pricing
- **A/B Testing**: Test different price points
- **Reader Feedback**: Consider reader input on pricing
- **Value Perception**: Ensure content justifies price

### Marketing and Promotion

#### Reader Acquisition
- **Social Media**: Promote on relevant platforms
- **Cross-Promotion**: Partner with other artists
- **Community Engagement**: Build relationships with readers
- **SEO Optimization**: Improve discoverability

#### Retention Strategies
- **Quality Content**: Maintain high standards
- **Regular Updates**: Keep readers engaged
- **Reader Interaction**: Respond to comments and feedback
- **Exclusive Content**: Offer special content for loyal readers

## Advanced Features

### Analytics and Reporting

#### Custom Reports
- **Date Ranges**: Analyze specific time periods
- **Content Filtering**: Focus on specific comics or chapters
- **Export Options**: Download data for external analysis
- **Trend Analysis**: Track performance over time

#### Performance Insights
- **Reader Behavior**: Understand how readers interact with content
- **Revenue Patterns**: Identify peak earning periods
- **Content Optimization**: Use data to improve content
- **Market Trends**: Stay informed about industry changes

### Financial Planning

#### Budgeting
- **Income Projections**: Estimate future earnings
- **Expense Tracking**: Monitor business costs
- **Investment Planning**: Plan for equipment and software
- **Emergency Fund**: Maintain financial reserves

#### Growth Strategies
- **Portfolio Expansion**: Create additional series
- **Skill Development**: Invest in improving abilities
- **Market Expansion**: Explore new audiences
- **Collaboration**: Partner with other creators

## Verifying Coin Earnings (Test Checklist)

Use this checklist when validating that coin monetization works end-to-end:

1. Publish your comic and paid chapter (admin must set chapter status to **Published**)
2. Use a **non-subscriber** test reader account with enough coins in their wallet
3. On the **comic page**, click **Purchase with Coins** on the paid chapter (do not only open the reader URL)
4. Confirm the reader sees a success message and can open the chapter
5. Log into the **artist panel** → Dashboard → **Coins Earned** should increase by the chapter coin price
6. Check **Payouts** for USD records only after the monthly payout batch has run

**Common mistakes**
- Testing with a **subscribed** user (no coin unlock, no Coins Earned increase)
- Opening the chapter without clicking **Purchase with Coins** first
- Expecting USD in Payouts immediately after a single unlock (monthly batch required)

## Troubleshooting

### Common Issues

#### Coins Earned Stays at Zero
- **Subscriber test**: Subscribers do not create coin unlocks; use a regular user without a subscription
- **No purchase action**: Reading alone does not charge coins; the reader must click **Purchase with Coins**
- **Wrong artist**: Confirm the comic's `artist_id` matches your artist account
- **Free chapter**: Chapters marked free or with zero coin price do not generate coin revenue

#### Chapter Reader Shows No Images
- **Symptom**: Purple reader page with no page images (or the message "No pages uploaded for this chapter")
- **Cause**: Chapter has no images saved, files are missing from storage, or pages need to be re-uploaded after a storage path fix
- **Fix**: Edit the chapter in the artist panel, re-upload page images, save, and ensure the comic/chapter is **Published**
- **Server**: Ensure `php artisan storage:link` has been run on the environment

#### Payment Problems
- **Delayed Payments**: Check processing times and contact support
- **Incorrect Amounts**: Verify calculations and report discrepancies
- **Failed Transfers**: Update payment information and retry
- **Missing Payments**: Contact support for investigation

#### Account Issues
- **Verification Problems**: Complete all required verification steps
- **Information Updates**: Keep payment details current
- **Security Concerns**: Report suspicious activity immediately
- **Access Problems**: Contact support for account issues

### Getting Help

#### Support Resources
- **Help Documentation**: Review platform guides
- **FAQ Section**: Find answers to common questions
- **Support Tickets**: Submit specific issues
- **Community Forums**: Connect with other artists

#### Professional Services
- **Tax Professionals**: Consult for tax planning
- **Legal Advisors**: Get advice on contracts and rights
- **Financial Planners**: Plan for long-term financial goals
- **Business Consultants**: Optimize your creative business

## Best Practices

### Financial Management
- **Regular Monitoring**: Check earnings and payouts regularly
- **Record Keeping**: Maintain detailed financial records
- **Tax Planning**: Plan for tax obligations throughout the year
- **Diversification**: Don't rely solely on one revenue stream

### Professional Development
- **Skill Investment**: Continuously improve your craft
- **Market Research**: Stay informed about industry trends
- **Networking**: Build relationships with other creators
- **Education**: Learn about business and marketing

### Content Quality
- **Consistent Standards**: Maintain high quality across all content
- **Reader Focus**: Prioritize reader experience and satisfaction
- **Innovation**: Experiment with new styles and formats
- **Feedback Integration**: Use reader feedback to improve

---

**Need help with support?** Continue to [Support System](./support-system.md) to learn how to get assistance when you need it.
