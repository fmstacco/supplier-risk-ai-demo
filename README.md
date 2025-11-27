# 🏭 Supplier Risk Assessment — AI & Data Science Demo Project

This repository contains a fully simulated end-to-end project demonstrating how supplier risk assessment  
can be automated using **Data Engineering**, **Python**, and **AI-assisted analysis**.

Although the data is fake, the workflow reflects how a real Supply Chain / Operations team  
in a large manufacturing company could significantly reduce manual effort (currently ~5 months)  
and gain faster visibility into supply risks.

---

## 📌 1. Project Goal

To build a prototype capable of:

- Consolidating supplier and component data from multiple sources  
- Computing dependency and performance-based risk scores  
- Highlighting components with *single-source vulnerability*  
- Accelerating the analysis that is currently done manually  
- Enabling future integration with dashboards or AI tools  

The idea is to show how automation + structured data → **faster, safer decisions**.

---

## 🧩 2. Business Problem (Context)

Manufacturing operations depend on ~140 components supplied by different suppliers worldwide.  
Currently, evaluating the risk for each component and its suppliers requires:

- Checking multiple scattered spreadsheets  
- Searching external sources for geopolitical or business risk  
- Reviewing delivery, lead time, and quality performance manually  
- Compiling everything into a master Excel  

⏳ **This process takes ~5 months.**

The objective is to reduce this dramatically using data consolidation + automated scoring.

---

## 🗂️ 3. Repository Structure

```text
supplier-risk-ai-demo/
├── data/
│   ├── components_master.csv
│   ├── suppliers_master.csv
│   ├── supplier_component_relationship.csv
│   └── logistics_data.csv
├── notebooks/
│   └── supplier_risk_demo.ipynb
├── docs/
│   ├── process_flow.md
│   └── data_requirements.md
└── README.md

## 📄 4. Documentation

### **✔️ Current vs Ideal Process**
`docs/process_flow.md`  
A clear description of the **manual process (AS IS)** and the **automated solution (TO BE)**.

### **✔️ Required Fields for SAP Queries / BI Extraction**
`docs/data_requirements.md`  
A detailed list of all data fields needed to enable automated scoring.

---

## 📊 5. Data Model (Simulated)

### 1. Components (`components_master.csv`)
- Component ID  
- Name  
- Category  
- Annual usage  
- Criticality  

### 2. Suppliers (`suppliers_master.csv`)
- Supplier ID  
- Name  
- Country / Region  
- Geo-risk  
- Financial rating  

### 3. Supplier–Component Relationship  
- Price per unit  
- Lead time  
- Contract dates  
- Quality incidents  
- Delivery delays  
- On-time rate  

### 4. Logistics  
- Transport mode  
- Distance  
- Average transport time  
- Cost  

---

## ⚙️ 6. Pipeline Overview

### **1 — Data Loading**
Load CSVs directly from GitHub into the notebook.

### **2 — Data Merging**
Merge components + suppliers + logistics + performance into a unified table.

### **3 — Basic Rule-Based Risk Classification**
Includes:
- Dependency score  
- Supplier reliability score  
- Logistics score  
- Simple risk-level classification  

### **4 — Preparation for Future AI Layer**
Once the structured dataset exists, AI tools can:
- Summarize risk per component  
- Flag geopolitical issues  
- Compare human vs AI assessment  
- Suggest dual sourcing strategies  

---

## 🏗️ 7. High-Level Architecture

```text
SAP / BI (source queries)
        ↓
Data Engineering (CSV / views)
        ↓
Python Pipeline (risk scoring)
        ↓
AI Layer (optional)
        ↓
Dashboard / Alerts (Power BI, Tableau)

## ▶️ 8. How to Run

To load CSVs directly from GitHub in your notebook:

```python
import pandas as pd

components = pd.read_csv("https://raw.githubusercontent.com/fmstacco/supplier-risk-ai-demo/main/data/components_master.csv")
suppliers = pd.read_csv("https://raw.githubusercontent.com/fmstacco/supplier-risk-ai-demo/main/data/suppliers_master.csv")
relationship = pd.read_csv("https://raw.githubusercontent.com/fmstacco/supplier-risk-ai-demo/main/data/supplier_component_relationship.csv")
logistics = pd.read_csv("https://raw.githubusercontent.com/fmstacco/supplier-risk-ai-demo/main/data/logistics_data.csv")

---

## ✅ **Item 9 — Next Steps (Roadmap)**
```markdown
## 🚀 9. Next Steps (Roadmap)

- Extend the risk scoring model (financial, geopolitical, capacity)
- Build a Power BI / Tableau dashboard
- Add AI-generated supplier and component summaries
- Add anomaly detection on delivery performance
- Prepare a business presentation for leadership

## 💬 10. Notes

- Entire project uses **fake, simulated data**
- Developed purely for learning and demonstration
- Inspired by real supply chain challenges, but not linked to any confidential information
