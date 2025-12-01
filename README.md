# 🧭 Sequential Multi-Agent Trip Planning System (Synchronous)

A fully **synchronous, sequential, multi-agent pipeline** that generates end-to-end travel plans using a chain-of-agents architecture.

This project demonstrates how multiple specialized agents collaborate **in sequence**, passing a shared state object as they build a complete trip plan:

1. **Destination Research**
2. **Flight Search**
3. **Accommodation Recommendations**
4. **Itinerary Creation**
5. **Budget Analysis**

Includes a comprehensive **observability system** with traces, logs, and evaluation metrics following **Google ADK Day-1B Agent Architectures**.

---

## 🚀 Features

* ✔️ **Fully synchronous execution** — no async/await required
* ✔️ **Multi-agent sequential processing**
* ✔️ **Shared state architecture** with accumulating context
* ✔️ **Detailed observability system**

  * Execution traces
  * Tool usage logs
  * Agent evaluations
  * JSON export
* ✔️ **Complete trip planning output**, including flights, hotels, itinerary, and budget
* ✔️ **Modular agent design** for easy extension

---

## 📁 Project Structure

```
├── TripPlannerApp.py
├── logs/
│   ├── trip_traces.json
│   └── trip_evaluations.json
└── README.md
```

---

## 🧠 Architecture Overview

### 🔹 Sequential Agent Flow

```
Agent1 → Agent2 → Agent3 → Agent4 → Agent5
```

### 🔹 Shared State: `TripPlanningState`

Tracks and accumulates:

* Destination
* User preferences
* Research results
* Flight search results
* Hotel options
* Full itinerary
* Budget analysis
* Agent order execution
* Timestamps

### 🔹 Observability Layer

Each agent logs:

| Metric        | Description                                   |
| ------------- | --------------------------------------------- |
| Trace logs    | Input, output length, tools used, state delta |
| Evaluations   | Completion rate, response time, quality       |
| Exported JSON | `trip_traces.json`, `trip_evaluations.json`   |
| Log file      | `trip_planning_trace.log`                     |

---

## 🛠️ Installation

### 1. Clone the Repository

```bash
git clone https://github.com/<your-repo>/trip-planner-agents.git
cd trip-planner-agents
```

### 2. Install Dependencies

```bash
pip install -r google-adk
```

### 3. Optional: Set Google API Key

```bash
export GOOGLE_API_KEY="your-key"
```

---

## ▶️ Running the System

Run the main script:

```bash
python TripPlannerApp.py
```

You will see:

* Agent-by-agent execution
* Logs and progress updates
* Final aggregated trip plan
* JSON exports of traces + evaluations

---

## 📊 Example Output

```
🌍 Starting SEQUENTIAL Trip Planning: Tokyo, Japan
[STEP 1/5] Agent1: Research Destination
...
[STEP 5/5] Agent5: Budget Analysis

✅ Sequential pipeline completed successfully!
Agents executed in order:
Agent1_ResearchDestination → Agent2_FindFlights → Agent3_FindAccommodation → Agent4_CreateItinerary → Agent5_BudgetAnalysis

Traces exported to: trip_traces.json
Evaluations exported to: trip_evaluations.json
```

---

## 📂 Generated Logs

| File                      | Description                   |
| ------------------------- | ----------------------------- |
| `trip_traces.json`        | Structured trace logs         |
| `trip_evaluations.json`   | Agent performance evaluations |
| `trip_planning_trace.log` | Full run logs                 |

---

## 🧩 Extending the Pipeline

Add a new agent by defining a class with a static `execute()` method:

```python
class Agent6_SafetyAnalysis:
    @staticmethod
    def execute(state, observability):
        # compute output
        state.update("Agent6_SafetyAnalysis", safety_info=output)
        observability.log_trace(...)
        return output
```

Add it to the pipeline in `SequentialTripPlanner.plan_trip()`.

---

## 🧪 Agent Evaluation

The built-in evaluator scores:

* Task completion
* Information quality
* Tool effectiveness
* Response time
* State consistency

These metrics are auto-logged after each agent run.

---

## 📝 Example Usage

```python
planner = SequentialTripPlanner()

preferences = {
    "duration": "5 days",
    "budget": "moderate",
    "travel_style": "cultural and culinary",
    "interests": ["history", "food"],
    "start_date": "2024-06-01"
}

results = planner.plan_trip("Tokyo, Japan", preferences)

print(results["response"])
```

---

## 📚 Technologies Used

* Python 3.10+
* Google ADK (Agents, LLM Models, Tools, Runners)
* Dataclasses (state modeling)
* Logging + JSON export

---

## 🛡️ License

MIT License — you are free to modify, extend, and integrate this system.

---

## 🙌 Contributing

Contributions are welcome!
Ideas:

* New agents
* Integrations with real APIs (weather, flights, maps)
* Observability dashboards
* LLM-powered summarizers

---
