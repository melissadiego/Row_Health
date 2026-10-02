# Row Health: Marketing Campaign Impact & Data Pipeline Analysis

## Overview
This repository contains the end-to-end data auditing pipeline, standardized cleaning architecture, and executive dashboard analysis for **Row Health** (`Row_Health_Data.xlsx`). 

Designed for Quarterly Business Reviews (QBRs), this analysis tracks customer acquisition, medical claims exposure, and marketing channel efficiency across campaign categories launched since 2019.

---

## Executive Summary & Key Findings

<img width="1448" height="306" alt="image" src="https://github.com/user-attachments/assets/956dcb4e-a0cd-4b98-98b7-d774a200b87c" />


### 1. Strategic Context & Channel Efficiency
* **Top Efficiency Driver:** `#CoverageMatters` demonstrated the lowest Cost-Per-Click ($0.03) and drove 3,536 total signups, representing our most cost-effective acquisition engine.
* **High Engagement Anchor:** `Health For All` achieved an outstanding 36.06% Click-Through Rate (CTR) while keeping spend low ($2,031.22).

### 2. Ad Spend Inefficiency & Budget Realignment
* **Spend Inefficiency (`#HealthyLiving`):** Represents our highest overall spend channel ($4,662.29), yet produces only average claim volume ($2.61M) and yields a sub-10% CTR (9.66%). A creative refresh or budget re-allocation is recommended.
* **Underperforming Campaign (`Tailored Health Plans`):** Yielded the lowest signup volume (1,107), lowest CTR (6.66%), and lowest total claims relative to cost despite moderate spend. Flagged for budget restructuring.

### 3. Claims Exposure & Risk Anomalies
* **Utilization Spike (`Compare Health Coverage`):** Generated the highest total claim liability ($3,902,044.66). Trend lines highlight a severe exposure surge between 2021 and 2022, pointing to a cohort of higher-utilization policyholders acquired during that campaign phase.

---

## Marketing Campaign Performance & Visual Analytics

<img width="1467" height="725" alt="image" src="https://github.com/user-attachments/assets/7faa362a-8be0-4bf4-8b87-6bbb16a744a9" />

### Cost vs. Claims Quadrant Analysis
* **Quadrant Matrix Overview:** The **Cost vs. Claims by Category** 4-quadrant plot evaluates acquisition spend against downstream claim liabilities, split by average cost and average claim reference lines.
* **High Spend / Average Yield Outlier (`#HealthyLiving`):** Positioned far right on the cost axis with $4,662.29 in total spend, but sitting directly on the horizontal average line for total claims. Paired with its low 9.66% CTR, this channel demonstrates low efficiency relative to capital invested.
* **High Liability Outlier (`Compare Health Coverage`):** Positioned in the upper-right quadrant, generating $3,902,044.66 in total claims against $3,976.40 in spend. This high exposure ratio highlights a customer cohort with significantly elevated healthcare utilization.
* **Low Volume Underperformer (`Tailored Health Plans`):** Positioned near the bottom center with the lowest total claim liability ($489,873.68) and lowest CTR (6.66%), underperforming across both acquisition and conversion metrics.

---

## Time-Series Trend Breakdown (2019 – 2023)


<img width="1487" height="652" alt="image" src="https://github.com/user-attachments/assets/8bd5666d-538d-421b-8270-7e0a54167aa4" />

### Claims Trend Analysis
* **`Compare Health Coverage` Drove Unprecedented Claims Liability Surge (2021–2022):** After maintaining low monthly claims through 2019–2020 (under $25,000/month), this channel experienced an unprecedented spike starting in early 2021, peaking at over $170,000 per month in mid-2022.
* **Baseline Stability Across Core Channels:** Channels like `#CoverageMatters`, `Health For All`, and `#HealthyLiving` exhibited steady monthly claim growth ranging between $40,000 and $75,000 per month, demonstrating predictable risk profiles.
* **Low Liability (`Tailored Health Plans`):** Maintained minimal claim impact across the entire 4-year lifecycle, rarely exceeding $15,000 in monthly claims.

