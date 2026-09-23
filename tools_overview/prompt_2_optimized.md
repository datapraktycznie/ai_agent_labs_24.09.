# Prompt 2 — Optimized (best-practice prompt engineering)

**Purpose:** structured, unambiguous prompt with explicit steps, criteria, and output format —
used to test whether good prompt engineering reduces the differences between tools observed
with Prompt 1.

**Dataset:** `sales_dataset.csv`

---

## Prompt

```
You are working with sales_dataset.csv — a raw sales export with data quality issues.

TASK — complete these steps in order:

1. Data audit
   - Inspect the file and report: number of rows/columns, duplicate transaction_id values,
     missing values per column, and inconsistent formats you detect (dates, prices/currency,
     text casing, country names, payment method labels, order status labels).

2. Data cleaning
   - Remove exact and near-duplicate transactions (same transaction_id, or same customer_id +
     product_id + date + amount).
   - Standardize all dates to YYYY-MM-DD.
   - Standardize all monetary values (unit_price, shipping_cost, total_amount) to a single
     numeric format with "." as decimal separator, no currency symbols or thousands separators.
   - Standardize categorical text fields (country, payment_method, order_status) to one
     consistent value per category.
   - Flag rows with clearly invalid values (e.g. negative prices, quantity > 1000) instead of
     silently deleting them — put them in a separate "flagged_for_review" output.
   - Do not drop rows solely because of missing customer_rating or notes — these are expected
     to be empty.

3. Analysis
   - Calculate monthly net revenue (after discount, excluding flagged rows) broken down by
     product category.
   - Identify the top 3 categories by revenue and the month-over-month revenue trend.
   - Calculate the return rate (return_flag) per category.

4. Output
   - Save the cleaned dataset as cleaned_sales_data.csv.
   - Save the flagged/invalid rows as flagged_for_review.csv.
   - Save the monthly revenue-by-category summary as revenue_summary.csv.
   - Present the top 3 categories and return rates as a short table in your final message.

5. Explanation
   - At the end, list every judgment call you made (e.g. what counted as a duplicate, how you
     handled ambiguous date formats) in 5 bullet points or fewer, so I can verify your reasoning.

Work through the steps yourself without asking me clarifying questions; if something is
genuinely ambiguous, state your assumption explicitly in step 5 instead of pausing to ask.
```

---

## Why this prompt follows best practices

- **Role + context up front** — states what the file is and its nature (raw, dirty export).
- **Numbered, ordered steps** — the model knows exactly what to do and in what sequence.
- **Unambiguous criteria** — "duplicate" is defined concretely, not left to interpretation.
- **Explicit output format** — file names and table structure specified, enabling a clean
  1:1 comparison across tools.
- **"Flag, don't drop" instruction** for edge cases — tests whether the tool actually respects
  constraints or "simplifies" the task instead.
- **Requires justification of decisions** at the end — feeds directly into the training
  discussion on where agents go wrong and how to verify them.
- **Explicit "don't ask, state assumptions" instruction** — removes the variable of "Tool A
  asked, Tool B didn't," keeping the comparison cleaner.
