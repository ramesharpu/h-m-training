# ITIL 4 — Service Value System (SVS) & Silos

## Training Notes with Examples

---

# 1. Service Value System (SVS)

---

# What is the Service Value System (SVS)?

The Service Value System (SVS) is the core operating model of ITIL 4.

It explains:

```text id="svs1aa"
How all organizational components work together to create value.
```

---

# Simple Explanation

The SVS helps organizations:

* Deliver services efficiently
* Align IT with business goals
* Improve collaboration
* Continuously create value

---

# Main Goal of SVS

Convert:

```text id="svs2bb"
Demand and opportunities
        ↓
Into value
```

---

# SVS High-Level Flow

```text id="svs3cc"
Opportunity / Demand
          ↓
Service Value System
          ↓
Value
```

---

# Why SVS is Important

Modern IT environments are complex:

* Cloud
* Kubernetes
* DevOps
* CI/CD
* Microservices
* Third-party services

SVS provides:

* Coordination
* Governance
* Collaboration
* Continuous improvement

---

# Example

## E-Commerce Platform

Customer demand:

```text id="svs4dd"
Fast and reliable online shopping
```

SVS helps coordinate:

* Developers
* Operations
* Security
* Monitoring
* Incident management

to deliver business value.

---

# Components of the SVS

ITIL 4 SVS has five major components:

| Component             | Purpose                       |
| --------------------- | ----------------------------- |
| Guiding Principles    | Recommendations for decisions |
| Governance            | Direction and control         |
| Service Value Chain   | Operational workflow          |
| Practices             | Organizational capabilities   |
| Continual Improvement | Ongoing optimization          |

---

# SVS Structure

```text id="svs5ee"
Guiding Principles
        ↓
Governance
        ↓
Service Value Chain
        ↓
Practices
        ↓
Continual Improvement
```

---

# 2. Guiding Principles

---

# What are Guiding Principles?

Recommendations that guide:

* Decisions
* Behaviors
* Improvements

across the organization.

---

# ITIL 4 Guiding Principles

| Principle                          | Meaning                      |
| ---------------------------------- | ---------------------------- |
| Focus on value                     | Deliver business value       |
| Start where you are                | Use existing capabilities    |
| Progress iteratively               | Improve gradually            |
| Collaborate and promote visibility | Work transparently           |
| Think holistically                 | Consider the whole system    |
| Keep it simple and practical       | Avoid unnecessary complexity |
| Optimize and automate              | Improve efficiency           |

---

# Example

## CI/CD Improvement

Instead of rebuilding everything:

```text id="svs6ff"
Start with existing pipeline and improve incrementally.
```

---

# 3. Governance

---

# What is Governance?

Governance ensures:

```text id="svs7gg"
The organization is directed and controlled properly.
```

---

# Governance Responsibilities

| Area                  | Example                 |
| --------------------- | ----------------------- |
| Strategic direction   | Cloud adoption          |
| Risk management       | Security policies       |
| Compliance            | Regulatory requirements |
| Performance oversight | SLA monitoring          |

---

# Example

## Banking System

Governance ensures:

* Secure deployments
* Compliance with regulations
* Risk-controlled changes

---

# Governance Flow

```text id="svs8hh"
Business Objectives
        ↓
Policies & Controls
        ↓
Operational Execution
```

---

# 4. Service Value Chain

---

# What is the Service Value Chain?

The operational core of the SVS.

Defines:

```text id="svs9ii"
How activities work together to create value.
```

---

# Six Value Chain Activities

| Activity            | Purpose                   |
| ------------------- | ------------------------- |
| Plan                | Strategic planning        |
| Improve             | Continuous optimization   |
| Engage              | Stakeholder communication |
| Design & Transition | Build/release services    |
| Obtain/Build        | Develop components        |
| Deliver & Support   | Operate services          |

---

# Value Chain Example

```text id="svs0jj"
Plan
  ↓
Build Application
  ↓
Deploy via CI/CD
  ↓
Monitor Service
  ↓
Improve Reliability
```

---

# Real DevOps Example

```text id="svs1kk"
Developer Pushes Code
         ↓
GitHub Actions CI/CD
         ↓
Docker Image Built
         ↓
Kubernetes Deployment
         ↓
Monitoring & Alerts
         ↓
User Receives Service
```

---

# 5. ITIL Practices

---

# What are Practices?

Practices are organizational capabilities that help perform work effectively.

ITIL 4 replaced:

```text id="svs2ll"
“Processes”
```

with:

```text id="svs3mm"
“Practices”
```

because modern IT needs flexibility.

---

# Common ITIL Practices

| Practice                      | Purpose                  |
| ----------------------------- | ------------------------ |
| Incident Management           | Restore service quickly  |
| Problem Management            | Prevent recurring issues |
| Change Enablement             | Safe deployments         |
| Monitoring & Event Management | Detect issues            |
| Service Desk                  | User support             |

---

# Example

## Incident Management

Monitoring detects outage:

```text id="svs4nn"
High API error rate
```

Incident practice coordinates:

* Investigation
* Recovery
* Communication

---

# 6. Continual Improvement

---

# What is Continual Improvement?

Continuous effort to:

* Improve services
* Optimize processes
* Reduce risks
* Increase value

---

# Continual Improvement Cycle

