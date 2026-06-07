# Activity Logs

## Overview

The Activity Logs module provides comprehensive tracking and monitoring of all user actions and system events within the application. It uses the Spatie Activity Log package with Filament integration to provide a powerful, searchable interface for administrators to monitor user behavior and system activities.

## Features

- **Comprehensive Logging**: Tracks all user actions and system events
- **Advanced Filtering**: Filter logs by user, action type, date range, and more
- **Searchable Interface**: Full-text search across all log entries
- **Collapsible Details**: Expandable view of detailed change information
- **Export Capabilities**: Export log data for analysis
- **Real-time Updates**: Live updates as new activities occur
- **Performance Optimized**: Efficient pagination and query optimization

## System Architecture

### Core Components

1. **Spatie Activity Log Package**: Core logging functionality
2. **Filament Activity Log**: Admin interface integration
3. **ActivityLogPage**: Custom admin page for log management
4. **Activity Model**: Database model for log entries
5. **Logger Classes**: Custom loggers for specific actions

### Logging Flow

1. User performs action → Event triggered
2. Activity logger captures event data
3. Log entry created with details
4. Admin interface displays logs with pagination
5. Filters and search applied to results

## Admin Interface

### Accessing Activity Logs

Navigate to **Admin Panel > Logs > Activity Log** to access the comprehensive activity monitoring interface.

### Main Interface Features

#### Log List View
- **Chronological Display**: Logs organized by date with sticky date headers
- **Collapsible Entries**: Expand/collapse detailed change information
- **Action Icons**: Visual indicators for different action types
- **User Information**: Shows which user performed each action
- **Timestamp**: Precise timing of each activity

#### Search and Filtering
- **Global Search**: Search across all log fields
- **User Filter**: Filter by specific users
- **Action Type Filter**: Filter by create, update, delete actions
- **Date Range Filter**: Filter by specific time periods
- **Model Filter**: Filter by affected model types

#### Pagination Controls
- **Records Per Page**: Selectable page sizes (10, 25, 50, 100, all)
- **Navigation**: Previous/next page controls
- **Page Information**: Shows current page and total records
- **Quick Navigation**: Jump to specific pages

## Understanding Log Entries

### Log Entry Structure

Each activity log entry contains:

#### Basic Information
- **User**: Who performed the action
- **Action**: Type of action (created, updated, deleted)
- **Model**: Which model was affected
- **Timestamp**: When the action occurred
- **Description**: Human-readable description of the action

#### Detailed Information
- **Properties**: JSON data containing changes
- **Old Values**: Previous values before changes
- **New Values**: New values after changes
- **Metadata**: Additional context information

### Action Types

#### Created Actions
- **Triggered**: When new records are created
- **Data**: Shows all initial field values
- **Use Case**: Track new user registrations, content creation

#### Updated Actions
- **Triggered**: When existing records are modified
- **Data**: Shows before/after values for changed fields
- **Use Case**: Track profile updates, content modifications

#### Deleted Actions
- **Triggered**: When records are deleted
- **Data**: Shows final state before deletion
- **Use Case**: Track content removal, account deletions

## Pagination and Performance

### Current Implementation

The Activity Log page uses Filament's standard pagination system with the following characteristics:

#### Pagination Settings
- **Default Page Size**: 25 records per page
- **Available Options**: 10, 25, 50, 100, all records
- **Database Queries**: Optimized with proper indexing
- **Memory Usage**: Efficient loading of paginated data

#### Performance Considerations
- **Indexed Fields**: Database indexes on frequently queried fields
- **Eager Loading**: Related data loaded efficiently
- **Query Optimization**: Minimal database queries per page
- **Caching**: Filament caches pagination results

### Pagination Issue Investigation

#### Known Issue: Large Dataset Performance

**Problem**: When the activity log contains many records, the pagination may load slowly or display fewer records than expected.

**Root Causes**:
1. **Large Dataset**: Activity logs can accumulate millions of records
2. **Complex Queries**: Filtering and searching on large datasets
3. **Memory Constraints**: Loading large result sets into memory
4. **Index Optimization**: Missing or inefficient database indexes

