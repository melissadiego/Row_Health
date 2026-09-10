# Row_Health_Data Audit & Change Log

**Live Data File:** https://docs.google.com/spreadsheets/d/1jbrJ43WiTR5jnm25LLGGvk8wR355UNhx/edit?usp=sharing&ouid=109618376264638907243&rtpof=true&sd=true

Step | Analyst | Data / Column | Action Taken | Logic / Reason | # Affected Rows | Before vs. After Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **LOG-01** | M.DIEGO | `customers_clean`, `claims_clean`, `campaigns_clean` | Freeze row 1, increase font size to 14, bold | Enhanced header contrast and table navigation | 3 tabs | `cost` &rarr; **`cost`** |
| **LOG-02** | M.DIEGO | `campaigns_clean / clicks` | Removed decimal points to whole numbers | Clicks represent discrete user actions and must be integers | 58 | `1348.5` &rarr; `1,348` |
| **LOG-03** | M.DIEGO | `claims_clean / claim_amount, covered_amount` | Changed text to currency format (`$#,##0.00`) | Standardized monetary format across all claim records | 38 | `126` &rarr; `$126.00` |
| **LOG-04** | M.DIEGO | `campaigns_clean / Rows 59–1000` | Deleted blank rows and empty grid columns | Optimized spreadsheet performance, load speed, and file size | 942 | Blank Grid &rarr; Truncated Table |
| **LOG-05** | M.DIEGO | `campaigns_clean / cost` | Formatted numeric values as currency (`$#,##0.00`) | Standardized spend metrics for financial reporting | 58 | `846.05` &rarr; `$846.05` |
| **LOG-06** | M.DIEGO | `campaigns_clean / impressions` | Formatted numbers with thousands separators | Enhanced numerical readability for high-volume metrics | 58 | `32272` &rarr; `32,272` |
| **LOG-07** | M.DIEGO | `campaigns_clean / clicks` | Imputed blank cells with `0` | Missing performance metrics represent zero click activity | 3 | `[BLANK]` &rarr; `0` |
| **LOG-08** | M.DIEGO | `customers_clean / campaign_id` | Standardized `unknown` & blanks to `Direct` | Ensures explicit attribution grouping for direct/organic users | 38 | `unknown` / `[BLANK]` &rarr; `Direct` |

