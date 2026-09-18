# ⚡ Power BI & Microsoft Fabric Journey

> A public learning portfolio documenting a 91-day Microsoft Power BI & Fabric certification path — built in the open, one commit at a time.

[![PL-300](https://img.shields.io/badge/PL--300-In%20Progress-blue?style=flat-square&logo=microsoft)](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/)
[![DP-600](https://img.shields.io/badge/DP--600-Planned-lightgrey?style=flat-square&logo=microsoft)](https://learn.microsoft.com/en-us/credentials/certifications/fabric-analytics-engineer-associate/)
[![DP-700](https://img.shields.io/badge/DP--700-Planned-lightgrey?style=flat-square&logo=microsoft)](https://learn.microsoft.com/en-us/credentials/certifications/fabric-data-engineer-associate/)

---

## 🗺️ About This Repository

This repo is my live study journal and code portfolio as I work through the full Microsoft Power BI and Fabric certification stack. Every DAX measure, every Power Query M snippet, every Fabric notebook I build during this journey lives here — documented, explained, and shared for the community.

**Started:** September 16, 2026  
**Goal:** Three Microsoft certifications by June 2027  
**Stretch goal:** Microsoft Fabric MVP nomination — October 2027

---

## 🎯 Certification Roadmap

| Certification | Full Name | Target Date | Status |
|--------------|-----------|-------------|--------|
| **PL-300** | Microsoft Power BI Data Analyst Associate | December 14, 2026 | 🔵 In Progress |
| **DP-600** | Microsoft Fabric Analytics Engineer Associate | February–March 2027 | ⬜ Planned |
| **DP-700** | Microsoft Fabric Data Engineer Associate | May–June 2027 | ⬜ Planned |

---

## 📂 Repository Structure

```
powerbi-fabric-journey/
│
├── 📁 dax/
│   ├── measures/           # Reusable DAX measures
│   ├── calculated-columns/ # Row-context DAX patterns
│   └── patterns/           # % of total, rankings, YTD, MTD
│
├── 📁 power-query/
│   ├── m-snippets/         # M language transformations
│   ├── parameters/         # Dynamic parameter patterns
│   └── query-folding/      # Folding examples and anti-patterns
│
├── 📁 fabric/
│   ├── notebooks/          # PySpark and Python notebooks
│   ├── pipelines/          # Data pipeline patterns
│   └── lakehouse/          # Lakehouse architecture examples
│
├── 📁 study-notes/
│   ├── pl-300/             # PL-300 module-by-module notes
│   ├── dp-600/             # DP-600 study notes (coming soon)
│   └── dp-700/             # DP-700 study notes (coming soon)
│
├── 📁 exam-prep/
│   ├── pl300-anki.txt      # Anki flashcard deck for PL-300
│   └── pl300-exam1.json    # Practice exam question bank
│
└── README.md
```

---

## 📚 Study Progress — PL-300

| Module | Topic | Status |
|--------|-------|--------|
| 1 | Discover Data Analysis | ✅ Done |
| 2 | Get Data in Power BI | 🔵 In Progress |
| 3 | Clean, Transform, and Load Data | ⬜ Pending |
| 4 | Design a Data Model in Power BI | ⬜ Pending |
| 5 | Create Model Calculations using DAX | ⬜ Pending |
| 6 | Optimize a Model for Performance | ⬜ Pending |
| 7 | Create Reports | ⬜ Pending |
| 8 | Create Dashboards | ⬜ Pending |
| 9 | Perform Advanced Analytics | ⬜ Pending |
| 10 | Manage Workspaces and Datasets | ⬜ Pending |
| 11 | Manage Files and Security | ⬜ Pending |

---

## 🧮 DAX Snippets — Quick Reference

### Basic Aggregations
```dax
-- Total Sales
Total Sales = SUM(Sales[SaleAmount])

-- Average Sales per Transaction
Avg Sale = AVERAGE(Sales[SaleAmount])

-- Count of Transactions
Transaction Count = COUNTROWS(Sales)
```

### Time Intelligence
```dax
-- Year to Date Sales
Sales YTD = TOTALYTD([Total Sales], 'Date'[Date])

-- Month to Date Sales
Sales MTD = TOTALMTD([Total Sales], 'Date'[Date])

-- Same Period Last Year
Sales SPLY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))

-- Year over Year Growth %
YoY Growth % =
DIVIDE(
    [Total Sales] - [Sales SPLY],
    [Sales SPLY],
    0
)
```

### CALCULATE Patterns
```dax
-- % of Total (ignores all filters on Sales table)
% of Total =
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Sales)),
    0
)

-- Activate inactive relationship (e.g. Ship Date)
Sales by Ship Date =
CALCULATE(
    [Total Sales],
    USERELATIONSHIP(Sales[ShipDate], 'Date'[Date])
)
```

### Ranking
```dax
-- Product Sales Rank (1 = highest)
Product Rank =
RANKX(
    ALL(Products[ProductName]),
    [Total Sales],
    ,
    DESC,
    Dense
)
```

---

## 🔄 Power Query M Snippets

### Dynamic File Path Parameter
```m
Source = Excel.Workbook(File.Contents(FilePath), null, true)
```

### Unpivot Month Columns to Rows
```m
= Table.UnpivotOtherColumns(Source, {"ProductID", "ProductName"}, "Month", "Sales")
```

### Replace Errors with Null
```m
= Table.ReplaceErrorValues(Source, {{"Revenue", null}, {"Quantity", null}})
```

### Dynamic Date Filter — Last N Days
```m
StartDate = Date.AddDays(DateTime.Date(DateTime.LocalNow()), -DaysBack),
FilteredRows = Table.SelectRows(Source, each [OrderDate] >= StartDate)
```

---

## 🔒 Row Level Security Patterns

### Dynamic RLS — One role for all users
```dax
-- Security table has: UserEmail | Region columns
-- Role filter on the Security table:
[UserEmail] = USERPRINCIPALNAME()
```

---

## 🏗️ Storage Mode Decision Framework

```
Data < 1GB AND refresh < 8x/day?   →  Import Mode      ✅
Need real-time OR data > 1GB?      →  DirectQuery       ✅
Mix of both needs?                 →  Composite Model   ✅
Enterprise shared model in AAS?    →  Live Connection   ✅
```

---

## 🛠️ Tools & Tech Stack

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Report and model authoring |
| Microsoft Fabric | Lakehouse, Notebooks, Pipelines |
| DAX | Measures and calculations |
| Power Query / M | Data transformation |
| Python / PySpark | Fabric notebook analysis |
| Microsoft Learn | Primary certification study platform |
| Anki | Spaced repetition flashcard review |
| Joplin | Daily study notes and module summaries |

---

## 📅 Learning Journal

### September 17, 2026

**Tracks Active:** Power BI / PL-300 | NJ Real Estate Pre-Licensing | Infrastructure

#### ✅ Completed Today

**Power BI & SQL Server**
- Installed SQL Server Express 2022 + SSMS 22 on local Windows machine
- Configured SSMS connection: `localhost\SQLEXPRESS` with Windows Authentication + Trust Server Certificate
- Restored `AdventureWorksDW2020` database from `.bak` file to SQL Server Backup folder
- Connected Power BI Desktop to local SQL Server
- Explored Power Query Editor: column quality, data distribution, column profiling
- Blended SQL Server + CSV data sources in a single Power BI model

**NJ Real Estate Pre-Licensing (75-Hour Course)**
- ✅ Unit 11 — Complete
- Progress: 47% content | 21h 44min logged | Expiry: Dec 14, 2026

**Infrastructure**
- ✅ Fiber internet installed and live

#### 📊 Overall Progress
| Track | Status |
|---|---|
| Power BI / PL-300 | 🟡 In Progress — Lab Phase |
| NJ Real Estate (75hr) | 🟡 47% Complete — 40h 46min remaining |
| SQL Server Local Setup | ✅ Complete |

---

## 🔷 Microsoft Fabric — 15-Day Trial (Started Sep 17, 2026)

**Fabric trial activated** alongside the Power BI 30-day challenge.  
**Workspace:** `Sastry-Fabric-Portfolio` — trial running, Day 1 complete.

> All Fabric project deep-dives live in a dedicated repo to keep this journey focused:  
> 👉 [github.com/svmalapaka/fabric-portfolio](https://github.com/svmalapaka/fabric-portfolio)


## 🔗 Resources

- [Microsoft Learn — PL-300 Learning Path](https://learn.microsoft.com/en-us/training/paths/get-data-power-bi/)
- [Microsoft Learn — DP-600 Learning Path](https://learn.microsoft.com/en-us/training/paths/get-started-fabric/)
- [DAX Guide](https://dax.guide)
- [SQLBI — DAX Patterns](https://www.daxpatterns.com)
- [Power Query M Reference](https://learn.microsoft.com/en-us/powerquery-m/)
- [Guy in a Cube — YouTube](https://www.youtube.com/@GuyInACube)
