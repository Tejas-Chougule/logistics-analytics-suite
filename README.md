# 📦 Logistics Operations Analytics Suite
**Power BI | DAX | Python | Supply Chain Analytics**

A four-dashboard Power BI analytics suite simulating real-world 3PL (third-party logistics) operations across warehouse KPIs, inventory forecasting, carrier delay analysis, and operational efficiency — built to demonstrate data analyst skills in a warehousing and logistics context.

🔗 **[View Live Portfolio Page](https://tejas-chougule.github.io/logistics-analytics-suite/)**

---

## 📊 Dashboards

| # | Dashboard | Key Metrics | Key Story |
|---|---|---|---|
| 1 | Warehouse KPI Dashboard | Fulfilment Rate, Pick Accuracy, UPH, SLA% | WH-DON-02 fulfilment dip in Q2 |
| 2 | Inventory Forecasting Dashboard | Stockout Risk, Overstock Flags, Days of Stock | Chilled category stockout event in March |
| 3 | Supply Chain Delay Analysis | OTIF Rate, Avg Delay Days, Delay Cost £ | XPO Logistics carrier crisis in Q2 |
| 4 | Logistics Operations Dashboard | Inbound/Outbound Vol, CPU £, Labour Efficiency | Q4 cost-per-unit spike during peak |

---

## 🗂️ Repository Structure

```
logistics-analytics-suite/
│
├── data/
│   ├── warehouse_ops.csv          # 2,670 rows — shift-level warehouse KPIs
│   ├── inventory.csv              # 25,120 rows — 80 SKUs × 6 categories × 12 months
│   ├── supply_chain_delays.csv    # 2,242 rows — shipment-level carrier delay data
│   └── logistics_ops.csv          # 2,670 rows — inbound/outbound/cost/labour data
│
├── powerbi/
│   └── Logistics_Analytics_Suite.pbix   # All 4 dashboards in one file
│
├── screenshots/
│   ├── Dashboard1_Warehouse_KPI.png
│   ├── Dashboard2_Inventory_Forecasting.png
│   ├── Dashboard3_Supply_Chain_Delays.png
│   └── Dashboard4_Logistics_Operations.png
│
├── index.html                     # Portfolio page (GitHub Pages)
└── README.md
```

---

## 🔢 Dataset Overview

All data is synthetically generated using Python to reflect realistic 3PL operational patterns. Data covers a full 12-month period (Jan–Dec 2024) across three UK warehouse sites.

### warehouse_ops.csv
- **2,670 rows** | Shift-level (Day / Night / Twilight)
- Warehouses: WH-DON-01, WH-DON-02, WH-LEE-01 (Doncaster & Leeds)
- Fields: `date`, `warehouse_id`, `shift`, `orders_received`, `orders_fulfilled`, `fulfillment_rate`, `pick_accuracy`, `units_per_hour`, `dock_to_stock_hrs`, `sla_met`
- **Baked-in pattern:** WH-DON-02 fulfilment dip in April–May

### inventory.csv
- **25,120 rows** | 80 SKUs × 6 product categories
- Categories: Ambient Food, Chilled, General Merchandise, Electronics, Apparel, Home & Garden
- Fields: `date`, `sku_id`, `product_category`, `stock_level`, `reorder_point`, `units_sold`, `units_received`, `overstock_flag`, `stockout_risk`
- **Baked-in pattern:** Chilled category stockout event in March; Q4 demand uplift

### supply_chain_delays.csv
- **2,242 rows** | Individual shipment records
- Carriers: DHL Supply Chain, XPO Logistics, Kuehne+Nagel, CEVA Logistics, Wincanton
- Origins: Rotterdam, Hamburg, Felixstowe, Southampton, Liverpool
- Fields: `shipment_id`, `ship_date`, `carrier`, `origin`, `destination`, `expected_delivery`, `actual_delivery`, `delay_days`, `delay_reason`, `otif`, `cost_impact_gbp`
- **Baked-in pattern:** XPO Logistics OTIF crisis in Q2 (April–June)

### logistics_ops.csv
- **2,670 rows** | Shift-level operational data
- Fields: `date`, `warehouse_id`, `shift`, `inbound_units`, `outbound_units`, `headcount`, `labour_hours`, `cost_per_unit_gbp`, `total_cost_gbp`, `throughput_rate`
- **Baked-in pattern:** Cost-per-unit rises ~12% in Q4 peak season

---

## ⚡ DAX Measures (Selected)

```dax
-- OTIF Rate %
OTIF Rate % =
DIVIDE(
    COUNTROWS(FILTER(supply_chain_delays, supply_chain_delays[otif] = 1)),
    COUNTROWS(supply_chain_delays), 0
) * 100

-- Fulfilment Rate %
Fulfilment Rate % =
DIVIDE(
    SUM(warehouse_ops[orders_fulfilled]),
    SUM(warehouse_ops[orders_received]), 0
) * 100

-- SLA Compliance %
SLA Compliance % =
DIVIDE(
    COUNTROWS(FILTER(warehouse_ops, warehouse_ops[sla_met] = 1)),
    COUNTROWS(warehouse_ops), 0
) * 100

-- Labour Efficiency
Labour Efficiency = DIVIDE([Total Outbound], [Total Labour Hours], 0)
```

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Power BI Desktop** | Dashboard building, visuals, slicers, conditional formatting |
| **DAX** | 25+ custom measures for KPIs, trends, and ratios |
| **Python** | Synthetic data generation with realistic logistics patterns |
| **Power Query** | Data loading, type enforcement, table relationships |
| **CSV / Excel** | Structured datasets modelling real 3PL operations |

---

## 🎯 Business Context

This project simulates the analytics workload of a Data Analyst embedded within a 3PL logistics operation — the kind of role found at companies like Maersk, DHL, XPO, or CEVA. The dashboards are designed for two audiences:

- **Operational teams** — shift supervisors and warehouse managers who need daily/weekly KPI visibility
- **Senior stakeholders & customers** — who need trend analysis, risk identification, and cost reporting

> *Data simulated to reflect realistic 3PL operational patterns. All warehouse names, carrier performance figures, and shipment records are fictional.*

---

## 📁 How to Use

1. Clone or download this repository
2. Open `powerbi/Logistics_Analytics_Suite.pbix` in Power BI Desktop
3. If prompted, update data source paths to point to the `/data/` folder
4. All 4 dashboards are on separate pages within the same `.pbix` file

---

## 👤 About

Built by **Tejas** — MSc Data Science, University of Sheffield.
Focused on data analyst and analytics engineering roles and operations.

🔗  [Portfolio](https://tejas-chougule.github.io/logistics-analytics-suite/) · [LinkedIn](https://www.linkedin.com/in/tejas-ashok-chougule/) · [GitHub](https://github.com/Tejas-Chougule)
