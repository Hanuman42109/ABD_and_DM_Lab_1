# MSCS 634 - Lab 1: Data Visualization, Data Preprocessing, and Statistical Analysis

## Purpose

This lab applies core data science techniques - visualization, preprocessing, and statistical analysis - to a synthetic **Superstore Sales** dataset (1,000 orders, 2020–2023) using Python, Pandas, Matplotlib/Seaborn, and scikit-learn inside a Jupyter Notebook.

---

## Dataset

`superstore_sales.csv` — 1,000 rows × 10 columns:

| Column | Type | Description |
| --- | --- | --- |
| Order Date | datetime | Date of order |
| Region | categorical | East / West / Central / South |
| Segment | categorical | Consumer / Corporate / Home Office |
| Ship Mode | categorical | Standard / Second / First / Same Day |
| Category | categorical | Technology / Furniture / Office Supplies |
| Sub-Category | categorical | 9 product sub-types |
| Sales | float | Order revenue ($) |
| Quantity | int | Units ordered |
| Discount | float | Discount rate applied (0–0.5) |
| Profit | float | Net profit ($) |

~5% missing values were intentionally injected into Sales and Profit, and 8 extreme outliers were added to Sales to simulate real-world data quality issues.

---

## Key Insights

### Visualizations

- **Scatter (Sales vs. Profit):** Technology orders cluster at high-sales/high-profit; Furniture shows many high-sales but low/negative-profit orders - heavy discounting is likely the cause.
- **Line (Monthly Trend):** Consistent Q4 sales spikes across all four years; gradual baseline growth from 2020 to 2023.
- **Bar (Sales by Region):** West leads in total revenue, followed by East. Central and South are roughly equal but trail significantly.
- **Histogram (Sales Distribution):** Heavy right skew - most orders are under $500 with a long tail of high-value outliers.
- **Box Plot (Profit by Category):** Technology has the highest median profit; Furniture contains the most negative-profit outliers; Office Supplies is tight and consistent.
- **Pie (Ship Mode Share):** Standard Class accounts for ~40% of orders; Same Day is ~10%.

### Statistical Analysis

- **Sales Mean ≈ $230, Median ≈ $165** - confirming right skew (mean pulled up by large orders).
- **Discount–Profit correlation is negative (~−0.45)** - higher discounts reliably reduce profit margins.
- **Sales–Profit correlation is moderately positive (~0.60)** - larger orders generally produce more profit, but with high variance.
- **Sales IQR ≈ $290** - inter-quartile range used to identify and remove ~25 outliers via the 1.5×IQR rule.

---

## Preprocessing Steps

1. **Missing Values** - Sales filled with column mean; Profit filled with column median.
2. **Outlier Removal** - IQR method on Sales; ~25 rows removed.
3. **Data Reduction** - 60% random sample; dropped `Ship Mode` and `Sub-Category` columns.
4. **Scaling & Discretization** - Min-Max scaling on Sales; Z-score standardization on Profit; Sales binned into Low / Medium / High / Very High.

---

## Challenges & Decisions

- **Right-skewed Sales:** Chose median (not mean) for Profit imputation to avoid inflating values with outlier sensitivity.
- **Outlier threshold:** Used the standard 1.5×IQR fence. A 3×IQR (less aggressive) was considered but the 8 injected extreme values were clearly non-representative.
- **Column dropping:** `Sub-Category` and `Ship Mode` were dropped in the reduction step because they had low correlation with the primary numeric targets and added categorical complexity without analytical benefit at this stage.

---

## How to Run

1.**Clone the repository**

```bash
   git clone https://github.com/Hanuman42109/ABD_and_DM_Lab_1
   cd ABD_and_DM_Lab_1
```

2.**Create and activate a virtual environment**

```bash
   python -m venv venv
   venv\Scripts\activate        # Windows
   source venv/bin/activate     # Mac/Linux
```

3.**Install dependencies**

```bash
   pip install pandas numpy matplotlib seaborn scikit-learn ipykernel
```

4.**Open in VS Code**

- Open the project folder in VS Code
- Press `Ctrl+Shift+P` → **Python: Select Interpreter** → choose `venv`
- Open `ABD_and_DM_Lab_1.ipynb`
- Click **Run All**