```text id="svs5oo"
Assess
   ↓
Plan
   ↓
Improve
   ↓
Measure
   ↓
Repeat
```

---

# Example

## Incident Reduction

Problem:

```text id="svs6pp"
Frequent deployment failures
```

Improvement:

* Add automated testing
* Improve rollback automation

Result:

* Fewer incidents

---

# Benefits of Continual Improvement

| Benefit                  | Example               |
| ------------------------ | --------------------- |
| Better reliability       | Reduced outages       |
| Faster deployments       | CI/CD optimization    |
| Improved user experience | Faster response times |
| Lower costs              | Automation            |

---

# 7. How SVS Works Together

---

# End-to-End Example

## Cloud-Native Application

---

# Step 1 — Demand

Users need:

```text id="svs7qq"
Reliable online payment service
```

---

# Step 2 — Plan

Architecture designed:

* Kubernetes
* Monitoring
* CI/CD

---

# Step 3 — Build & Deploy

Developers:

* Push code
* GitHub Actions deploys application

---

# Step 4 — Deliver & Support

Operations:

* Monitor service
* Handle incidents
* Maintain uptime

---

# Step 5 — Improve

After incidents:

* RCA performed
* Alerts improved
* Performance optimized

---

# Complete SVS Flow

```text id="svs8rr"
Demand
   ↓
Plan
   ↓
Build & Deploy
   ↓
Operate & Support
   ↓
Monitor & Improve
   ↓
Value Delivered
```

---

# 8. Silos

---

# What are Silos?

Silos occur when teams work:

```text id="svs9ss"
Independently with poor communication and collaboration.
```

---

# Traditional IT Silos

```text id="svs0tt"
Development Team
       ↓
Operations Team
       ↓
Security Team
```

Each team works separately.

---

# Problems Caused by Silos

| Problem            | Example                              |
| ------------------ | ------------------------------------ |
| Poor communication | Delayed incidents                    |
| Slow deployments   | Manual approvals                     |
| Lack of ownership  | “Not my responsibility”              |
| Conflicting goals  | Dev wants speed, Ops wants stability |

---

# Example of a Silo Problem

Developer says:

```text id="svs1uu"
“The application works fine.”
```

Operations says:

```text id="svs2vv"
“It crashes in production.”
```

No shared visibility.

---

# Impact of Silos

Silos can cause:

* Downtime
* Delayed recovery
* Frustration
* Security gaps
* Inefficient workflows

---

# Why Modern IT Avoids Silos

Modern systems require:

* Fast deployments
* Continuous monitoring
* Shared responsibility

Silos slow everything down.

---

# DevOps vs Silos

---

# Traditional Siloed Model

```text id="svs3ww"
Developers → QA → Operations
```

Slow handoffs.

---

# DevOps Collaborative Model

```text id="svs4xx"
Developers ↔ Operations ↔ Security ↔ SRE
```

Shared ownership.

---

# Example

## CI/CD Pipeline

Instead of separate teams:

* Developers write code
* Automated testing validates
* Security scans run
* Deployment automated
* SRE monitors reliability

All teams collaborate.

---

# Breaking Down Silos

---

# Best Practices

| Practice               | Benefit              |
| ---------------------- | -------------------- |
| Cross-functional teams | Better collaboration |
| Shared dashboards      | Visibility           |
| Automation             | Fewer handoffs       |
| Shared goals           | Common objectives    |
| Blameless culture      | Better learning      |

---

# Example Shared Goal

```text id="svs5yy"
99.9% application uptime
```

Everyone works toward same outcome.

---

# Real Enterprise Example

## E-Commerce Platform

Without collaboration:

* Slow releases
* Frequent outages
* Finger-pointing

After DevOps adoption:

* Faster deployments
* Shared monitoring
* Faster incident resolution

---

# SVS + DevOps + SRE

Modern organizations combine:

* ITIL SVS
* DevOps collaboration
* SRE reliability practices

to deliver:

* Fast changes
* Stable systems
* Better customer experience

---

# Modern Service Delivery Flow

```text id="svs6zz"
Business Need
      ↓
Collaborative Teams
      ↓
Automated CI/CD
      ↓
Monitoring & Incident Response
      ↓
Continual Improvement
      ↓
Customer Value
```

---

# Enterprise Incident Example

## Problem

Checkout service outage.

---

# Siloed Organization

| Team       | Problem                |
| ---------- | ---------------------- |
| Developers | Blame infrastructure   |
| Operations | Blame application      |
| Security   | Separate communication |

Recovery delayed.

---

# Collaborative Organization

Shared dashboards and incident bridge:

* Logs analyzed together
* Root cause identified quickly
* Service restored faster

---

# Key Takeaways

| Topic                 | Important Idea                         |
| --------------------- | -------------------------------------- |
| SVS                   | Framework for creating service value   |
| Guiding Principles    | Decision-making guidance               |
| Governance            | Organizational control                 |
| Service Value Chain   | Operational workflow                   |
| Practices             | Operational capabilities               |
| Continual Improvement | Ongoing optimization                   |
| Silos                 | Teams working independently            |
| Problems with Silos   | Delays, poor communication, outages    |
| Modern IT Approach    | Collaboration, DevOps, automation      |
| Goal                  | Deliver value efficiently and reliably |
