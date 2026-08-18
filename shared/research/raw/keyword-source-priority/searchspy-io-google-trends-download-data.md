<!--
URL: https://searchspy.io/google-trends/download-data
Fetch date: 2026-08-18
Source type: vendor/community guide
Research cluster: keyword-source-priority
Archived by: forge stage 2 sweep round 2 (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., covering the 8 pairs left uncovered by round 1.
-->

# Downloading & Exporting Google Trends Data — Google Trends Guide
URL: https://searchspy.io/google-trends/download-data
Author: SearchSpy

Downloading & Exporting Google Trends Data — Google Trends Guide

Chapter 12

# Downloading & Exporting Google Trends Data

Part of the Google Trends Complete Guide· Last updated April 2026

Google Trends lets you export data as a CSV from three separate modules: Interest Over Time, Interest By Region, and Related Queries. This is useful for custom analysis in Excel, Google Sheets, Python, R, or any data tool you prefer — but there are important caveats about what the exported data actually contains.

## How to download Google Trends data

1. Go to trends.google.com and run your search
2. Set your preferred filters: search type, geographic filter, time range, and category
3. In the Interest Over Time chart (or Interest By Region table, or Related Queries table), look for the download icon (↓) in the top-right corner of that section
4. Click it — a CSV file will download immediately. No account or sign-in required.
5. If comparing multiple terms, each term's data will be included as a separate column in the same CSV file

## What the exported CSV contains

Interest Over Time CSV

Date (week or month), relative interest score (0–100) for each search term. Dates are bucketed based on your selected time range (daily for <90 days, weekly for 90 days–5 years, monthly for 5+ years).

Interest By Region CSV

Geographic unit (country, state, city, or metro area), relative interest score (0–100) for each location. Higher scores indicate higher relative interest in that location, not absolute volume.

Related Queries CSV

Query text, interest score (for Top queries) or percentage growth (for Rising queries). Breakout queries show as 'Breakout' instead of a percentage.

All exported Google Trends data is in relative terms (0–100 scale), not absolute search counts. You cannot determine actual monthly search volume from Google Trends CSV exports. A score of 87 tells you it's near peak — not how many people searched.

## Opening the CSV in Excel or Google Sheets

The exported file is a standard UTF-8 CSV with a short metadata header (including the search term and parameters used). To open it:

- Excel: Download the file, then double-click to open. Excel should automatically detect the CSV format.
- Google Sheets: Create a blank sheet → File → Import → Upload. Drag and drop the CSV file, ensure "Replace spreadsheet" is selected, then click Import.
- Python/Pandas: Use`pd.read_csv('multiTimeline.csv', skiprows=1)` to skip the metadata header row.

## Exporting comparison data for multiple terms

When you're comparing multiple terms, the Interest Over Time CSV includes all terms as separate columns — making it easy to chart them in a spreadsheet. However, remember that the scores are normalized together: if you download Term A and Term B in the same export, they share the same 0–100 scale. Downloading them separately would produce different scores because each becomes its own maximum.

## Automating Google Trends data collection

There is no official Google Trends API. Options for programmatic access:

pytrends (Python)

Unreliable

Unofficial Python library that scrapes Google Trends. Works but is rate-limited, frequently breaks when Google updates its UI, and is not suitable for production use. Best for personal projects and ad-hoc research.

SearchSpy API (via Google Trends + Google Ads v20)

✓ Reliable

SearchSpy uses the Google Ads Keyword Planner API and Google Trends to deliver exact monthly search volume, CPC, and competition data programmatically. Unlike pytrends, this uses official Google APIs.

SerpAPI / Google Trends endpoint

✓ Reliable (paid)

Real Time Google Trends Data coming from the Google Ads API. More reliable than pytrends but cost money per query. Suitable for production applications that need trend data at scale.

Continue reading

← PreviousGoogle Trends API

Next →How to Cite Google Trends
