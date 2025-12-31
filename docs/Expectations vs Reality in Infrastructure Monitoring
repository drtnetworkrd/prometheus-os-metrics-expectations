# Expectations vs Reality in Infrastructure Monitoring

There’s a recurring debate in infrastructure monitoring that usually misses the real point.

It’s not about whether a tool *can* collect certain metrics.  
It’s about whether it was *designed* to model them accurately.

## When metrics don’t match reality

Many engineers start with Prometheus exporters for host-level metrics.

On paper, it works:
- CPU usage
- Memory consumption
- Disk I/O

But in practice, you often see this:

- `top` shows 80% CPU usage
- Prometheus dashboards show 40–50%
- You adjust formulas
- You tweak scrape intervals
- You normalize cores, idle time, averages

Eventually, you can get *close enough*.

But the real question becomes:

**Why did this require so much effort?**

## Tool responsibility matters

Prometheus was built around a *metrics-first*, pull-based model.

It excels at:
- service metrics
- application instrumentation
- time-series analysis
- alerting on trends

It was not primarily designed to be a real-time host state observer.

That doesn’t mean it’s “bad” at it.
It means it wasn’t its core responsibility.

## Why some tools feel “easier” for OS metrics

Tools like Zabbix were built with a different mental model:

- hosts as first-class entities
- stateful checks
- OS-level semantics
- immediate interpretation of system data

As a result:
- CPU usage “just makes sense”
- memory behaves as expected
- less formula gymnastics are required

Not because the tool is magic —  
but because the abstraction matches the problem.

## The hammer and the nail

You *can* drive a nail with a rock.
Sometimes it even works.

But that doesn’t make the rock the right tool.

And when something feels unnecessarily hard,  
it’s often a signal that the tool’s model doesn’t align with the job.

## The real takeaway

This isn’t about choosing sides.

It’s about understanding:
- what problem a tool was designed to solve
- what assumptions it makes
- where it fits naturally

Good observability isn’t about forcing everything into one system.

It’s about letting each tool do what it does best.
