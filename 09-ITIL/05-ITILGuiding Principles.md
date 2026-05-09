# ITIL 4 — Guiding Principles

## Training Notes with Examples

---

# 1. Introduction to Guiding Principles

---

# What are Guiding Principles?

Guiding Principles are:

```text id="gp1aa"
Recommendations that guide organizations in all circumstances.
```

They help teams:

* Make decisions
* Improve services
* Manage change
* Deliver value

---

# Why Guiding Principles Matter

Modern IT environments are:

* Complex
* Fast-changing
* Cloud-native
* Distributed

Organizations need flexible guidance rather than rigid rules.

---

# Key Idea

Guiding principles apply to:

* IT operations
* DevOps
* SRE
* Incident management
* Cloud platforms
* Business processes

---

# Benefits of Guiding Principles

| Benefit                | Example                  |
| ---------------------- | ------------------------ |
| Better decisions       | Faster incident handling |
| Improved collaboration | DevOps teamwork          |
| Reduced complexity     | Simpler workflows        |
| Continuous improvement | Iterative releases       |

---

# Seven Guiding Principles Overview

```text id="gp2bb"
1. Focus on Value
2. Start Where You Are
3. Progress Iteratively with Feedback
4. Collaborate and Promote Visibility
5. Think and Work Holistically
6. Keep It Simple and Practical
7. Optimize and Automate
```

---

# 2. Focus on Value

---

# Meaning

Everything an organization does should:

```text id="gp3cc"
Create value for customers and stakeholders.
```

---

# Important Question

Ask:

```text id="gp4dd"
“How does this activity help users or the business?”
```

---

# Examples of Value

| Area              | Example           |
| ----------------- | ----------------- |
| Customer value    | Faster website    |
| Business value    | Increased revenue |
| Operational value | Reduced downtime  |

---

# Example

## E-Commerce Website

Users value:

* Fast checkout
* Reliable payments
* Quick page loading

Technology changes should improve these outcomes.

---

# Bad Example

```text id="gp5ee"
Adding unnecessary features nobody uses
```

Creates complexity without value.

---

# Good Example

```text id="gp6ff"
Improving checkout speed to reduce cart abandonment
```

Direct business value.

---

# In DevOps/SRE

Focus on:

* Reliability
* User experience
* Deployment speed
* Reduced incidents

---

# 3. Start Where You Are

---

# Meaning

Do not rebuild everything from scratch.

Instead:

```text id="gp7gg"
Assess existing systems and improve them.
```

---

# Why This Matters

Organizations already have:

* Processes
* Tools
* Knowledge
* Monitoring systems

These may still provide value.

---

# Example

## Existing CI/CD Pipeline

Instead of replacing everything:

* Improve automation gradually
* Add security scanning
* Optimize deployments

---

# Bad Approach

```text id="gp8hh"
Delete existing infrastructure without evaluation
```

---

# Good Approach

```text id="gp9ii"
Analyze current system and improve incrementally
```

---

# Real Example

Current monitoring:

* Prometheus already installed

Improvement:

* Add better dashboards
* Improve alerts

No need for full replacement.

---

# Benefits

| Benefit             | Explanation                   |
| ------------------- | ----------------------------- |
| Lower risk          | Less disruption               |
| Faster improvements | Reuse existing systems        |
| Reduced cost        | Avoid unnecessary replacement |

---

# 4. Progress Iteratively with Feedback

---

# Meaning

Work in:

* Small steps
* Continuous improvement cycles

while collecting feedback.

---

# Key Idea

Large changes are risky.

Smaller improvements are:

* Safer
* Easier to validate
* Faster to adjust

---

# Iterative Workflow

```text id="gp0jj"
Plan Small Change
       ↓
Implement
       ↓
Collect Feedback
       ↓
Improve Further
```

---

# Example

## Kubernetes Migration

Bad approach:

```text id="gp1kk"
Migrate all applications at once
```

