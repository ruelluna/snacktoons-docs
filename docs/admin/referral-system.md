# Referral System

## Overview

The Referral System allows users to generate unique referral links and earn commissions from their friends' subscription and coin purchases. The system automatically tracks referrals, calculates payouts, and provides comprehensive management tools for administrators.

## Features

- **Referral Link Generation**: Users can create unique referral links
- **Automatic Tracking**: Referrals are tracked via cookies and middleware
- **Commission Calculation**: Automatic calculation of referral payouts
- **Bank Account Management**: Users can provide payment details
- **Admin Management**: Complete control over referral payouts
- **Email Notifications**: Automated notifications for payout processing

## System Architecture

### Core Components

1. **ReferralPayout Model**: Stores payout information and calculations
2. **UserDetail Model**: Stores bank account and payment information
3. **TrackReferral Middleware**: Automatically processes referral tracking
4. **CalculateReferralPayouts Command**: Processes payout calculations
5. **ReferralPayoutResource**: Admin interface for managing payouts

### Referral Tracking Flow

1. User clicks referral link → Cookie set with referral code
2. User makes purchase → Middleware checks for referral cookie
3. Referral relationship created → Cookie cleared
4. Payout calculated → Admin can mark as paid

## Admin Management

### Accessing Referral Data

Navigate to **Admin Panel > Referral Payouts** to manage all referral-related data.

### Referral Payout Management

#### Viewing Payouts

1. **List View**: See all referral payouts with filtering options
2. **Filters Available**:
   - **Purchase Type**: Filter by subscription or coin purchases
   - **Payment Status**: Filter by pending, paid, or failed status
   - **Date Range**: Filter by period start/end dates

#### Payout Details

Each payout record includes:
- **Referred User**: The user who made the purchase
- **Purchase Type**: Subscription or coin purchase
- **Amount**: The purchase amount
- **Commission**: Calculated referral commission
- **Status**: Pending, paid, or failed
- **Period**: The time period for the payout

#### Processing Payouts

1. **Review Payouts**: Check calculated payouts for accuracy
2. **Mark as Paid**: Click the "Mark as Paid" action
3. **Email Notification**: User automatically receives payout notification
4. **Status Update**: Payout status changes to "Paid"

### User Referral Management

#### Viewing User Referrals

1. Navigate to **Users > [Specific User]**
2. Access the **Referred Users** tab
3. View all users referred by this person

#### Referral Information

For each referred user, you can see:
- **Name**: Referred user's full name
- **Email**: Referred user's email address
- **Join Date**: When they joined via referral
- **Status**: Active or inactive status

#### User Payout History

1. Navigate to **Users > [Specific User]**
2. Access the **Referral Payouts** tab
3. View complete payout history for the user

### Bank Account Management

#### Viewing Bank Details

1. Navigate to **Users > [Specific User]**
2. Access the **Bank Details** tab
3. View user's payment information

#### Bank Account Information

Stored information includes:
- **Bank Name**: User's bank name
- **Account Number**: Bank account number
- **Routing Number**: Bank routing number
- **PayPal Email**: Alternative PayPal payment method

## Configuration

### Referral Settings

The referral system uses these configuration options:

#### Referral Percentage
- **Default**: 10% of purchase amount
- **Configurable**: Can be adjusted in admin settings
- **Applies to**: Both subscription and coin purchases

#### Referral Cookie
- **Name**: `snacktoons_ref`
- **Expiry**: 1 year
- **Purpose**: Tracks referral relationships

#### Referral Routes
- **Prefix**: `refer`
- **Redirect**: `dashboard` after referral link click

### Payout Calculation

#### Commission Structure
- **Subscription Purchases**: 10% of subscription amount
- **Coin Purchases**: 10% of coin purchase amount
- **Frequency**: Calculated per purchase
- **Minimum**: No minimum payout threshold

#### Calculation Process
1. System identifies referral relationship
2. Calculates commission based on purchase amount
3. Creates payout record with pending status
4. Admin reviews and marks as paid

## Automation

### Payout Calculation Command

The system includes an automated command for calculating payouts:

```bash
php artisan app:calculate-referral-payouts
```

#### Command Features
- **Automatic Processing**: Finds all eligible referrals
- **Subscription Payouts**: Calculates for subscription purchases
- **Coin Payouts**: Calculates for coin purchases
- **Duplicate Prevention**: Avoids creating duplicate payouts

#### Scheduling
The command can be scheduled to run automatically:

```php
// In routes/console.php
$schedule->command('app:calculate-referral-payouts')->daily();
```

