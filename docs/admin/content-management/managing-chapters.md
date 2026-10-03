---
sidebar_position: 2
title: Managing Chapters
description: A guide for administrators on how to manage comic chapters in the admin panel
---

# Managing Chapters

This guide explains how to manage comic chapters in the admin panel. As an administrator, you can view, edit, and manage individual chapters of comics on the platform.

## Accessing the Chapters Section

1. Log in to the admin panel with your administrator credentials
2. Navigate to the main sidebar navigation
3. Click on **Chapters** to access the chapter management interface

## Viewing Chapters

The Chapters page displays a table with all chapters in the system. The table includes the following information:

- **Comic**: The title of the comic the chapter belongs to
- **Title**: The chapter's title
- **Chapter Number**: The sequential number of the chapter
- **Free**: Whether the chapter is available for free
- **Prologue**: Whether the chapter is marked as a prologue
- **Coin Price**: The cost in coins to unlock the chapter (if not free)
- **Status**: Current publication status
- **Total Reads**: How many times the chapter has been read
- **Unique Readers**: Number of different users who have read the chapter
- **Completion Rate**: Percentage of readers who complete the chapter

You can:
- **Search** for chapters by ID, comic title, or chapter title
- **Sort** the table by clicking on column headers
- **Filter** chapters, including viewing trashed (deleted) chapters
- **Toggle columns** to customize your view

## Viewing Chapter Details

To view detailed information about a chapter:

1. Find the chapter in the table
2. Click on the **View** button (eye icon) in the actions column

The chapter detail page shows comprehensive information about the chapter, organized into sections:

### Chapter Details Section
- Chapter number and title
- Associated comic
- Description/content

### Access & Pricing Section
- Free chapter status
- Prologue status
- Coin price

### Metadata Section
- Publication status
- Language
- Display order

### Media Section
- Thumbnail image
- Chapter pages (images)

### Timestamps Section
- Creation date
- Last update date
- Deletion date (if applicable)

## Editing a Chapter

To edit a chapter's information:

1. Find the chapter in the table
2. Click the **Edit** button (pencil icon) in the actions column
3. Update the chapter information as needed across different sections:

### Chapter Details Section
- **Comic**: Change the associated comic
- **Title**: Update the chapter's title
- **Chapter Number**: Change the sequential number
- **Content**: Update the chapter description

### Configuration Section
- **Free**: Toggle whether the chapter is free to read
- **Prologue**: Toggle whether the chapter is a prologue
- **Coin Price**: Set the cost in coins to unlock the chapter
- **Status**: Change the publication status
- **Language**: Set the chapter's language
- **Order**: Adjust the display order

### Chapter Media Section
- **Thumbnail Image**: Update the chapter's thumbnail
- **Images**: Upload, reorder, or remove the chapter's pages

4. Click **Save** to apply your changes

## Managing Chapter Status

The status of a chapter determines its visibility and availability to readers:

1. Navigate to the chapter's edit page
2. In the **Configuration** section, find the **Status** dropdown
3. Select the appropriate status:
   - **Published**: Visible and available to readers
   - **Draft**: Not publicly visible, still in development
   - **Scheduled**: Held after review until **Publish at** is reached
   - **Archived**: No longer actively promoted but still available
   - **Rejected**: Not approved for publication
4. Optionally set **Publish at** (date and time in the admin timezone)
5. Click **Save** to apply the status change

**How scheduled release works:**

- **Publish at** is a hold **after** review. Draft and Requested Review chapters never go live from the schedule alone.
- Saving a **Published** chapter with a future **Publish at** moves it to **Scheduled**. Readers cannot see it yet.
- Saving a **Scheduled** chapter with a blank or past **Publish at** publishes it immediately.
- When **Publish at** arrives, the chapter becomes **Published** automatically. The public site still only shows published chapters.

## Managing Chapter Access

You can control how readers access chapters through several settings:

### Free vs. Paid Chapters

1. Navigate to the chapter's edit page
2. In the **Configuration** section:
   - Toggle **Is Free** to ON to make the chapter available without payment
   - Toggle **Is Free** to OFF and set a **Coin Price** to make it a paid chapter
3. Click **Save** to apply the changes

### Prologue Chapters

Prologue chapters are special chapters that are only accessible via direct links:

1. Navigate to the chapter's edit page
2. In the **Configuration** section, toggle **Is Prologue** to ON
3. Click **Save** to apply the change

## Managing Chapter Media

Chapters consist of a series of images that readers navigate through:

1. Navigate to the chapter's edit page
2. In the **Chapter Media** section:
   - Upload a **Thumbnail Image** to represent the chapter in listings
   - Upload **Images** for the chapter's pages
   - Reorder images by dragging and dropping them
   - Use the image editor to make adjustments if needed
3. Click **Save** to apply the changes

## Viewing the Public Page

To see how a chapter appears to readers:

1. Find the chapter in the table
2. Click the **View Public Page** button in the actions column
3. The chapter's public page will open in a new tab

This allows you to experience the chapter as readers do and verify its presentation.

## Bulk Actions

You can perform actions on multiple chapters at once:

1. Select chapters by checking the boxes next to their names
2. Use the bulk actions menu to choose an action:
   - **Delete**: Move chapters to trash
   - **Force Delete**: Permanently remove chapters
   - **Restore**: Recover chapters from trash

## Best Practices

- Ensure chapter numbers are sequential and consistent within each comic
- Verify that images are properly ordered and display correctly
- Set appropriate pricing for premium chapters
- Regularly review analytics to understand reader engagement
- Use the status field to control chapter visibility during review processes
- Check that chapter thumbnails accurately represent the content
- Ensure prologue chapters are properly marked to maintain reading order