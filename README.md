# Why Prometheus OS Metrics Don’t Match Operator Expectations

If you’ve ever looked at a Grafana dashboard and thought:

> “This doesn’t match what I’m seeing on the server.”

You’re not alone.

This repository explains **why Prometheus OS-level metrics (CPU, memory, load)** often don’t align with what operators expect from tools like `top`, `htop`, or Task Manager — and why this is usually **not a bug**, but a mismatch of expectations.

---

## The Common Symptom

Typical situations:

- Prometheus shows 10–20% CPU usage, but the server feels overloaded
- Memory usage looks fine in Grafana, yet applications are struggling
- Load average is high, but CPU metrics seem “low”
- Metrics don’t reflect what you see during incidents

This often leads to:
- distrust in metrics
- endless PromQL tweaking
- questioning whether Prometheus is “wrong”

---

## The Important Distinction

Prometheus is **not a real-time system monitor**.

It is:
- pull-based
- sample-driven
- time-series oriented
- designed primarily for **service and workload metrics**

Tools like `top` and `htop`, on the other hand:
- operate on very short time windows
- emphasize instantaneous state
- are optimized for **human operational intuition**

These are fundamentally different perspectives.

---

## Why OS Metrics Feel “Off” in Prometheus

Some common reasons:

### 1. Sampling & Aggregation
Prometheus averages data over time ranges. Short spikes, waits, and contention can disappear inside averages.

### 2. CPU Semantics Are Non-Intuitive
Metrics like `node_cpu_seconds_total` expose raw counters that require interpretation:
- idle vs iowait vs steal
- per-core vs aggregated
- time-based rates vs instantaneous load

Prometheus is precise — but not opinionated.

### 3. PromQL Formulas ≠ Operational Reality
Many “correct” formulas still don’t answer the operator question:

> “Is this host under stress *right now*?”

---

## A Real-World Outcome

Many engineers (myself included) start by trying to force Prometheus to behave like a system monitor:
- exporters
- complex queries
- dashboard tweaks

It works — **to a point**.

But over time, it becomes clear that Prometheus excels at **service-level observability**, not at being the primary source of operational host truth.

---

## Tool Responsibility Matters

In real-world self-hosted setups, tools are often combined intentionally:

- **Prometheus** → service metrics, APIs, workloads, SLOs
- **Zabbix / similar tools** → OS-level and infrastructure monitoring
- **Grafana** → unified visualization layer

This separation avoids forcing one tool to answer questions it wasn’t designed to answer.

---

## This Is Not a Criticism of Prometheus

Prometheus is excellent at what it does.

The problem usually isn’t Prometheus — it’s the assumption that one tool should cover **every observability layer equally well**.

Understanding tool boundaries leads to simpler, more reliable systems.

---

## If You’re Building a Self-Hosted Observability Stack

If you want a practical baseline that:
- separates service metrics from operational host metrics
- avoids common Prometheus pitfalls
- uses each tool where it makes the most sense

I documented a complete, ready-to-run self-hosted observability baseline here:

👉 https://payhip.com/b/gTHjP

---

## Final Thought

Observability isn’t about choosing the “best” tool.

It’s about choosing the **right tool for the question you’re asking**.
