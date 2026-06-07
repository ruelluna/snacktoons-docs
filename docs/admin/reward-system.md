# Reward System (Promotions)

## Overview

The Reward System allows users to earn Cherries (points) by performing various actions in the application. The system uses dynamic event mapping and flexible conditions to create targeted promotions that encourage user engagement and retention.

## Features

- **Dynamic Event Mapping**: Flexible event system for any user action
- **Conditional Rewards**: Advanced filtering and conditions for targeted promotions
- **Multiple Frequencies**: Always, once, daily, per chapter, per user
- **Real-time Processing**: Instant reward distribution
- **Admin Management**: Complete control over promotion creation and management
- **Event Tracking**: Comprehensive logging of all reward events

## System Architecture

### Core Components

1. **Promotion Model**: Defines reward rules and conditions
2. **DynamicRewardDispatcher**: Processes events and awards points
3. **Event Mapping System**: Maps events to promotion triggers
4. **Gamify Package**: Handles point calculations and user rewards
5. **PromotionResource**: Admin interface for managing promotions

### Event Processing Flow

1. User performs action → Event dispatched
2. DynamicRewardDispatcher catches event
3. System finds matching active promotions
4. Conditions evaluated → Points awarded if conditions met
5. Reward logged and user points updated

## Admin Management

### Accessing the Reward System

Navigate to **Admin Panel > Rewards > Promotions** to manage all reward-related configurations.

### Creating Promotions

#### Basic Promotion Setup

1. **Title**: Descriptive name for the promotion
2. **Event**: Select the event that triggers the reward
3. **Points Reward**: Number of Cherries to award
4. **Frequency**: How often the reward can be given

#### Event Selection

The system provides a comprehensive list of available events:

**Standard Events:**
- `user_daily_login`: User logs in daily
- `chapter_completed`: User completes a chapter
- `user_registered`: New user registration
- `user_subscribed`: User purchases subscription
- `chapter_purchased`: User purchases a chapter

**Custom Events:**
- `comic_favorited`: User favorites a comic
- `user_profile_updated`: User updates profile
- `chapter_completed`: Chapter completion
- Any custom event you define

#### Frequency Options

- **Always**: Award every time the event occurs
- **Once**: Award only the first time
- **Daily**: Award once per day per user
- **Per Chapter**: Award once per chapter per user
- **Per User**: Award once per user total

### Advanced Conditions

The **Conditions** field is a powerful feature that allows you to create highly targeted promotions using JSON-based filtering.

#### Condition Structure

Conditions are defined as JSON objects that evaluate against the event data:

```json
{
  "field_name": "expected_value",
  "numeric_field": 123,
  "boolean_field": true,
  "array_field": ["value1", "value2"]
}
```

#### Common Condition Examples

**Chapter-Specific Rewards:**
```json
{
  "chapter_id": 123
}
```
Only awards points when the specific chapter (ID: 123) is completed.

**Comic-Specific Rewards:**
```json
{
  "comic_id": 456
}
```
Only awards points for actions related to the specific comic.

**User Role Conditions:**
```json
{
  "user_role": "premium"
}
```
Only awards points to premium users.

**Time-Based Conditions:**
```json
{
  "hour": 9,
  "day_of_week": "monday"
}
```
Only awards points during specific times.

**Complex Conditions:**
```json
{
  "chapter_id": 123,
  "user_role": "premium",
  "comic_category": "action"
}
```
Combines multiple conditions for highly targeted rewards.

#### Condition Field Reference

**User-Related Fields:**
- `user_id`: Specific user ID
- `user_role`: User role/type
- `user_subscription_status`: Subscription status
- `user_join_date`: When user joined

**Content-Related Fields:**
- `chapter_id`: Specific chapter
- `comic_id`: Specific comic
- `comic_category`: Comic category
- `comic_genre`: Comic genre
- `chapter_number`: Chapter number

**Time-Related Fields:**
- `hour`: Hour of day (0-23)
- `day_of_week`: Day of week (monday, tuesday, etc.)
- `month`: Month of year
- `is_weekend`: Boolean for weekend