Good approach:

```text id="gp2ll"
Migrate one service at a time
```

---

# Feedback Sources

| Source     | Example              |
| ---------- | -------------------- |
| Monitoring | Error rates          |
| Users      | User complaints      |
| Metrics    | Latency              |
| Logs       | Application failures |

---

# Agile & DevOps Alignment

This principle supports:

* Agile sprints
* CI/CD
* Continuous delivery
* Continuous improvement

---

# Real Example

Deployment pipeline improvement:

1. Add automated tests
2. Monitor failures
3. Improve gradually

---

# Benefits

| Benefit         | Example                 |
| --------------- | ----------------------- |
| Reduced risk    | Smaller failures        |
| Faster learning | Immediate feedback      |
| Better quality  | Continuous optimization |

---

# 5. Collaborate and Promote Visibility

---

# Meaning

Teams should:

* Work together
* Share information
* Increase transparency

---

# Why Collaboration Matters

Modern IT systems involve:

* Developers
* Operations
* Security
* Support
* SRE teams

No single team can manage everything alone.

---

# Visibility Means

Everyone can see:

* System health
* Deployment status
* Incidents
* Metrics
* Risks

---

# Example

## Shared Dashboard

Teams view:

* API latency
* Error rate
* Kubernetes health
* Deployment progress

---

# Bad Example

```text id="gp3mm"
Only operations team has access to monitoring
```

---

# Good Example

```text id="gp4nn"
Shared observability dashboards for all teams
```

---

# DevOps Example

```text id="gp5oo"
Developers + Operations + Security collaborate during deployment
```

---

# Benefits

| Benefit                | Example              |
| ---------------------- | -------------------- |
| Faster troubleshooting | Shared logs          |
| Better decisions       | Shared visibility    |
| Reduced silos          | Cross-team ownership |

---

# 6. Think and Work Holistically

---

# Meaning

Services should be viewed:

```text id="gp6pp"
As complete systems, not isolated components.
```

---

# Why This Matters

A service depends on:

* Applications
* Infrastructure
* Databases
* Networking
* Monitoring
* Vendors

---

# Example

## Slow Application

Problem may involve:

* Database
* Network
* API
* Kubernetes node
* External provider

Not just application code.

---

# Holistic View Example

```text id="gp7qq"
Users
  ↓
Frontend
  ↓
API
  ↓
Database
  ↓
Cloud Infrastructure
```

---

# Silo Problem

Teams focusing only on their area may miss:

* System-wide failures
* Dependencies
* Business impact

---

# Real Example

Checkout issue caused by:

* External payment provider latency

Not frontend application.

---

# Benefits

| Benefit                | Example                  |
| ---------------------- | ------------------------ |
| Better reliability     | Full-system awareness    |
| Faster RCA             | Dependency understanding |
| Improved collaboration | Shared responsibility    |

---

# 7. Keep It Simple and Practical

---

# Meaning

Use:

```text id="gp8rr"
The minimum number of steps needed to achieve objectives.
```

---

# Why Simplicity Matters

Complex systems create:

* Confusion
* Failures
* Maintenance difficulty
* Slow troubleshooting

---

# Example

Bad process:

```text id="gp9ss"
15 manual approval steps for deployment
```

---

# Better process

```text id="gp0tt"
Automated CI/CD with risk-based approval
```

---

# Simplicity in Practice

| Area          | Simplification          |
| ------------- | ----------------------- |
| Monitoring    | Clear dashboards        |
| Deployment    | Automated pipelines     |
| Documentation | Easy-to-follow runbooks |

---

# Real Example

Instead of:

* Multiple monitoring tools

Use:

* Centralized observability platform

---

# Benefits

| Benefit            | Explanation          |
| ------------------ | -------------------- |
| Easier maintenance | Simpler systems      |
| Faster onboarding  | Easier learning      |
| Reduced incidents  | Fewer failure points |

