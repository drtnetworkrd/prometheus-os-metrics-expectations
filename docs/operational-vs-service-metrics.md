# Operational Metrics vs Service Metrics  
## Choosing the Right Tool for the Question You’re Asking

One of the most common sources of confusion in observability setups isn’t tooling —  
it’s **mixing different kinds of questions and expecting one metric system to answer all of them**.

This document clarifies the difference between **service metrics** and **operational metrics**, and why separating them leads to simpler, more reliable observability.

---

## The Question Operators Actually Ask

Most operational confusion starts with a simple question:

> **“Is this system healthy right now?”**

This sounds straightforward, but it hides multiple layers of meaning.

Depending on context, you might really be asking:
- Are requests succeeding?
- Is latency acceptable?
- Is the host under resource pressure?
- Is the system about to fail?

These are **not the same question**, and they should not be answered with the same metrics.

---

## Service Metrics

Service metrics describe **how a service behaves from the outside**.

Typical examples:
- request rate
- latency
- error rate
- saturation
- SLO / SLI indicators

Characteristics:
- event-driven
- time-series friendly
- statistically meaningful over windows
- optimized for trends and alerting

These metrics answer questions like:
- *“Are users affected?”*
- *“Is performance degrading?”*
- *“Are we meeting our objectives?”*

**Prometheus excels here.**  
It was designed for this exact class of problems.

---

## Operational Metrics

Operational metrics describe **the state and pressure of a system itself**.

Typical examples:
- CPU pressure
- memory contention
- swap usage
- IO wait
- filesystem state
- host availability

Characteristics:
- state-oriented
- closer to OS semantics
- often interpreted by humans
- concerned with *capacity and stress*, not trends

These metrics answer questions like:
- *“Is this host under stress?”*
- *“Are resources constrained?”*
- *“Is this system stable right now?”*

Agent-based monitoring systems (such as Zabbix and similar tools) are naturally aligned with this layer.

---

## Why Mixing These Creates Confusion

Problems arise when:
- service-oriented metrics are used to infer host health
- averaged time-series are expected to reflect instantaneous system state
- dashboards try to answer multiple question types at once

Common outcomes:
- CPU “looks low” while systems feel overloaded
- memory metrics seem fine while applications struggle
- operators lose trust in dashboards
- increasingly complex queries try to compensate

This is usually not a tooling failure —  
it’s a **responsibility mismatch**.

---

## A Practical Mental Model

Before choosing a metric source, ask:

> **“What question am I trying to answer?”**

- If the question is about **service behavior**, use service metrics.
- If the question is about **system state**, use operational metrics.
- If the question mixes both, separate the views.

Observability becomes simpler when tools are allowed to do what they’re best at.

---

## Real-World Observability Is Layered

In many self-hosted environments, effective observability stacks naturally separate concerns:

- Service metrics for application behavior
- Operational metrics for host and infrastructure state
- Logs for event-level detail
- Visualization layers to unify context

This is not overengineering — it’s clarity.

---

## Closing Thought

Observability is not about forcing one tool to answer every question.

It’s about:
- understanding the nature of the question
- choosing the right signal
- and trusting tools within their intended scope

---

*This separation of responsibilities is the same principle used in the self-hosted observability baseline documented here:*  
👉 https://payhip.com/b/gTHjP