### Signup Trends Analysis
* **Early Acquisition Volume Shifted from `#CoverageMatters` to `Compare Health Coverage`:** Following campaign launches in 2019, `#CoverageMatters` and `#HealthyLiving` saw a massive volume spike in early 2020, reaching peak acquisition rates of 160+ signups per month.
* **Cohort Shift to `Compare Health Coverage` (2021–2022):** As early 2020 channels began to taper, `Compare Health Coverage` surged to become the dominant acquisition driver throughout 2021 and 2022, averaging 80 to 120 signups monthly.
* **Lagging Acquisition (`Tailored Health Plans`):** Consistently generated the lowest monthly user additions, peaking briefly at only 60 signups during late 2021.

---

## Data Architecture & Audit Trail (`Modification_History`)

To preserve strict data lineage, raw baseline sheets are maintained alongside clean operational tabs (`_clean`). All modifications are tracked in `Modification_History`:

| Step | Analyst | Data / Column | Action Taken | Logic / Business Reason | # Rows | Before vs. After Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **LOG-01** | M. DIEGO | `customers_clean`, `claims_clean`, `campaigns_clean` | Frozen top row; header font 14pt bold | Establishes executive visual hierarchy across sheets | 3 tabs | `cost` &rarr; **`cost`** |
| **LOG-02** | M. DIEGO | `campaigns_clean / clicks` | Cast decimals to whole numbers | Clicks are discrete user interaction events | 58 | `1348.5` &rarr; `1,348` |
| **LOG-03** | M. DIEGO | `claims_clean / claim_amount, covered_amount` | Standardized to currency (`$#,##0.00`) | Standardizes accounting precision for claims financial modeling | 38 | `$126.0` &rarr; `$126.00` |
| **LOG-04** | M. DIEGO | `campaigns_clean / Rows 59–1000` | Removed trailing unused blank grid cells | Optimizes spreadsheet performance and reduces file overhead | 942 | Blank Grid &rarr; Truncated Table |
| **LOG-05** | M. DIEGO | `campaigns_clean / cost` | Formatted float strings to currency (`$#,##0.00`) | Ensures uniform financial reporting across spend metrics | 58 | `846.05` &rarr; `$846.05` |
| **LOG-06** | M. DIEGO | `campaigns_clean / impressions` | Formatted with standard thousands separators | Improves executive readability for high-volume marketing metrics | 58 | `32272` &rarr; `32,272` |
| **LOG-07** | M. DIEGO | `campaigns_clean / clicks` | Imputed blank entries with `0` | Unrecorded metric events indicate zero active engagement | 3 | `[BLANK]` &rarr; `0` |
| **LOG-08** | M. DIEGO | `customers_clean / campaign_id` | Standardized `unknown` & blanks to `Direct` | Ensures explicit attribution for organic/direct traffic cohorts | 38 | `unknown` / `[BLANK]` &rarr; `Direct` |

---

## Technical Transformation Summary

1. **Attribution Categorization (`customers_clean`):** Replaced untracked campaign labels (`[BLANK]`, `unknown`) with `"Direct"` to prevent null-handling failures in downstream SQL/Tableau aggregations.
2. **Financial Precision (`claims_clean`):** Applied strict `$#,##0.00` currency formatting to guarantee accounting consistency across all claim entries.
3. **Metric Integrity (`campaigns_clean`):** Standardized clicks to whole integers, imputed missing metric cells with zero, and purged 900+ empty grid rows to streamline workbook processing.

---
## 📊 Interactive Tableau Dashboard

Access the live interactive dashboard on Tableau Public:
👉 **[View Live Tableau Dashboard](https://public.tableau.com/app/profile/melissa.diego7336/viz/rowhealth_analysis/Dashboard1)**

---

## Data

<img width="822" height="570" alt="image" src="https://github.com/user-attachments/assets/665272f5-789c-4903-8cee-bac19ca0b798" />


---
## Repository Structure

```text
├── README.md                      # Primary documentation, Executive Summary, & Audit Trail
├── Row_Health_Data_Clean.xlsx      # Cleaned Excel workbook containing raw & clean tabs
└── docs/
    └── Executive_Dashboard.png     # QBR Tableau Dashboard Overview