**Action-Related Fields:**
- `action_type`: Type of action performed
- `action_value`: Value associated with action
- `device_type`: User's device type
- `platform`: Platform (web, mobile, app)

#### Condition Operators

**Exact Match:**
```json
{
  "chapter_id": 123
}
```

**Array Contains:**
```json
{
  "comic_genre": ["action", "adventure"]
}
```

**Range Conditions:**
```json
{
  "chapter_number": {"min": 1, "max": 10}
}
```

**Boolean Conditions:**
```json
{
  "is_premium_user": true,
  "has_completed_tutorial": false
}
```

### Promotion Status & Timing

#### Active Status
- **Active**: Promotion is currently running
- **Inactive**: Promotion is paused but not deleted

#### Validity Period
- **Valid From**: When the promotion starts
- **Valid To**: When the promotion ends
- **Null Values**: No time restrictions

## Event Mapping System

### How Event Mapping Works

The system uses a flexible event mapping mechanism that allows you to:

1. **Define Custom Event Keys**: Map events to custom keys
2. **Use Standard Events**: Leverage built-in event classes
3. **Extend Event System**: Add new events as needed

### Configuring Event Mappings

#### Method 1: Configuration File

Edit `config/gamify-events.php`:

```php
return [
    'event_mappings' => [
        'user_daily_login' => \App\Events\UserLoggedIn::class,
        'chapter_completed' => \App\Events\ChapterRead::class,
        'custom_event' => \App\Events\CustomEvent::class,
    ],
];
```

#### Method 2: Service Provider

Register mappings in `EventMappingServiceProvider`:

```php
public function boot(): void
{
    $this->registerEventMappings([
        'comic_favorited' => \App\Events\ComicFavorited::class,
        'user_profile_updated' => \App\Events\ProfileUpdated::class,
    ]);
}
```

#### Method 3: Programmatically

Add mappings at runtime:

```php
use Illuminate\Support\Facades\Config;

$eventMappings = Config::get('gamify-events.event_mappings', []);
$newMappings = array_merge($eventMappings, [
    'new_event' => \App\Events\NewEvent::class,
]);
Config::set('gamify-events.event_mappings', $newMappings);
```

### Creating Custom Events

#### Event Class Structure

```php
<?php

namespace App\Events;

use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;

class CustomEvent
{
    use Dispatchable, SerializesModels;

    public $user;
    public $data;

    public function __construct($user, $data = [])
    {
        $this->user = $user;
        $this->data = $data;
    }
}
```

#### Dispatching Events

```php
// Dispatch the event
event(new CustomEvent($user, [
    'chapter_id' => 123,
    'comic_id' => 456,
    'action_type' => 'read'
]));
```

## Promotion Management

### Viewing Promotions

#### List View Features
- **Search**: Search by title or event key
- **Filtering**: Filter by active status, frequency, or date range
- **Sorting**: Sort by any column
- **Bulk Actions**: Delete multiple promotions

#### Promotion Details
Each promotion shows:
- **Title**: Promotion name
- **Event**: Triggering event
- **Points**: Cherries awarded
- **Frequency**: Award frequency
- **Status**: Active/inactive
- **Validity**: Start and end dates

### Editing Promotions

#### Modifying Conditions
1. Navigate to the promotion
2. Click **Edit**
3. Modify the **Conditions** field
4. Save changes

#### Testing Conditions
Use the test routes to verify conditions:
- `/test-reward`: Test basic reward system
- `/add-event-mapping`: Test event mapping

### Promotion Analytics

#### Performance Metrics
- **Total Awards**: Number of times promotion was triggered
- **Unique Users**: Number of users who received the reward
- **Average Points**: Average points awarded per trigger
- **Success Rate**: Percentage of eligible events that received rewards

#### Export Capabilities
- **CSV Export**: Download promotion data
- **Date Filtering**: Filter by specific time periods
- **Event Filtering**: Focus on specific events

## Advanced Features

### Conditional Logic

#### Complex Conditions Example

```json
{
  "user_role": "premium",
  "chapter_id": {"in": [123, 124, 125]},
  "time_of_day": {"between": [9, 17]},
  "day_of_week": {"not_in": ["saturday", "sunday"]},
  "comic_category": "action"
}
```

