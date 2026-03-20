# 📘 tyk-hybrid-docker

A simple, developer-friendly **Docker Compose setup** for a Standard **Tyk Hybrid Gateway + Pump** deployment, including optional ephemeral or persistent Redis storage. This repo makes running a Tyk Hybrid API Gateway + analytics Pump locally easy — with minimal configuration.

Inspired by the official [Tyk Gateway Docker repo](https://github.com/TykTechnologies/tyk-gateway-docker), this setup adds Pump support for analytics streaming.

---

## 💡 Overview

This repository contains:

- A **Docker Compose** setup for:
  - **Tyk Gateway** — Open Source API Gateway  
  - **Tyk Pump** — streams analytics to remote services  
  - **Redis** — used by the Gateway for storage  

- Two Redis modes:
  - **Persistent Redis** — stores data in a named volume (default)  
  - **Ephemeral Redis** — no volume, in-memory storage  

- Simple `.env`-based configuration for easy customization  

This setup targets developers and engineers who want to **run a Hybrid Tyk Gateway + analytics pipeline locally** without the complexity of the full Tyk stack.

---

## 📌 What this repo solves

The official [`tyk-gateway-docker`](https://github.com/TykTechnologies/tyk-gateway-docker) repository provides:

- ✅ Tyk Gateway  
- ✅ Redis  
- ✅ Example API definitions  

But it **does not include Pump**, which is often needed in hybrid or production-like setups.  

This repo adds **Tyk Pump support**, giving you:

- Analytics forwarding  
- Optional remote MDCB/Tyk Cloud integration  
- Prometheus Pump support (metrics)  
- Better analytics tooling than plain Redis stats

---

## 🚀 Features

### 🔹 Simple to Use

- One-file Docker Compose with optional override  
- Works with `docker compose up`  
- Minimal boilerplate — get Tyk running fast

### 🔹 Flexible Redis Support

- Persistent mode stores Redis data on disk  
- Ephemeral mode drops all data on stop  
- Useful for dev vs testing vs disposable environments

### 🔹 Analytics Pump

- Streams analytics from Gateway logs to supported backends  
- Base config is flexible via environment variables  
- Supports Prometheus (metrics) out of the box

### 🔹 Minimal Dependencies

- No upstream dashboards or extra services  
- All controlled with one `.env`-based config

---

## 🧩 Repository Structure

```text
├── confs/                      # Gateway + Pump config templates
├── docker-compose.yml          # Default (persistent) compose
├── docker-compose.ephemeral.yml # Compose override for ephemeral Redis
├── .env.example                # Sample environment variables
├── README.md                  # This file
```

---

## 🧪 Requirements

- Docker Engine installed  
- Docker Compose v2+  
- Optional HTTP client (curl or Postman)

---

## ⚡ Quick Start

Setup you Dataplane configuration via the simple to use `.env` Environment Variable File

## 🛠️ Environment Configuration

Copy the example `.env`:

```bash
cp .env.example .env
```

Edit the following variables as needed:

- `ORG_ID`
- `API_KEY`
- `MDCB_INGRESS`
- `GROUP_ID`
- `GATEWAY_VERSION`
- `PUMP_VERSION`
- `REDIS_VERSION`

These configure both the Gateway and Pump.

---

### 🟢 Default (Persistent Redis)

```bash
docker compose up -d
```

This will start:

- Tyk Gateway
- Tyk Pump
- Redis (with persistent volume)

### 🔁 Ephemeral Mode (No Redis Persistence)

```bash
docker compose -f docker-compose.yml -f docker-compose.ephemeral.yml up -d
```

Redis will be in-memory and will not persist data between restarts.

### ✅ Test the Gateway

```bash
curl http://localhost:8080/hello
```

You should see JSON indicating Redis connectivity.

---

## 👏 Contributing / Future Work

- Add Traefik/Nginx load balancer for scaled Gateway  
- Automated tests or local Prometheus dashboards

---

## 📚 Useful Links

- Tyk Gateway official repo: <https://github.com/TykTechnologies/tyk-gateway-docker>  
- Tyk Pump docs & config: <https://github.com/TykTechnologies/tyk-pump>  
- Tyk official docs (Hybrid deployment): <https://tyk.io/docs/5.9/tyk-cloud/environments-deployments/hybrid-gateways/>