### Email Notifications

#### Payout Processed Email
When a payout is marked as paid:
- **Recipient**: User who earned the referral
- **Content**: Payout amount, purchase type, and payment details
- **Template**: `resources/views/emails/referral-payout-paid.blade.php`

## Data Management

### Referral Payout Records

#### Database Structure
- **id**: Unique payout identifier
- **referrer_id**: User who earned the referral
- **referred_user_id**: User who made the purchase
- **purchase_type**: Subscription or coin
- **amount**: Purchase amount
- **commission**: Calculated commission
- **status**: Pending, paid, or failed
- **period_start/end**: Payout period dates

#### Data Integrity
- **Read-only Events**: Referral events cannot be modified
- **Audit Trail**: Complete history of all referral activities
- **Relationship Tracking**: Maintains referrer-referred relationships

### User Bank Details

#### Security Considerations
- **Encrypted Storage**: Sensitive payment information is encrypted
- **Access Control**: Only admins can view bank details
- **Data Retention**: Follows privacy regulations

## Reporting & Analytics

### Referral Performance

#### Key Metrics
- **Total Referrals**: Number of successful referrals
- **Conversion Rate**: Percentage of referrals who make purchases
- **Total Payouts**: Sum of all paid commissions
- **Average Commission**: Average payout per referral

#### Export Capabilities
- **CSV Export**: Download referral data for analysis
- **Date Filtering**: Filter reports by specific time periods
- **User Filtering**: Focus on specific referrers

### Payout Reports

#### Financial Tracking
- **Pending Payouts**: Total amount awaiting payment
- **Paid Payouts**: Total amount already paid
- **Failed Payouts**: Payouts that couldn't be processed
- **Monthly Totals**: Payout summaries by month

## Troubleshooting

### Common Issues

#### Referral Links Not Working
1. **Check Referral Code**: Verify the referral code is valid
2. **Cookie Settings**: Ensure cookies are enabled
3. **Self-Referral**: Users cannot refer themselves
4. **Domain Issues**: Check if referral links are accessible

#### Payouts Not Calculating
1. **Referral Relationship**: Verify referral relationship exists
2. **Purchase Records**: Check if purchase records are present
3. **Duplicate Prevention**: Ensure no duplicate payouts exist
4. **Command Execution**: Run calculation command manually

#### Email Notifications Not Sending
1. **Email Configuration**: Check Laravel email settings
2. **User Email**: Verify user has valid email address
3. **Template Issues**: Check email template syntax
4. **Queue Processing**: Ensure email queue is running

### Debug Information

#### Logging
The system logs errors for debugging:
- **Referral Dashboard Errors**: `Error in referral dashboard: [message]`
- **Payout Errors**: `Error in referral payouts: [message]`
- **Bank Detail Errors**: `Error loading bank details: [message]`

#### Manual Verification
1. **Check Database**: Verify referral records exist
2. **Test Commands**: Run calculation command manually
3. **Review Logs**: Check application logs for errors
4. **User Testing**: Test referral flow with test users

## Best Practices

### Admin Management
- **Regular Review**: Check pending payouts weekly
- **Data Validation**: Verify payout calculations before marking as paid
- **Communication**: Inform users about payout processing times
- **Documentation**: Keep records of all payout decisions

### System Maintenance
- **Backup Data**: Regular backups of referral data
- **Monitor Performance**: Watch for calculation command performance
- **Update Settings**: Review and update referral percentages as needed
- **Security Audits**: Regular review of bank detail access

### User Support
- **Clear Communication**: Explain referral process to users
- **FAQ Maintenance**: Keep referral FAQ updated
- **Support Tickets**: Handle referral-related support requests promptly
- **Training**: Provide training for new admin users

## API Reference

### Referral Payout Endpoints

#### Get User Referrals
```
GET /api/users/{user}/referrals
```

#### Get User Payouts
```
GET /api/users/{user}/referral-payouts
```

#### Mark Payout as Paid
```
POST /api/referral-payouts/{payout}/mark-paid
```

### Data Models

#### ReferralPayout Model
```php
class ReferralPayout extends Model
{
    protected $fillable = [
        'referrer_id',
        'referred_user_id',
        'purchase_type',
        'amount',
        'commission',
        'status',
        'period_start',
        'period_end'
    ];
}
```

## Support

For technical support with the Referral System:

1. **Check Documentation**: Review this guide for common solutions
2. **Review Logs**: Check application logs for error messages
3. **Test Commands**: Run calculation commands manually
4. **Contact Development**: Provide specific error details and user IDs
