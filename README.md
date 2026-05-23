# Retail Allocation Analysis — Inverse Weeks of Supply Method

## Overview

This project simulates a real-world retail inventory allocation decision across 6 store locations and 3 SKUs over an 8-week period. Built entirely in Excel, it demonstrates the end-to-end allocation workflow used by planning and allocation analysts in retail and supply chain environments.

-----

## Business Problem

A warehouse has incoming shipments to distribute across 6 Ontario stores. Some stores are critically low on stock. Some are already well supplied. The goal is to allocate available units where they are most needed — preventing stockouts at high-velocity stores while avoiding over-allocation to stores that are already healthy.

-----

## Methodology

### Step 1 — Sales History Analysis

8 weeks of weekly sales data across 6 stores and 3 SKUs with seasonal variation built in. Weeks 4 and 5 reflect mid-quarter demand peaks. Store velocity varies — Toronto is the highest volume store, Scarborough the lowest.

### Step 2 — Inventory Health Assessment

Current inventory levels assessed against weeks of supply thresholds:

|Status  |Threshold    |Meaning          |
|--------|-------------|-----------------|
|Critical|Below 1 week |Stockout imminent|
|Low     |Below 2 weeks|At reorder point |
|Healthy |Above 3 weeks|No action needed |

Reorder points and safety stock calculated using:

- Supplier lead time: 2 weeks
- Safety stock buffer: 1 week
- Reorder trigger: 3 weeks of supply

### Step 3 — Allocation Calculator — Inverse WOS Method

Stores ranked by urgency using inverse weeks of supply. Stores with less supply get a higher urgency score and a larger share of available units.

**Three refinements applied:**

1. Stores above the healthy WOS threshold (3 weeks) are excluded from allocation entirely
1. Each store’s allocation is capped at the units needed to reach exactly 3 weeks of supply
1. Leftover units after capping are redistributed equally among stores that received allocation

**Allocation formula:**

```
Inverse WOS = 1 ÷ Weeks of Supply
% Share = Store Inverse WOS ÷ SUM(eligible stores Inverse WOS)
Recommended Units = MIN(Units Needed to reach 3 WOS, % Share × Available Units)
```

### Step 4 — Supply Gap Analysis

Stores still insufficient after allocation are flagged with the exact units needed in the next purchase order recommendation.

### Step 5 — Sell-Through Analysis

Weekly sell-through percentages calculated by store and SKU against opening stock. Opening stock intentionally misaligned to show realistic variation — some stores under-bought, some over-bought.

-----

## Key Findings

- **Toronto (Store 1)** was critically low across all three SKUs with less than 0.1 weeks of supply — received the highest allocation priority
- **Scarborough (Store 6)** was already at healthy WOS levels and received zero allocation
- Incoming shipments were sufficient to bring all needy stores to approximately **3.0 weeks of supply** after cap and redistribute logic was applied
- Sell-through analysis revealed Toronto was **under-bought** at the start of the quarter while Mississauga and Scarborough were **over-bought** — suggesting a rebalancing of the opening buy for the next quarter

-----

## Tools Used

- Microsoft Excel — SUMIFS, COUNTIF, IFERROR, MIN, MAX, conditional formatting
- Power Query — data transformation
- GitHub — version control and portfolio hosting

-----

## Sheets

|Sheet                    |Description                                                                                    |
|-------------------------|-----------------------------------------------------------------------------------------------|
|Assumptions              |All input parameters — lead time, safety stock, WOS thresholds, incoming shipment quantities   |
|Sales History            |8 weeks of weekly sales by store and SKU with totals and averages                              |
|Inventory & Replenishment|Current inventory, weeks of supply, reorder points, safety stock, status flags                 |
|Allocation Calculator    |Inverse WOS weighting, cap and redistribute logic, supply gap flags, next order recommendations|
|Sell-Through Analysis    |Weekly sell-through % by store and SKU against opening stock                                   |

-----

## Files

- `Retail_Allocation_Analysis.xlsx` — full Excel workbook with all 5 sheets

-----

## Author

**Vwede Okojie**
[github.com/VwedeOkojie](https://github.com/VwedeOkojie)