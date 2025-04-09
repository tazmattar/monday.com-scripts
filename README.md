# Monday.com to Google Sheets Sync

This Google Apps Script pulls items from a [Monday.com](https://monday.com) board and syncs them into a Google Sheet.  
Designed for internal studio workflow at Cavendish Music, it supports full pagination and avoids duplicate entries by checking item IDs.

## Features

- Syncs all **top-level items** from a Monday.com board
- Automatically maps and appends data to matching Google Sheet columns
- Prevents duplicate entries using `item.id`
- Dynamically creates sheet and headers if they don't exist
- Supports pagination with `items_page` and `cursor`
- Simple, fast, and fully serverless via Google Apps Script

## How It Works

1. Authenticates with the Monday.com API using a personal token
2. Uses GraphQL to fetch all items from the specified board
3. Checks existing rows in the sheet to prevent re-importing the same data
4. Appends only new items, mapping values to column headers in the sheet

## Folder Structure

This script is designed to be run inside a Google Apps Script bound to a Google Sheet.

The ID column is used to track imported items. It can be hidden in the Google Sheet if desired.

## Scheduling
To automate syncs:

Open Apps Script Editor from your Sheet (Extensions → Apps Script)

Go to Triggers → + Add Trigger

Select syncCavendishJobLogToSheet

Choose a time-driven event (e.g. every hour)

## Requirements
Google Workspace or Gmail account with access to Apps Script

A Monday.com board with data and a valid personal API token

A Google Sheet with a header row matching your Monday board columns

## Notes
Sub-items are not currently supported in this implementation

The script supports only top-level board items via items_page

Designed for internal use at Cavendish Music but can be adapted for any workflow


## Configuration

Edit the following constants at the top of the script:

```javascript
const MONDAY_API_KEY = "Bearer YOUR_TOKEN"; // Your Monday.com personal API token
const BOARD_ID = 1234567890; // The ID of the Monday board to sync from
const SPREADSHEET_ID = "your-spreadsheet-id"; // Google Sheet ID
const SHEET_NAME = "JOB LOG"; // Name of the tab to sync to
const ID_COLUMN = 22; // Column number (1-based) where the unique item ID is stored

