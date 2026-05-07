# Practical SRE & Observability Exercises

## Training Notes with Hands-on Examples

---

# Scenario: Sample Application

Assume we have an online shopping application with:

* Login page
* Product catalog
* Cart
* Checkout
* Payment API

We will define:

* SLIs
* Error budgets
* Golden signals
* Observability dashboards
* User journey mapping

---

# 1. Define a User-Joy SLI for the Sample App

---

# What is a User-Joy SLI?

A User-Joy SLI measures something users directly experience.

Goal:

```text id="gx4y2j"
Measure user happiness, not just infrastructure health.
```

---

# Bad SLI Example

```text id="jlwm1c"
CPU utilization = 60%
```

Why bad?

* Users do not care about CPU directly.

---

# Good User-Joy SLIs

| User Action    | SLI                      |
| -------------- | ------------------------ |
| Login          | Login success rate       |
| Product search | Search latency           |
| Checkout       | Checkout completion rate |
| Payment        | Payment API success      |
| Website access | Page load time           |

---

# Example SLI: Page Load Time

Definition:

```text id="jlwm2d"
95% of homepage loads should complete within 2 seconds.
```

---

# Example SLI Formula

Page\ Load\ SLI = \frac{Requests\ Loaded\ Under\ 2s}{Total\ Page\ Requests} \times 100

---

# Example Calculation

If:

* Total requests = 100,000
* Requests under 2 seconds = 98,000

Then:

SLI = \frac{98000}{100000} \times 100 = 98%

---

# Additional User-Centric SLIs

| Feature   | Example SLI                 |
| --------- | --------------------------- |
| Checkout  | 99.95% successful orders    |
| Search    | Average latency < 500ms     |
| Streaming | Buffering rate < 1%         |
| Chat app  | Message delivery < 1 second |

---

# 2. Calculate an Error Budget Based on 99.9% SLO

---

# Step 1: Define SLO

Example:

```text id="jlwm3e"
Application uptime target = 99.9%
```

---

# Step 2: Calculate Error Budget

Formula:

Error\ Budget = 100% - SLO

---

# Example Calculation

For 99.9% SLO:

100% - 99.9% = 0.1%

---

# Monthly Downtime Calculation

30 days/month:

```text id="jlwm4f"
30 × 24 × 60 = 43,200 minutes
```

Allowed downtime:

43200 \times 0.001 = 43.2\ minutes

---

# Final Result

| SLO          | Error Budget               |
| ------------ | -------------------------- |
| 99.9% uptime | ~43 minutes downtime/month |

---

# Meaning of Error Budget

If downtime exceeds 43 minutes:

* Stop risky deployments
* Focus on reliability improvements

---

# Real Enterprise Example

## Streaming Platform

### SLO

```text id="jlwm5g"
99.95% playback availability
```

### Error Budget

```text id="jlwm6h"
~21 minutes downtime/month
```

If exhausted:

* Feature launches paused
* Reliability fixes prioritized

---

# 3. Set Up Splunk Dashboard with Golden Signals

