# Kubernetes Failure Patterns & Troubleshooting

## Training Notes with Examples

---

# 1. Introduction to Kubernetes Failures

[Kubernetes Documentation](https://kubernetes.io/docs/home/?utm_source=chatgpt.com)

Modern Kubernetes environments are highly distributed.

Failures can occur in:

* Pods
* Nodes
* Networking
* Storage
* Scaling
* Configuration
* DNS

A Site Reliability Engineer (SRE) or DevOps Engineer must:

* Detect failures quickly
* Troubleshoot efficiently
* Recover services safely
* Prevent recurring incidents

---

# Kubernetes Architecture Refresher

```text id="k8s1aa"
Users
   ↓
Ingress / Service
   ↓
Pods
   ↓
Node
   ↓
Cluster
```

---

# Common Failure Categories

| Failure Area    | Example                   |
| --------------- | ------------------------- |
| Pod failures    | CrashLoopBackOff          |
| Node failures   | Node unreachable          |
| Resource issues | OOMKilled                 |
| Networking      | Blocked traffic           |
| Configuration   | Wrong secrets             |
| Storage         | PVC pending               |
| Scaling         | HPA not scaling           |
| DNS             | Service discovery failure |

---

# 2. Pod Crashes & Evictions

---

# What is a Pod?

A Pod is the smallest deployable unit in Kubernetes.

Contains:

* One or more containers
* Shared networking
* Shared storage

---

# Common Pod Failure States

| Failure          | Meaning                          |
| ---------------- | -------------------------------- |
| CrashLoopBackOff | Container repeatedly crashes     |
| OOMKilled        | Out of memory                    |
| Error            | Application exited               |
| Pending          | Cannot schedule                  |
| Evicted          | Removed due to resource pressure |

---

# A. CrashLoopBackOff

---

# What is CrashLoopBackOff?

Kubernetes repeatedly restarts a crashing container.

---

# Typical Causes

| Cause                | Example                      |
| -------------------- | ---------------------------- |
| Application bug      | App exits immediately        |
| Missing config       | Environment variable missing |
| Database unavailable | Startup dependency failure   |
| Port conflicts       | App cannot bind port         |

---

# Example Pod Status

```bash id="k8s2bb"
kubectl get pods
```

Output:

```text id="k8s3cc"
myapp-abc123   CrashLoopBackOff
```

---

# Troubleshooting CrashLoopBackOff

---

# Step 1: View Logs

```bash id="k8s4dd"
kubectl logs myapp-abc123
```

Example:

```text id="k8s5ee"
Database connection failed
```

---

# Step 2: Describe Pod

```bash id="k8s6ff"
kubectl describe pod myapp-abc123
```

Shows:

* Events
* Restart count
* Container state
* Errors

---

# Recovery Strategies

| Solution                 | Example               |
| ------------------------ | --------------------- |
| Fix application bug      | Correct startup issue |
| Correct configs          | Add missing variables |
| Verify dependencies      | Ensure DB accessible  |
| Increase readiness delay | Allow startup time    |

---

# Prevention

* Health probes
* Better testing
* Dependency validation
* Monitoring alerts

---

# B. OOMKilled (Out of Memory)

---

# What is OOMKilled?

Container exceeds memory limit and gets terminated.

---

# Example

```text id="k8s7gg"
Reason: OOMKilled
```

---

# Why It Happens

Application uses more memory than allocated.

---

# Example Resource Limits

```yaml id="k8s8hh"
resources:
  limits:
    memory: "512Mi"
```

If app exceeds 512Mi:

* Kubernetes kills container.

---

# Troubleshooting

```bash id="k8s9ii"
kubectl describe pod myapp
```

Look for:

```text id="k8s0jj"
Last State: Terminated
Reason: OOMKilled
```

---

# Recovery

| Solution              | Explanation            |
| --------------------- | ---------------------- |
| Increase memory limit | Allow more memory      |
| Optimize application  | Reduce leaks           |
| Tune JVM/Node/Python  | Better runtime configs |

---

# Prevention

* Monitor memory usage
* Right-size resources
* Load testing

---

# C. Pod Evictions

---

# What is Eviction?

Kubernetes removes pods when node resources are exhausted.

---

# Common Reasons

| Resource Pressure | Example            |
| ----------------- | ------------------ |
| Memory pressure   | Low RAM            |
| Disk pressure     | Full disk          |
| PID pressure      | Too many processes |

---

# Example

```text id="k8s1kk"
Evicted: node had memory pressure
```

---

# Troubleshooting

```bash id="k8s2ll"
kubectl describe pod myapp
```

---

# Prevention

* Resource requests/limits
* Node monitoring
* Cluster autoscaling

---

# 3. Node Failures & Taints

---

# What is a Node?

A worker machine running pods.

Can be:

* Virtual machine
* Physical server
* Cloud instance

---

# Common Node Failures

| Failure             | Meaning           |
| ------------------- | ----------------- |
| NotReady            | Node unhealthy    |
| Network unavailable | Node disconnected |
| Disk pressure       | Low storage       |
| Kubelet failure     | Agent not running |

---

# Checking Nodes

```bash id="k8s3mm"
kubectl get nodes
```

Example:

```text id="k8s4nn"
worker-1   NotReady
```

---

# Taints

Taints prevent pods from scheduling onto nodes.

---

# Example Taint

```text id="k8s5oo"
node.kubernetes.io/memory-pressure
```

---

# View Taints

```bash id="k8s6pp"
kubectl describe node worker-1
```

---

# Tolerations

Pods require tolerations to run on tainted nodes.

---

# Example

```yaml id="k8s7qq"
tolerations:
- key: "node.kubernetes.io/memory-pressure"
  operator: "Exists"
```

---

# Recovery Strategies

| Problem          | Recovery        |
| ---------------- | --------------- |
| Node unreachable | Restart node    |
| Kubelet failure  | Restart kubelet |
| Disk pressure    | Cleanup disk    |
| Hardware issue   | Replace node    |

---

# Prevention

* Node monitoring
* Cluster autoscaling
* Infrastructure redundancy

---

# 4. Resource Quotas & Limits Exhaustion

---

# Resource Quotas

Restrict namespace resource consumption.

---

# Example Quota

```yaml id="k8s8rr"
apiVersion: v1
kind: ResourceQuota
metadata:
  name: app-quota
spec:
  hard:
    pods: "10"
```

---

# Problem

Application cannot create new pods.

---

# Example Error

```text id="k8s9ss"
Exceeded quota: app-quota
```

---

# Troubleshooting

```bash id="k8s0tt"
kubectl describe quota
```

---

# Recovery

* Increase quota
* Remove unused resources
* Optimize workloads

---

# Prevention

* Capacity planning
* Resource monitoring

---

# 5. Network Policies Blocking Traffic

---

# What are Network Policies?

Firewall-like rules controlling pod communication.

---

# Example Problem

Frontend cannot reach backend API.

---

# Example Policy

```yaml id="k8s1uu"
kind: NetworkPolicy
```

---

# Symptoms

| Symptom            | Example         |
| ------------------ | --------------- |
| Timeouts           | API unreachable |
| Connection refused | Traffic blocked |

---

# Troubleshooting

---

# Check Policies

```bash id="k8s2vv"
kubectl get networkpolicy
```

---

# Describe Policy

```bash id="k8s3ww"
kubectl describe networkpolicy
```

---

# Recovery

* Update allow rules
* Verify namespaces/labels
* Test connectivity

---

# Prevention

* Use least restrictive testing first
* Validate policies in staging

---

# 6. ConfigMap & Secret Misconfigurations

---

# ConfigMaps

Store non-sensitive configuration.

---

# Secrets

Store sensitive data:

* Passwords
* Tokens
* Certificates

---

# Common Problems

| Problem                    | Example                |
| -------------------------- | ---------------------- |
| Missing key                | App startup failure    |
| Wrong environment variable | Incorrect behavior     |
| Expired secret             | Authentication failure |

---

# Example ConfigMap Error

```text id="k8s4xx"
ConfigMap not found
```

---

# Troubleshooting

---

# View ConfigMaps

```bash id="k8s5yy"
kubectl get configmaps
```

---

# Describe ConfigMap

```bash id="k8s6zz"
kubectl describe configmap app-config
```

---

# View Secrets

```bash id="k8s7aaa"
kubectl get secrets
```

---

# Recovery

* Correct values
* Redeploy application
* Rotate secrets

---

# Prevention

* Validation testing
* GitOps review process
* Secret management tools

---

# 7. PVC (Persistent Volume Claim) Storage Issues

---

# What is PVC?

Persistent Volume Claim requests storage for applications.

Used by:

* Databases
* Stateful applications

---

# Common Problems

| Problem       | Example              |
| ------------- | -------------------- |
| PVC Pending   | No storage available |
| Mount failure | Volume cannot attach |
| Disk full     | No capacity          |

---

# Example Error

```text id="k8s8bbb"
PersistentVolumeClaim is pending
```

---

# Troubleshooting

---

# Check PVCs

```bash id="k8s9ccc"
kubectl get pvc
```

---

# Describe PVC

```bash id="k8s0ddd"
kubectl describe pvc app-storage
```

---

# Recovery

| Problem             | Recovery          |
| ------------------- | ----------------- |
| No PV available     | Create volume     |
| Storage class issue | Fix storage class |
| Disk full           | Expand storage    |

---

# Prevention

* Storage monitoring
* Capacity planning
* Backups

---

# 8. HPA (Horizontal Pod Autoscaler) Failures

---

# What is HPA?

Automatically scales pods based on metrics.

---

# Example

```text id="k8s1eee"
CPU usage increases
        ↓
HPA creates more pods
```

---

# Common Failures

| Failure               | Example             |
| --------------------- | ------------------- |
| Metrics unavailable   | HPA cannot scale    |
| Resource limits wrong | Scaling ineffective |
| Max replicas reached  | Traffic overload    |

---

# Troubleshooting

---

# Check HPA

```bash id="k8s2fff"
kubectl get hpa
```

---

# Describe HPA

```bash id="k8s3ggg"
kubectl describe hpa myapp
```

---

# Recovery

* Fix metrics server
* Adjust scaling thresholds
* Increase max replicas

---

# Prevention

* Load testing
* Proper CPU/memory requests
* Autoscaling validation

---

# 9. Service & Ingress DNS Resolution Issues

---

# Services

Provide stable networking for pods.

---

# Ingress

Manages external HTTP/HTTPS access.

---

# Common Problems

| Problem                  | Example              |
| ------------------------ | -------------------- |
| DNS failure              | Service not resolved |
| Wrong selector           | No endpoints         |
| Ingress misconfiguration | 404 errors           |

---

# Troubleshooting Services

---

# Check Services

```bash id="k8s4hhh"
kubectl get svc
```

---

# Describe Service

```bash id="k8s5iii"
kubectl describe svc myservice
```

---

# Check Endpoints

```bash id="k8s6jjj"
kubectl get endpoints
```

---

# Troubleshooting DNS

---

# DNS Lookup Test

```bash id="k8s7kkk"
nslookup myservice.default.svc.cluster.local
```

---

# Troubleshooting Ingress

```bash id="k8s8lll"
kubectl describe ingress
```

---

# Recovery

* Correct selectors
* Verify DNS
* Fix ingress rules

---

# Prevention

* Service testing
* Health checks
* Automated validation

---

# 10. Troubleshooting with kubectl describe & logs

---

# kubectl describe

Provides detailed object information.

---

# Example

```bash id="k8s9mmm"
kubectl describe pod myapp
```

Shows:

* Events
* Conditions
* Restart history
* Scheduling issues

---

# kubectl logs

Displays container logs.

---

# Example

```bash id="k8s0nnn"
kubectl logs myapp
```

---

# Previous Container Logs

Useful after crashes.

```bash id="k8s1ooo"
kubectl logs myapp --previous
```

---

# Troubleshooting Workflow

```text id="k8s2ppp"
User Reports Issue
        ↓
Check Pod Status
        ↓
Describe Resource
        ↓
View Logs
        ↓
Identify Root Cause
        ↓
Recover Service
```

---

# 11. Recovery Strategies & Prevention

---

# Recovery Strategies

| Failure          | Recovery               |
| ---------------- | ---------------------- |
| CrashLoopBackOff | Fix app/config         |
| OOMKilled        | Increase memory        |
| Node failure     | Reschedule workloads   |
| PVC issue        | Expand/fix storage     |
| DNS issue        | Correct service config |

---

# Prevention Strategies

---

# 1. Resource Requests & Limits

Prevent resource exhaustion.

---

# 2. Health Probes

Use:

* Liveness probes
* Readiness probes

---

# Example

```yaml id="k8s3qqq"
livenessProbe:
  httpGet:
    path: /health
    port: 8080
```

---

# 3. Monitoring & Alerts

Use:

* Prometheus
* Grafana
* Datadog

---

# 4. GitOps & Validation

Validate:

* ConfigMaps
* Secrets
* Network policies

before deployment.

---

# 5. High Availability

Use:

* Multiple replicas
* Multi-node clusters
* Autoscaling

---

# Real Enterprise Example

## E-Commerce Platform Incident

### Problem

Checkout API failing.

---

# Investigation

```text id="k8s4rrr"
kubectl get pods
```

Shows:

```text id="k8s5sss"
CrashLoopBackOff
```

---

# Logs

```bash id="k8s6ttt"
kubectl logs checkout-api
```

Output:

```text id="k8s7uuu"
Database password missing
```

---

# Root Cause

Secret misconfiguration after deployment.

---

# Recovery

* Correct Kubernetes Secret
* Restart deployment

---

# Prevention

* Secret validation in CI/CD
* Pre-deployment checks

---

# End-to-End Kubernetes Troubleshooting Flow

```text id="k8s8vvv"
Monitoring Alert
        ↓
Check Cluster Health
        ↓
Inspect Pods/Nodes
        ↓
Describe Resources
        ↓
Analyze Logs
        ↓
Identify Root Cause
        ↓
Recover Service
        ↓
Implement Prevention
```

---

# Key Takeaways

| Topic                 | Important Idea                 |
| --------------------- | ------------------------------ |
| CrashLoopBackOff      | Repeated pod crashes           |
| OOMKilled             | Memory limit exceeded          |
| Node Taints           | Scheduling restrictions        |
| Resource Quotas       | Namespace resource limits      |
| Network Policies      | Pod traffic control            |
| ConfigMaps/Secrets    | Configuration management       |
| PVC Issues            | Persistent storage failures    |
| HPA Failures          | Autoscaling problems           |
| kubectl describe/logs | Primary troubleshooting tools  |
| Prevention            | Monitoring, probes, automation |
