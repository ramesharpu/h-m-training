# Incident Management & Reliability Operations

## Training Notes with Examples

---

# 1. Incident Lifecycle

## Detect → Respond → Resolve → Learn

---

# What is an Incident?

An incident is any unplanned event that:

* Reduces service quality
* Causes downtime
* Impacts users
* Threatens business operations

---

# Examples of Incidents

| Incident       | Example                   |
| -------------- | ------------------------- |
| Website outage | Users cannot access app   |
| Slow API       | Checkout takes 20 seconds |
| Database issue | Transactions failing      |
| Security issue | Unauthorized access       |

---

# Incident Lifecycle Overview

```text id="inc1aa"
Detect
   ↓
Respond
   ↓
Resolve
   ↓
Learn
```

---

# Stage 1: Detect

Identify that something is wrong.

Detection sources:

* Monitoring alerts
* Logs
* User complaints
* Automated health checks

---

# Example

```text id="inc2bb"
API error rate exceeds threshold
```

Monitoring system triggers alert.

---

# Stage 2: Respond

Incident responders investigate and mitigate impact.

Activities:

* Acknowledge alert
* Assign responders
* Analyze issue
* Communicate status

---

# Example

```text id="inc3cc"
SRE team joins incident bridge call
```

---

# Stage 3: Resolve

Restore normal service operation.

Possible actions:

* Restart service
* Rollback deployment
* Scale infrastructure
* Fix configuration

---

# Example

```text id="inc4dd"
Rollback faulty deployment
```

---

# Stage 4: Learn

Post-incident analysis to prevent recurrence.

Activities:

* Root Cause Analysis (RCA)
* Documentation
* Process improvements
* Automation

---

# Example

```text id="inc5ee"
Add automated deployment validation
```

---

# Full Incident Lifecycle Example

```text id="inc6ff"
Monitoring detects high API errors
        ↓
On-call engineer investigates
        ↓
Deployment rollback performed
        ↓
Service restored
        ↓
RCA identifies bad configuration
        ↓
CI/CD validation improved
```

---

# 2. Incident Detection and Response

---

# Incident Detection

Goal:

```text id="inc7gg"
Identify issues before users are heavily impacted.
```

---

# Detection Sources

| Source            | Example                |
| ----------------- | ---------------------- |
| Monitoring tools  | CPU alerts             |
| Logs              | Application exceptions |
| Synthetic testing | Failed health checks   |
| User reports      | “Website not loading”  |

---

# Monitoring Example

```text id="inc8hh"
Error rate > 5%
```

Triggers:

* PagerDuty alert
* Slack notification
* Email alert

---

# Incident Severity Levels

| Severity | Impact            |
| -------- | ----------------- |
| SEV-1    | Complete outage   |
| SEV-2    | Major degradation |
| SEV-3    | Minor issue       |
| SEV-4    | Informational     |

---

# Example Severity

| Incident                   | Severity |
| -------------------------- | -------- |
| Entire payment system down | SEV-1    |
| Slow analytics dashboard   | SEV-3    |

---

# Incident Response Process

```text id="inc9ii"
Alert Triggered
      ↓
Engineer Acknowledges
      ↓
Initial Investigation
      ↓
Mitigation Actions
      ↓
Escalation if Needed
      ↓
Service Restored
```

---

# Response Roles

| Role                | Responsibility            |
| ------------------- | ------------------------- |
| Incident Commander  | Coordinates response      |
| SRE/DevOps Engineer | Technical troubleshooting |
| Communications Lead | Updates stakeholders      |
| Developers          | Fix application issue     |

---

# Good Incident Response Practices

* Respond quickly
* Communicate clearly
* Reduce user impact first
* Avoid panic
* Document actions

---

# 3. Root Cause Analysis (RCA) & Blameless Culture

---

# What is RCA?

Root Cause Analysis identifies:

```text id="inc0jj"
Why the incident happened.
```

Goal:

* Prevent recurrence
* Improve systems/processes

---

# Important Principle

Focus on:

```text id="inc1kk"
Systems and processes, not blaming people.
```

---

# Blameless Culture

A blameless culture means:

* Engineers are encouraged to report mistakes
* Learning is prioritized
* Fear is reduced
* Reliability improves

---

# Bad RCA Example