---

# 8. Optimize and Automate

---

# Meaning

Improve processes first, then automate them.

---

# Important Principle

Do NOT automate broken processes.

First:

* Optimize workflow

Then:

* Automate repetitive tasks

---

# Example

## CI/CD Pipeline

Manual deployment:

```text id="gp1uu"
Engineer manually deploys application
```

Optimized & automated:

```text id="gp2vv"
GitHub Actions deploys automatically
```

---

# Common Automation Areas

| Area              | Example              |
| ----------------- | -------------------- |
| CI/CD             | Automated deployment |
| Monitoring        | Alerting             |
| Scaling           | Kubernetes HPA       |
| Incident response | Auto-remediation     |

---

# Example Automation Workflow

```text id="gp3ww"
Code Commit
     ↓
Automated Testing
     ↓
Security Scan
     ↓
Deployment
     ↓
Monitoring Validation
```

---

# Benefits

| Benefit            | Example                 |
| ------------------ | ----------------------- |
| Faster delivery    | Automated releases      |
| Reduced errors     | Less manual work        |
| Better consistency | Standardized operations |

---

# Risks of Bad Automation

Poor automation can:

* Spread failures faster
* Increase outages
* Create hidden complexity

---

# Best Practice

```text id="gp4xx"
Optimize first → Automate second
```

---

# 9. Interaction Between Principles

---

# Principles Work Together

The guiding principles are:

```text id="gp5yy"
Interconnected and complementary.
```

They should not be applied independently.

---

# Example Interaction

---

# Scenario: Improving Deployment Pipeline

### Focus on Value

Improve deployment reliability.

### Start Where You Are

Reuse existing GitHub Actions workflow.

### Progress Iteratively

Add automation step-by-step.

### Collaborate and Promote Visibility

Developers and SRE teams share dashboards.

### Think Holistically

Consider monitoring, rollback, and infrastructure.

### Keep It Simple

Avoid unnecessary approval complexity.

### Optimize and Automate

Automate testing and deployments.

---

# Combined Workflow Example

```text id="gp6zz"
Business Need
      ↓
Collaborative Planning
      ↓
Incremental Improvements
      ↓
Automation
      ↓
Monitoring & Feedback
      ↓
Continuous Optimization
```

---

# Real Enterprise Example

## E-Commerce Platform

Goal:

```text id="gp7aaa"
Reduce checkout failures during peak traffic
```

Applied principles:

* Value → Better customer experience
* Iterative → Small scaling improvements
* Collaboration → Shared incident dashboard
* Holistic → Analyze API + DB + network
* Automation → Auto-scaling + alerts

Result:

* Faster checkout
* Fewer outages
* Better reliability

---

# Modern DevOps + ITIL Example

```text id="gp8bbb"
Developers Commit Code
          ↓
CI/CD Pipeline Runs
          ↓
Automated Testing
          ↓
Deployment
          ↓
Observability & Alerts
          ↓
Feedback Loop
          ↓
Continuous Improvement
```

---

# Common Mistakes

| Mistake           | Problem                |
| ----------------- | ---------------------- |
| Over-automation   | Complex failures       |
| Ignoring feedback | Repeated incidents     |
| Siloed work       | Poor collaboration     |
| Overengineering   | Unnecessary complexity |

---

# Key Takeaways

| Principle                          | Core Idea                         |
| ---------------------------------- | --------------------------------- |
| Focus on Value                     | Deliver business/user value       |
| Start Where You Are                | Improve existing capabilities     |
| Progress Iteratively with Feedback | Small continuous improvements     |
| Collaborate and Promote Visibility | Shared ownership and transparency |
| Think and Work Holistically        | Consider end-to-end systems       |
| Keep It Simple and Practical       | Avoid unnecessary complexity      |
| Optimize and Automate              | Improve first, automate wisely    |
| Interaction Between Principles     | Principles work together          |