This condition awards points only to premium users who complete specific chapters during business hours on weekdays for action comics.

#### Nested Conditions

```json
{
  "user": {
    "subscription_status": "active",
    "join_date": {"after": "2024-01-01"}
  },
  "content": {
    "chapter_id": 123,
    "comic_genre": ["action", "adventure"]
  }
}
```

### Dynamic Conditions

#### Time-Based Promotions

```json
{
  "hour": {"between": [18, 22]},
  "day_of_week": "friday"
}
```
Weekend evening promotions.

#### Seasonal Promotions

```json
{
  "month": {"in": [12, 1, 2]},
  "user_region": "northern_hemisphere"
}
```
Winter season promotions.

### Performance Optimization

#### Efficient Conditions
- Use specific field names
- Avoid complex nested conditions
- Use indexed fields when possible
- Test conditions with sample data

#### Monitoring Performance
- Check promotion processing times
- Monitor database query performance
- Review event processing logs
- Optimize frequently used conditions

## Troubleshooting

### Common Issues

#### Promotions Not Triggering
1. **Check Event Mapping**: Verify event is properly mapped
2. **Validate Conditions**: Test conditions with sample data
3. **Check Active Status**: Ensure promotion is active
4. **Verify Timing**: Check validity dates
5. **Review Frequency**: Ensure frequency allows new awards

#### Condition Evaluation Issues
1. **JSON Syntax**: Validate JSON format
2. **Field Names**: Check field names match event data
3. **Data Types**: Ensure data types match expectations
4. **Nested Fields**: Verify nested field access

#### Performance Problems
1. **Complex Conditions**: Simplify overly complex conditions
2. **Database Indexes**: Ensure proper indexing
3. **Event Volume**: Monitor high-volume events
4. **Caching**: Implement caching for frequent conditions

### Debug Tools

#### Testing Routes
- `/test-reward`: Test basic reward functionality
- `/add-event-mapping`: Test event mapping system

#### Logging
Check application logs for:
- Event processing errors
- Condition evaluation failures
- Performance issues

#### Manual Testing
1. Create test promotions with simple conditions
2. Trigger events manually
3. Verify reward distribution
4. Check user point balances

## Best Practices

### Promotion Design
- **Clear Objectives**: Define specific goals for each promotion
- **Targeted Conditions**: Use conditions to reach specific user segments
- **Reasonable Rewards**: Set appropriate point values
- **Frequency Limits**: Prevent reward abuse with frequency limits

### Condition Management
- **Documentation**: Document complex conditions
- **Testing**: Test conditions before deployment
- **Monitoring**: Monitor condition performance
- **Optimization**: Regularly review and optimize conditions

### System Maintenance
- **Regular Review**: Review promotion performance monthly
- **Cleanup**: Remove inactive or ineffective promotions
- **Updates**: Update conditions based on user behavior
- **Backup**: Backup promotion configurations

## API Reference

### Promotion Endpoints

#### Get Promotions
```
GET /api/promotions
```

#### Create Promotion
```
POST /api/promotions
```

#### Update Promotion
```
PUT /api/promotions/{id}
```

#### Delete Promotion
```
DELETE /api/promotions/{id}
```

### Event Endpoints

#### Dispatch Event
```
POST /api/events/dispatch
```

#### Get Event Mappings
```
GET /api/events/mappings
```

### Data Models

#### Promotion Model
```php
class Promotion extends Model
{
    protected $fillable = [
        'title',
        'event_key',
        'points_reward',
        'frequency',
        'conditions',
        'is_active',
        'valid_from',
        'valid_to'
    ];

    protected $casts = [
        'conditions' => 'array',
        'is_active' => 'boolean',
        'valid_from' => 'datetime',
        'valid_to' => 'datetime'
    ];
}
```

## Support

For technical support with the Reward System:

1. **Check Documentation**: Review this guide for common solutions
2. **Test Conditions**: Use the test routes to verify functionality
3. **Review Logs**: Check application logs for error messages
4. **Contact Development**: Provide specific error details and promotion configurations