```text id="inc2ll"
“John deployed bad code.”
```

This creates fear.

---

# Good RCA Example

```text id="inc3mm"
Deployment validation failed to detect invalid configuration.
```

Focus:

* Process improvement

---

# Common RCA Questions

| Question                        | Purpose         |
| ------------------------------- | --------------- |
| What happened?                  | Timeline        |
| Why did it happen?              | Root cause      |
| Why wasn’t it detected earlier? | Monitoring gaps |
| How do we prevent recurrence?   | Improvements    |

---

# RCA Techniques

---

# 1. Five Whys

Repeatedly ask:

```text id="inc4nn"
“Why?”
```

---

# Example

Problem:

```text id="inc5oo"
Website crashed
```

Why?

* Database overloaded

Why?

* Too many connections

Why?

* Connection pooling misconfigured

Why?

* Config validation missing

Root Cause:

```text id="inc6pp"
Missing deployment validation
```

---

# Example RCA Structure

| Section          | Example          |
| ---------------- | ---------------- |
| Incident summary | Checkout outage  |
| Timeline         | Events sequence  |
| Root cause       | Config error     |
| Impact           | Payments failed  |
| Resolution       | Rollback         |
| Prevention       | CI/CD validation |

---

# 4. Incident Escalation & Communication

---

# Why Escalation Matters

Some incidents require:

* Additional expertise
* Leadership involvement
* Vendor support

---

# Escalation Example

```text id="inc7qq"
L1 Support
    ↓
SRE Team
    ↓
Platform Engineering
    ↓
Cloud Provider Support
```

---

# Escalation Triggers

| Trigger                    | Example          |
| -------------------------- | ---------------- |
| Incident unresolved        | After 30 minutes |
| Customer impact increasing | Major outage     |
| Security concern           | Data exposure    |

---

# Communication During Incidents

Goals:

* Keep teams informed
* Reduce confusion
* Maintain transparency

---

# Communication Channels

| Tool        | Purpose             |
| ----------- | ------------------- |
| Slack       | Team collaboration  |
| Email       | Stakeholder updates |
| Status page | Customer updates    |
| Zoom/Meet   | War room calls      |

---

# Good Incident Communication

Example:

```text id="inc8rr"
We are investigating elevated API errors affecting checkout.
```

Avoid:

* Blame
* Guessing
* Overpromising

---

# Incident Timeline Example

```text id="inc9ss"
10:00 Alert triggered
10:05 Incident declared
10:10 Engineers engaged
10:20 Root cause identified
10:30 Rollback completed
10:35 Service restored
```

---

# 5. Logging & Troubleshooting Basics

---

# What are Logs?

Logs are records of application/system events.

---

# Example Log

```text id="inc0tt"
2026-05-09 ERROR Payment timeout
```

---

# Types of Logs

| Type             | Example            |
| ---------------- | ------------------ |
| Application logs | API failures       |
| System logs      | Disk errors        |
| Security logs    | Unauthorized login |
| Access logs      | HTTP requests      |

---

# Why Logs Matter

Logs help:

* Debug failures
* Analyze incidents
* Investigate security events

---

# Troubleshooting Workflow

```text id="inc1uu"
Alert
   ↓
Check Metrics
   ↓
View Logs
   ↓
Identify Error
   ↓
Fix Problem
```

---

# Common Troubleshooting Areas

| Area     | Example          |
| -------- | ---------------- |
| CPU      | High utilization |
| Memory   | OOM issues       |
| Disk     | Full filesystem  |
| Network  | Latency          |
| Database | Slow queries     |

---

# Example Log Investigation

```text id="inc2vv"
kubectl logs payment-api
```

Output:

```text id="inc3ww"
Database connection timeout
```

Root cause:

* Database overload

---

# Useful Troubleshooting Tools

| Tool         | Purpose            |
| ------------ | ------------------ |
| kubectl logs | Kubernetes logs    |
| journalctl   | Linux logs         |
| Splunk       | Log analysis       |
| Grafana      | Metrics dashboards |

---

# 6. Performance Bottlenecks

---

# What is a Bottleneck?

A bottleneck is a component limiting system performance.

---

# Common Bottlenecks

