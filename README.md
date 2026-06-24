# Part 1 - Data Cleaning and Excel Reporting

**Name:** Ansh Singh
**Student ID:** 2511922
**Assignment:** Business Data Cleaning, Validation and Excel Reporting

---

## What is this about

So basically our company had sales data exported from different systems and it was really messy. there were spelling issues, wrong dates, missing values and some duplicate rows too. my job was to clean all of that and make proper reports out of it.

---

## About the Dataset

the file is raw_orders.xlsx. it has 932 rows of order data. columns include things like order id, customer name, region, category, discount, sales, profit etc.

main problems i found in the raw data:
- dates were in like 7 different formats which was annoying
- some region and ship mode values were missing
- discount column had negative values and also some had % sign instead of decimal
- customer names had extra spaces
- some order ids were duplicated but with different info

---

## Tools I Used

- Python (pandas, openpyxl)
- Excel
- Git and GitHub

---

## Folder Structure

```
part1_data_cleaning/
├── data/
│   ├── raw_orders.xlsx
│   └── cleaned_orders.xlsx
├── outputs/
│   ├── data_quality_report.xlsx
│   ├── pivot_summary.xlsx
│   └── cleaning_log.md
├── screenshots/
│   ├── raw_data_preview.png
│   ├── cleaned_data_preview.png
│   ├── pivot_summary_1.png
│   └── pivot_summary_2.png
└── README.md
```

---

## What I Did Step by Step

**Step 1 - kept raw file unchanged**
i didnt touch raw_orders.xlsx at all. made a copy and did all cleaning on cleaned_orders.xlsx

**Step 2 - cleaned text columns**
removed extra spaces from customer name, region, city, state etc. also fixed the casing like some had UPPERCASE some had lowercase so made everything consistent

**Step 3 - fixed dates**
this was the hardest part honestly. there were so many formats like DD-MM-YYYY and MM/DD/YYYY and DD Mon YYYY all mixed together. wrote a parser to handle all of them. also made a new column called shipping_delay_days

**Step 4 - handled duplicates**
found 63 order ids that appeared more than once with different data. i flagged them instead of deleting because i wasnt sure which one was correct

**Step 5 - fixed discounts**
some were negative, some were above 90%, one had % sign. fixed the % ones and flagged the invalid ones

**Step 6 - added new columns**
added calculated_sales, calculated_profit, profit_margin, order_month, order_year and data_quality_flag

---

## Business Rules I Applied

- if region was missing i put Unknown
- if ship_mode was missing i put Unknown  
- if discount was missing and other fields were fine i set it to 0
- cancelled and failed payment orders are not in the sales summary
- refunded orders are shown separately

---

## Data Quality Summary

| thing | count |
|-------|-------|
| total records | 932 |
| clean records | 760 |
| warning records | 134 |
| invalid records | 38 |
| missing region (filled) | 26 |
| missing ship mode (filled) | 22 |
| conflicting duplicates flagged | 63 |

---

## Pivot Reports Summary

made 7 pivot sheets in pivot_summary.xlsx:
- sales and profit by region
- sales by category and sub category
- orders by ship mode
- profit margin by segment
- cancelled and failed orders by region
- monthly sales trend
- refunded orders summary

---

## What I Found Interesting

- west region had the highest sales
- technology category made the most money
- standard class shipping is used the most
- there were quite a lot of duplicate order ids which seems like a system problem
- some orders had ship date before order date which makes no sense

---

## Screenshots

all 4 screenshots are in the screenshots folder. they show raw data, cleaned data and the pivot summaries.

---

## Assumptions I Made

- max discount allowed is 90%, anything above that i flagged
- missing discounts = 0 if rest of the data was fine
- only completed + paid orders are used for sales reports
- dates followed indian format where it was unclear

---

*submitted by Ansh Singh - 2511922*
