# Supply Chain Agent Lab Guide

## Use Case Implementation Guide

This guide provides step-by-step instructions for building and testing a modular supply chain planning system using IBM Watsonx Orchestrate (WXO).

---

## Use Case Summary

The use case demonstrates how multiple specialized agents can coordinate to manage the entire supply chain lifecycle, including:

1. **Demand Forecasting**: Predict product demand based on historical data.

2. **Inventory Evaluation**: Monitor and assess stock levels.

3. **Procurement Decisioning**: Automate vendor selection and purchase order creation.

4. **Logistics Planning**: Optimize delivery routes and timelines.

5. **Compliance Monitoring**: Validate actions against business policies and regulatory requirements.

!!! info "Info"
    This system mirrors real-world workflows in manufacturing, retail, and logistics enterprises where decentralization and automation are key to efficiency.

---

## Example Scenarios

### Scenario 1: End-to-End Order Fulfillment

A user submits a request to fulfill an order of 500 units:

- Forecast Agent checks future demand.
- Inventory Agent checks for stock availability.
- Procurement Agent raises a PO for the shortfall.
- Logistics Agent schedules the delivery.
- Compliance agent checks the valid list of vendors

### Scenario 2: Predictive Planning

- User: "What’s the demand forecast for Product Y next month?"
- Forecast Agent predicts using past sales.
- Inventory Agent alerts on overstock/under-stock.

### Scenario 3: Compliance Check

- User: "Is our supplier list aligned with ISO standards?"
- Compliance Agent checks against policy documents.

---

## Prerequisites

Make sure you've already setup the environment:

- [Lab Environment setup](../../../../lab-environment-setup.md)
- [ADK Installation](https://developer.watson-orchestrate.ibm.com/getting_started/installing){:target="_blank"}

---

## Step 1: Environment Setup

### Create and Activate Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### `requirements.txt`

```text
# Core packages
pandas

# Forecasting
prophet  # Use 'fbprophet' if needed for compatibility

# Date utilities
python-dateutil

```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

### Step 2: **Create project structure**

Create following folder structure -
    
    wxo-agents ---
                  |---agents
                  |---tools
                  |---knowledge_base
                      |---documents
                  |---requirements.txt
                  |---.importAll.sh


---


## Step 3: Define Tool Logic

Each tool file implements the logic invoked by the respective agent.

### tools/compliance_tool.py
Enforces business rules and audits operations.
```python
from ibm_watsonx_orchestrate.agent_builder.tools import tool

@tool(description="Verify supplier compliance based on certification, ESG adherence, and blacklist status.")
def verify_compliance() -> list:
    """
    Check whether suppliers are compliant based on certification, ESG status, and blacklist inclusion.

    Returns:
    - A list of dictionaries with:
        - 'supplier'
        - 'certified'
        - 'blacklisted'
        - 'esg_compliant'
        - 'status' (Approved or Blocked)
    """
    try:
        suppliers_data = [
            {"supplier": "Supplier A", "certified": "Yes", "blacklisted": "No", "esg_compliant": "Yes"},
            {"supplier": "Supplier E", "certified": "Yes", "blacklisted": "No", "esg_compliant": "Yes"},
        ]

        for row in suppliers_data:
            if row["certified"] != "Yes" or row["esg_compliant"] != "Yes" or row["blacklisted"] == "Yes":
                row["status"] = "Blocked"
            else:
                row["status"] = "Approved"

        return suppliers_data
    
    except Exception as e:
        return [{"error": str(e)}]

```

### tools/forecast_tool.py
Forecasts demand for products over time.
```python
from ibm_watsonx_orchestrate.agent_builder.tools import tool
from prophet import Prophet
import pandas as pd

@tool
def generate_sales_forecast(freq: str = 'W', periods: int = 4) -> list:
    """
    Forecast sales using hardcoded data and return predictions.

    Parameters:
    - freq: Frequency of forecast ('W' for weekly)
    - periods: Number of periods to forecast

    Returns:
    - A list of dictionaries with forecast results:
      - 'date'
      - 'predicted_sales'
      - 'lower_bound'
      - 'upper_bound'
    """
    # Hardcoded historical sales data
    data = pd.DataFrame({
        "ds": pd.date_range(start="2025-01-01", periods=10, freq="W"),
        "y": [180, 190, 200, 210, 205, 215, 220, 225, 230, 235]
    })

    model = Prophet()
    model.fit(data)
    future = model.make_future_dataframe(periods=periods, freq=freq)
    forecast = model.predict(future)

    result = forecast.tail(periods)[["ds", "yhat", "yhat_lower", "yhat_upper"]]
    return [
        {
            "date": row["ds"].strftime("%Y-%m-%d"),
            "predicted_sales": round(row["yhat"], 2),
            "lower_bound": round(row["yhat_lower"], 2),
            "upper_bound": round(row["yhat_upper"], 2),
        }
        for _, row in result.iterrows()
    ]

```

### tools/inventory_tool.py
Evaluates and maintains optimal inventory levels.
```python
from ibm_watsonx_orchestrate.agent_builder.tools import tool
import pandas as pd

@tool
def check_inventory_levels() -> list:
    """
    Checks hardcoded inventory levels and flags items that need restocking.

    Returns:
    - A list of dictionaries with keys:
        - 'sku'
        - 'current_stock'
        - 'reorder_level'
        - 'action' ('Restock' or 'OK')
    """
    data = {
        "sku": ["SKU001", "SKU002", "SKU003", "SKU004"],
        "current_stock": [5, 12, 2, 20],
        "reorder_level": [10, 10, 5, 15]
    }
    df = pd.DataFrame(data)
    df["action"] = df.apply(
        lambda row: "Restock" if row["current_stock"] <= row["reorder_level"] else "OK",
        axis=1
    )
    return df[["sku", "current_stock", "reorder_level", "action"]].to_dict(orient="records")

```

### tools/logistics_tool.py
Simulates delivery routes and schedules logistics.
```python
from ibm_watsonx_orchestrate.agent_builder.tools import tool
from datetime import datetime, timedelta

@tool
def plan_deliveries(today: str = None) -> list:
    """
    Generate delivery ETA and priority based on procurement plan.
    
    Returns:
    - A list of dictionaries with:
        - 'sku'
        - 'supplier'
        - 'dispatch_date'
        - 'delivery_eta'
        - 'priority' (High if lead_time_days <= 3, else Normal)
    """
    try:
        # Simulated procurement plan (from previous step)
        procurement_plan = [
            {"sku": "SKU001", "supplier": "Supplier A", "lead_time_days": 3},
            {"sku": "SKU002", "supplier": "Supplier C", "lead_time_days": 5},
            {"sku": "SKU003", "supplier": "Supplier B", "lead_time_days": 2},  # Blocked
        ]

        # Only allow compliant suppliers
        approved_suppliers = {"Supplier A", "Supplier E"}  # From verify_compliance()

        base_date = datetime.strptime(today, "%Y-%m-%d") if today else datetime.today()
        schedule = []

        for row in procurement_plan:
            supplier = row.get("supplier")
            if supplier not in approved_suppliers:
                continue  # Skip blocked suppliers

            try:
                lead_time = int(row["lead_time_days"])
                eta = base_date + timedelta(days=lead_time)
                schedule.append({
                    "sku": row["sku"],
                    "supplier": supplier,
                    "dispatch_date": base_date.strftime("%Y-%m-%d"),
                    "delivery_eta": eta.strftime("%Y-%m-%d"),
                    "priority": "High" if lead_time <= 3 else "Normal"
                })
            except Exception as e:
                schedule.append({
                    "sku": row.get("sku", "Unknown"),
                    "supplier": supplier,
                    "error": f"Failed to calculate ETA: {str(e)}"
                })

        return schedule if schedule else [{"info": "No deliveries scheduled due to compliance filtering."}]

    except Exception as e:
        return [{"error": str(e)}]

```

### tools/procurement_tool.py
Triggers supplier selection and order placements.
```python
from ibm_watsonx_orchestrate.agent_builder.tools import tool

@tool(description="Generate procurement plan by matching SKUs needing restock with the best supplier.")
def generate_procurement_plan() -> list:
    """
    Match SKUs needing restock with the best supplier (based on cost and lead time).

    Returns:
    - List of procurement plans, each with:
        - 'sku'
        - 'quantity_needed'
        - 'supplier'
        - 'lead_time_days'
        - 'unit_cost'
    """
    try:
        # Hardcoded restock data
        restock_data = [
            {"sku": "SKU001", "current_stock": 5, "reorder_level": 15},
            {"sku": "SKU002", "current_stock": 20, "reorder_level": 25},
            {"sku": "SKU003", "current_stock": 2, "reorder_level": 10},
        ]

        # Hardcoded supplier data
        suppliers_data = [
            {"sku": "SKU001", "supplier": "Supplier A", "lead_time_days": 3, "unit_cost": 10.5},
            {"sku": "SKU001", "supplier": "Supplier B", "lead_time_days": 2, "unit_cost": 11.0},
            {"sku": "SKU002", "supplier": "Supplier C", "lead_time_days": 5, "unit_cost": 9.0},
            {"sku": "SKU003", "supplier": "Supplier A", "lead_time_days": 1, "unit_cost": 15.0},
            {"sku": "SKU003", "supplier": "Supplier B", "lead_time_days": 2, "unit_cost": 14.5},
        ]

        plan_rows = []

        for restock in restock_data:
            quantity_needed = restock["reorder_level"] - restock["current_stock"]
            if quantity_needed <= 0:
                continue

            options = [s for s in suppliers_data if s["sku"] == restock["sku"]]
            if options:
                best_option = sorted(options, key=lambda x: (x["unit_cost"], x["lead_time_days"]))[0]
                plan_rows.append({
                    "sku": restock["sku"],
                    "quantity_needed": quantity_needed,
                    "supplier": best_option["supplier"],
                    "lead_time_days": best_option["lead_time_days"],
                    "unit_cost": best_option["unit_cost"],
                })

        return plan_rows

    except Exception as e:
        return [{"error": str(e)}]

```
---

## Step 4: Agent Configuration

Each agent is defined in YAML and linked to a tool that performs a domain-specific function.

### compliance_agent.yaml
Ensures regulatory and operational compliance.
```yaml
spec_version: v1
style: react
name: compliance_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are a compliance agent responsible for validating supplier eligibility.
  Your task is to check vendor certifications, ESG status, and blacklist status before procurement approval.

instructions: >
  Use the `verify_compliance` tool to validate suppliers.
  Only approve suppliers who are certified, not blacklisted, and have ESG compliance marked "Yes".

  Respond in a markdown table with: Supplier, Certified, ESG Compliant, Blacklisted, Status (Approved/Blocked).
  Be strict. If any condition fails, mark supplier as Blocked.

collaborators: []

tools:
  - verify_compliance

```

### controller_agent.yaml
Acts as a central orchestrator and routes tasks to other agents.
```yaml
spec_version: v1
style: react
name: controller_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are the orchestrator agent for supply chain planning. You coordinate forecasting, inventory checks,
  procurement, logistics, and compliance to generate a unified operational plan.

instructions: >
  You are a supply chain orchestration agent that coordinates multiple specialized agents.

  DEFAULT VALUES (use these always unless the user explicitly overrides):
  - SKU: SKU001
  - Forecast frequency: weekly (freq='W')
  - Forecast periods: 4 weeks
  - Supplier: Supplier A
  - Reorder threshold: 100 units
  - Lead time: 7 days

  WORKFLOW STEPS:

  1. FORECAST (Step 1)
     - Delegate to the forecast_agent collaborator
     - Always use freq='W', periods=4 unless user specifies otherwise
     - Default SKU is SKU001

  2. INVENTORY CHECK (Step 2)
     - Delegate to the inventory_agent collaborator
     - Checks all SKUs automatically — no parameters needed
     - Default focus SKU is SKU001

  3. PROCUREMENT (Step 3)
     - Delegate to the procurement_agent collaborator
     - Only run if: inventory shows SKU001 needs restocking OR user explicitly requests it
     - Default supplier selection based on lowest cost and shortest lead time

  4. COMPLIANCE (Step 4)
     - Delegate to the compliance_agent collaborator
     - Only run if: procurement was done OR user explicitly requests it
     - Default supplier to verify: Supplier A

  5. LOGISTICS (Step 5)
     - Delegate to the logistics_agent collaborator
     - Only run if: compliance check passed OR user explicitly requests it
     - Default delivery window: 7 days from dispatch

  EXECUTION MODES:

  Mode A - Single Step: If user asks for one specific step (e.g., "check inventory"), only execute
  that step by delegating to the appropriate collaborator agent using the defaults above.

  Mode B - End-to-End: If user asks for "end to end planning" or "complete cycle" or "run all steps"
  or "next 4 weeks":
     1. Delegate to forecast_agent — SKU001, freq='W', periods=4
     2. Delegate to inventory_agent — check all SKUs
     3. If restocking needed for SKU001, delegate to procurement_agent
     4. If procurement done, delegate to compliance_agent — verify Supplier A
     5. If compliance passed, delegate to logistics_agent — schedule deliveries
     6. Present the complete plan as a unified markdown summary

  CRITICAL RULES:
  - ALWAYS delegate tasks to the appropriate collaborator agent — do NOT call tools directly
  - NEVER ask follow-up questions for missing parameters — always fall back to defaults above
  - ALWAYS proceed with the workflow automatically when conditions are met
  - Present results in clear markdown tables
  - Be concise and action-oriented


collaborators:
  - forecast_agent
  - inventory_agent
  - procurement_agent
  - compliance_agent
  - logistics_agent

tools: []
```

### forecast_agent.yaml
Handles demand forecasting using statistical or ML models.
```yaml
spec_version: v1
style: react
name: forecast_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are a supply chain agent that specializes in **demand forecasting** for retail, pharma, and manufacturing clients.
  Your purpose is to help supply chain planners make better stocking decisions by forecasting demand patterns.

instructions: >
  Always use **weekly frequency** for the next **4 periods** unless the user specifies otherwise. Make a note that one month is 4 weeks. If user asks for a month,then it is for 4 weeks and so on. 
  Forecast future demand using the `generate_sales_forecast` tool. Return the forecast in a **GitHub markdown table** with the following columns: - Date - Forecast Value (yhat) - Confidence Interval (yhat_lower - yhat_upper)
  Avoid explaining how the forecast is calculated. Assume the user is a domain expert. If confidence interval is narrow (upper - lower < 10), mention it's a **high confidence** forecast. Otherwise, note it's a **moderate confidence** forecast.

collaborators: []

tools:
  - generate_sales_forecast
```

### inventory_agent.yaml
Monitors stock levels, generates reorder alerts.
```yaml
spec_version: v1
style: react
name: inventory_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are a supply chain agent that monitors inventory levels across warehouses and SKUs.
  Your job is to identify low stock, stockouts, and flag restocking needs proactively.

instructions: >
  Use the `check_inventory_levels` tool to evaluate current stock levels.
  Respond with a markdown table including SKU, current stock, reorder level, and action (Restock/OK).
  
  Only flag items for restocking if the current stock is less than or equal to the reorder threshold.
  Do not recommend specific vendors – leave that to the ProcurementAgent.

  After identifying SKUs needing restocking, trigger optimization by calling the `optimizer_agent` with `agent_type: "inventory"`.

collaborators: []

tools:
  - check_inventory_levels
```

### logistics_agent.yaml
Plans and simulates transport, routing, and deliveries.
```yaml
spec_version: v1
style: react
name: logistics_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are a supply chain agent responsible for delivery and shipment planning.
  Your role is to schedule and prioritize deliveries based on procurement lead times and urgency.

instructions: >
  Use the `plan_deliveries` tool to generate delivery schedules from the procurement plan.
  Use the supplier lead time to calculate the expected delivery date.
  If today's date is provided, use it to compute the delivery ETA. Otherwise, assume today.

  Respond with a markdown table containing: SKU, Supplier, Dispatch Date, Delivery ETA, Priority (High/Normal).
  Mark items with lead_time <= 3 as High priority.

collaborators: []

tools:
  - plan_deliveries

```

### procurement_agent.yaml
Handles vendor communication and purchase order execution.
```yaml
spec_version: v1
style: react
name: procurement_agent
llm: groq/openai/gpt-oss-120b
description: >
  You are a supply chain agent responsible for procurement decisions.
  You decide which supplier to order from based on stock needs, vendor lead time, and cost.

instructions: >
  Use the `generate_procurement_plan` tool to match SKUs needing restock with the best available supplier.
  Always choose the vendor with the lowest cost and acceptable lead time.

  Respond in a markdown table with columns: SKU, Quantity Needed, Supplier, Lead Time (days), Unit Cost.

  Use internal data — no need to ask the user for SKUs or supplier information.


collaborators: []

tools:
  - generate_procurement_plan
```


---
## Step 5: Register All Tools

This script imports all tools and registers them in your Orchestrate environment.

### `import-all.sh`
```bash
#!/usr/bin/env bash
set -x

# Activate the local environment
orchestrate env activate local

# Resolve absolute path of current script
SCRIPT_DIR=$( cd -- "$( dirname -- "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )

# Import tools
for tool_path in forecast_tool.py inventory_tool.py procurement_tool.py logistics_tool.py compliance_tool.py; do
  orchestrate tools import -k python -f "${SCRIPT_DIR}/tools/${tool_path}" -r "${SCRIPT_DIR}/tools/requirements.txt"
done

# Import agents
for agent_yaml in forecast_agent.yaml inventory_agent.yaml procurement_agent.yaml logistics_agent.yaml compliance_agent.yaml controller_agent.yaml; do
  orchestrate agents import -f "${SCRIPT_DIR}/agents/${agent_yaml}"
done

# (Optional) List everything
orchestrate tools list
orchestrate agents list
orchestrate knowledge-bases list
```
---

## Sample User Questions
Use the controller agent to handle business queries such as:

- "Forecast sales for SKU001 for the next month"
- "We need to restock SKU001 and choose the best vendor."
- "Can you do a end to end planning for the upcoming cycle?"
- "Verify compliance of Supplier A with ESG norms."

---

## Done!

Your WXO-powered multi-agent supply chain simulation is now up and running!

---

## Additional Notes

- Ensure all credentials, endpoints, and tokens are set in environment variables or passed securely.
- Logging and debugging utilities are recommended for production.

---

Feel free to update the guide as your implementation evolves!

!!! success "Conclusion"

    👏 Congratulations on completing the lab! 🎉