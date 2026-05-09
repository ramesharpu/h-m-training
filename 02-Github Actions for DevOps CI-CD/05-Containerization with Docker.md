# Containers & Docker Fundamentals

## Training Notes with Examples

---

# 1. Problem: “It Works on My Machine!” → Solution: Containers

---

# The Traditional Problem

Developers often say:

```text id="s4j9ae"
“It works on my machine.”
```

But when deployed:

* Application crashes
* Dependencies missing
* Different OS behavior
* Different library versions

---

# Real Example

Developer system:

* Python 3.12
* NodeJS 20
* Ubuntu

Production server:

* Python 3.8
* NodeJS 16
* CentOS

Result:

* Application behaves differently.

---

# Why This Happens

Applications depend on:

* OS libraries
* Runtime versions
* Environment variables
* Network configuration
* System packages

Differences between environments cause failures.

---

# Solution: Containers

Containers package:

* Application code
* Dependencies
* Runtime
* Libraries
* Configuration

into one portable unit.

---

# Container Analogy

Think of containers like shipping containers.

Regardless of:

* Ship
* Truck
* Country

the container behaves consistently.

Similarly:

* Containers run consistently everywhere.

---

# Benefits of Containers

| Benefit         | Explanation                 |
| --------------- | --------------------------- |
| Portability     | Run anywhere                |
| Consistency     | Same environment everywhere |
| Isolation       | Apps separated safely       |
| Scalability     | Easy replication            |
| Fast deployment | Lightweight startup         |

---

# Container Workflow

```text id="jlwm1d"
Developer Laptop
       ↓
Container Image Built
       ↓
Same Container Runs in:
   - Test
   - Staging
   - Production
```

---

# 2. Container Architecture

---

# What is a Container?

A container is a lightweight isolated runtime environment.

It shares the host OS kernel while isolating:

* Processes
* Filesystems
* Networking

---

# Container vs Virtual Machine

---

# Virtual Machine Architecture

```text id="jlwm2e"
Hardware
   ↓
Hypervisor
   ↓
Guest OS
   ↓
Application
```

---

# Container Architecture

```text id="jlwm3f"
Hardware
   ↓
Host OS
   ↓
Container Runtime (Docker)
   ↓
Containers
```

---

# Key Difference

| Virtual Machines | Containers        |
| ---------------- | ----------------- |
| Full guest OS    | Share host kernel |
| Heavyweight      | Lightweight       |
| Slower startup   | Fast startup      |
| Larger storage   | Smaller size      |

---

# Container Runtime

Software responsible for:

* Running containers
* Managing images
* Networking
* Storage

Examples:

* Docker
* containerd
* CRI-O

---

# Important Components

| Component | Purpose             |
| --------- | ------------------- |
| Image     | Blueprint/template  |
| Container | Running instance    |
| Registry  | Stores images       |
| Runtime   | Executes containers |

---

# Container Lifecycle

```text id="jlwm4g"
Image
   ↓
Container Created
   ↓
Container Running
   ↓
Stopped/Removed
```

---

# 3. Images and Containers

---

# What is an Image?

A container image is a read-only template.

Contains:

* Application code
* Dependencies
* Runtime
* OS libraries

---

# Example

```text id="jlwm5h"
nginx:latest
```

Image for NGINX web server.

---

# What is a Container?

A container is a running instance of an image.

---

# Analogy

| Concept   | Analogy       |
| --------- | ------------- |
| Image     | Recipe        |
| Container | Prepared meal |

---

# Multiple Containers from One Image

```text id="jlwm6i"
Docker Image
   ↓
Container 1
Container 2
Container 3
```

---

# Container Registries

Used to store/share images.

Examples:

* Docker Hub
* GitHub Container Registry
* Amazon ECR

---

# Pulling an Image

```bash id="jlwm7j"
docker pull nginx
```

---

# Listing Images

```bash id="jlwm8k"
docker images
```