#### Solutions and Optimizations

**1. Database Indexing**
```sql
-- Add indexes for commonly filtered fields
CREATE INDEX idx_activity_log_causer_id ON activity_log(causer_id);
CREATE INDEX idx_activity_log_subject_type ON activity_log(subject_type);
CREATE INDEX idx_activity_log_created_at ON activity_log(created_at);
CREATE INDEX idx_activity_log_log_name ON activity_log(log_name);
```

**2. Query Optimization**
- Use date range filters to limit dataset size
- Implement proper eager loading for related data
- Add database query caching for frequently accessed data

**3. Pagination Improvements**
- Reduce default page size for better performance
- Implement cursor-based pagination for large datasets
- Add loading states during pagination

**4. Data Archiving**
- Archive old log entries to separate tables
- Implement log rotation and cleanup policies
- Use soft deletes for audit trail preservation

### Recommended Configuration

#### Optimal Pagination Settings
```php
// In ActivityLogPage.php
protected function getTableRecordsPerPageSelectOptions(): array
{
    return [10, 25, 50]; // Reduced options for better performance
}

protected function getDefaultTableRecordsPerPageSelectOption(): int
{
    return 25; // Smaller default page size
}
```

#### Performance Monitoring
- Monitor query execution times
- Track memory usage during pagination
- Set up alerts for slow log queries
- Regular performance audits

## Advanced Features

### Custom Loggers

#### Creating Custom Loggers
```php
<?php

namespace App\Filament\Admin\Loggers;

use Noxo\FilamentActivityLog\ResourceLogger\ResourceLogger;

class UserLogger extends ResourceLogger
{
    protected static string $resource = UserResource::class;

    protected function getLabel(): string
    {
        return 'User';
    }

    protected function getIcon(): string
    {
        return 'heroicon-o-user';
    }
}
```

#### Logger Configuration
```php
// In config/filament-activity-log.php
'loggers' => [
    'directory' => app_path('Filament/Admin/Loggers'),
    'namespace' => 'App\\Filament\\Admin\\Loggers',
],
```

### Filtering and Search

#### Advanced Filters
- **Date Range**: Filter by specific time periods
- **User Selection**: Filter by specific users
- **Action Types**: Filter by create, update, delete
- **Model Types**: Filter by affected models
- **Custom Fields**: Filter by specific log properties

#### Search Functionality
- **Full-text Search**: Search across all log fields
- **Fuzzy Matching**: Find similar terms
- **Case Insensitive**: Search regardless of case
- **Multiple Terms**: Search for multiple keywords

### Export and Reporting

#### Export Options
- **CSV Export**: Download log data for analysis
- **Date Filtering**: Export specific time periods
- **Field Selection**: Choose which fields to export
- **Format Options**: Various export formats

#### Reporting Features
- **Activity Summary**: Overview of recent activities
- **User Activity**: Activity reports by user
- **Model Activity**: Activity reports by model type
- **Trend Analysis**: Activity trends over time

## Configuration

### Activity Log Settings

#### Basic Configuration
```php
// In config/activitylog.php
return [
    'enabled' => env('ACTIVITY_LOGGER_ENABLED', true),
    'delete_records_older_than_days' => 365,
    'default_log_name' => 'default',
    'table_name' => 'activity_log',
];
```

#### Performance Settings
```php
// Optimize for large datasets
'performance' => [
    'default_page_size' => 25,
    'max_page_size' => 100,
    'enable_caching' => true,
    'cache_ttl' => 300, // 5 minutes
],
```

### Filament Integration

#### Page Configuration
```php
// In ActivityLogPage.php
protected static ?string $navigationIcon = 'heroicon-o-clipboard-document-list';
protected static ?string $navigationGroup = 'Logs';
protected static ?int $navigationSort = 210;

public static function canAccess(): bool
{
    return auth()->user()->hasAnyRole('admin');
}
```

