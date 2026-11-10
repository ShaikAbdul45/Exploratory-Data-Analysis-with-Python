# EDA Capstone Project: Online Retail Sales

Exploratory data analysis of a UK-based online retailer's transactions (01 Dec 2010 to 09 Dec 2011). The project looks at **when** customers buy, **what** sells best and **where** revenue comes from.

> **Important: the bundled dataset is a synthetic sample.**
> `Dataset/Online_Retail.xlsx` was generated to match the schema of the real UCI Online Retail dataset so the whole pipeline runs end to end. The charts and report currently show illustrative numbers only. To get real results, follow *Using the real dataset* below.

## Project structure

```
EDA_Capstone_Project/
├── Dataset/
│   └── Online_Retail.xlsx          # input data (sample; replace with the real file)
├── Notebooks/
│   └── EDA_Analysis.ipynb          # full analysis; also builds charts and the PDF report
├── Visualizations/
│   ├── Monthly_Sales.png
│   ├── Top_Products.png
│   └── Country_Sales.png
├── Reports/
│   └── EDA_Project_Report.pdf      # generated summary report
├── Dashboard/
│   └── Sales_Dashboard.html        # interactive dashboard (open in a browser)
├── requirements.txt
└── README.md
```

## Using the real dataset

1. Download **Online Retail** from the UCI Machine Learning Repository (search "UCI Online Retail dataset").
2. Save it as `Dataset/Online_Retail.xlsx`, replacing the sample.
3. Run the notebook (below). The charts and PDF report regenerate automatically, and the "sample data" warnings disappear.

## How to run

```bash
pip install -r requirements.txt
cd Notebooks
jupyter notebook EDA_Analysis.ipynb      # then Run All
```

Run the notebook from inside `Notebooks/`, because file paths are relative (`../Dataset`, `../Visualizations`, `../Reports`).

## Dataset columns

| Column | Description |
|---|---|
| InvoiceNo | Invoice number; a `C` prefix marks a cancellation |
| StockCode | Product code |
| Description | Product name |
| Quantity | Units per line item |
| InvoiceDate | Invoice timestamp |
| UnitPrice | Price per unit (GBP) |
| CustomerID | Customer identifier (often missing) |
| Country | Customer's country |

## Analysis workflow

1. **Load and inspect** the data: shape, types, summary statistics.
2. **Data quality checks**: missing values, duplicates, cancellations, zero/negative prices, non-product codes.
3. **Cleaning**: remove duplicates, cancellations, invalid quantity/price, missing descriptions and non-product codes. Rows with a missing CustomerID are kept for sales analysis.
4. **Feature engineering**: `Revenue = Quantity x UnitPrice`, plus month, weekday and hour.
5. **Visualisation**: monthly sales trend, top 10 products, revenue by country (with and without the UK), orders by weekday and hour.
6. **Findings and report**: key metrics are computed in the notebook and written into the PDF.

## Outputs

| File | What it shows |
|---|---|
| `Visualizations/Monthly_Sales.png` | Monthly revenue trend with the peak month highlighted |
| `Visualizations/Top_Products.png` | Top 10 products by revenue |
| `Visualizations/Country_Sales.png` | Top countries by revenue, with and without the UK |
| `Dashboard/Sales_Dashboard.html` | Interactive dashboard: KPI cards, monthly trend, countries, top products, weekday/hour patterns and key insights (needs internet for the chart library) |
| `Reports/EDA_Project_Report.pdf` | Objectives, cleaning log, headline metrics, findings, recommendations, limitations |

## Limitations

- The data covers roughly one year, so seasonality can't be fully separated from growth.
- Cancelled orders are removed, not netted off, so revenue is gross of returns.
- Rows without a CustomerID can't be used for customer-level metrics.
- The analysis is descriptive and doesn't establish causes.

## Possible next steps

RFM customer segmentation, market-basket analysis, and monthly revenue forecasting.
