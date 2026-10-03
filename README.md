# Supplement Sales KPI Dashboard

Week 1 lab for OMSBA 5068 (AI for Business) at Seattle University, Fall 2026.

This notebook turns five years of weekly supplement sales data into a set of monthly KPIs, comparison tables, and interactive charts broken down by country, sales platform, and product category. All charts use a custom Plotly template styled after The Economist.

## Dataset

`Supplement_Sales_Weekly_Expanded.csv` contains 4,384 weekly sales records from January 2020 through March 2025.

* **Countries:** Canada, UK, USA
* **Platforms:** Amazon, Walmart, iHerb
* **Categories:** 10 (Amino Acid, Fat Burner, Herbal, Hydration, Mineral, Omega, Performance, Protein, Sleep Aid, Vitamin)
* **Products:** 16
* **Columns:** Date, Product Name, Category, Units Sold, Price, Revenue, Discount, Units Returned, Location, Platform

The dataset was provided as part of the course materials.

## What the notebook covers

Each KPI includes a latest month summary table with month over month (MoM) % change, a monthly trend chart, and a MoM % change chart.

1. **Total Revenue per Country**
2. **Platform Revenue per Country:** one chart per country, one line per platform
3. **Platform Revenue per Country per Category:** one chart per country and platform pair, one line per category
4. **Platform Returns per Country per Category:** same layout as KPI 3, using units returned
5. **Product Rankings:** top 5 products by revenue and by units returned in each country for the latest month (March 2025)

In total the notebook produces 6 summary tables and 44 interactive charts.

## Approach

* Weekly records are rolled up to monthly periods with `pandas` (`groupby`, `pivot`, `pct_change`).
* At the category level, roughly half of the country, platform, and month combinations have no sales. These months are filled with 0, and any % change from a zero month is treated as undefined and shown as n/a rather than infinity.
* Summary tables use pandas `Styler` with green and red conditional formatting on the MoM column.
* Charts are built with `plotly.graph_objects`, with the latest value of each series highlighted and labeled.
* A single `go.layout.Template` applies the Economist styling to every chart: left aligned bold title with a unit subtitle, red rule and tag along the top, right side value axis, horizontal gridlines only, and a source note.
* Ties in the returns ranking are broken alphabetically so results are the same on every run.

## Notes on the results

* March 2025 contains 5 weekly reporting dates while February 2025 contains 4, so the latest MoM figures are inflated. For example, USA revenue shows +28.5% MoM, largely due to the extra week.
* Category level MoM charts are noisy because many categories sell only intermittently on a given platform.

## How to run

Requirements: Python 3.10 or later and Jupyter.

```bash
pip install pandas numpy matplotlib seaborn plotly jupyter
```

1. Clone the repository and keep `lab1.ipynb` and `Supplement_Sales_Weekly_Expanded.csv` in the same folder. The notebook loads the CSV by file name.
2. Open the notebook with `jupyter notebook lab1.ipynb` (or in VS Code or JupyterLab).
3. Run all cells.

The notebook was developed on Python 3.13 and runs on both pandas 2.x (2.1 or later) and pandas 3.x.

GitHub's notebook preview does not render interactive Plotly charts. To view them, run the notebook locally or open it in [nbviewer](https://nbviewer.org/).

## Files

* `lab1.ipynb`: the analysis notebook
* `Supplement_Sales_Weekly_Expanded.csv`: source data
* `README.md`: this file

## Tools

Python, pandas, NumPy, Plotly, Jupyter