---

# Running a Container

```bash id="jlwm9l"
docker run nginx
```

---

# 4. Docker Basics

[Docker Documentation](https://docs.docker.com/?utm_source=chatgpt.com)

---

# What is Docker?

Docker is the most popular container platform.

It helps:

* Build containers
* Run containers
* Ship applications consistently

---

# Docker Workflow

```text id="jlwm0m"
Dockerfile
    ↓
Docker Build
    ↓
Docker Image
    ↓
Docker Run
    ↓
Container
```

---

# Understanding Dockerfile

A Dockerfile defines how to build an image.

---

# Example Dockerfile

```dockerfile id="jlwm1n"
FROM node:20

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

---

# Dockerfile Explanation

| Instruction | Purpose           |
| ----------- | ----------------- |
| FROM        | Base image        |
| WORKDIR     | Working directory |
| COPY        | Copy files        |
| RUN         | Execute commands  |
| EXPOSE      | Open port         |
| CMD         | Start application |

---

# Building Docker Image

```bash id="jlwm2o"
docker build -t myapp:v1 .
```

---

# Command Breakdown

| Part     | Meaning            |
| -------- | ------------------ |
| build    | Create image       |
| -t       | Tag image          |
| myapp:v1 | Image name/version |
| .        | Current directory  |

---

# Running Container

```bash id="jlwm3p"
docker run -p 3000:3000 myapp:v1
```

---

# Port Mapping

```text id="jlwm4q"
Host Port 3000 → Container Port 3000
```

---

# Running in Background

```bash id="jlwm5r"
docker run -d nginx
```

---

# Listing Running Containers

```bash id="jlwm6s"
docker ps
```

---

# Stopping Container

```bash id="jlwm7t"
docker stop <container_id>
```

---

# Removing Container

```bash id="jlwm8u"
docker rm <container_id>
```

---

# Removing Image

```bash id="jlwm9v"
docker rmi myapp:v1
```

---

# 5. Container Networking

---

# Why Networking Matters

Containers must communicate with:

* Other containers
* Databases
* External services
* Users

---

# Docker Networking Types

| Network Type | Purpose                  |
| ------------ | ------------------------ |
| Bridge       | Default local networking |
| Host         | Shares host network      |
| None         | No networking            |
| Overlay      | Multi-host networking    |

---

# Default Bridge Network

Containers communicate internally.

---

# Example

```bash id="jlwm0w"
docker network ls
```

Lists available networks.

---

# Creating Custom Network

```bash id="jlwm1x"
docker network create mynetwork
```

---

# Running Containers in Same Network

```bash id="jlwm2y"
docker run --network=mynetwork nginx
```

---

# Container Communication Example

```text id="jlwm3z"
Frontend Container
        ↓
Backend API Container
        ↓
Database Container
```

---

# Port Exposure

```bash id="jlwm4a"
docker run -p 8080:80 nginx
```

Meaning:

* Host port 8080 maps to container port 80.

---

# Container DNS

Containers on same network can communicate using names.

Example:

```text id="jlwm5b"
http://database:5432
```

---

# 6. Container Best Practices

---

# 1. Use Small Base Images

Good:

```dockerfile id="jlwm6c"
FROM alpine
```

Benefits:

* Faster downloads
* Reduced vulnerabilities

---

# 2. Avoid Running as Root

Bad:

```text id="jlwm7d"
Container runs as root user
```

Better:

```dockerfile id="jlwm8e"
USER appuser
```

---

# 3. Use Multi-Stage Builds

Reduces image size.

---

# Example

```dockerfile id="jlwm9f"
FROM node:20 AS build

WORKDIR /app
COPY . .
RUN npm install

FROM node:20-alpine

COPY --from=build /app /app
```

---

# 4. Keep Images Immutable

Do not modify running containers manually.

Always rebuild image instead.

---

# 5. Store Secrets Securely

Never hardcode:

* Passwords
* API keys
* Tokens

Use:

* Environment variables
* Secret managers

---

# 6. Use .dockerignore

Exclude unnecessary files.

Example:

```text id="jlwm0g"
node_modules
.git
logs/
```

---

# 7. Health Checks

Ensure container is healthy.

Example:

```dockerfile id="jlwm1h"
HEALTHCHECK CMD curl --fail http://localhost:3000 || exit 1
```

---

# 8. Scan Images for Vulnerabilities

Tools:

* Trivy
* Docker Scout
* Grype

---

# Example Trivy Scan

```bash id="jlwm2i"
trivy image myapp:v1
```

---

# 7. Container Debugging

---

# Why Container Debugging is Important

Containers may fail because of:

* Application errors
* Missing dependencies
* Networking issues
* Resource exhaustion

---

# Common Debugging Commands

| Command        | Purpose                |
| -------------- | ---------------------- |
| docker ps      | Running containers     |
| docker logs    | View logs              |
| docker exec    | Access container shell |
| docker inspect | Detailed metadata      |
| docker stats   | Resource usage         |

---

# Viewing Logs

```bash id="jlwm3j"
docker logs <container_id>
```

---

# Live Logs

```bash id="jlwm4k"
docker logs -f <container_id>
```

---

# Access Container Shell

```bash id="jlwm5l"
docker exec -it <container_id> bash
```

---

# Inspect Container

```bash id="jlwm6m"
docker inspect <container_id>
```

Shows:

* IP address
* Mounts
* Environment variables
* Network config

---

# Monitor Resource Usage

```bash id="jlwm7n"
docker stats
```

---

# Common Container Problems

| Problem            | Example               |
| ------------------ | --------------------- |
| Port conflict      | Port already used     |
| Crash loop         | App exits repeatedly  |
| Missing dependency | Library not installed |
| Memory exhaustion  | OOM kill              |
| Networking failure | Service unreachable   |

---

# Example Debugging Scenario

## Problem

Container crashes immediately.

---

# Step 1: Check Logs

```bash id="jlwm8o"
docker logs myapp
```

Output:

```text id="jlwm9p"
Error: Database connection failed
```

---

# Step 2: Verify Environment Variables

```bash id="jlwm0q"
docker inspect myapp
```

Find:

* Database URL missing.

---

# Step 3: Restart with Correct Variable

```bash id="jlwm1r"
docker run -e DB_HOST=db myapp:v1
```

---

# Container Observability

Modern container environments use:

* Logs
* Metrics
* Traces

Tools:

* Prometheus
* Grafana
* ELK Stack
* OpenTelemetry

---

# Real Enterprise Example

## E-Commerce Application

Containers:

* Frontend
* Product API
* Payment API
* Redis cache
* PostgreSQL

Benefits:

* Easy scaling
* Consistent deployments
* Faster releases

---

# Modern Container Deployment Flow

```text id="jlwm2s"
Developer Writes Dockerfile
          ↓
Docker Image Built
          ↓
Image Pushed to Registry
          ↓
Kubernetes Pulls Image
          ↓
Containers Run in Cluster
          ↓
Monitoring & Logs Collected
```

---

# Containers + CI/CD Example

```text id="jlwm3t"
GitHub Actions
       ↓
Build Docker Image
       ↓
Run Security Scan
       ↓
Push to Registry
       ↓
Deploy to Kubernetes
```

---

# Key Takeaways

| Topic                 | Important Idea                             |
| --------------------- | ------------------------------------------ |
| “Works on my machine” | Containers solve environment inconsistency |
| Images                | Blueprint/template                         |
| Containers            | Running image instances                    |
| Dockerfile            | Defines image build steps                  |
| Networking            | Enables container communication            |
| Best Practices        | Security, small images, immutability       |
| Debugging             | Logs, inspect, exec, stats                 |
| Containers            | Foundation for cloud-native apps           |
