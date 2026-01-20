# Google Sheets CMS Setup Guide

This guide will help you set up Google Sheets as a lightweight CMS for The Mamdani Meter.

## Step 1: Create Your Google Sheets

You'll need **TWO sheets** in one Google Spreadsheet:

### Sheet 1: "Promises"
Create a sheet with these columns (exact spelling matters):

| id | title | category | status | statusLabel | oneLineSummary |
|----|-------|----------|--------|-------------|----------------|
| p1 | Fund tenant legal support citywide | Housing | Oof | Budget pending | Funding discussions are active, but no final commitment yet. |
| p2 | Expand bus lanes on key corridors | Transit | Alright-Alright | In motion | Agencies are coordinating next steps and public input. |

**Column descriptions:**
- `id`: Unique identifier (e.g., p1, p2, p3...)
- `title`: The promise title
- `category`: Category (Housing, Transit, Education, Labor, etc.)
- `status`: Must be one of: `LET'S GOOO`, `Alright-Alright`, `Oof`, `Yikes`
- `statusLabel`: Short status description
- `oneLineSummary`: Brief summary of current state

### Sheet 2: "Updates"
Create a sheet with these columns:

| date | promiseId | headline | category |
|------|-----------|----------|----------|
| 01/18 | 123 | Council hearing scheduled for bus lane expansion | Transit |
| 01/12 | 456 | Draft bill released for tenant legal support funding | Housing |

**Column descriptions:**
- `date`: Display date (e.g., 01/18)
- `promiseId`: Link to promise detail page
- `headline`: Update headline text
- `category`: Category tag

### Sheet 3: "Overall" (optional but recommended)
Create a sheet for the overall meter status:

| status | label | lastUpdated |
|--------|-------|-------------|
| Alright-Alright | Momentum Building | 2026-01-18T19:45:00-05:00 |

**Column descriptions:**
- `status`: Overall status (LET'S GOOO, Alright-Alright, Oof, Yikes)
- `label`: Description text
- `lastUpdated`: ISO date string

## Step 2: Publish Your Sheet to the Web

1. In Google Sheets, go to **File > Share > Publish to web**
2. Choose **Entire Document** or select specific sheets
3. Choose format: **Comma-separated values (.csv)**
4. Click **Publish**
5. You'll get a URL like: `https://docs.google.com/spreadsheets/d/e/SPREADSHEET_ID/pub?output=csv`

**Important:** You need separate CSV URLs for each sheet:
- For "Promises" sheet: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/pub?gid=SHEET_GID&single=true&output=csv`
- For "Updates" sheet: Use a different `gid` value
- For "Overall" sheet: Use a different `gid` value

### Finding the GID (Sheet ID):
1. Open your Google Sheet
2. Click on the sheet tab (e.g., "Promises")
3. Look at the URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit#gid=123456789`
4. The number after `gid=` is your sheet's GID

## Step 3: Update Your Website Configuration

In [index.html](index.html), you'll need to add your sheet URLs to the configuration section (I'll add this in the next step).

## Step 4: Test Your Setup

1. Publish your changes to GitHub Pages
2. Open your website
3. Check the browser console for any errors
4. Verify that promises and updates are loading correctly

## Tips

- **Cache**: The website caches sheet data for 5 minutes to avoid hitting rate limits
- **Updates**: Changes to your Google Sheet will appear on the website within 5 minutes
- **Backup**: Keep a backup copy of your sheet
- **Version History**: Use Google Sheets' version history to track changes

## Troubleshooting

**Data not loading?**
- Check that the sheet is published to web
- Verify the GID matches your sheet
- Check browser console for errors
- Make sure column names match exactly

**CORS errors?**
- Google Sheets CSV URLs should work without CORS issues
- If you see CORS errors, try using a different publishing method

**Data looks wrong?**
- Check that column names in your sheet match exactly (case-sensitive)
- Verify date formats and special characters
- Check the browser console for parsing errors
