# ServiceNow / ITIL — Problem Management & Change Management

## Training Notes with Examples

---

# 1. Problem Management

---

# What is a Problem?

In ITIL:

```text id="pm1aa"
A problem is the underlying cause of one or more incidents.
```

---

# Important Difference

| Incident                   | Problem                         |
| -------------------------- | ------------------------------- |
| Service interruption       | Root cause behind interruptions |
| Focus on restoring service | Focus on preventing recurrence  |

---

# Example

## Incident

```text id="pm2bb"
Website crashes during high traffic
```

Restoring service:

* Restart application

---

# Problem

Why did it crash repeatedly?

Root cause investigation begins.

---

# Goal of Problem Management

* Identify root causes
* Prevent recurring incidents
* Improve reliability
* Reduce downtime

---

# Incident vs Problem Workflow

```text id="pm3cc"
Incident Occurs
       ↓
Service Restored
       ↓
Problem Investigation
       ↓
Root Cause Identified
       ↓
Permanent Fix Applied
```

---

# Types of Problems

| Type      | Example                         |
| --------- | ------------------------------- |
| Reactive  | Investigate after outage        |
| Proactive | Analyze trends before incidents |

---

# Reactive Example

```text id="pm4dd"
Repeated database crashes
```

Investigated after multiple incidents.

---

# Proactive Example

Monitoring shows:

```text id="pm5ee"
Increasing memory usage trend
```

Team fixes before outage occurs.

---

# Root Cause Analysis (RCA)

---

# What is RCA?

RCA identifies:

```text id="pm6ff"
The true underlying cause of an issue.
```

---

# Example RCA Flow

```text id="pm7gg"
API Failure
    ↓
Database Timeout
    ↓
Connection Pool Exhausted
    ↓
Misconfigured Scaling
```

Root cause:

```text id="pm8hh"
Incorrect autoscaling configuration
```

---

# Common RCA Techniques

| Technique         | Purpose                  |
| ----------------- | ------------------------ |
| Five Whys         | Repeated “Why?” analysis |
| Fishbone Diagram  | Categorize causes        |
| Log analysis      | Identify failures        |
| Monitoring review | Detect patterns          |

---

# Five Whys Example

Problem:

```text id="pm9ii"
Application crashed
```

Why?

* Out of memory

Why?

* Memory leak

Why?

* Improper cache cleanup

Root cause:

```text id="pm0jj"
Application bug causing memory leak
```

---

# Known Errors

---

# What is a Known Error?

A known error is:

```text id="pm1kk"
A problem with a documented root cause and workaround.
```

---

# Example

Known issue:

```text id="pm2ll"
Application crashes when cache exceeds 2GB
```

Workaround:

```text id="pm3mm"
Restart service every 12 hours
```

Permanent fix still pending.

---

# Known Error Database (KEDB)

Organizations maintain:

* Documented issues
* Workarounds
* Root causes

Benefits:

* Faster incident resolution
* Shared knowledge
* Reduced troubleshooting time

---

# Example KEDB Entry

| Field         | Example         |
| ------------- | --------------- |
| Problem ID    | PRB001245       |
| Root Cause    | Memory leak     |
| Workaround    | Restart service |
| Permanent Fix | Patch planned   |

---

# Benefits of Problem Management

| Benefit                  | Example                |
| ------------------------ | ---------------------- |
| Reduced repeat incidents | Permanent fixes        |
| Faster recovery          | Known workarounds      |
| Better reliability       | Root cause elimination |

---

# Problem Management Example

## E-Commerce Checkout Failures

### Incidents

Repeated payment API outages.

### Problem Investigation

Logs show:

```text id="pm4nn"
Database connections exhausted during traffic spikes
```

### Root Cause

Improper connection pool configuration.

### Known Error

Temporary workaround documented.

### Permanent Fix

Connection pool optimization deployed.

---

# 2. Change Management (Change Enablement)

---

