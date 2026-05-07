# Site Reliability Engineering (SRE) Fundamentals

## Training Notes with Examples

---

# 1. Service Level Indicators (SLI)

---

# What is an SLI?

A Service Level Indicator (SLI) is a measurable metric used to evaluate service reliability from the user’s perspective.

SLIs answer:

```text id="shyiv0"
“How well is the service performing?”
```

---

# Common SLI Categories

| SLI Type     | Measures                    |
| ------------ | --------------------------- |
| Availability | Is service accessible?      |
| Latency      | How fast is response?       |
| Error Rate   | How many requests fail?     |
| Throughput   | Requests processed          |
| Durability   | Data protection reliability |

---

# Examples of SLIs

| Service            | Example SLI              |
| ------------------ | ------------------------ |
| E-commerce website | Checkout success rate    |
| Streaming app      | Video buffering latency  |
| Banking API        | Transaction success rate |
| Food delivery app  | API response time        |

---

# Example SLI Formula

Availability SLI:

Availability\ SLI = \frac{Successful\ Requests}{Total\ Requests} \times 100

---

# Real Example

If:

* Total Requests = 1,000,000
* Successful Requests = 999,500

Then:

Availability = \frac{999500}{1000000} \times 100 = 99.95%

---

# Important Idea

SLIs should reflect actual user experience.

Bad SLI:

* CPU usage only

Good SLI:

* Successful login rate

---

# 2. Service Level Objectives (SLO)

---

# What is an SLO?

A Service Level Objective (SLO) is the target reliability goal for an SLI.

It defines:

```text id="sqjlwm"
“How reliable should the service be?”
```

---

# Example SLO

```text id="dfas5q"
Login API should be available 99.9% of the time monthly.
```

---

# SLI vs SLO

| SLI                | SLO                 |
| ------------------ | ------------------- |
| Measurement        | Target              |
| Actual performance | Desired performance |

---

# Real Example

| Metric | Value               |
| ------ | ------------------- |
| SLI    | 99.92% uptime       |
| SLO    | 99.9% uptime target |

Result:

* Objective achieved.

---

# Why SLOs Matter

SLOs help:

* Define reliability expectations
* Balance innovation vs stability
* Prevent overengineering

---

# Common SLO Targets

| Service Type             | Typical SLO |
| ------------------------ | ----------- |
| Internal tools           | 99%         |
| Business applications    | 99.9%       |
| Critical banking systems | 99.99%      |
| Cloud providers          | 99.999%     |

---

# Understanding Availability Levels

| Availability | Maximum Downtime/Month |
| ------------ | ---------------------- |
| 99%          | ~7.2 hours             |
| 99.9%        | ~43 minutes            |
| 99.99%       | ~4 minutes             |
| 99.999%      | ~26 seconds            |

---

# 3. Service Level Agreements (SLA)

---

# What is an SLA?

A Service Level Agreement (SLA) is a formal business contract defining service expectations.

SLAs usually include:

* Availability guarantees
* Response times
* Penalties for failures

---

# SLA Example

Cloud provider guarantees:

```text id="icbyuw"
99.95% uptime per month
```

If violated:

* Customer receives service credits.

---

# SLI vs SLO vs SLA

| Concept | Description                |
| ------- | -------------------------- |
| SLI     | Measurement                |
| SLO     | Internal reliability goal  |
| SLA     | Customer-facing commitment |

---

# Real Example

## Streaming Platform

| Item | Example                |
| ---- | ---------------------- |
| SLI  | Video startup latency  |
| SLO  | Startup < 2 seconds    |
| SLA  | 99.9% uptime guarantee |

---

# Important Difference

SLO:

* Engineering target

SLA:

* Legal/business agreement

---

# 4. Error Budgets

---

# What is an Error Budget?

Error budget defines:

```text id="vx4gdl"
“How much failure is acceptable?”
```

It is derived from the SLO.

---

# Example

SLO:

```text id="m5f2v5"
99.9% uptime
```

Allowed failure:

```text id="jlwm4p"
0.1% downtime
```

