# CFO-Level Financial Performance Dashboard
> Tableau · Financial Intelligence · YoY Variance Analysis · Multi-Division · 2024–2025

![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=Tableau&logoColor=white)
![Finance](https://img.shields.io/badge/Domain-Financial_Analytics-0052CC?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Production_Ready-2E8B57?style=for-the-badge)

---

## The Business Problem

A global organisation operating across **4 regions** (APAC, EMEA, LATAM, North America) and **4 divisions** (Cloud Services, Hardware Solutions, etc.) relied on fragmented, static financial reports. Leadership had no unified view to compare **YTD performance vs. the prior year** — and standard BI tools couldn't handle partial-year data, producing skewed margin comparisons.

---

## What I Built

An executive-ready **Financial Intelligence Suite** in Tableau that delivers instant clarity on profitability and asset efficiency — without requiring users to understand the underlying data model.

https://github.com/Data-Sherlock/CFO-Level-Financial-Performance-Dashboard/blob/main/Financial%20Dashboard.png

### Dashboard Features

| Feature | Description |
|---|---|
| **Dynamic KPI Cards** | Gross Margin, Operating Margin, ROA with real-time YoY delta + colour-coded arrows |
| **Parameter-Driven Trend Line** | Toggle across 9 financial metrics (Revenue → Net Income) on a single axis |
| **COGS Trend Chart** | Side-by-side monthly comparison: This Year vs. Last Year |
| **Income Statement Visual** | Waterfall-style bar chart from Revenue to Net Income |
| **Contextual Slicers** | Division & Region filters for business-unit drill-down |

---

## Technical Highlights

### 1. Custom Time Anchor Logic
The dataset ends in **August 2025** but was built in 2026. Standard "current year" logic would break — so I implemented a reference date to lock the YTD window:

```sql
// Reference anchor — locks "Current Year" to Aug 2025
[Reference Date] = MAKEDATE(2025, 08, 01)

// YTD filter — only includes months up to the anchor month
MONTH([Date]) <= MONTH([Reference Date])
  AND YEAR([Date]) = YEAR([Reference Date])
```

### 2. YoY Delta Calculations

```sql
// Gross Margin — Current Year
SUM(IF YEAR([Date]) = YEAR([Reference Date]) THEN [Gross Profit] END)
/ SUM(IF YEAR([Date]) = YEAR([Reference Date]) THEN [Revenue] END)

// YoY Delta
[Gross Margin CY] - [Gross Margin PY]
```

### 3. Parameter-Controlled Metric Switching
A single `[Selected Metric]` string parameter drives the trend line — executives toggle between Revenue, COGS, Gross Profit, Operating Expenses, Operating Income, Interest Expense, Pre-Tax Income, Income Tax, and Net Income without any additional views.

---

## Impact

- **40% reduction** in monthly financial review prep time
- Single source of truth across all regions and divisions
- Accurate partial-year comparisons — a problem unsolved by out-of-the-box tools

---

## Dataset

| Field | Detail |
|---|---|
| Period | Jan 2024 – Aug 2025 |
| Rows | ~20 million aggregated records |
| Granularity | Monthly · Division · Region |
| Metrics | Revenue, COGS, Gross Profit, OpEx, Operating Income, Interest, Pre-Tax, Tax, Net Income, Assets |

---

## Skills Demonstrated

`Tableau Desktop` · `LOD Expressions` · `Table Calculations` · `Parameter Actions` · `Financial KPI Design` · `YoY Variance Analysis` · `Executive Dashboard UX` · `Time Intelligence` · `Data Modelling`

---

*Dashboard screenshot above shows All Divisions / All Regions view. Use the filter dropdowns to slice by specific business units.*