# What is Change Management?

ITIL 4 calls it:

```text id="pm5oo"
Change Enablement
```

Purpose:

* Ensure changes are implemented safely
* Minimize risk
* Reduce outages

---

# What is a Change?

A change is:

```text id="pm6pp"
Addition, modification, or removal of anything that could affect services.
```

---

# Examples of Changes

| Change                 | Example            |
| ---------------------- | ------------------ |
| Application deployment | New API version    |
| Infrastructure update  | Kubernetes upgrade |
| Security patch         | OS patching        |
| Configuration change   | Database settings  |

---

# Why Change Management Matters

Poorly managed changes can cause:

* Downtime
* Security issues
* Failed deployments
* Business disruption

---

# Example

```text id="pm7qq"
Production deployment causes checkout outage
```

Proper change management reduces such risks.

---

# Change Lifecycle

```text id="pm8rr"
Request Change
      ↓
Risk Assessment
      ↓
Approval
      ↓
Implementation
      ↓
Validation
      ↓
Closure
```

---

# 3. Types of Changes

---

# A. Normal Change

Requires:

* Review
* Risk assessment
* Approval

---

# Example

```text id="pm9ss"
Major database version upgrade
```

---

# B. Emergency Change (ECN)

Emergency Change:

```text id="pm0tt"
Urgent change needed to resolve critical issue.
```

---

# Example

```text id="pm1uu"
Critical security vulnerability patch
```

Must be deployed immediately.

---

# Characteristics of Emergency Changes

| Feature        | Example                 |
| -------------- | ----------------------- |
| Fast approval  | Immediate authorization |
| High urgency   | Security risk           |
| Limited review | Minimize delay          |

---

# C. Standard Change

Pre-approved low-risk change.

---

# Example

```text id="pm2vv"
Routine SSL certificate renewal
```

No CAB review needed.

---

# Change Type Comparison

| Type      | Risk            | Approval           |
| --------- | --------------- | ------------------ |
| Standard  | Low             | Pre-approved       |
| Normal    | Medium/High     | CAB approval       |
| Emergency | Critical/Urgent | Emergency approval |

---

# 4. CAB Process (Change Advisory Board)

---

# What is CAB?

CAB stands for:

```text id="pm3ww"
Change Advisory Board
```

A group reviewing important changes.

---

# CAB Responsibilities

| Responsibility     | Example               |
| ------------------ | --------------------- |
| Risk review        | Production deployment |
| Impact analysis    | Business downtime     |
| Approval decisions | Go/No-Go              |

---

# Typical CAB Members

| Role              | Example             |
| ----------------- | ------------------- |
| Operations        | Infrastructure lead |
| Security          | Security engineer   |
| Business          | Product owner       |
| Application teams | Developers          |
| SRE/DevOps        | Reliability review  |

---

# CAB Workflow

```text id="pm4xx"
Change Request
      ↓
Risk Assessment
      ↓
CAB Review
      ↓
Approved / Rejected
      ↓
Implementation
```

---

# Example CAB Review

Change:

```text id="pm5yy"
Kubernetes cluster upgrade
```

CAB reviews:

* Downtime risk
* Rollback plan
* Business impact
* Testing results

---

# Emergency CAB (ECAB)

Used for urgent changes.

Example:

```text id="pm6zz"
Critical production security patch
```

---

# 5. Risk & Impact Assessment

---

# Why Risk Assessment Matters

Changes may affect:

* Availability
* Security
* Performance
* Business operations

---

# Risk Assessment Questions

| Question              | Example                   |
| --------------------- | ------------------------- |
| What can fail?        | Deployment rollback issue |
| Who is impacted?      | Customers                 |
| How severe is impact? | Production outage         |
| Is rollback possible? | Yes                       |

---

# Example Risk Levels

| Risk   | Example              |
| ------ | -------------------- |
| Low    | Documentation update |
| Medium | Minor API deployment |
| High   | Database migration   |

