# Prompt 1 — General ("baseline")

**Purpose:** deliberately minimal/general prompt, used to observe each tool's default
behavior — what it decides to do on its own, what it asks about, and how it presents results.

**Dataset:** `sales_dataset.csv`

---

## Prompt

```
I have a sales dataset called sales_dataset.csv. Can you take a look and give me some insights?
```

---

## What to observe when running this prompt in each tool

- Did it clean the data at all, or analyze it as-is?
- What did it decide "insights" means (metrics, breakdowns, charts)?
- Did it ask clarifying questions before starting, or just proceed?
- What format did it return results in (text, table, file, chart)?
- Did it notice and mention data quality issues on its own?