| Area     | Example              |
| -------- | -------------------- |
| CPU      | High processing load |
| Memory   | Swapping/OOM         |
| Disk IO  | Slow storage         |
| Database | Slow queries         |
| Network  | Latency/congestion   |

---

# Example Performance Issue

```text id="inc4xx"
Checkout page takes 15 seconds
```

Possible causes:

* Slow database query
* API latency
* Resource saturation

---

# Bottleneck Investigation Flow

```text id="inc5yy"
High Latency Alert
       ↓
Check CPU/Memory
       ↓
Analyze Logs
       ↓
Review Database Queries
       ↓
Identify Slow Component
```

---

# Example Database Bottleneck

Problem:

```text id="inc6zz"
SELECT query taking 12 seconds
```

Solution:

* Add index
* Optimize query
* Scale database

---

# Performance Metrics

| Metric     | Meaning             |
| ---------- | ------------------- |
| Latency    | Response time       |
| Throughput | Requests handled    |
| Error rate | Failed requests     |
| Saturation | Resource exhaustion |

---

# Golden Signals Connection

Performance bottlenecks often appear in:

* Latency
* Saturation
* Error rate

---

# 7. Alerting — Setup & Thresholds

---

# What is Alerting?

Alerting notifies engineers when systems behave abnormally.

---

# Goals of Alerting

* Detect issues early
* Reduce downtime
* Improve response speed

---

# Good Alerts Should Be

| Quality    | Meaning              |
| ---------- | -------------------- |
| Actionable | Engineer can act     |
| Timely     | Early detection      |
| Accurate   | Minimal false alarms |

---

# Bad Alerts

Examples:

* Noisy alerts
* Non-actionable alerts
* Frequent false positives

---

# Example Alert Conditions

| Alert       | Threshold   |
| ----------- | ----------- |
| CPU usage   | > 90%       |
| Error rate  | > 5%        |
| API latency | > 2 seconds |
| Disk usage  | > 85%       |

---

# Example Prometheus Alert

```yaml id="inc7aaa"
- alert: HighErrorRate
  expr: error_rate > 5
  for: 5m
```

Meaning:

* Trigger if error rate exceeds 5% for 5 minutes.

---

# Alert Severity Example

| Severity | Example              |
| -------- | -------------------- |
| Critical | Production outage    |
| Warning  | High memory usage    |
| Info     | Deployment completed |

---

# Alert Fatigue

Too many alerts cause engineers to:

* Ignore notifications
* Miss real incidents

---

# Prevent Alert Fatigue

* Tune thresholds
* Remove noisy alerts
* Use meaningful SLIs
* Aggregate related alerts

---

# Example Alert Flow

```text id="inc8bbb"
Monitoring Detects High Latency
          ↓
Alert Triggered
          ↓
PagerDuty Notification
          ↓
Engineer Investigates
          ↓
Issue Mitigated
```

---

# Real Enterprise Incident Example

## Incident

E-commerce checkout failures during flash sale.

---

# Detection

```text id="inc9ccc"
Error rate exceeded 10%
```

---

# Investigation

Logs show:

```text id="inc0ddd"
Database connection pool exhausted
```

---

# Response

* Increase DB connections
* Scale application pods

---

# Resolution

Checkout restored.

---

# RCA

Root cause:

```text id="inc1eee"
Load testing underestimated traffic spike.
```

---

# Prevention

* Better autoscaling
* Improved load testing
* Alert threshold tuning

---

# End-to-End Incident Management Flow

```text id="inc2fff"
Monitoring Detects Issue
          ↓
Alert Sent to On-Call Engineer
          ↓
Investigation Begins
          ↓
Logs & Metrics Analyzed
          ↓
Root Cause Identified
          ↓
Service Restored
          ↓
RCA Conducted
          ↓
Preventive Improvements Added
```

---

# Key Takeaways

| Topic              | Important Idea                          |
| ------------------ | --------------------------------------- |
| Incident Lifecycle | Detect → Respond → Resolve → Learn      |
| Detection          | Monitoring & alerting                   |
| RCA                | Focus on systems, not blame             |
| Escalation         | Engage right teams quickly              |
| Logs               | Core troubleshooting data               |
| Bottlenecks        | Identify limiting components            |
| Alerting           | Actionable and meaningful notifications |
| Blameless Culture  | Encourages learning and reliability     |
