# ServiceNow — Incident Management Module

## Training Notes with Examples

---

# 1. Introduction to Incident Management in ServiceNow

---

# What is an Incident?

An incident is:

```text id="sn1aa"
An unplanned interruption or reduction in the quality of an IT service.
```

---

# Examples of Incidents

| Incident         | Example                         |
| ---------------- | ------------------------------- |
| Website outage   | Users cannot access application |
| Login failure    | Authentication not working      |
| Slow application | API latency very high           |
| Email issue      | Corporate mail unavailable      |

---

# Goal of Incident Management

Restore normal service:

* Quickly
* Efficiently
* With minimal business impact

---

# What is ServiceNow?

[ServiceNow Official Website](https://www.servicenow.com/?utm_source=chatgpt.com)

ServiceNow is an enterprise IT Service Management (ITSM) platform used for:

* Incident management
* Change management
* Problem management
* Asset management
* Workflow automation

---

# ServiceNow Incident Module

The Incident module helps organizations:

* Track issues
* Assign work
* Monitor SLAs
* Escalate problems
* Improve support operations

---

# Incident Lifecycle in ServiceNow

```text id="sn2bb"
Incident Created
       ↓
Assigned
       ↓
Investigated
       ↓
Resolved
       ↓
Closed
```

---

# Real Example

## E-Commerce Website

Issue:

```text id="sn3cc"
Checkout API returning 500 errors
```

ServiceNow incident created to:

* Track outage
* Assign SRE team
* Monitor resolution
* Communicate updates

---

# 2. Incident Module Overview

---

# Purpose of the Incident Module

The Incident module centralizes:

* Incident tracking
* Support workflows
* Escalation processes
* SLA monitoring

---

# Main Features

| Feature              | Purpose                     |
| -------------------- | --------------------------- |
| Incident records     | Store issue details         |
| Assignment groups    | Route incidents             |
| Priority management  | Determine urgency           |
| SLA tracking         | Measure response/resolution |
| Escalation workflows | Handle unresolved issues    |
| Notifications        | Alert teams                 |

---

# Typical Incident Record Fields

| Field             | Example             |
| ----------------- | ------------------- |
| Incident Number   | INC001234           |
| Short Description | API unavailable     |
| Category          | Network/Application |
| Priority          | P1                  |
| Assignment Group  | SRE Team            |
| State             | In Progress         |
| SLA               | 30-minute response  |

---

# ServiceNow Incident Dashboard

Support teams can monitor:

* Open incidents
* Critical outages
* SLA breaches
* Escalated tickets

---

# Example Incident Flow

```text id="sn4dd"
Monitoring Alert
       ↓
ServiceNow Incident Created
       ↓
Assigned to Team
       ↓
Investigation Begins
       ↓
Issue Resolved
       ↓
Incident Closed
```

---

# 3. Creating and Logging Incidents

---

# Ways to Create Incidents

| Method                 | Example                     |
| ---------------------- | --------------------------- |
| Manual creation        | Helpdesk logs ticket        |
| Email integration      | User sends support email    |
| Monitoring integration | Splunk/Prometheus alert     |
| API integration        | Automated incident creation |
| Self-service portal    | User submits issue          |

---

# Manual Incident Creation

Typical steps:

1. Open Incident module
2. Click “Create New”
3. Enter issue details
4. Assign category/priority
5. Save incident

---

# Example Incident

| Field             | Value               |
| ----------------- | ------------------- |
| Short Description | Payment API failing |
| Category          | Application         |
| Priority          | P1                  |
| Impact            | High                |
| Urgency           | High                |

---

# Example Incident Record

```text id="sn5ee"
INC001245
Payment service unavailable for users
```

---

# Best Practices for Logging Incidents

Include:

* Clear description
* Error messages
* Affected systems
* Impact details
* Steps to reproduce

---

# Bad Example

```text id="sn6ff"
“Application broken”
```

Too vague.

---

# Good Example

```text id="sn7gg"
Users receive HTTP 500 error during checkout after deployment.
```

---

# Automated Incident Creation

Modern monitoring tools integrate with ServiceNow.

---

# Example Integration

```text id="sn8hh"
Prometheus Alert
       ↓
Webhook
       ↓
ServiceNow Incident Automatically Created
```

---

# Benefits of Automation

| Benefit               | Example                   |
| --------------------- | ------------------------- |
| Faster response       | Immediate ticket creation |
| Reduced manual effort | Monitoring integration    |
| Better accuracy       | Automated incident data   |

---

# 4. Assignment, Categorization, and Prioritization

---

# A. Assignment

Incidents must be routed to the correct team.

---

# Assignment Groups Example

| Team          | Responsibility        |
| ------------- | --------------------- |
| Network Team  | Connectivity issues   |
| Database Team | DB failures           |
| SRE Team      | Reliability incidents |
| Security Team | Security alerts       |

---

# Example

```text id="sn9ii"
Database connection failure
→ Assigned to Database Team
```

---

# Automatic Assignment

ServiceNow can automatically assign tickets based on:

* Category
* Keywords
* CI (Configuration Item)
* Business rules

---

# Example Workflow

```text id="sn0jj"
Application Issue
      ↓
Category = Application
      ↓
Assigned to Application Support Team
```

---

# B. Categorization

Categorization helps:

* Organize incidents
* Route tickets
* Generate reports

---

# Common Categories

| Category    | Example             |
| ----------- | ------------------- |
| Network     | DNS failure         |
| Application | API crash           |
| Hardware    | Server failure      |
| Security    | Unauthorized access |

---

# Example

```text id="sn1kk"
Category: Network
Subcategory: DNS
```

---

# Why Categorization Matters

Benefits:

* Faster routing
* Better analytics
* Trend identification

---

# C. Prioritization

Priority determines:

```text id="sn2ll"
How quickly the incident must be handled.
```

---

# Priority Calculation

Usually based on:

* Impact
* Urgency

---

# Priority Matrix

| Impact | Urgency | Priority |
| ------ | ------- | -------- |
| High   | High    | P1       |
| High   | Medium  | P2       |
| Medium | Medium  | P3       |
| Low    | Low     | P4       |

---

# Example Priorities

| Incident                 | Priority |
| ------------------------ | -------- |
| Entire production outage | P1       |
| Minor UI bug             | P4       |
| Slow API response        | P2       |

---

# P1 Example

```text id="sn3mm"
Checkout service unavailable globally
```

Requires immediate response.

---

# 5. Incident States and SLAs

---

# Incident States

Incident states show the current status of the ticket.

---

# Common Incident States

| State       | Meaning               |
| ----------- | --------------------- |
| New         | Incident created      |
| Assigned    | Team assigned         |
| In Progress | Investigation ongoing |
| On Hold     | Waiting for input     |
| Resolved    | Fix implemented       |
| Closed      | Incident completed    |

---

# State Flow Example

```text id="sn4nn"
New
 ↓
Assigned
 ↓
In Progress
 ↓
Resolved
 ↓
Closed
```

---

# Example Scenario

## Database Outage

| State       | Action                    |
| ----------- | ------------------------- |
| New         | Alert created incident    |
| Assigned    | Routed to DBA team        |
| In Progress | Engineers troubleshooting |
| Resolved    | DB restarted              |
| Closed      | Validation completed      |

---

# What is SLA?

SLA stands for:

```text id="sn5oo"
Service Level Agreement
```

Defines expected service performance.

---

# SLA Examples

| SLA Type         | Example                |
| ---------------- | ---------------------- |
| Response SLA     | Respond within 15 mins |
| Resolution SLA   | Resolve within 2 hours |
| Availability SLA | 99.9% uptime           |

---

# SLA Tracking in ServiceNow

ServiceNow automatically tracks:

* Response times
* Resolution times
* SLA breaches

---

# Example

```text id="sn6pp"
P1 incidents must be acknowledged within 10 minutes.
```

---

# SLA Breach Example

```text id="sn7qq"
Incident unresolved after SLA deadline
```

Triggers escalation.

---

# SLA Dashboard Example

Teams monitor:

* Open P1 incidents
* Breached SLAs
* Average resolution time

---

# Why SLAs Matter

SLAs help:

* Measure support performance
* Improve accountability
* Ensure business expectations

---

# 6. Escalation Workflows

---

# What is Escalation?

Escalation means:

```text id="sn8rr"
Increasing attention or involvement for unresolved incidents.
```

---

# Why Escalation is Needed

Some incidents:

* Become critical
* Need expert involvement
* Risk SLA breaches

---

# Types of Escalation

| Type                    | Example                    |
| ----------------------- | -------------------------- |
| Functional escalation   | Assign to higher expertise |
| Hierarchical escalation | Notify management          |
| Automated escalation    | Triggered by SLA breach    |

---

# Example Escalation Flow

```text id="sn9ss"
L1 Support
    ↓
L2 Engineering
    ↓
SRE Team
    ↓
Management Escalation
```

---

# Functional Escalation Example

Issue:

```text id="sn0tt"
Kubernetes cluster failure
```

Escalated from:

* Helpdesk
  → SRE Engineering Team

---

# SLA-Based Escalation

If:

```text id="sn1uu"
Incident not resolved within SLA
```

Then:

* Notifications sent
* Priority increased
* Managers alerted

---

# Example Workflow

```text id="sn2vv"
Incident Created
       ↓
No Response for 15 Minutes
       ↓
Automatic Escalation Triggered
       ↓
Manager Notification Sent
```

---

# Major Incident Management

Critical incidents may trigger:

* War room calls
* Incident commander assignment
* Executive communication

---

# P1 Incident Example

```text id="sn3ww"
Online banking platform outage
```

Actions:

* Immediate escalation
* Multiple teams engaged
* Status page updated

---

# Escalation Best Practices

| Best Practice           | Reason              |
| ----------------------- | ------------------- |
| Define escalation paths | Faster resolution   |
| Automate notifications  | Reduce delays       |
| Monitor SLA breaches    | Improve reliability |
| Use clear priorities    | Avoid confusion     |

---

# Real Enterprise Example

## E-Commerce Outage

### Detection

Monitoring detects:

```text id="sn4xx"
Checkout API failures
```

---

# ServiceNow Workflow

```text id="sn5yy"
Monitoring Alert
      ↓
Incident Created Automatically
      ↓
Assigned to SRE Team
      ↓
Priority Set to P1
      ↓
SLA Timer Starts
      ↓
Escalation Triggered After 10 Minutes
      ↓
Rollback Performed
      ↓
Incident Resolved
```

---

# Integration with Modern Tools

ServiceNow commonly integrates with:

* [PagerDuty](https://www.pagerduty.com/?utm_source=chatgpt.com)
* [Splunk](https://www.splunk.com/?utm_source=chatgpt.com)
* [Datadog](https://www.datadoghq.com/?utm_source=chatgpt.com)
* [GitHub](https://github.com/?utm_source=chatgpt.com)
* Kubernetes

---

# Modern Incident Workflow Example

```text id="sn6zz"
Application Failure
        ↓
Prometheus Alert
        ↓
ServiceNow Incident
        ↓
PagerDuty Notification
        ↓
SRE Investigation
        ↓
Resolution
        ↓
RCA Documented
```

---

# Key Takeaways

| Topic            | Important Idea                             |
| ---------------- | ------------------------------------------ |
| Incident Module  | Centralized incident tracking              |
| Incident Logging | Record issues clearly                      |
| Assignment       | Route incidents to correct teams           |
| Categorization   | Organize and analyze tickets               |
| Prioritization   | Determine urgency                          |
| Incident States  | Track lifecycle progress                   |
| SLA              | Defines expected response/resolution       |
| Escalation       | Handle unresolved critical incidents       |
| Automation       | Faster and more accurate incident response |
