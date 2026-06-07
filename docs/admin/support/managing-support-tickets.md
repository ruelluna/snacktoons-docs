---
sidebar_position: 1
title: Managing Support Tickets
---

# Managing Support Tickets

This documentation explains how the support ticket system works in the Snacktoons platform, including how artists and users can create tickets and how administrators can manage them.

## Overview

The support ticket system allows three types of users to interact with tickets:

1. **Regular Users/Readers**: Can create and reply to their own support tickets
2. **Artists**: Can create and manage their own support tickets through the artist panel
3. **Administrators**: Can view and manage all tickets through the admin panel

## How Users Create Support Tickets

### Regular Users/Readers

Regular users can create support tickets through the web interface:

1. Users navigate to `/support/tickets/new` or click on a "Support" link in the navigation
2. They fill out a form with the following information:
   - Subject (required)
   - Category selection (required)
   - Message body (required)
   - Optional file attachment (images, PDFs, or documents up to 10MB)
3. After submission, the ticket is created with "open" status and "medium" priority by default
4. Users can view their tickets at `/support/tickets` and individual tickets at `/support/tickets/{id}`
5. Users can reply to their own tickets, which will automatically change a "closed" ticket to "in-progress"

### Artists

Artists have a dedicated interface in the artist panel:

1. Artists access the "Support Tickets" section in their artist dashboard
2. They can create tickets with:
   - Subject
   - Message
   - Category selection (multiple categories can be selected)
   - Optional file attachment
3. Artists can only view and manage their own tickets
4. The interface allows them to reply to admin responses

## Managing Tickets in the Admin Panel

As an administrator, you have full control over all support tickets through the TicketResource in the admin panel.

### Accessing Support Tickets

1. Log in to the admin panel
2. Navigate to the "Support" section in the sidebar
3. Click on "Tickets" to view all support tickets

### Ticket Dashboard Features

The ticket listing page displays:

- A count of open tickets as a badge on the navigation item
- Color-coded status indicators (open: red, in progress: yellow, closed: green)
- Color-coded priority indicators (low: blue, medium: yellow, high: red)
- Filtering options by status, category, and submitter role
- Search functionality for ticket content

### Viewing and Managing Individual Tickets

When viewing a ticket, you can:

1. See all ticket details including:
   - Subject
   - Original message
   - Status and priority
   - Categories
   - Submitter information
   - Attachments (if any)
   - Complete message history

2. Edit ticket properties:
   - Change status (open, in progress, closed)
   - Adjust priority (low, medium, high)
   - Add or remove categories

3. Reply to tickets:
   - Add a response message
   - Attach files to your response (images, PDFs, or documents)
   - All replies are tracked with timestamps and user information

### Bulk Actions

You can perform bulk actions on multiple tickets:
- Close multiple tickets at once using the "Close Selected" bulk action

### Ticket Categories

Ticket categories help organize support requests by topic. These categories are used by both users and artists when creating tickets.

## Best Practices for Ticket Management

1. **Response Time**: Try to respond to open tickets promptly, especially those marked as high priority
2. **Status Management**: 
   - Use "open" for new tickets
   - Change to "in progress" when you're working on the issue
   - Set to "closed" when the issue is resolved
3. **Priority Assignment**:
   - Set "high" for urgent issues affecting multiple users
   - Use "medium" for standard requests
   - Use "low" for minor issues or suggestions
4. **Clear Communication**: Provide clear, concise responses to users and artists

## Technical Details

The support ticket system uses:
- A Ticket model with relationships to users and categories
- Media attachments for files
- A messaging system for ticket replies
- Separate interfaces for different user roles (admin, artist, regular user)