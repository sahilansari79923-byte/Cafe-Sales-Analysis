# Cafe Sales Analysis

Six months of coffee shop transaction data, three NYC locations, 149,116 rows. I built this in Excel — Power Query for cleaning, Power Pivot for the data model, DAX for measures, and a dashboard with slicers on top.

The questions I was trying to answer: when are customers actually showing up, which products are making the money, and do the three stores perform differently or are they basically the same?

---

## Dataset

- 149,116 transactions, Jan–Jun 2023
- Stores: Astoria, Hell's Kitchen, Lower Manhattan
- 45 products across 9 categories
- Raw columns: transaction ID, date, time, quantity, unit price, total price, store ID, store location, product category, product type, product detail, size

---

## Cleaning and transformation (Power Query)

The raw data needed work before it was usable. I did all of this in Power Query Editor:

Removed duplicates first. Then fixed data types — the date and time columns were coming in as text, which would've broken any time-based analysis. Dropped rows with nulls or blanks in the columns that actually matter (transaction ID, price, store location, product detail). Filtered out rows that didn't belong in the analysis scope. Renamed a bunch of columns that had inconsistent or unclear names.

Then built four custom columns from scratch:
- `Month Name` — pulled from the transaction date
- `Day Name` — pulled from the transaction date
- `Hour` — extracted from the transaction time
- `Day of Week` — numeric, so charts sort correctly instead of alphabetically

After all that, loaded into the data model.

---

## What I built in Excel

Loaded 149K rows into Power Pivot and wrote DAX measures for Total Sales and Average Order Value. Built separate pivot tables for each angle of the analysis — by store, by month, by weekday, by hour, by category, by product. Pulled everything into a single dashboard sheet with KPI cards at the top and charts below. Connected two slicers (Month Name and Day Name) so all charts filter together.

Charts used: line chart for hourly trends, clustered bar for store footfall vs revenue, column chart for monthly revenue, pie and donut for category and size distribution.

---

## What the data actually showed

**Total: $698,812 across 149,116 transactions. Average order: $4.69.**

### Stores

| Store | Revenue |
|---|---|
| Hell's Kitchen | $236,511 |
| Astoria | $232,244 |
| Lower Manhattan | $230,057 |

Closer than I expected. Less than $7K separates top and bottom across six months. Either all three are run consistently well, or they're pulling from similar customer volumes.

### Monthly trend

| Month | Revenue |
|---|---|
| June | $166,486 |
| May | $156,728 |
| April | $118,941 |
| March | $98,835 |
| January | $81,678 |
| February | $76,145 |

February to June is basically a straight climb. June is more than double February. No prior year data to compare against, so hard to say if this is seasonal or just growth — but 118% in five months is steep either way.

### Weekdays vs weekends

Monday is the top day ($101,677), Saturday the lowest ($96,894). But the spread across all seven days is only ~$5K. Weekends don't drop the way you'd expect for a coffee shop.

### Peak hours

10 AM — $88,673  
9 AM — $85,170  
8 AM — $82,700  

Everything falls off sharply after 11 AM. Three hours in the morning are doing most of the work. That's where staffing and stock decisions should be focused.

### Products

| Product | Revenue |
|---|---|
| Ethiopia | $42,304 |
| Sustainably Grown Organic | $39,065 |
| Jamaican Coffee River | $38,781 |
| Brazilian | $37,747 |
| Latte | $36,370 |

Four of the top five are whole bean coffee, not prepared drinks. Latte is the only cup in the top 5. The specialty bean category is quietly carrying a lot of revenue.

### Categories

| Category | Revenue |
|---|---|
| Coffee | $269,952 |
| Tea | $196,406 |
| Bakery | $82,316 |
| Drinking Chocolate | $72,416 |
| Coffee beans | $40,085 |
| Branded | $13,607 |
| Loose Tea | $11,214 |
| Flavours | $8,409 |
| Packaged Chocolate | $4,408 |

Coffee is 38.6% of revenue. Tea at 28.1% is a solid second. The bottom four categories combined — Branded, Loose Tea, Flavours, Packaged Chocolate — bring in under $38K total across six months.

### Order sizes

Regular and Large are nearly tied (~45K each). Small is a distant third at 13,924. The 44,518 "not specified" are mostly whole bean and bakery items where size doesn't apply — not a data quality issue, just how those products are sold.

---

## Things worth digging into further

The 8–10 AM window generates roughly $256K of the $698K total. Three hours out of the full operating day. If supply runs short or staffing is thin during that window, the revenue impact is immediate.

The bottom categories are still on the menu, which probably means they're either high-margin or kept for variety. Without cost data it's hard to say if they're worth the current stock levels.

The monthly growth curve is steep enough that H2 data would tell a more complete story — whether June holds, dips, or keeps climbing.

---

## File structure

```
Cafe_Sales_analysis.xlsx
├── Transactions    - raw data, 149,116 rows
├── pivot table     - all pivot tables + DAX measures
└── Sheet4          - dashboard
```

---

