# Zone X Stores — Data Cleaning

## Overview
This repository documents the data cleaning process applied to a raw export of 1,200 e-commerce orders for Zone X Stores (Jan 2023 – Jun 2025). The raw data was preserved untouched in an "Origin Data" sheet as an audit trail; all cleaning happened in a separate "Clean Data" sheet.

## Cleaning Summary

| Issue Found | Detail | Action Taken |
|---|---|---|
| Missing CouponCode | 309 of 1,200 rows (~25.8%) were blank whenever no coupon was used | Relabeled `N/P` (Not Provided) instead of left blank — "no coupon used" is a meaningful category, not a null |
| Duplicate OrderIDs | Checked all 1,200 order records | Verified unique — no action needed |
| TotalPrice formula integrity | Checked Quantity × UnitPrice against TotalPrice on every row | Matches exactly on all 1,200 rows — field is trustworthy as-is |
| ShippingAddress lacks real location variety | All 1,200 addresses share the same street name ("Main St") — only house numbers differ | Left as-is, but flagged: cannot support city/region-level analysis despite looking like a location field |
| 2025 is a partial year | Date range runs 01/01/2023–30/06/2025 — 2023 and 2024 each have 12 months, 2025 has only 6 | Not a data error, but flagged — affects how year-over-year comparisons should be read downstream |

## Tools Used
Excel — manual audit, formula verification (`=Quantity*UnitPrice`), conditional formatting to spot blanks/duplicates

## Files
- `Origin Data` — raw, untouched export (1,200 rows, 14 columns)
- `Clean Data` — cleaned working copy used for all downstream analysis