[Splunk Documentation](https://docs.splunk.com/Documentation?utm_source=chatgpt.com)

---

# What is Splunk?

Splunk Enterprise is used for:

* Log analysis
* Monitoring
* Observability
* Dashboard creation

---

# Goal

Create dashboard for:

* Latency
* Traffic
* Errors
* Saturation

These are Google SRE Golden Signals.

---

# Golden Signals Overview

| Signal     | What It Measures |
| ---------- | ---------------- |
| Latency    | Response time    |
| Traffic    | Request volume   |
| Errors     | Failure rate     |
| Saturation | Resource usage   |

---

# Sample Dashboard Layout

```text id="jlwm7i"
+----------------------------------+
| API Latency                      |
+----------------------------------+
| Request Traffic                  |
+----------------------------------+
| Error Rate                       |
+----------------------------------+
| CPU / Memory Saturation          |
+----------------------------------+
```

---

# Step 1: Ingest Application Logs

Example logs:

```text id="jlwm8j"
timestamp=2026-05-07
service=checkout-api
latency=320ms
status=200
cpu=72%
```

---

# Step 2: Create Latency Panel

Example Splunk query:

```spl id="jlwm9k"
index=shopping-app
| stats avg(latency) by service
```

Purpose:

* Average response time by service.

---

# Step 3: Create Traffic Panel

```spl id="jlwm0l"
index=shopping-app
| timechart count by service
```

Purpose:

* Requests over time.

---

# Step 4: Create Error Rate Panel

```spl id="jlwm1m"
index=shopping-app status>=500
| timechart count
```

Purpose:

* Server-side failures.

---

# Step 5: Create Saturation Panel

```spl id="jlwm2n"
index=infra-metrics
| stats avg(cpu), avg(memory)
```

Purpose:

* Infrastructure resource utilization.

---

# Example Dashboard Outcome

| Signal     | Observation                     |
| ---------- | ------------------------------- |
| Latency    | Increased during traffic spikes |
| Traffic    | Peak during sale                |
| Errors     | Payment API failures            |
| Saturation | CPU near 95%                    |

---

# 4. Explore Logs and Traces in a Sample Application

---

# Sample Microservices Application

```text id="jlwm3o"
Frontend
   ↓
API Gateway
   ↓
Order Service
   ↓
Payment Service
   ↓
Database
```

---

# Exploring Logs

---

# Example Application Log

```text id="jlwm4p"
2026-05-07T10:15:23 ERROR Payment timeout order_id=1234
```

---

# What Logs Help Identify

| Problem           | Example             |
| ----------------- | ------------------- |
| Exceptions        | Null pointer        |
| API failures      | Timeout             |
| Security events   | Unauthorized access |
| Deployment issues | Container crash     |

---

# Searching Logs in Splunk

Example:

```spl id="jlwm5q"
index=shopping-app ERROR
```

Purpose:

* Find all error events.

---

# Filtering Payment Failures

```spl id="jlwm6r"
index=shopping-app service=payment ERROR
```

---

# Exploring Traces

---

# What are Traces?

Traces follow requests across services.

---

# Example Request Trace

```text id="jlwm7s"
User Checkout Request
       ↓
Frontend Service
       ↓
Checkout API
       ↓
Payment API
       ↓
Database Query
```

---

# Example Trace Problem

Trace shows:

* Payment service took 8 seconds.

This identifies:

* Root cause of slow checkout.

---

# Observability Flow

```text id="jlwm8t"
Metrics → Detect Problem
Logs → Understand Events
Traces → Find Root Cause
```

---

# Popular Tracing Tools

| Tool          | Purpose               |
| ------------- | --------------------- |
| Jaeger        | Distributed tracing   |
| Zipkin        | Trace visualization   |
| OpenTelemetry | Unified observability |

---

# 5. Map SLI to User Journeys

---

# What is a User Journey?

Sequence of steps users perform.

Example:

```text id="jlwm9u"
Login → Search → Add to Cart → Checkout → Payment
```

---

# Why Mapping Matters

Infrastructure metrics alone are insufficient.

Need to measure:

```text id="jlwm0v"
Real user experience.
```

---

# Example User Journey Mapping

| User Journey Step | User Expectation     | SLI                  |
| ----------------- | -------------------- | -------------------- |
| Login             | Fast access          | Login latency        |
| Product Search    | Quick results        | Search response time |
| Add to Cart       | Successful operation | Cart success rate    |
| Checkout          | Fast checkout        | Checkout latency     |
| Payment           | Secure completion    | Payment success rate |

---

# Example User-Centric SLI Mapping

## Checkout Journey

### User Goal

Complete purchase successfully.

### Important SLIs

* Checkout success rate
* Payment latency
* API availability

---

# Example SLI Mapping Diagram

```text id="jlwm1w"
User Opens Website
        ↓
Homepage Loads Quickly
        ↓
Search Works Fast
        ↓
Checkout Completes
        ↓
Payment Succeeds
        ↓
Positive User Experience
```

---

# Bad vs Good Monitoring Example

| Infrastructure Metric | User-Centric Metric      |
| --------------------- | ------------------------ |
| CPU usage             | Checkout completion rate |
| Memory utilization    | Page load latency        |
| Disk IO               | Search response time     |

---

# Real Enterprise Example

## Video Streaming Platform

### User Complaint

“Videos buffer constantly.”

### Correct SLI

```text id="jlwm2x"
Video startup latency
```

### Incorrect Sole Focus

```text id="jlwm3y"
Server CPU utilization
```

---

# Example End-to-End SRE Workflow

```text id="jlwm4z"
Users Experience Slow Checkout
          ↓
SLI Detects High Checkout Latency
          ↓
Monitoring Triggers Alert
          ↓
Logs Show Payment Errors
          ↓
Trace Identifies Slow Database Query
          ↓
Engineering Optimizes Query
          ↓
User Experience Improves
```

---

# Best Practices

| Best Practice               | Reason                             |
| --------------------------- | ---------------------------------- |
| Use user-focused SLIs       | Reflect actual experience          |
| Track golden signals        | Core reliability visibility        |
| Combine metrics/logs/traces | Better troubleshooting             |
| Use dashboards              | Centralized observability          |
| Define error budgets        | Balance reliability and innovation |

---

# Key Takeaways

| Topic                | Important Idea                       |
| -------------------- | ------------------------------------ |
| User-Joy SLI         | Measure actual user happiness        |
| Error Budget         | Allowed downtime from SLO            |
| Golden Signals       | Latency, Traffic, Errors, Saturation |
| Splunk Dashboards    | Visualize reliability metrics        |
| Logs                 | Detailed event history               |
| Traces               | Request flow analysis                |
| User Journey Mapping | Align SLIs with real usage           |
