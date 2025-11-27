# 📊 Data Requirements — Supplier Risk Assessment (SAP → CSV)

This document defines the **data fields required from SAP** to automate the supplier risk assessment process.  
These fields will allow us to build the unified dataset, compute risk scores, and eliminate the current 5-month manual cycle.

---

## 🟦 1. Component Data (components_master.csv)

| Field | Description |
|------|-------------|
| component_id | Unique component identifier (SAP code) |
| component_name | Description / short text |
| category | Component category or classification |
| annual_usage_units | Average units used per year |
| criticality_level | High / Medium / Low (if available) |

**Reason needed:**  
To understand how critical a component is and to link it to its suppliers.

---

## 🟩 2. Supplier Data (suppliers_master.csv)

| Field | Description |
|------|-------------|
| supplier_id | Unique supplier identifier |
| supplier_name | Supplier full name |
| country | Country of operation |
| region | Region within country |
| geo_risk_rating | External geopolitical risk rating (if available) |
| supplier_financial_rating | Financial stability rating (if available) |

**Reason needed:**  
Country/region + geopolitical risk + financial stability = core input for risk scoring.

---

## 🟧 3. Supplier–Component Relationship Data (supplier_component_relationship.csv)

| Field | Description |
|------|-------------|
| component_id | Foreign key |
| supplier_id | Foreign key |
| price_per_unit | Contracted price |
| lead_time_days | Contractual lead time |
| contract_start_date | Start of current agreement |
| contract_end_date | Expiration date |
| years_relationship | Calculated from historical data |
| annual_delays | Number of delivery delays/year |
| quality_incidents | Number of quality issues/year |
| on_time_delivery_rate | % deliveries on time |
| defect_rate | % defective units delivered |

**Reason needed:**  
This is the core table for evaluating supplier performance and dependency.

---

## 🟪 4. Logistics Data (logistics_data.csv)

| Field | Description |
|------|-------------|
| supplier_id | Foreign key |
| component_id | Optional — if different components use different modes |
| transport_mode | Air / Sea / Road |
| distance_km | Approx. distance to manufacturing site |
| avg_transport_time_days | Average historical transport time |
| avg_transport_cost_eur | Cost per shipment (if available) |

**Reason needed:**  
Helps compute logistics risk + probability of delays + cost sensitivity.

---

## 🟫 5. Additional Optional Data (if SAP or BI can provide)

### (A) Risk Indicators
- political_risk_index (country)
- economic_risk_index
- currency_risk_index
- inflation_rate_country
- macro_events_flag (e.g., elections, strikes, instability)

### (B) Supplier Diversity / Redundancy
- backup_supplier_available? (Boolean)
- supplier_capacity_utilization (%)
- min_order_quantity (MOQ)

### (C) Spend / Cost Insights
- annual_spend_eur (per component per supplier)
- price_variance_vs_last_year (%)

---

## 🟦 6. Expected file outputs (CSV)

The project requires **four clean CSV files**:

1. `components_master.csv`  
2. `suppliers_master.csv`  
3. `supplier_component_relationship.csv`  
4. `logistics_data.csv`

All files must use:
- UTF-8 encoding  
- comma separation  
- consistent naming conventions  
- SAP IDs (no free text inconsistencies)

---

## 🟩 7. How this data will be used

- Unified into a single master table  
- Used for automated risk scoring (Python)  
- Used by AI models to summarize supplier risk  
- Used for dashboards (Power BI / Tableau)  
- Used for alerts (high dependency, contract expiring, geopolitical risks)

---

## 🟧 8. Notes for Data Engineering / BI Team

- Data extraction can be done via SAP queries or existing BI views.  
- Ideally delivered as automated weekly / monthly exports.  
- Confidential fields are NOT required (financial statements, invoices, etc.).  
- All data will be used for supply chain risk mitigation, not audit.

---
