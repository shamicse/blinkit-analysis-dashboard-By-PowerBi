# Blinkit Grocery Data Analysis Dashboard

An end-to-end retail analytics project analyzing Blinkit's (India's last-minute grocery delivery app) sales performance, customer satisfaction, and inventory distribution — combining SQL-based data cleaning and analysis with an interactive Power BI dashboard.

## Project Overview

**Business Requirement:** Conduct a comprehensive analysis of Blinkit's sales performance, customer satisfaction, and inventory distribution to identify key insights and optimization opportunities using KPIs and visualizations in Power BI.

The project covers 8,523 item-level sales records across outlets of varying size, type, and location, and answers targeted business questions around fat content, item type, outlet establishment year, outlet size, and outlet location.

**Total Sales: 1.20M** | **Avg Sales: 140.99** | **No. of Items: 9K** | **Avg Rating: 3.92**

## Dataset

| | |
|---|---|
| **File** | `BlinkIT Grocery Data.csv` / `BlinkIT_Grocery_Data.xlsx` |
| **Records** | 8,523 items |
| **Key fields** | Item Fat Content, Item Type, Item Weight, Item Visibility, Outlet Establishment Year, Outlet Location Type, Outlet Size, Outlet Type, Total Sales, Rating |

## Data Cleaning (SQL)

Before analysis, the `Item_Fat_Content` field was standardized in SQL to remove inconsistent category labels (`LF`, `low fat` → `Low Fat`; `reg` → `Regular`), ensuring accurate aggregation and filtering.

```sql
UPDATE blinkit_data
SET Item_Fat_Content =
  CASE
    WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
    WHEN Item_Fat_Content = 'reg' THEN 'Regular'
    ELSE Item_Fat_Content
  END;
```

## SQL Analysis

All KPIs and breakdowns were first validated in SQL before being built into the dashboard, including:

- Total Sales, Average Sales, Number of Items, Average Rating (core KPIs)
- Total Sales by Fat Content
- Total Sales by Item Type
- Fat Content by Outlet Location Type (pivoted)
- Total Sales by Outlet Establishment Year
- Percentage of Sales by Outlet Size
- All metrics broken down by Outlet Type

See `queries/Query_Doc.docx` (or the SQL scripts) for the full annotated query set.

## Dashboard

**`Blinkit_Grocery_Data_Analysis_Dashboard.pbix`** — a single-page, Blinkit-branded interactive dashboard including:
- KPI cards: Total Sales, Average Sales, No. of Items, Average Rating
- Donut charts: Total Sales vs Outlet Size, Fat Content, Fat Content by Outlet Tier
- Line/area chart: Outlet Establishment trend over time
- Bar chart: Item Type by Total Sales / Average Sales / No. of Items (switchable)
- Horizontal bar chart: Sales by Outlet Location Tier
- Data table: All metrics by Outlet Type (Total Sales, No. of Items, Average Sales, Avg Rating, Item Visibility)
- Slicers: Outlet Location (x3), Reset and Home navigation buttons

![Blinkit Grocery Data Analysis Dashboard]
<img width="1473" height="815" alt="Image" src="https://github.com/user-attachments/assets/3289dc41-1066-470f-98c3-c91b77c1b7f1" />

## Key Insights

- **Low Fat items drive nearly 2x the sales of Regular items** — ₹776K (64.6%) vs ₹425K (35.1%) of total sales.
- **Fruits & Vegetables (₹178K) and Snack Foods (₹175K)** are the top two item types by sales, together accounting for roughly 30% of total revenue; **Seafood (₹9K) and Breakfast (₹16K)** are the lowest.
- **Tier 3 locations generate the most sales (₹472K, 39.3%)**, ahead of Tier 2 (₹393K, 32.7%) and Tier 1 (₹336K, 28.0%) — despite the "Tier" naming, lower-tier cities are outperforming Tier 1 in this dataset.
- **Medium-sized outlets contribute the most sales (42.3%)**, followed by Small (37.0%) and High (20.7%) — outlet count and footprint matter more than size classification alone.
- **Supermarket Type1 dominates the outlet type mix**, generating ₹787.5K in sales from 5,577 items — more than 5x any other outlet type — while Grocery Stores post the fewest items (1,083) despite a comparable average sale value.
- **Outlets established in 1998 significantly outperform every other cohort** (₹204.5K in sales), while all other establishment years cluster tightly around ₹129K–₹133K, suggesting the 1998 cohort of outlets has had the longest time to build customer base and loyalty.
- **Average rating is highly consistent (3.91–3.99) across all outlet types**, indicating customer satisfaction is stable and not a differentiator of outlet performance in this dataset.

## Tools & Tech Stack

- **SQL** — data cleaning and KPI validation
- **Power BI Desktop** — data modeling and interactive dashboard design
- **Power Query / DAX** — data transformation and measures
- **Excel** — source data

## Repository Structure

```
blinkit-analysis-dashboard-By-PowerBi/
├── BlinkIT_Grocery_Data.xlsx                       # Source dataset
├── Blinkit_Grocery_Data_Analysis_Dashboard.pbix     # Power BI dashboard
├── queries/
│   ├── Query_Doc.docx                              # Annotated SQL queries & explanations
│   └── Blinkit_Analysis.pptx                       # Business requirements deck
├── assets/
│   └── dashboard-screenshot.png                     # Dashboard preview
└── README.md
```

## How to Use

1. Clone this repository.
2. Open `Blinkit_Grocery_Data_Analysis_Dashboard.pbix` in [Power BI Desktop](https://app.powerbi.com/groups/me/reports/dc4cba4d-243c-479b-afec-c4f425004e52/0e3eaa2b0e487d3ca323?experience=power-bi).
3. Run the SQL scripts in `queries/` against your own `blinkit_data` table to reproduce the underlying analysis.
4. Use the Outlet Location slicers to filter the dashboard by tier, and the Item Type panel to switch between Total Sales, Average Sales, and No. of Items views.

## Author

**Shami**
📎 [GitHub](https://github.com/shamicse) · [Repository](https://github.com/shamicse/blinkit-analysis-dashboard-By-PowerBi)

---
⭐ If you found this project useful, consider giving it a star!
