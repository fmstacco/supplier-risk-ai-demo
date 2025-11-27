# Supplier Risk Assessment — Process Flow (AS IS → TO BE)

## 🟦 1. Current Manual Process (AS IS)  
*(Based on what was described — slow, fragmented and highly manual)*

### Step 1 — Identify the component
- Select a component ID.  
- Search across multiple spreadsheets to locate relevant information.

### Step 2 — Find its suppliers
- Look through different Excel files (no single source of truth).  
- Identify which suppliers provide that specific component.  
- Confirm information manually.

### Step 3 — Collect supplier information manually
For each supplier:
- Country and region (looked up manually).  
- Geopolitical risks searched on Google or MedtronicGPT.  
- Check for business risk, instability, news, etc.  
- Past performance checked in different spreadsheets.

### Step 4 — Check logistics manually
- Transport mode.  
- Estimated distance to manufacturing site.  
- Average delivery time.  
- These values come from older spreadsheets or previous notes.

### Step 5 — Review relationship/contract info
- Contract end date.  
- Years of relationship.  
- Price per unit.  
- Lead time (manual lookup).  
- Quality incidents.  
- Delivery delays.

### Step 6 — Compile everything manually
- Copy/paste information into a master Excel.  
- Risk is estimated manually (no scoring model).  
- Repeat the process for the next component.  
- **Entire cycle takes ~5 months for 140 components.**

---

## 🟩 2. Ideal Automated Process (TO BE)  
*(Combining Data Engineering + Automated Risk Scoring + AI)*

### Step 1 — Automated data extraction from SAP
A single query should return:
- Component ID  
- Supplier IDs per component  
- Country & region  
- Contract length & end date  
- Lead time (contractual + historical)  
- Price per unit  
- Delivery performance  
- Quality incidents  
- Transport mode  
- Risk categories (if available)

This should be provided by Data Engineering / BI as structured CSVs or views.

### Step 2 — Unified dataset creation
Merge the following (just like in the fake project):
- `components_master.csv`  
- `suppliers_master.csv`  
- `supplier_component_relationship.csv`  
- `logistics_data.csv`

This produces a clean, single table ready for analysis.

### Step 3 — Automated risk scoring
For each component:
- **Dependency Score** → how many suppliers?  
- **Supplier Reliability Score** → quality, delays, contract age.  
- **Logistics Risk Score** → transport, distance, time.  
- **Geopolitical Risk** → via API or GPT search.  
- **Cost Risk** → price vs. market average.  

Final risk classification:  
**High / Medium / Low**, with full transparency.

### Step 4 — Dashboard + Alerts
- Live dashboard (Power BI / Tableau).  
- Highlight components with **single supplier**.  
- Alerts for:  
  - Contracts expiring soon  
  - Increased lead time  
  - New quality incidents  
  - Rising geopolitical risk  

**5 months → a few minutes.**

---

## 🟧 3. Business impact
- Dramatically reduces analysis time.  
- Eliminates human error.  
- Creates standardisation across the supply chain.  
- Enables early detection of high-risk components.  
- Supports strategic decisions (supplier consolidation, negotiation, dual sourcing).  
- Strengthens resilience and reduces disruption cost.

---

## 🟪 4. High-level architecture (simple)
```text
SAP (source data)
      ↓
Data Engineering (Queries / Views)
      ↓
Unified Dataset (CSV / Database)
      ↓
Risk Scoring (Python / Automated Pipeline)
      ↓
Dashboard & Alerts (Power BI / Tableau)
      ↓
Supply Chain & Leadership consume insights
