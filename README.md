# ProcureX – Intel Procurement Decision Agent

ProcureX is an AI-powered procurement decision agent that **compresses supplier databases + order history** into fast, explainable recommendations.  
It is built for **enterprise-scale supply chain decision support** and includes an audit-friendly **Decision Trace & Counterfactual Reasoning** layer to make recommendations trustworthy.

## Why it’s unique (Creative Feature)
### Decision Trace & Counterfactual Reasoning
ProcureX doesn’t just output “Supplier A is best”.
It produces:
- **Decision Trace**: top contributing factors and an auditable explanation
- **Counterfactuals**: “What would need to change for Supplier B to become #1?”

Example:
> “Supplier S2 was not selected because on-time performance and lead time underperform.  
> If S2 improved on-time rate by ~6% (holding other factors constant), it could challenge the top recommendation.”

This turns a typical recommendation demo into a **decision-support system**.
## What it does
1. **Context Compression**: summarizes raw order history into supplier KPIs (delay risk, quality risk, spend, trends)
2. **Constraint-aware Ranking**: filters suppliers by constraints (budget, lead time, risk, MOQ/capacity) and ranks with normalized weighted scoring
3. **Explainability**: exposes normalized score components + decision trace and counterfactuals



## Tech stack
- Python, Pandas, NumPy
- Scikit-learn (normalization utilities)
- Streamlit (fast UI)


## Quickstart

### 1) Setup
```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# Mac/Linux: source .venv/bin/activate
pip install -r requirements.txt
### 2) Run the app
```bash
streamlit run app.py


### 3) Use sample data
In the sidebar, click **“Load sample data”**.



## Data schema

### `data/suppliers.csv`
Required columns:
- supplier_id, name
- cost_per_unit, on_time_rate, defect_rate, lead_time_days, risk_score
Optional (for constraints realism):
- min_order_qty, max_capacity, region

### `data/orders.csv`
Required columns:
- order_id, supplier_id, quantity, order_date
- delivery_delay_days, defect_rate_observed, total_cost
## How scoring works (transparent)
Features are min-max normalized and combined:

- Lower is better: cost, defect_rate, lead_time, risk
- Higher is better: on_time_rate

Score is a weighted sum of normalized components (0..1). Higher is better.  
Weights are user-adjustable and normalized to sum to 1.



## Repo structure

intel-procurex-agent/
├── app.py
├── requirements.txt
├── data/
├── src/
│   ├── analysis.py
│   ├── scoring.py
│   ├── agent.py
│   └── decision_trace.py
├── docs/
└── tests/


## Next improvements (optional)
- Multi-supplier allocation optimization (linear programming)
- Real-time risk feeds (region risk, news-based disruptions)
- ERP/warehouse integration (SQL + dashboards)