This 0.1% is the error budget.

---

# Error Budget Formula

Error\ Budget = 100% - SLO

---

# Example Calculation

If SLO is 99.9%:

Error\ Budget = 100% - 99.9% = 0.1%

---

# Why Error Budgets Matter

Error budgets balance:

* Innovation speed
* Reliability

---

# Practical Meaning

If error budget is exhausted:

* Stop releasing risky features
* Focus on stability

---

# Example Scenario

## E-Commerce Platform

SLO:

```text id="0n4z8d"
99.9% uptime
```

Monthly downtime allowed:

```text id="4hqjlwm"
43 minutes
```

If outages exceed 43 minutes:

* Deployment freeze may occur.

---

# 5. Monitoring vs Observability

---

# Monitoring

Monitoring answers:

```text id="jlwm5k"
“What is broken?”
```

It tracks predefined metrics and alerts.

Examples:

* CPU usage alerts
* API failure alerts
* Disk space warnings

---

# Observability

Observability answers:

```text id="jlwm6m"
“Why is it broken?”
```

It helps investigate unknown problems.

---

# Monitoring vs Observability Comparison

| Monitoring        | Observability         |
| ----------------- | --------------------- |
| Known failures    | Unknown failures      |
| Alerting          | Root-cause analysis   |
| Static dashboards | Deep system insights  |
| Threshold-based   | Exploratory debugging |

---

# Real Example

## Monitoring

Alert:

```text id="jlwm7n"
API latency exceeded 5 seconds
```

## Observability

Investigation finds:

* Database lock issue
* Memory exhaustion
* Slow external API

---

# 6. Metrics, Logs, and Traces Basics

These are the three pillars of observability.

---

# 1. Metrics

Numeric measurements over time.

Examples:

* CPU %
* Request count
* Memory usage
* Error rate

---

# Example Metric

```text id="jlwm8o"
API latency = 250ms
```

---

# Characteristics of Metrics

* Lightweight
* Aggregated
* Good for dashboards

---

# 2. Logs

Detailed event records generated by applications.

---

# Example Log

```text id="jlwm9p"
2026-05-07 ERROR Payment failed for order 1234
```

---

# Characteristics of Logs

* Human-readable
* Detailed troubleshooting
* Historical records

---

# 3. Traces

Track request flow across distributed systems.

---

# Example Trace Flow

```text id="jlwm0q"
User Request
    ↓
API Gateway
    ↓
Payment Service
    ↓
Database
```

---

# Why Traces Matter

Modern microservices involve many components.

Tracing helps identify:

* Slow services
* Bottlenecks
* Failed dependencies

---

# Metrics vs Logs vs Traces

| Type    | Best For                     |
| ------- | ---------------------------- |
| Metrics | Monitoring trends            |
| Logs    | Detailed debugging           |
| Traces  | Distributed request tracking |

---

# Popular Observability Tools

| Tool          | Purpose               |
| ------------- | --------------------- |
| Prometheus    | Metrics               |
| Grafana       | Dashboards            |
| ELK Stack     | Logs                  |
| Jaeger        | Distributed tracing   |
| OpenTelemetry | Unified observability |

---

# 7. Reliability vs Availability vs Performance

---

# Reliability

Reliability means:

```text id="jlwm1r"
“System works correctly over time.”
```

Focus:

* Consistency
* Stability

---

# Availability

Availability means:

```text id="jlwm2s"
“Can users access the service?”
```

Even slow systems can still be “available.”

---

# Performance

Performance means:

```text id="jlwm3t"
“How fast and efficient is the service?”
```

---

# Comparison Table

| Concept      | Focus                 |
| ------------ | --------------------- |
| Reliability  | Correctness over time |
| Availability | Accessibility         |
| Performance  | Speed/efficiency      |

---

# Example Scenario

## Banking App

| Situation                   | Meaning          |
| --------------------------- | ---------------- |
| App accessible              | Available        |
| Transactions work correctly | Reliable         |
| Fast transaction processing | Good performance |

---

