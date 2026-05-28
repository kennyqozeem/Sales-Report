# 📊 Sales Data Analysis & Power BI Report

A multi-year sales dataset paired with an interactive Power BI dashboard, covering transactional records across **2015–2017** for a California-based retail operation.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `Sales_Data.xlsx` | Core dataset — sales transactions + reference tables |
| `Sales_Data_Report.pbix` | Power BI report with interactive visualizations |
| `Sales_Report_Dashboard.png` | Power BI report snapshot |

---

## 🗂️ Dataset Overview

The Excel workbook contains **7 sheets** organised into fact and dimension tables.

### Fact Tables — Sales Transactions

| Sheet | Records | Description |
|-------|---------|-------------|
| `2015 Sales` | 4,980 | Full-year order transactions for 2015 |
| `2016 Sales` | 4,909 | Full-year order transactions for 2016 |
| `2017 Sales` | 1,000 | Partial-year order transactions for 2017 |

Each row represents a single order and contains:

| Column | Description |
|--------|-------------|
| `Order ID` | Unique order identifier (e.g. `AX10004`) |
| `Product ID` | Links to the Products table |
| `Location ID` | Links to the Locations table |
| `Sales Person ID` | Links to the Sales People table |
| `Customer ID` | Links to the Customers table |
| `Purchase Date` | Date of transaction |
| `Quantity` | Units purchased |
| `Price` | Unit sale price at time of purchase |

### Dimension / Reference Tables

#### 🛍️ Products (101 products)
| Column | Description |
|--------|-------------|
| `Product ID` | Unique identifier |
| `Product Name` | Product label |
| `Cost` | Unit cost of goods |
| `Original Sale Price` | Pre-discount list price |
| `Discount` | Applied discount amount |
| `Current Price` | Final selling price |
| `Taxes` | Tax amount per unit |

#### 📍 Locations (74 cities)
All locations are in **California**, with rich demographic context:
`Location ID`, `Name`, `County`, `State`, `Type`, `Latitude`, `Longitude`, `Area Code`, `Population`, `Households`, `Median Income`, `Land Area`, `Water Area`, `Time Zone`

#### 👤 Customers (801 customers)
`Customer ID`, `Customer Name`

#### 🧑‍💼 Sales People (45 salespeople)
`Salesperson ID`, `Salesperson Name`

---

## 📈 Power BI Report

`Sales_Data_Report.pbix` is an interactive dashboard built on the dataset above.

**To open the report:**
1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Open `Sales_Data_Report.pbix`
3. If prompted, re-link to `Sales_Data.xlsx` via **Transform Data → Data Source Settings**

**Possible analyses the report may cover:**
- Revenue and sales volume trends across 2015–2017
- Top-performing products by revenue and margin
- Sales performance by salesperson
- Geographic breakdown across California cities
- Customer purchase behaviour and repeat orders

---

## 🔗 Data Relationships

```
2015 Sales ──┐
2016 Sales ──┤── Product ID  ──► Products
2017 Sales ──┤── Location ID ──► Locations
             ├── Customer ID ──► Customers
             └── Sales Person ID ──► Sales People
```

---

## 🚀 Getting Started

### With Excel
Open `Sales_Data.xlsx` directly. Each sheet is self-contained — use Power Query or pivot tables to join and analyse across sheets.

### With Python
```python
import pandas as pd

# Load all sheets
sales_2015 = pd.read_excel("Sales_Data.xlsx", sheet_name="2015 Sales")
sales_2016 = pd.read_excel("Sales_Data.xlsx", sheet_name="2016 Sales")
sales_2017 = pd.read_excel("Sales_Data.xlsx", sheet_name="2017 Sales")
products   = pd.read_excel("Sales_Data.xlsx", sheet_name="Products")
locations  = pd.read_excel("Sales_Data.xlsx", sheet_name="Locations")

# Combine all years
all_sales = pd.concat([sales_2015, sales_2016, sales_2017], ignore_index=True)

# Enrich with product details
enriched = all_sales.merge(products, on="Product ID", how="left")
```

---

## 📋 Notes

- Purchase dates in the raw Excel file are stored as Excel serial numbers — convert with `pd.to_datetime(df['Purchase Date'], origin='1899-12-30', unit='D')` in Python, or format the column as **Date** in Excel.
- The 2017 data contains only 1,000 records compared to ~5,000 per year for 2015–2016, suggesting it covers a partial period.
- All location data is scoped to **California** cities only.

---

## 🛠️ Tools Used

- **Microsoft Excel** — data storage and structure
- **Power BI Desktop** — interactive reporting and visualisation
