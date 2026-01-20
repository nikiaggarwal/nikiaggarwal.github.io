# Quick Start: Google Sheets CMS

This is a simplified guide to get your Google Sheets CMS up and running quickly.

## Step 1: Create Your Google Sheet

1. Go to [Google Sheets](https://sheets.google.com) and create a new spreadsheet
2. Name it "Mamdani Meter Data" (or whatever you prefer)

## Step 2: Create Three Sheets

Click the "+" button at the bottom to add sheets. You'll need three sheets total:

### Sheet 1: "Promises"

Create columns with these EXACT names (copy and paste to be safe):

```
id | title | category | status | statusLabel | oneLineSummary
```

Example data:
```
p1 | Fund tenant legal support citywide | Housing | Oof | Budget pending | Funding discussions are active, but no final commitment yet.
p2 | Expand bus lanes on key corridors | Transit | Alright-Alright | In motion | Agencies are coordinating next steps and public input.
```

**Status options:** Must be exactly one of these:
- `LET'S GOOO`
- `Alright-Alright`
- `Oof`
- `Yikes`

### Sheet 2: "Updates"

Create columns:
```
date | promiseId | headline | category
```

Example data:
```
01/18 | 123 | Council hearing scheduled for bus lane expansion | Transit
01/12 | 456 | Draft bill released for tenant legal support funding | Housing
```

### Sheet 3: "Overall"

Create columns:
```
status | label | lastUpdated
```

Example data (only ONE row needed):
```
Alright-Alright | Momentum Building | 2026-01-18T19:45:00-05:00
```

## Step 3: Publish Each Sheet

For EACH sheet (Promises, Updates, Overall), do this:

1. Click on the sheet tab to select it
2. Go to **File > Share > Publish to web**
3. In the dropdown, select **the specific sheet** (e.g., "Promises")
4. Choose format: **Comma-separated values (.csv)**
5. Click **Publish**
6. Copy the URL that appears

You should get a URL like:
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vS.../pub?gid=0&single=true&output=csv
```

**Important:** The `gid` number will be different for each sheet!

## Step 4: Add URLs to Your Website

1. Open [index.html](index.html)
2. Find this section near line 223:

```javascript
const SHEETS_CONFIG = {
  promises: "YOUR_PROMISES_SHEET_URL_HERE",
  updates: "YOUR_UPDATES_SHEET_URL_HERE",
  overall: "YOUR_OVERALL_SHEET_URL_HERE",
  cacheDuration: 5 * 60 * 1000 // 5 minutes
};
```

3. Replace the placeholder URLs with your actual published CSV URLs:

```javascript
const SHEETS_CONFIG = {
  promises: "https://docs.google.com/spreadsheets/d/e/2PACX-1vS.../pub?gid=0&single=true&output=csv",
  updates: "https://docs.google.com/spreadsheets/d/e/2PACX-1vS.../pub?gid=123456&single=true&output=csv",
  overall: "https://docs.google.com/spreadsheets/d/e/2PACX-1vS.../pub?gid=789012&single=true&output=csv",
  cacheDuration: 5 * 60 * 1000
};
```

## Step 5: Test

1. Save index.html
2. Push to GitHub (if using GitHub Pages)
3. Open your website
4. Open browser console (F12) - you should see: `✓ Data loaded from Google Sheets`

## Updating Content

To update your website content:

1. Edit your Google Sheet
2. Wait up to 5 minutes for the cache to refresh
3. Reload your website

## Troubleshooting

**Not loading?**
- Make sure you published each sheet as CSV (not "web page")
- Check that the `gid` parameter is different for each sheet
- Open the CSV URL directly in your browser to verify it works
- Check browser console (F12) for errors

**Wrong data showing?**
- Clear your browser's localStorage
- Check column names match exactly (case-sensitive!)

## Tips

- Keep the spreadsheet organized with one sheet per data type
- Use Google Sheets' built-in version history to track changes
- Share the sheet with team members so multiple people can edit
- The website caches data for 5 minutes, so changes aren't instant

Need more details? See [SHEETS_SETUP.md](SHEETS_SETUP.md)