## Troubleshooting

### Common Issues

#### Slow Pagination Performance
1. **Check Database Indexes**: Ensure proper indexing on activity_log table
2. **Reduce Page Size**: Use smaller page sizes for better performance
3. **Add Date Filters**: Limit data range to improve query speed
4. **Monitor Queries**: Check slow query log for optimization opportunities

#### Missing Log Entries
1. **Check Logging Enabled**: Verify ACTIVITY_LOGGER_ENABLED is true
2. **Review Logger Registration**: Ensure loggers are properly registered
3. **Check Permissions**: Verify user has permission to view logs
4. **Database Issues**: Check for database connection problems

#### Search Not Working
1. **Index Issues**: Ensure full-text search indexes are created
2. **Query Optimization**: Check search query performance
3. **Character Encoding**: Verify proper UTF-8 encoding
4. **Search Configuration**: Review search settings

### Performance Optimization

#### Database Optimization
```sql
-- Add composite indexes for common queries
CREATE INDEX idx_activity_log_composite ON activity_log(causer_id, created_at);
CREATE INDEX idx_activity_log_search ON activity_log(description, properties);

-- Add full-text search index
ALTER TABLE activity_log ADD FULLTEXT(description, properties);
```

#### Application Optimization
```php
// Implement query caching
protected function getActivities()
{
    return cache()->remember(
        "activity_log_page_{$this->page}",
        300,
        fn() => Activity::query()
            ->with(['causer', 'subject'])
            ->latest()
            ->paginate($this->perPage)
    );
}
```

#### Memory Optimization
```php
// Use cursor pagination for large datasets
protected function getActivities()
{
    return Activity::query()
        ->latest()
        ->cursorPaginate($this->perPage);
}
```

## Best Practices

### Log Management
- **Regular Cleanup**: Archive old logs to prevent database bloat
- **Performance Monitoring**: Monitor query performance regularly
- **Access Control**: Limit log access to authorized administrators
- **Data Retention**: Implement appropriate data retention policies

### Performance Optimization
- **Efficient Indexing**: Create indexes on frequently queried fields
- **Query Optimization**: Use efficient queries and avoid N+1 problems
- **Caching Strategy**: Implement appropriate caching for log data
- **Pagination Limits**: Use reasonable page sizes for optimal performance

### Security Considerations
- **Access Control**: Ensure only authorized users can view logs
- **Data Privacy**: Be mindful of sensitive information in logs
- **Audit Trail**: Maintain complete audit trail for compliance
- **Data Encryption**: Consider encrypting sensitive log data

## API Reference

### Activity Log Endpoints

#### Get Activity Logs
```
GET /api/activity-logs
```

#### Get Activity Log by ID
```
GET /api/activity-logs/{id}
```

#### Filter Activity Logs
```
GET /api/activity-logs?user_id=123&action=updated&date_from=2024-01-01
```

### Data Models

#### Activity Model
```php
class Activity extends Model
{
    protected $fillable = [
        'log_name',
        'description',
        'subject_id',
        'subject_type',
        'causer_id',
        'causer_type',
        'properties'
    ];

    protected $casts = [
        'properties' => 'collection'
    ];
}
```

## Support

For technical support with Activity Logs:

1. **Check Performance**: Monitor pagination performance and query times
2. **Review Configuration**: Verify activity log settings are correct
3. **Database Optimization**: Ensure proper indexing and query optimization
4. **Contact Development**: Provide specific performance issues and error details

### Performance Monitoring

#### Key Metrics to Monitor
- **Query Execution Time**: Time taken for log queries
- **Memory Usage**: Memory consumption during pagination
- **Page Load Time**: Time to load activity log pages
- **Database Connections**: Number of database connections used

#### Optimization Checklist
- [ ] Database indexes created on activity_log table
- [ ] Pagination page size optimized for performance
- [ ] Query caching implemented where appropriate
- [ ] Date range filters used for large datasets
- [ ] Regular log cleanup and archiving implemented
