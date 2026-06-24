# Cleaning Log

**Name:** Ansh Singh  
**ID:** 2511922  

---

## Issues I Found

### Text Fields
- customer_name had extra spaces in between like "Vikram  Iyer"
- region had mixed case like "NORTH", "north", "North" all in same column
- ship_mode also had inconsistent spacing and casing
- some fields had trailing spaces which i didnt even notice at first

### Date Problems
honestly this was the most frustrating part. found like 7 different formats:
- DD Mon YYYY (like 21 Jul 2024)
- MM/DD/YYYY
- DD-MM-YYYY
- YYYY-MM-DD
all mixed in the same column. some were not even valid dates.

also found some records where ship date was earlier than order date which doesnt make sense

### Missing Values
- region was missing in 26 rows
- ship_mode missing in 22 rows
- discount missing in 18 rows

### Discount Issues
- some discounts were negative (clearly wrong)
- one had "70%" written instead of 0.70
- a few were above 90% which seems too high

### Duplicates
- found 63 order ids that had same id but different data in other columns
- this was confusing because i didnt know which one to keep

### Sales Mismatch
- in some rows the sales value didnt match what you get when you calculate quantity x price x discount
- about 45 rows had this problem

---

## What I Did to Fix Things

### Text Cleaning
- used strip() to remove spaces from start and end
- used regex to fix extra spaces in middle
- made everything title case for consistency

### Dates
- wrote a function that tries multiple formats one by one
- if none worked i left it as blank and flagged it
- made shipping_delay_days by subtracting order date from ship date

### Missing Values
- region → filled as "Unknown"
- ship_mode → filled as "Unknown"
- discount → set to 0 if quantity, price, sales, cost were all there

### Discounts
- converted "70%" type values to 0.70
- negative discounts → flagged as invalid
- discounts above 0.9 → flagged as invalid
- did not change them because i wasnt sure what the real value should be

### Duplicates
- exact duplicates → removed, kept first one
- conflicting duplicates → flagged them, did not delete
- reason: if i delete them i might remove correct data

---

## Business Rules

| Rule | What I did |
|------|-----------|
| missing region | filled Unknown, added to report |
| missing ship_mode | filled Unknown, added to report |
| missing discount | set 0 if other fields ok |
| negative discount | flagged invalid |
| discount above 90% | flagged invalid |
| cancelled orders | not included in sales summary |
| failed payment | not included in sales summary |
| refunded orders | shown in separate sheet |
| ship before order date | flagged invalid |

---

## New Columns I Added

- cleaned_discount - fixed version of discount
- calculated_sales - quantity x price x (1 - discount)
- calculated_profit - sales minus cost
- profit_margin - profit divided by sales
- shipping_delay_days - difference in dates
- order_month - month number from order date
- order_year - year from order date
- data_quality_flag - Clean, Warning or Invalid
- duplicate_flag - shows if record is a flagged duplicate
- sales_mismatch - True if calculated sales doesnt match raw sales

---

## Final Numbers

- started with 932 rows
- removed 0 exact duplicates
- flagged 63 conflicting duplicates
- 760 clean records
- 134 warning records
- 38 invalid records

---

## Limitations

- i couldnt fix conflicting duplicates because i dont know which version is right
- some dates might be wrong because DD/MM and MM/DD look the same sometimes
- negative discounts are flagged but not corrected
- no master product list to verify product names

---

*Ansh Singh - 2511922*
