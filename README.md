# 📊 Retail Sales Performance Dashboard (Excel)

An interactive, formula-driven **Excel dashboard** that analyses **4.58 lakh retail orders (2022 – 2026)** across India — sales, profit, orders, regions, products and customers — with live slicers and 3D charts.

![Dashboard 3D preview](images/dashboard-3d-preview.png)

> *3D preview rendered outside Excel; the look inside Microsoft Excel may differ slightly.*

---

## 📌 Table of Contents
- [Overview](#-overview)
- [Key Insights](#-key-insights)
- [Dashboard Features](#-dashboard-features)
- [Dataset](#-dataset)
- [Workbook Structure](#-workbook-structure)
- [How It Works](#-how-it-works)
- [How to Use](#-how-to-use)
- [Large File](#-large-file-how-to-upload-to-github)
- [Repository Structure](#-repository-structure)
- [Tools & Skills](#-tools--skills)
- [Author](#-author)

---

## 🎯 Overview

Business question: **where does the money come from, and what drives profit?**

This dashboard turns a raw order table (**458,490 rows × 26 columns**) into one screen that answers:

- How much did we sell and earn, and at what margin?
- Which **categories, products, brands, cities and states** perform best?
- Which **channels and payment modes** do customers prefer?
- How do **sales trend** by month, quarter, year and weekday?
- How many orders are **cancelled / returned**, and how fast is delivery?

Everything updates live when you change a filter.

## 💡 Key Insights

| KPI | Value |
|-----|-------|
| Net Sales (valid orders) | **₹468.2 Cr** (₹4.68 B) |
| Profit | **₹101.2 Cr** — margin **21.6%** |
| Valid Orders | **3,91,228** out of 4,58,490 |
| Avg Order Value | **₹11,968** |
| Cancelled / Returned | **14.7%** |
| Avg Delivery Time | **5.9 days** |

**What stands out**

- 🔌 **Electronics ≈ 50%** of all sales (₹232.7 Cr), far ahead of Home Appliances (₹92.6 Cr) and Furniture (₹69.5 Cr).
- 💻 **Gaming Laptop RTX** is the #1 product (₹106.2 Cr); Acer, Asus and MSI are the top 3 brands.
- 🗺️ **North region = ~43%** of sales (₹200.2 Cr). **Uttar Pradesh** is the top state (₹82.5 Cr); **Delhi** is the top city (₹42.9 Cr).
- 📱 **UPI is the #1 payment mode (~38%)**, and **Online is the #1 channel (~38%)**.
- 📈 **Yearly sales grew every full year:** 2022 → 2023 **+27%**, 2023 → 2024 **+10%**, 2024 → 2025 **+18%** (2026 is a partial year).
- 📅 **Seasonality:** March (₹50.5 Cr) and January (₹48.9 Cr) are the strongest months; February is the weakest. Q4 and Q1 lead the quarters.
- 👥 Male customers account for ~62% of sales, female ~34%.
- 🚚 Weekday sales are almost flat — no single "best day".

## ✨ Dashboard Features

- **6 KPI cards** — Net Sales, Profit, Profit Margin, Avg Order Value, Valid Orders, Cancelled/Returned %
- **5 live filters (slicers):** Year, Region, Category, Channel, Payment Mode
- **3D charts:** Monthly sales, Yearly sales, Weekday sales, Sales by Channel & Payment Mode (3D pie), Category, Top 10 Cities, Top 10 Products, Delivery Speed, Device
- **India filled map** — *Sales by State* (colour-bucketed by sales)
- **Top 10 States** ranking table
- **Quarter-wise** and **Region-wise** (Sales, Profit, Orders) tables with colour-scale conditional formatting
- Navigation buttons between **Dashboard / Analysis / Data** sheets

| Original (2D) | 3D version |
|---|---|
| ![Original](images/dashboard-original.png) | ![3D](images/dashboard-3d-preview.png) |

## 🗃️ Dataset

- **Rows:** 458,490 order lines (391,228 valid sales)
- **Columns:** 26 — date, product hierarchy, geography, channel, payment, delivery, and financials
- **Period:** Jan 2022 – 2026 (2026 is partial)
- **Currency:** Indian Rupees (₹)

📖 Full column list and KPI definitions → [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md)
🔍 A 1,000-row sample for quick browsing → [`data/sample_orders.csv`](data/sample_orders.csv)

## 🧱 Workbook Structure

| Sheet | Purpose |
|-------|---------|
| **Dashboard** | The final visual report: KPIs, filters, charts, map and tables |
| **Analysis** | Formula-driven summary tables (monthly, yearly, quarterly, weekday, channel, payment, category, device, delivery, region, gender, top-10 city/state/product/brand) that feed the charts |
| **Data** | The raw order table (458,490 rows × 26 columns) |
| **Calc** | Helper sheet: filter lists, active filter criteria, and ranking helpers for the top-10 tables |
| **MapData** | Geometry and colour buckets that draw the India state map |

## ⚙️ How It Works

1. The user picks a value (or **All**) in the five dropdown filters on the **Dashboard**.
2. The **Calc** sheet converts each choice into a criterion (`All` → match everything).
3. The **Analysis** sheet calculates every table with `SUMIFS` / `COUNTIFS` over **named ranges** on the `Data` sheet (e.g. `d_net`, `d_profit`, `d_year`, `d_region`), using only rows where `Valid Sale = "Yes"`.
4. Charts, KPI cards, the map and the ranking tables read from **Analysis** and refresh automatically.

> No PivotTables or macros — everything is plain formulas, so it recalculates instantly with the filters.

## 🚀 How to Use

1. Download the workbook (see [Large File](#-large-file-how-to-upload-to-github) / the **Releases** page).
2. Open it in **Microsoft Excel (desktop)**. Enable editing if Excel opens it in *Protected View*.
3. Click a **yellow-bordered filter box** on the Dashboard and pick a value. Choose **All** to clear a filter.
4. Watch the KPIs and charts update. Use the left menu to jump to *Analysis* or *Data*.

**Notes**
- The file has 4.5 lakh rows, so it can take a few seconds to open or recalculate after changing a filter.
- Excel for the web, phone apps and Google Sheets are not recommended for a file this size.

## 📦 Large file: how to upload to GitHub

The workbook is about **54 MB**. GitHub's browser upload limit is 25 MB, so use one of these:

**Option A — Git command line** (works up to 100 MB; GitHub will show a size warning above 50 MB)

```bash
git add dashboard/Retail_Sales_Dashboard.xlsx
git commit -m "Add dashboard workbook"
git push
```

**Option B — Git LFS** (recommended for large binaries)

```bash
git lfs install
git lfs track "*.xlsx"
git add .gitattributes dashboard/Retail_Sales_Dashboard.xlsx
git commit -m "Add dashboard workbook via Git LFS"
git push
```

**Option C — GitHub Releases** (simple, browser-friendly, up to 2 GB per file)
Go to **Releases → Draft a new release**, attach the `.xlsx`, publish, then link it here.

## 📁 Repository Structure

```
excel-retail-sales-dashboard-india/
├── README.md
├── LICENSE
├── .gitignore
├── dashboard/
│   ├── README.md
│   └── Retail_Sales_Dashboard.xlsx      ← add your workbook here
├── data/
│   ├── README.md
│   └── sample_orders.csv                ← 1,000-row sample
├── docs/
│   └── DATA_DICTIONARY.md               ← columns + KPI definitions
└── images/
    ├── dashboard-3d-preview.png
    ├── dashboard-original.png
    └── dashboard-summary-infographic.png
```

## 🛠️ Tools & Skills

`Microsoft Excel` · `SUMIFS / COUNTIFS / IFERROR` · `Named Ranges` · `Data Validation (dropdown filters)` · `Conditional Formatting` · `3D Charts` · `Dashboard Design` · `Data Storytelling`

## 👤 Author

**Mayank Pandey**
🔗 LinkedIn: [linkedin.com/in/mayank-pandey-62b179327](https://www.linkedin.com/in/mayank-pandey-62b179327)
💻 GitHub: [@mp7286921-debug](https://github.com/mp7286921-debug)

⭐ If you found this useful, consider giving the repo a star!


