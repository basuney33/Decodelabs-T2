# Project 2: Exploratory Data Analysis (EDA) 🔎

**DecodeLabs Industrial Training Kit — Data Analytics Track | Batch 2026**

> Step into the role of a Data Analyst at DecodeLabs. Project 2 is the discovery phase: Exploratory Data Analysis. This track isn't about "simple reporting" — it's about **uncovering the story**. Before building dashboards or predictive models, you must master the art of interrogating data to find hidden patterns, trends, and outliers.

---

## 🎯 Project Goal

Analyze a dataset to understand patterns, trends, and distributions by:
- Calculating basic statistics (mean, median, count)
- Identifying trends and outliers
- Summarizing key observations

...and translating every finding into a business diagnosis via the **"So What?" Test**, documented in a stakeholder-facing Executive Summary.

## 🧭 The Forensic Framework (IPO)

| Stage | Description |
|---|---|
| **Input** | The Evidence — raw or sanitized data (here: Project 1's cleaned dataset) |
| **Process** | The Investigation — mathematical transformations & statistical logic |
| **Output** | The Verdict — actionable insights, summary reports, and decision support |

> *"A correlation is a CLUE, not a VERDICT. Always check for hidden variables."*

## 📁 Repository Structure

```
project2_eda/
├── README.md                          ← you are here
├── data/
│   ├── raw/
│   │   ├── cleaned_dataset.csv                 ← input: Project 1's verified output
│   │   └── cleaned_dataset.xlsx                ← same, Excel format
│   └── processed/
│       ├── eda_summary_statistics.csv          ← mean/median/std/min/max per numeric column
│       ├── correlation_matrix.csv               ← Pearson correlation matrix
│       └── flagged_outliers.csv                 ← outlier records (IQR method)
├── notebooks/
│   └── Project2_EDA.ipynb              ← full, reproducible EDA workflow (Jupyter Notebook)
├── visuals/
│   ├── 01_distributions.png            ← histograms: mean vs median, skewness
│   ├── 02_boxplot_totalprice.png       ← boxplot + outliers (IQR method)
│   ├── 03_correlation_heatmap.png      ← Pearson correlation heatmap
│   ├── 04_scatter_unitprice_totalprice.png
│   ├── 05_categorical_breakdowns.png   ← OrderStatus / PaymentMethod / ReferralSource
│   ├── 06_avg_value_by_product.png
│   └── 07_monthly_trend.png            ← revenue over time
└── docs/
    ├── EXECUTIVE_SUMMARY.md            ← 4-part stakeholder summary (Problem → Methodology → Findings → Recommendations)
    └── key_findings.json               ← machine-readable findings log
```

## 📊 Dataset

| | |
|---|---|
| **Input file** | `cleaned_dataset.csv` / `.xlsx` |
| **Source** | Output of [Project 1: Data Cleaning & Preparation](../project1_data_cleaning) |
| **Rows** | 1,200 verified e-commerce orders |
| **Columns** | 14 — `OrderID`, `Date`, `CustomerID`, `Product`, `Quantity`, `UnitPrice`, `ShippingAddress`, `PaymentMethod`, `OrderStatus`, `TrackingNumber`, `ItemsInCart`, `CouponCode`, `ReferralSource`, `TotalPrice` |
| **Quality** | 0% duplicate IDs, 0% incorrectly formatted dates, 0 missing values (verified in Project 1) |

## 🧪 Methodology

The notebook follows the diagnostic framework defined in the project brief:

1. **Phase 0 — Load the Evidence**: bring in the verified dataset from Project 1.
2. **Phase 1 — The Geometry of Distribution**: univariate analysis of every numeric column; symmetrical vs. skewed shape; mean vs. median comparison.
3. **Phase 2 — The Logic Skeleton**: five-number summary (min, Q1, median, Q3, max) for every numeric variable.
4. **Phase 3 — Unmasking the Outliers**: IQR and Z-score outlier detection, followed by forensic investigation to classify flagged records as **noise** (errors, to clean) or **signal** (genuine rare events, to investigate).
5. **Phase 4 — Mapping Relationships**: Pearson correlation matrix and scatter plots, with the Correlation ≠ Causation rule explicitly applied.
6. **Phase 5 — Trends Over Time**: monthly revenue trend, product/payment/referral breakdowns, fulfillment outcome analysis.
7. **The "So What?" Test**: every statistical finding translated into a one-line business diagnosis.
8. **Executive Summary**: the final verdict, documented for non-technical stakeholders.

## 🛠️ Tools & Skills Used

- **Python** — pandas, numpy, matplotlib
- **Jupyter Notebook** — for a reproducible, step-by-step workflow
- **Statistical techniques**: skewness, five-number summary, IQR & Z-score outlier detection, Pearson correlation

## 🔑 Key Findings (Summary)

1. `TotalPrice` is right-skewed — the mean overstates the typical order by ~28% vs. the median.
2. 8 high-value orders flagged as statistical outliers are confirmed **signal** (genuine bulk orders), not data errors.
3. `UnitPrice` is the strongest driver of `TotalPrice` (r = 0.72) — pricing strategy matters more than cart size.
4. **41.4%** of orders end in `Cancelled` or `Returned` status — a major fulfillment signal for operations.
5. `Chair` leads total revenue, but this is driven by order volume, not price premium.

Full detail and supporting numbers: [`docs/EXECUTIVE_SUMMARY.md`](docs/EXECUTIVE_SUMMARY.md)

## ▶️ How to Run

```bash
# 1. Clone the repository
git clone <YOUR_GITHUB_REPO_URL_HERE>
cd project2_eda

# 2. Install dependencies
pip install pandas numpy matplotlib jupyter

# 3. Launch the notebook
jupyter notebook notebooks/Project2_EDA.ipynb

# 4. Run all cells (Cell → Run All)
# Outputs will be written to data/processed/, visuals/, and docs/
```

## 📦 Outputs

| File | Description |
|---|---|
| `data/processed/eda_summary_statistics.csv` | Mean/median/std/min/max for all numeric columns |
| `data/processed/correlation_matrix.csv` | Pearson correlation matrix |
| `data/processed/flagged_outliers.csv` | Outlier records flagged by the IQR method |
| `visuals/*.png` | 7 charts generated from the analysis |
| `docs/EXECUTIVE_SUMMARY.md` | Stakeholder-facing 4-part executive summary |
| `docs/key_findings.json` | Machine-readable findings log |

## 🔗 Project Links

| Resource | Link |
|---|---|
| GitHub Repository | `<ADD_YOUR_GITHUB_REPO_URL_HERE>` |
| Project 1 Repository (Data Cleaning) | `<ADD_PROJECT_1_REPO_URL_HERE>` |
| Notebook (nbviewer) | `<ADD_NBVIEWER_OR_GITHUB_LINK_HERE>` |

> Replace the placeholders above once you've pushed this folder to your own GitHub repository (see **Publishing to GitHub** below).

## 🚀 Publishing to GitHub

1. Create a new repository on GitHub, e.g. `data-analytics-project2-eda`.
2. From inside this folder:
   ```bash
   git init
   git add .
   git commit -m "Project 2: Exploratory Data Analysis (EDA)"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo-name>.git
   git push -u origin main
   ```
3. Update the **Project Links** section above with your live repo URL.
4. Continue the same repo-per-project pattern for Project 3 onward — one clean, self-contained repository per milestone.

## 🏆 Status

**Project 2: COMPLETE** — distributions characterized, outliers investigated and classified, correlations mapped, business diagnosis documented. Ready to unlock Project 3.

---
*DecodeLabs | Industrial Training Kit | Batch 2026*
*📞 +91 89330 06408 · ✉ decodelabs.tech@gmail.com · 🌎 www.decodelabs.tech*
