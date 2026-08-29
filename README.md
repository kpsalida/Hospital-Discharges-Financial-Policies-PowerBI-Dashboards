# Strategic Insights from Technical to Management Level: Private Hospital Finance

A role-based Power BI dashboard suite analyzing hospital discharge, cost, and revenue data across three private hospitals, built for the Data Visualization course (ITC6004B1) at The American College of Greece.

**Authors:** [Katerina Psallida](https://github.com/kpsalida) & [Kimon Lappas](https://github.com/kitlapp)

---

## Overview

Patient discharge data is directly tied to hospital efficiency, operational cost, and quality of care. This project explores costs, revenues, and patient flow across three hospitals — **Maimonides**, **Hudson Valley**, and **St. Joseph's** — to uncover where profitability is concentrated, where inefficiencies hide, and what strategic actions each level of management should take.

Rather than a single dashboard, the project presents the *same underlying data* through three different lenses, matched to how each audience actually makes decisions:

| Role | Focus |
|---|---|
| **Technical** | Detailed KPIs, insurance mix, diagnosis-level cost analysis, K-Means clustering, and forecasting |
| **Director** | Cross-facility comparisons and performance benchmarking |
| **C-level** | A simplified, minute-long view of the KPIs that matter most |

## Dashboards

### Technical Dashboard
![Technical Dashboard](technical_dashboard.png)

This dashboard is built around two core financial KPIs and a clustering model that explains *why* they vary:

- **Charge-to-Cost Ratio (CCR)** — `Total Charges / Total Costs`. Across the full dataset, the average CCR is **3.65x**, meaning charges are, on average, 3.65 times higher than the underlying cost. This ratio is the primary lens for comparing markup strategy across facilities: Maimonides operates with a **3.13x–3.42x** complexity-driven markup that scales with severity of illness, Hudson Valley holds a stable **~2.3x**, and St. Joseph's stays under **2.0x** across every severity band — leaving it with little financial buffer against rising costs.
- **Cross-Subsidy Ratio (CSR)** — currently **1.02**, indicating that, in aggregate, surplus from high-margin cases is just barely sufficient to cover losses from high-complexity, loss-making admissions.
- **LOS (Length of Stay)** - is the number of days a patient remains admitted, from intake to discharge — one of the core drivers of both cost and CCR in this analysis.
- **K-Means Clustering (k = 3)** — to understand *what kind of cases* drive these ratios, we isolated Maimonides' Medicaid population and clustered cases by CCR into three groups, then used the fitted model to label the rest of the dataset:
  - **Group 0 – Routine Cases:** average Length of Stay (LOS), moderate cost, mid-range CCR (e.g., standard maternity admissions) — the hospital's baseline activity.
  - **Group 1 – Loss Makers:** long LOS, high total cost, low CCR — cases where extended, resource-intensive care isn't matched by adequate reimbursement (e.g., Schizophrenia at St. Joseph's).
  - **Group 2 – Cash Cows:** short LOS, low cost, high CCR — cases where billed charges convert efficiently into margin (e.g., Neonate Birth).

    
  Cluster quality was validated with a silhouette score. The segmentation shows that profitability is driven more by *facility-specific pricing behavior* than by payer type alone — Maimonides balances heavy Medicaid demand against a deliberate mix of high-efficiency case lines to stay financially viable.

The full preprocessing, EDA, regression, and clustering work behind these numbers is in [`visualization_eda.ipynb`](visualization_eda.ipynb) in this repo.

### Director Dashboard
![Director Dashboard](director_dashboard.png)

Compares revenue, cost, and profit concentration across facilities — highlighting that Maimonides alone drives 82.5% of group revenue, and that state/federal payers account for 85% of total revenue.

### C-Level Dashboard
![C-Level Dashboard](clevel_dashboard.png)

A six-KPI summary (Revenue, Discharges, CPD, Avg. Length of Stay, Profit, Profit Margin) built to be read in under a minute.

## Key Findings & Strategic Recommendations

1. **(Re)invest in Maimonides** to strengthen its position within the group — it's the clear performance leader.
2. **Secure and expand relationships with state/federal payers**, who drive the large majority of group revenue.
3. **Reallocate staff from St. Joseph's to Maimonides** to address potential understaffing at Maimonides while reducing St. Joseph's operating costs.
4. **Restructure St. Joseph's around high-profitability cases** (e.g., normal neonate births) to directly improve its revenue position.

## Data & Tools

- **Data source:** [NY SPARCS Hospital Inpatient Discharges (2018–2019)](https://health.data.ny.gov/Health/Hospital-Inpatient-Discharges-SPARCS-De-Identified/4ny4-j5zv)
- **Preprocessing, EDA & clustering:** Python (pandas, scikit-learn — KMeans, silhouette scoring, linear regression) in Google Colab
- **Dashboards:** Power BI Desktop
- **Report & presentation:** MS Word, PowerPoint

## Files in This Repository

| File | Description |
|---|---|
| `visualization_eda.ipynb` | Full data preprocessing, EDA, K-Means clustering, and forecasting notebook |
| `Technical.pbix` | Technical-level Power BI dashboard |
| `Director_and_C.pbix` | Director and C-level dashboards (two report pages) |
| `Report.pdf` | Full written report (~4,700 words) covering methodology, EDA, and strategic analysis |
| `Presentation.pdf` / `Presentation.pptx` | Project presentation slides |

## My Contribution

I led the technical exploratory data analysis for this project — cleaning and structuring the two-year SPARCS discharge dataset, and identifying the Charge-to-Cost Ratio (CCR) and Cross-Subsidy Ratio (CSR) as the core financial KPIs for the analysis. I also designed and ran the K-Means clustering work that uncovered the three case-profitability groups (Routine Cases, Loss Makers, and Cash Cows), and built the Technical dashboard around these findings.

---

*Class project for ITC6004B1 – Data Visualization, Winter Term 2026, The American College of Greece.*
