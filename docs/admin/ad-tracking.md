# Ad Tracking Module

## Overview

The Ad Tracking module provides comprehensive campaign management and event tracking capabilities for marketing campaigns. It allows administrators to create campaigns, track user interactions (impressions, clicks, conversions), and analyze performance through real-time analytics.

## Features

- **Campaign Management**: Create and manage advertising campaigns with detailed settings
- **Event Tracking**: Track impressions, clicks, and conversions via lightweight JavaScript
- **Real-time Analytics**: View campaign performance in real-time
- **UTM Parameter Support**: Automatic tracking of UTM parameters
- **Cross-platform Compatibility**: Works with WordPress, external sites, and any web platform
- **Daily Email Reports**: Automated performance reports
- **Read-only Event Logs**: Secure, immutable tracking data

## Campaign Management

### Creating a Campaign

1. Navigate to **Admin Panel > Ad Tracking > Ad Campaigns**
2. Click **Create** to add a new campaign
3. Fill in the required information:

   **Basic Information:**
   - **Campaign Name**: Internal reference name for the campaign
   - **Target URL**: Destination URL where users will be directed
   - **Client ID**: Optional identifier for client-specific tracking
   - **Budget**: Total budget allocated in USD

   **Timing:**
   - **Start Date**: When the campaign begins (events tracked after this date)
   - **End Date**: When the campaign ends (events not tracked after this date)

   **Security:**
   - **Allowed Domains**: Comma-separated list of domains allowed to send tracking data
     - Example: `https://client.com,http://localhost:3000`
     - Leave empty to allow all domains (not recommended for production)

### Campaign Status

Campaigns automatically display their status based on current date:

- **Active**: Currently running (start date ≤ today ≤ end date)
- **Upcoming**: Scheduled to start in the future
- **Ended**: Past the end date

### Campaign Actions

- **View**: See campaign details and related events
- **Edit**: Modify campaign settings
- **Delete**: Remove campaign (does not delete tracked events)

## Event Tracking

### Implementation

To track events for a campaign, add the following JavaScript code to your website:

```html
<script>
  window.CAPI_CAMPAIGN_ID = 1; // Replace with your actual campaign ID
  window.CAPI_API_HOST = 'https://yourdomain.com';
</script>
<script src="https://yourdomain.com/tracker.js" defer></script>
```

### Automatic Event Tracking

The tracking script automatically:

- **Tracks impressions** when the page loads
- **Tracks clicks** on elements with `data-track-click` attribute
- **Collects UTM parameters** from the URL

### Manual Event Tracking

For conversions, add this script to your thank you/order complete page:

```html
<script>
  if (typeof track === "function") {
    track("conversion");
  }
</script>
```

### Click Tracking

Add the `data-track-click` attribute to any clickable element:

```html
<a href="https://yourstore.com/sale?utm_source=facebook" data-track-click>
  Shop Now
</a>
```

## Event Types

### Impression
- **Triggered**: When a page loads with the tracking script
- **Data Collected**: IP address, user agent, timestamp, UTM parameters
- **Use Case**: Measure reach and visibility

### Click
- **Triggered**: When user clicks an element with `data-track-click`
- **Data Collected**: IP address, user agent, timestamp, UTM parameters, clicked element
- **Use Case**: Measure engagement and interest

### Conversion
- **Triggered**: When manually called on completion page
- **Data Collected**: IP address, user agent, timestamp, UTM parameters
- **Use Case**: Measure actual sales or goal completions

## Analytics & Reporting

### Real-time Analytics

View campaign performance in the admin panel:

1. Navigate to **Ad Campaigns**
2. Click on a campaign to view details
3. See related events in the **Ad Events** tab

### Event Logs

Access comprehensive event logs:

1. Navigate to **Ad Tracking > Ad Events**
2. Use filters to narrow down results:
   - **Event Type**: Filter by impression, click, or conversion
   - **Campaign**: Filter by specific campaign
   - **Date Range**: Filter by creation date

### Daily Email Reports

Automated reports include:
- Total impressions
- Total clicks
- Total conversions
- Click-through rate (CTR)
- Conversion rate

## Data Security

### Privacy Considerations

- **IP Addresses**: Stored for fraud prevention and geographic analysis
- **User Agents**: Stored for device/browser analytics
- **Metadata**: Stored as JSON for detailed analysis
- **Data Retention**: Configured in system settings

### Domain Restrictions

Use the **Allowed Domains** field to restrict which websites can send tracking data:

```
https://client.com,https://landing-page.com
```

This prevents unauthorized tracking and ensures data integrity.

## Troubleshooting

### Common Issues

**Events Not Tracking:**
1. Verify campaign ID is correct
2. Check if campaign is active (within date range)
3. Ensure domain is in allowed domains list
4. Check browser console for JavaScript errors

**Script Not Loading:**
1. Verify the tracker.js URL is accessible
2. Check if CORS is properly configured
3. Ensure the script is loaded before page content

**Conversion Not Recording:**
1. Verify the `track()` function is called
2. Check if the page loads completely
3. Ensure the campaign is still active

### Debug Mode

Enable debug mode by adding this to your tracking script:

```html
<script>
  window.CAPI_DEBUG = true;
</script>
```

This will log tracking events to the browser console for debugging.

## Best Practices

### Campaign Setup
- Use descriptive campaign names for easy identification
- Set realistic start and end dates
- Configure allowed domains for security
- Set appropriate budgets for tracking

### Implementation
- Test tracking on staging environments first
- Use UTM parameters for detailed attribution
- Implement conversion tracking on all goal completion pages
- Monitor event logs regularly for anomalies

### Performance
- The tracking script is lightweight and won't impact page load times
- Events are sent asynchronously to avoid blocking user interactions
- Failed tracking attempts are logged but don't break the user experience

## API Reference

### Event Data Structure

Each tracked event includes:

```json
{
  "id": 123,
  "campaign_id": 1,
  "event_type": "impression",
  "ip_address": "192.168.1.1",
  "user_agent": "Mozilla/5.0...",
  "metadata": {
    "utm_source": "facebook",
    "utm_medium": "cpc",
    "utm_campaign": "summer2025",
    "referrer": "https://facebook.com"
  },
  "created_at": "2025-01-15T10:30:00Z"
}
```

### UTM Parameters

The system automatically captures these UTM parameters:
- `utm_source`: Traffic source (e.g., facebook, google)
- `utm_medium`: Marketing medium (e.g., cpc, email)
- `utm_campaign`: Campaign name
- `utm_term`: Keywords (for paid search)
- `utm_content`: Content variation

## Support

For technical support or questions about the Ad Tracking module:

1. Check the troubleshooting section above
2. Review event logs for error patterns
3. Contact the development team with specific error messages
4. Provide campaign ID and affected domain for faster resolution
