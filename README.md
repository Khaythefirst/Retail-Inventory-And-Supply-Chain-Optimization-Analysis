# Retail Inventory & Supply Chain Optimization Analysis

> **Tool:** Google Spreadsheet (Pivot Tables, Charts, Formulas)
> 
> **Dataset:** 73,100 rows · 18 columns (15 original + 3 engineered)
> 
> **Source:** [Kaggle: Retail Store Inventory Forecasting Dataset](https://www.kaggle.com/datasets/anirudhchauhan/retail-store-inventory-forecasting-dataset)

---

## Links

| | |
|---|---|
| Full Project (Google Sheets) | [View Here](https://docs.google.com/spreadsheets/d/1v7W445TIZtJWWsrbyfztTBqpNGzUeaUdcH9KupQbxbI/edit?usp=sharing) |
| Data Cleaning Process | [Data Cleaning Process.docx](https://github.com/kpepime/Retail-Inventory-And-Supply-Chain-Optimization-Analysis/blob/main/Data%20Cleaning%20Process.docx) |

---

## Project Overview

A retail business carrying 73,000+ inventory records across four regions needed to understand why its stock levels, demand forecasts, and promotional strategy weren't translating into optimised performance. This project analyses the full supply chain, from inventory levels and demand forecasting to weather conditions, promotions, and competitor pricing, to identify where the gaps are and what to do about them.

Four business impact areas are investigated:

- **Forecast Accuracy**: Is the demand forecast reliable, or is it consistently off in one direction?
- **Weather Impact**: Does weather meaningfully affect sales volume, and should it drive inventory decisions?
- **Holiday/Promotion Effectiveness**: Are discounts and promotions actually driving incremental sales?
- **Regional Inventory Distribution**: Is inventory being allocated equitably and efficiently across regions?

---

## Data Structure

### Original Columns (15)

| Column | Type | Description |
|---|---|---|
| `Date` | Date | Transaction date |
| `Store_ID` | Text | Store identifier |
| `Product_ID` | Text | Product identifier |
| `Category` | Text | Product category |
| `Region` | Text | Geographic region (North/South/East/West) |
| `Inventory_Level` | Numeric | Units currently in stock |
| `Unit_Sold` | Numeric | Actual units sold |
| `Units_Ordered` | Numeric | Units ordered for replenishment |
| `Demand_Forecast` | Numeric | System-generated demand prediction |
| `Price` | Numeric | Selling price (USD) |
| `Discount` | Numeric | Discount percentage applied |
| `Weather_Condition` | Text | Sunny/Cloudy/Rainy/Snowy |
| `Holiday/Promotion` | Text | Yes/No whether a promotion was active |
| `Competitor_Pricing` | Numeric | Competitor's price for the same product |
| `Seasonality` | Text | Season label (Summer/Autumn/Winter/Spring) |

### Engineered Columns (3)

| Column | Formula | Purpose |
|---|---|---|
| `Stock_Gap` | `Inventory_Level - Demand_Forecast` | Measures the difference between available stock and forecasted demand. Negative values indicate potential stockout risk. |
| `Stockout_Risk` | Conditional flag based on `Stock_Gap` | Classifies each record as `Safe`, `At Risk`, or `Critical` based on how far inventory falls below forecast |
| `Price_Difference` | `Price - Competitor_Pricing` | Identifies whether the store is priced above or below competitors for each product |

> These three columns were added after cleaning and are not present in the original Kaggle dataset. They form the basis for the stockout risk and pricing analyses.

---

## Data Cleaning Summary

Full cleaning documentation: [Data Cleaning Process.docx](https://github.com/kpepime/Retail-Inventory-And-Supply-Chain-Optimization-Analysis/blob/main/Data%20Cleaning%20Process.docx)

- Checked all 73,100 rows for duplicates, none found
- Checked all columns for null or blank values, none found
- Standardised all column names and categorical text values for consistency
- Validated numeric ranges (prices, inventory levels, discount percentages) for anomalies
- Added `Stock_Gap`, `Stockout_Risk`, and `Price_Difference` columns after validation

---

## Key Findings

### 1. Forecast Accuracy: The System Consistently Over-Forecasts

The demand forecast is not wildly inaccurate, there is a strong, steady correlation between forecast and actuals. However, the forecast is **consistently higher than reality** across all categories and regions. This means the store is routinely ordering and holding more safety stock than demand justifies.

**Business impact:** Excess inventory ties up cash flow in stock that moves slower than expected. This is a systematic bias in the forecasting model, not a random error, which means it can be corrected.

**What to investigate:** Whether the forecast model is calibrated against older, higher-demand periods that no longer reflect current buying patterns.

---

### 2. Weather Impact: This Store Is Weather-Resilient

Across all weather conditions, Sunny, Cloudy, Rainy, and Snowy, sales volumes remain consistent. Unlike many retail datasets where adverse weather suppresses demand, this store shows no meaningful drop in units sold during rain or snow.

**Business impact:** Weather should **not** be used as a trigger for inventory adjustments or supply chain decisions at this store. Building weather-based safety stock buffers would add cost without reducing stockout risk.

**What this signals:** The store likely operates in product categories (or serves customers) where purchasing behaviour is not weather-driven, purchases are planned rather than impulse-driven.

---

### 3. Holiday/Promotion Effectiveness: Promotions Are Not Driving Incremental Sales

This is the most commercially significant finding. When promotions are active (`Holiday/Promotion = Yes`), total units sold are **not higher** than periods without promotions. The discount is being absorbed without generating the additional volume needed to justify it.

**Business impact:** The store is reducing its margin on promoted products without expanding its customer base or basket size. Effectively, it is discounting to its existing customers rather than acquiring new ones or accelerating purchases.

**What to do:** Redesign the promotion strategy. Options include switching from blanket percentage discounts to bundle offers, limited-time SKU promotions, or category-specific campaigns where price elasticity is higher.

---

### 4. Regional Inventory Distribution: Perfectly Balanced

Inventory is distributed almost exactly 25% per region across North, South, East, and West. No region is being over- or under-served.

**Business impact:** Distribution logistics are operating efficiently. This rules out regional supply imbalance as a cause of any stockout risk, if stockouts are occurring, they are driven by forecasting or demand variability, not by uneven allocation.

**What this signals:** The business uses a centralised, formula-driven distribution model. This is operationally clean but may not account for regional demand differences, a region with higher sales velocity may need a slightly larger share even if distribution is currently equal.

---

## Recommendations

**1. Recalibrate the demand forecast model downward**
The consistent over-forecasting bias suggests the model is anchored to historical demand that is higher than current actuals. A rolling 90-day recalibration, weighting recent periods more heavily, would reduce excess safety stock and free up working capital without increasing stockout risk.

**2. Remove weather as a supply chain variable**
Since weather has no measurable effect on sales at this store, any weather-adjusted ordering rules should be removed. They add process complexity without improving outcomes.

**3. Audit the promotion strategy before the next campaign**
Before running another discount promotion, identify whether past promotions attracted net-new customers or simply moved the same customers' purchases forward in time. If it's the latter, the current discount model is a margin drain with no growth upside.

**4. Test demand-weighted regional allocation**
The perfectly equal 25/25/25/25 split is operationally elegant but may be leaving performance on the table. If one region consistently sells faster (higher `Unit_Sold` relative to `Inventory_Level`), it should receive a proportionally larger allocation to reduce its stockout risk before it becomes critical.

**5. Monitor `Stockout_Risk = Critical` records proactively**
The engineered `Stockout_Risk` column identifies records where `Stock_Gap` falls into critical territory. These should be reviewed weekly, not after a stockout occurs, to trigger early reorder before inventory is depleted.

---

## Repository Structure

```
Retail-Inventory-And-Supply-Chain-Optimization-Analysis/
├── images/ # Charts and visualisation screenshots
├── Data Cleaning Process.docx # Step-by-step cleaning documentation
└── README.md
```

---

## Tools & Methods

- **Microsoft Excel**: data cleaning, validation, pivot table analysis, charting
- **Engineered Metrics**: `Stock_Gap`, `Stockout_Risk`, `Price_Difference` derived via Excel formulas
- **Analysis techniques**: pivot table aggregation, conditional classification, comparative segmentation by region, weather, season, and promotion status
