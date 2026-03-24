# ⚡ Electric Vehicle Market Analysis Dashboard

> An interactive Tableau dashboard analyzing EV adoption trends, market share, technological progress, and regional concentration across the United States (2010–2024).

**Author:** Supratim Maity  
**Tool:** Tableau Desktop 2025.3.2  
**Data Source:** Electric_Vehicle_Population_Data.csv  

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dataset Description](#dataset-description)
- [KPIs & Key Metrics](#kpis--key-metrics)
- [Dashboard Visualizations](#dashboard-visualizations)
- [Calculated Fields](#calculated-fields)
- [Parameters & Filters](#parameters--filters)
- [Key Insights](#key-insights)
- [Tools & Technologies](#tools--technologies)
- [Project Structure](#project-structure)
- [How to Open the Dashboard](#how-to-open-the-dashboard)
- [Recommendations](#recommendations)

---

## 🔍 Project Overview

This project delivers a comprehensive **360° view of the U.S. Electric Vehicle (EV) market** using Tableau's interactive visualization capabilities. It was built to help stakeholders understand:

- Total EV market size (BEV + PHEV)
- Average electric range and technological efficiency
- Dominance of BEVs vs. PHEVs
- Top EV manufacturers and models by market share
- State-wise geographical distribution of EV adoption
- Impact of CAFV (Clean Alternative Fuel Vehicle) incentives

---

## 📊 Dataset Description

| Property | Details |
|---|---|
| **File Name** | `Electric_Vehicle_Population_Data.csv` |
| **Total Records** | 150,000+ |
| **Time Period** | 2010 – 2024 |
| **Geographical Scope** | United States |
| **Vehicle Types Covered** | BEV (Battery Electric Vehicle) & PHEV (Plug-in Hybrid Electric Vehicle) |
| **Format** | CSV (UTF-8, comma-delimited) |

### Data Fields

| Field | Data Type | Description |
|---|---|---|
| `VIN (1-10)` | String | First 10 characters of Vehicle Identification Number |
| `County` | String | County of vehicle registration |
| `City` | String | City of vehicle registration |
| `State` | String | U.S. state of registration |
| `Postal Code` | Integer | ZIP code |
| `Model Year` | Integer | Year of vehicle model |
| `Make` | String | Vehicle manufacturer (e.g., Tesla, Nissan) |
| `Model` | String | Specific vehicle model (e.g., Model Y, Leaf) |
| `Electric Vehicle Type` | String | BEV or PHEV classification |
| `Clean Alternative Fuel Vehicle (CAFV) Eligibility` | String | Eligibility status for CAFV incentives |
| `Electric Range` | Integer | Electric range in miles |
| `Base MSRP` | Integer | Manufacturer's Suggested Retail Price |
| `Legislative District` | Integer | Legislative district of registration |
| `DOL Vehicle ID` | Integer | Unique vehicle identifier (WA Dept. of Licensing) |
| `Vehicle Location` | String | Geographic coordinates |
| `Electric Utility` | String | Electric utility provider |
| `2020 Census Tract` | Integer | U.S. Census tract identifier |

---

## 📈 KPIs & Key Metrics

These KPI cards are displayed at the top of the dashboard for an at-a-glance summary:

| KPI | Value | Insight |
|---|---|---|
| **Total Vehicles** | 150.41K | Total EV population in the dataset |
| **Average Electric Range** | 67.83 miles | Reflects city-usage focus; indicates room for improvement in long-range EVs |
| **Total BEV Vehicles** | 116.75K (~78%) | Battery Electric Vehicles dominate the market |
| **Total PHEV Vehicles** | 33,668 (~22%) | Plug-in Hybrids hold a smaller but significant share |

---

## 🖼️ Dashboard Visualizations

The dashboard (Dashboard 1) is composed of **9 worksheets**:

### 1. 📅 Total Vehicles by Model Year *(Area Chart)*
- Plots EV registrations from 2010 onwards
- **Slow growth** 2011–2015 → **Gradual increase** 2016–2018 → **Dip** 2019–2020 → **Massive surge** 2021–2023 → **Peak: 37.1K vehicles in 2023**
- 2024 shows a drop likely due to incomplete year data

### 2. 🗺️ Total Vehicles by State *(Geographic Map — Mapbox)*
- Visualizes the geographical spread of EV registrations across all U.S. states
- **Washington** has the highest concentration
- Strong clusters in **California, Texas, Florida**, and East Coast states

### 3. 🏭 Top 10 Total Vehicles by Make *(Horizontal Bar Chart)*

| Rank | Make | Market Share |
|---|---|---|
| 1 | TESLA | 63.54% |
| 2 | NISSAN | 12.44% |
| 3 | CHEVROLET | 11.08% |
| 4 | FORD | 7.01% |
| 5 | BMW | 5.93% |

- Tesla alone controls **over 60%** of the entire EV market — driven by early-mover advantage, brand trust, and superior battery technology.

### 4. 🍩 Total Vehicles by CAFV Eligibility *(Donut Chart)*

| Category | Share |
|---|---|
| CAFV Eligible | 41.81% |
| CAFV Not Eligible | 11.85% |
| CAFV Unknown | 46.34% |

- The large **Unknown** share (46.34%) highlights a data quality gap and a potential area for better classification.

### 5. 🌳 Top 10 Total Vehicles by Model *(Treemap)*

| Rank | Model | Share |
|---|---|---|
| 1 | Tesla Model Y | 18.95% |
| 2 | Tesla Model 3 | 18.42% |
| 3 | Nissan Leaf | 8.77% |
| 4 | Tesla Model S | 5.06% |
| 5 | Chevrolet Bolt EV | 3.81% |

- Tesla dominates not just by brand, but by **multiple top-performing models**.

### KPI Worksheets (4 cards)
- **Total Vehicles** — Shows aggregate count
- **Avg Electric Range** — Shows average EV range in miles
- **Total BEV Vehicles** — Shows BEV count and % share
- **Total PHEV Vehicles** — Shows PHEV count and % share

---

## 🧮 Calculated Fields

All calculations are defined directly in the Tableau workbook:

| Field Name | Formula | Description |
|---|---|---|
| `Total Vehicles` | `COUNTD([DOL Vehicle ID])` | Distinct count of all EVs |
| `Avg Electric Range` | `AVG([Electric Range])` | Average electric range across all vehicles |
| `Total BEV Vehicles` | `COUNTD(IF [Electric Vehicle Type]="Battery Electric Vehicle (BEV)" THEN [DOL Vehicle ID] END)` | Count of BEV-type vehicles only |
| `% of BEV Vehicles` | `[Total BEV Vehicles] / [Total Vehicles]` | BEV share of total EV population |
| `Total PHEV Vehicles` | `COUNTD(IF [Electric Vehicle Type]="Plug-in Hybrid Electric Vehicle (PHEV)" THEN [DOL Vehicle ID] END)` | Count of PHEV-type vehicles only |
| `% of PHEV Vehicles` | `[Total PHEV Vehicles] / [Total Vehicles]` | PHEV share of total EV population |

---

## 🎛️ Parameters & Filters

| Parameter / Filter | Type | Range / Options | Default |
|---|---|---|---|
| **Top N** | Integer Parameter | 1 – 15 | 5 |
| **State** | Dimension Filter | All U.S. States | All |
| **EV Type** | Dimension Filter | BEV / PHEV | All |
| **Model** | Dimension Filter | All models | All |
| **(CAFV) Eligibility** | Dimension Filter | Eligible / Not Eligible / Unknown | All |

The **Top N parameter** dynamically controls how many manufacturers/models appear in the bar chart and treemap, allowing interactive exploration from Top 1 to Top 15.

---

## 💡 Key Insights

1. **EV adoption accelerated sharply after 2020**, peaking at 37,100 vehicles in 2023.
2. **BEVs dominate the market at ~78%**, signalling a strong shift away from hybrids.
3. **Tesla holds a commanding 63.5% market share** — driven by Model Y and Model 3 which together account for ~37% of all EVs.
4. **Washington state leads in EV adoption**, likely due to charging infrastructure, state incentives, and higher income levels.
5. **Average electric range of ~68 miles** reflects a city/commuter-use focus in the current EV fleet.
6. **46.34% of vehicles have unknown CAFV eligibility**, suggesting a data completeness issue for policy analysis.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **MS Excel 2021** | Data cleaning and pre-processing |
| **Tableau Desktop 2025.3.2** | Dashboard development and visualization |
| **Mapbox** | Geographic map visualization (state-level EV distribution) |

---

## 📁 Project Structure

```
EV-Market-Analysis-Tableau/
│
├── Electric_Vehicle_Population_Data.csv   # Source dataset (150K+ records)
├── EV_Dashboard.twb                       # Tableau workbook file
├── Electric_Vehicle_Problem_Statement.pptx  # Project requirements & KPI definitions
├── Electric-Vehicle-Market-Analysis-Dashboard.pptx  # Presentation of findings
└── README.md                              # This file
```

---

## 🚀 How to Open the Dashboard

1. **Install Tableau Desktop** (version 2025.3.2 or later recommended).
2. Place `Electric_Vehicle_Population_Data.csv` in the following path or update the data source connection:
   ```
   E:/Weskitters/Projects/Tableau_Project/EV/Electric_Vehicle_Population_Data.csv
   ```
   > ⚠️ If your CSV is stored elsewhere, open `EV_Dashboard.twb` in Tableau, go to **Data > Edit Data Source**, and point the connection to your local copy of the CSV.
3. Open `EV_Dashboard.twb` in Tableau Desktop.
4. Navigate to **Dashboard 1** in the bottom tab bar.
5. Use the **interactive filters** (State, EV Type, Model, CAFV Eligibility) and the **Top N parameter** to explore the data.

---

## ✅ Recommendations

Based on the analysis, the following actions are suggested for stakeholders and policymakers:

1. **Improve CAFV classification transparency** — The 46% "Unknown" category limits policy analysis; better data collection is needed.
2. **Expand EV infrastructure in low-adoption states** — Focus on states lagging in EV registrations to drive national growth.
3. **Encourage PHEV-to-BEV transition** — Incentivize PHEV owners to switch to fully electric vehicles through subsidies.
4. **Track Year-over-Year growth rate explicitly** — Build YoY growth metrics into the dashboard for trend acceleration analysis.
5. **Introduce model-wise electric range comparison** — Compare range across models to track technological advancement over time.
6. **Target high-growth states for policy intervention** — States like Washington and California can serve as models for nationwide adoption strategies.

---

*This dashboard was developed as part of a Tableau data visualization project to demonstrate analytical storytelling with real-world EV population data.*
