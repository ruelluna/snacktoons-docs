---
sidebar_position: 2
title: Managing System Users
description: A guide for administrators on how to manage system users in the admin panel
---

# Managing System Users

This guide explains how to manage system users (administrators) in the admin panel. As an administrator, you can create, edit, delete, and manage other admin users in the system.

## Accessing the System Users Section

1. Log in to the admin panel with your administrator credentials
2. Navigate to the **Settings** section in the sidebar
3. Click on **System Users** to access the user management interface

## Viewing System Users

The System Users page displays a table with all administrator accounts in the system. The table includes the following information:

- **Name**: The user's full name
- **Email**: The user's email address
- **Created At**: When the user account was created (hidden by default)
- **Updated At**: When the user account was last updated (hidden by default)

You can:
- **Search** for users by name or email using the search bar
- **Sort** the table by clicking on column headers
- **Toggle columns** by clicking the column visibility button

## Creating a New System User

To create a new administrator account:

1. Click the **New System User** button at the top of the System Users page
2. Fill in the required information:
   - **Name**: Enter the full name of the user
   - **Email**: Enter a valid email address
   - **Password**: Create a secure password
3. Click **Create** to add the new user

## Editing a System User

To edit an existing user:

1. Find the user in the table
2. Click the **Edit** button (pencil icon) in the actions column
3. Update the user information as needed:
   - **Name**: Update the user's name
   - **Email**: Update the user's email address
   - **Password**: Leave blank to keep the current password, or enter a new password to change it
4. Click **Save** to apply your changes

## Sending Password Reset Links

If a user needs to reset their password:

1. Find the user in the table
2. Click the **Send Reset Link** button (envelope icon) in the actions column
3. The system will send a password reset link to the user's email address
4. You'll see a notification confirming the reset link was sent successfully

## Deleting System Users

To delete a user:

1. Find the user in the table
2. Click the **Delete** button (trash icon) in the actions column
3. Confirm the deletion when prompted

**Important Notes:**
- The primary admin user (with email admin@example.com) cannot be deleted
- Deleting a user is permanent and cannot be undone

## Bulk Actions

You can perform actions on multiple users at once:

1. Select users by checking the boxes next to their names
2. Use the bulk actions menu to choose an action:
   - **Delete**: Remove multiple users at once

**Note:** The primary admin user cannot be deleted, even as part of a bulk action.

## Best Practices

- Create individual accounts for each administrator rather than sharing credentials
- Use strong, unique passwords for each account
- Regularly review the list of system users and remove accounts that are no longer needed
- Send password reset links instead of manually setting passwords for other users when possible
- Be cautious when deleting user accounts, as this action cannot be undone