# 8. Golden Signals

Google SRE introduced four key monitoring signals.

---

# The Four Golden Signals

| Signal     | Meaning                 |
| ---------- | ----------------------- |
| Latency    | Request processing time |
| Traffic    | Demand on system        |
| Errors     | Failed requests         |
| Saturation | Resource exhaustion     |

---

# 1. Latency

Measures response time.

Example:

```text id="jlwm4u"
Checkout API responding in 5 seconds
```

High latency impacts user experience.

---

# 2. Traffic

Measures workload.

Examples:

* Requests per second
* Active users
* Transactions

---

# 3. Errors

Measures failed operations.

Examples:

* HTTP 500 errors
* Database failures
* Timeout errors

---

# 4. Saturation

Measures system capacity usage.

Examples:

* CPU near 100%
* Memory exhaustion
* Full disk usage

---

# Golden Signals Visualization

```text id="jlwm5v"
Users
  ↓
Traffic
  ↓
Application
  ↓
Latency + Errors
  ↓
Infrastructure Saturation
```

---

# 9. Toil vs Engineering Work

---

# What is Toil?

Toil is repetitive manual operational work.

Characteristics:

* Manual
* Repetitive
* No long-term value
* Automatable

---

# Examples of Toil

| Toil Task             | Better Solution   |
| --------------------- | ----------------- |
| Manual server restart | Auto-healing      |
| Manual deployments    | CI/CD             |
| Manual log checks     | Monitoring alerts |

---

# Engineering Work

Engineering work creates long-term improvements.

Examples:

* Automation
* Scalability
* Monitoring systems
* Self-healing infrastructure

---

# SRE Mindset

Goal:

```text id="jlwm6w"
Reduce repetitive operational work through automation.
```

---

# Real Example

## Bad Practice

Engineer manually deploys app daily.

## Better Practice

GitHub Actions automatically deploys application.

---

# 10. Mapping SLIs to User Experience

---

# Why User-Centric SLIs Matter

Infrastructure metrics alone do not reflect user happiness.

Users care about:

* Fast responses
* Successful transactions
* Smooth experience

---

# Bad vs Good SLIs

| Bad SLI      | Good User-Centric SLI  |
| ------------ | ---------------------- |
| CPU usage    | Checkout success rate  |
| Memory usage | Video playback success |
| Disk usage   | Login success latency  |

---

# Example Mapping

## Food Delivery App

| User Experience    | SLI                  |
| ------------------ | -------------------- |
| Fast ordering      | API latency          |
| Successful payment | Payment success rate |
| App accessibility  | Availability         |

---

# Example User Journey

```text id="jlwm7x"
User Opens App
      ↓
Login Works Quickly
      ↓
Order Placement Succeeds
      ↓
Payment Completes
      ↓
Positive User Experience
```

---

# Important Principle

Best SRE metrics reflect:

```text id="jlwm8y"
What users actually experience.
```

---

# Real Enterprise Example

## Streaming Platform

### User Complaint

“Videos buffer too much.”

### Useful SLI

```text id="jlwm9z"
Video startup latency
```

### Not Useful Alone

```text id="jlwm0a"
CPU usage
```

---

# End-to-End SRE Flow

```text id="jlwm1b"
Users Interact with Application
          ↓
SLIs Measure User Experience
          ↓
SLOs Define Reliability Goals
          ↓
Monitoring Detects Problems
          ↓
Observability Finds Root Cause
          ↓
Engineering Improves Reliability
```

---

# Key Takeaways

| Topic               | Important Idea                 |
| ------------------- | ------------------------------ |
| SLI                 | Reliability measurement        |
| SLO                 | Reliability target             |
| SLA                 | Customer commitment            |
| Error Budget        | Allowed failure amount         |
| Monitoring          | Detect known issues            |
| Observability       | Investigate unknown issues     |
| Metrics/Logs/Traces | Observability pillars          |
| Golden Signals      | Core reliability metrics       |
| Toil                | Repetitive manual work         |
| User-Centric SLIs   | Measure actual user experience |
