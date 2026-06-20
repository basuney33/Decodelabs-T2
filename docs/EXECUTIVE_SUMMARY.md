# Executive Summary — Project 2: Exploratory Data Analysis (EDA)

**Dataset:** `cleaned_dataset.csv` (1,200 verified e-commerce orders, output of Project 1)
**Prepared by:** Data Analyst Intern, DecodeLabs (Batch 2026)
**Methodology framework:** IPO (Input → Process → Output) — *"The analyst's objective is to uncover the underlying 'pulse' of the evidence before any predictive modeling or amplification through visualization occurs."*

---

## 1. Problem Statement

What is the underlying pattern of customer ordering behavior in this dataset, and where are the signals — in pricing, order volume, product mix, and fulfillment outcomes — that should inform business decisions before any dashboard or predictive model is built?

## 2. Methodology

1. **Distribution analysis (univariate):** measured skewness for all four numeric variables (`Quantity`, `UnitPrice`, `ItemsInCart`, `TotalPrice`) to determine whether mean or median best represents the "center of gravity" of each.
2. **Five-number summary:** computed minimum, Q1, median, Q3, and maximum for every numeric variable.
3. **Outlier detection:** applied both the **IQR method** (`< Q1 - 1.5×IQR` or `> Q3 + 1.5×IQR`) and the **Z-score method** (`|Z| > 3`), then forensically investigated flagged records to classify them as noise (errors) or signal (real, high-value behavior).
4. **Correlation analysis:** computed the Pearson correlation coefficient (r) across all numeric variable pairs, explicitly applying the Correlation ≠ Causation rule.
5. **Trend analysis:** aggregated revenue and order counts by month, product, payment method, referral source, and order status.
6. **The "So What?" Test:** translated every statistical finding into a plain-language business diagnosis.

## 3. Key Findings

| # | What the Data Says | The Business Diagnosis |
|---|---|---|
| 1 | `TotalPrice` is right-skewed (skew = 0.89); mean ($1,054) sits 28.0% above the median ($824) | A handful of large bulk orders inflate the "average sale" figure. Use the **median** ($824), not the mean, when setting realistic sales targets or typical-customer benchmarks |
| 2 | 8 orders flagged as statistical outliers in `TotalPrice` by the IQR method (all above $3,330) | Investigated and confirmed as **signal, not noise** — every flagged order reconciles exactly with `Quantity × UnitPrice` and occurs at the dataset's maximum quantity (5 units) with normal unit pricing. These represent a genuine high-value bulk-order segment, not data entry errors |
| 3 | `UnitPrice` correlates strongly with `TotalPrice` (r = 0.72); `Quantity` correlates moderately (r = 0.62); `ItemsInCart` correlates weakly with `UnitPrice` (r ≈ 0.00) | **Pricing strategy is the primary revenue lever** — item price drives total order value more than cart size or quantity. Cart size and item price appear to be independent customer behaviors |
| 4 | **41.4%** of all 1,200 orders end in `Cancelled` or `Returned` status — nearly matching the 231 `Delivered` orders | This is a **material fulfillment/quality signal**. Nearly 1 in 2 orders fails to complete successfully — likely costing more revenue than any marketing initiative could recover. Recommend escalating to operations for root-cause investigation |
| 5 | `Chair` leads total revenue ($195,620 across 178 orders), but average order values across all 7 products are tightly clustered ($973–$1,111) | Revenue differences between products are driven by **order volume**, not price differentiation — there is no single "premium" product line outperforming on price |
| 6 | Monthly revenue is volatile, ranging from $27,752 to $68,069 across a 30-month window, with no clear seasonal pattern | Revenue planning should not assume strong seasonality in this data; further investigation (e.g. marketing spend, promotions calendar) is needed to explain month-to-month swings |

### Supporting Statistics

| Metric | Quantity | UnitPrice | ItemsInCart | TotalPrice |
|---|---|---|---|---|
| Count | 1,200 | 1,200 | 1,200 | 1,200 |
| Mean | 2.95 | $356.41 | 5.49 | $1,053.97 |
| Median | 3.00 | $364.21 | 5.00 | $823.62 |
| Std Dev | 1.41 | $197.18 | 2.28 | $819.86 |
| Min | 1 | $11.39 | 1 | $11.39 |
| Max | 5 | $699.93 | 10 | $3,456.40 |

**Correlation matrix (Pearson r):**

| | Quantity | UnitPrice | ItemsInCart | TotalPrice |
|---|---|---|---|---|
| **Quantity** | 1.00 | 0.02 | 0.65 | 0.62 |
| **UnitPrice** | 0.02 | 1.00 | 0.00 | 0.72 |
| **ItemsInCart** | 0.65 | 0.00 | 1.00 | 0.39 |
| **TotalPrice** | 0.62 | 0.72 | 0.39 | 1.00 |

> **Forensic note (Correlation ≠ Causation):** `Quantity` and `ItemsInCart` are correlated (r = 0.65), but neither causes the other — both are more plausibly driven by a hidden variable such as general customer purchasing behavior. We report the association; we do not claim a causal relationship.

## 4. Recommendations

1. **Use the median, not the mean, for typical-order benchmarking.** The mean order value is inflated by a small segment of large bulk orders.
2. **Investigate the 41.4% cancellation/return rate as a priority.** This is the single largest value-at-risk finding in the dataset and warrants its own root-cause analysis (e.g., by payment method, shipping region, or product).
3. **Treat the 8 high-value outlier orders as a VIP/bulk-buyer segment**, not as data quality issues — consider a dedicated retention or bulk-discount program.
4. **Prioritize pricing strategy over cart-size incentives** when planning revenue growth initiatives, since `UnitPrice` is the strongest driver of `TotalPrice`.
5. **Do not assume seasonality** in revenue planning without further investigation — the current 30-month window shows volatility without a clear repeating pattern.

---

*Generated as part of `notebooks/Project2_EDA.ipynb`. See that notebook for the full reproducible analysis and all supporting visuals in `visuals/`.*