---

# Impact Assessment

Impact evaluates:

```text id="pm7aaa"
How many users/services are affected.
```

---

# Example Impact Levels

| Impact | Example                  |
| ------ | ------------------------ |
| Low    | Internal tool            |
| Medium | Single business service  |
| High   | Entire production system |

---

# Risk Matrix Example

| Impact | Likelihood | Risk     |
| ------ | ---------- | -------- |
| High   | High       | Critical |
| High   | Low        | Medium   |
| Low    | Low        | Low      |

---

# Example

## Database Upgrade

### Risks

* Downtime
* Data corruption
* Performance issues

### Mitigation

* Backup database
* Test in staging
* Rollback plan

---

# 6. Change Models and Workflows

---

# What is a Change Model?

A predefined workflow for handling recurring changes.

---

# Benefits

| Benefit          | Example                   |
| ---------------- | ------------------------- |
| Consistency      | Standard deployment steps |
| Faster approvals | Predefined process        |
| Reduced errors   | Clear validation          |

---

# Example Change Model

## Standard Application Deployment

```text id="pm8bbb"
Code Commit
      ↓
CI/CD Pipeline
      ↓
Automated Testing
      ↓
Approval
      ↓
Deployment
      ↓
Validation
```

---

# Common Workflow Stages

| Stage          | Purpose                |
| -------------- | ---------------------- |
| Request        | Submit change          |
| Assessment     | Evaluate risks         |
| Approval       | CAB authorization      |
| Implementation | Deploy change          |
| Review         | Validate results       |
| Closure        | Complete documentation |

---

# Example Workflow in ServiceNow

```text id="pm9ccc"
Change Request Created
         ↓
Manager Approval
         ↓
CAB Review
         ↓
Deployment Scheduled
         ↓
Implementation
         ↓
Post-Implementation Review
         ↓
Closed
```

---

# DevOps and Modern Change Management

Modern organizations automate change workflows.

---

# Example

Using:

* [GitHub Actions](https://github.com/features/actions?utm_source=chatgpt.com)
* Kubernetes
* Automated testing
* Monitoring

Low-risk deployments can be auto-approved.

---

# CI/CD + Change Management Example

```text id="pm0ddd"
Developer Pushes Code
         ↓
Automated Security Scan
         ↓
Automated Testing
         ↓
Deployment Approval
         ↓
Production Release
         ↓
Monitoring Validation
```

---

# Post-Implementation Review (PIR)

After major changes:

* Review outcomes
* Identify issues
* Document lessons learned

---

# Example PIR Questions

| Question                   | Purpose             |
| -------------------------- | ------------------- |
| Was deployment successful? | Validation          |
| Were incidents caused?     | Risk evaluation     |
| Was rollback needed?       | Process improvement |

---

# Real Enterprise Example

## Banking Platform Deployment

### Change

Core banking API upgrade.

### Process

* Risk assessment completed
* CAB approval obtained
* Deployment tested in staging
* Monitoring enabled

### Result

Successful deployment with zero downtime.

---

# Problem + Change Management Combined Example

```text id="pm1eee"
Repeated Incidents
        ↓
Problem Investigation
        ↓
Root Cause Identified
        ↓
Known Error Created
        ↓
Change Request Submitted
        ↓
CAB Approval
        ↓
Permanent Fix Deployed
```

---

# Key Takeaways

| Topic              | Important Idea                     |
| ------------------ | ---------------------------------- |
| Problem Management | Identify and eliminate root causes |
| RCA                | Understand why failures happen     |
| Known Errors       | Documented problems/workarounds    |
| Change Management  | Implement changes safely           |
| Normal Change      | Standard approval process          |
| Emergency Change   | Urgent critical changes            |
| CAB                | Reviews significant changes        |
| Risk Assessment    | Evaluate potential failures        |
| Change Models      | Standardized workflows             |
| Modern ITSM        | Automation + DevOps integration    |
