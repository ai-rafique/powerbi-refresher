# powerbi-refresher

A self-paced Power BI learning project built on the **Contoso** dataset — a realistic, multi-table fictional retail company used by Microsoft for BI demos.

The project is structured in phases. Each phase builds on the last, progressively adding complexity to the data model, DAX layer, and report canvas.

---

## Dataset

Source: [Contoso (cleaned CSVs)](https://www.kaggle.com/datasets/bhanuthakurr/cleaned-contoso-dataset) — 25 tables covering sales, inventory, HR, IT ops, and financial planning.

All raw files live in `/data`.

---

## Phase 1 — Star schema + core sales model

**Goal:** Build a clean, well-structured data model from scratch and write foundational DAX measures.

**Tables in scope:**

| Type | Table | Purpose |
|------|-------|---------|
| Fact | `FactSales` | In-store transactions |
| Fact | `FactOnlineSales` | Ecommerce transactions |
| Fact | `FactSalesQuota` | Sales targets (budget vs actuals) |
| Fact | `FactExchangeRate` | Multi-currency bridge |
| Dim | `DimDate` | Time intelligence backbone |
| Dim | `DimProduct` | Product details |
| Dim | `DimProductCategory` | Top-level product grouping |
| Dim | `DimProductSubcategory` | Mid-level product grouping |
| Dim | `DimCustomer` | Customer profiles |
| Dim | `DimGeography` | Country, city, region |
| Dim | `DimStore` | Store locations |
| Dim | `DimSalesTerritory` | Sales regions |
| Dim | `DimChannel` | Store vs online vs reseller |
| Dim | `DimCurrency` | Currency codes |
| Dim | `DimPromotion` | Discounts and campaigns |
| Dim | `DimEmployee` | Salespeople |

**Power Query steps:**
- Load all CSVs, fix data types, remove nulls
- Append `FactSales` + `FactOnlineSales` into a single unified `Fact_Sales` table
- Merge `DimProductCategory` → `DimProductSubcategory` → `DimProduct` into one flat `Dim_Product`
- Mark `DimDate` as the Date Table

**Data model:**
- Star schema — all relationships one-to-many from Dim → Fact
- Hide all foreign key columns from report view

**DAX layer (base measures):**
- `Revenue`, `Units Sold`, `COGS`, `Gross Margin`, `Gross Margin %`
- `PY Revenue`, `YoY Growth %`, `Revenue YTD`
- `Quota Attainment %`

**Deliverable:** `phase1.pbix`

---
