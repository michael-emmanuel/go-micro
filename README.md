# 🚀 EventMesh (Go Microservices Platform)

**Microservices architecture written in Go (Golang)**  
REST, gRPC, RPC, AMQP (RabbitMQ), Postgres, MongoDB — fully containerized and orchestration-ready  
Built with learning, maintainability, observability, and scalability in mind.

---

## 🧠 Overview

This repository contains a suite of loosely coupled microservices demonstrating a real distributed backend built with Go.

Unlike monoliths, each service:

- Is independently deployable
- Encapsulates a single business concern
- Communicates via HTTP/REST, gRPC, and asynchronous messaging
- Has its own datastore where applicable

This project includes:

| Service      | Tech              | Purpose                                |
| ------------ | ----------------- | -------------------------------------- |
| **frontend** | Go HTML templates | Static UI + API gateway                |
| **auth**     | Go + Postgres     | JWT auth, user accounts                |
| **logging**  | Go + MongoDB      | Structured log ingestion               |
| **broker**   | Go                | Unified entrypoint for client requests |
| **listener** | Go + RabbitMQ     | Async event handler                    |
| **mail**     | Go + SMTP         | Email delivery service                 |

---

## 🧱 Key Features

✔ Clean service boundaries, independent deployments  
✔ Multi-protocol communication: REST, RPC, gRPC, AMQP  
✔ Docker-first containerization  
✔ Deployable to Swarm or Kubernetes  
✔ Comprehensive health, logs, metrics, and error handling  
✔ Zero-downtime rolling updates

---

## 🛠️ Tech Stack

**Languages:** Go (1.20+)  
**Containers:** Docker, Docker Compose  
**Databases:** Postgres, MongoDB  
**Message Broker:** RabbitMQ  
**Orchestration:** Docker Swarm / Kubernetes  
**CI/CD:** GitHub Actions (template included)  
**Monitoring:** Prometheus / Grafana (optional)

---

## 🚀 Getting Started (Local)

### 1) Clone

```sh
git clone https://github.com/michael-emmanuel/go-micro.git
cd go-micro
```

### 2) Environment Setup

Copy example env:

```sh
cp .env.example .env
# Update DB creds, ports, secrets
```

> Credentials should be stored securely in Vault / Kubernetes secrets for prod.

### 3) Build & Run (Kubernetes)

From k8s folder run:

```sh
kubectl apply -f k8s
```

Setup minikube tunner

```sh
minikube tunnel
```

Services will be available at:

- `frontend.info` — Frontend
- `broker-service.info` — Broker API

---

## 💡 Architecture Diagram

```
                                       +----------------+
                                       |   Frontend UI  |
                                       | (Static Web UI)|
                                       +--------+-------+
                                                |
                                                | REST / HTTP
                                                v
                                      +----------------------+
                                      |      API Gateway     |
                                      | (Broker Service)     |
                                      +---+--------------+---+
                                          |              |
                        REST/HTTP         |              | gRPC / HTTP / JSON
                                          |              |
                     +----------------+   v              v +------------------+
                     | Auth Service   |------------------->| Logging Service  |
                     | (PostgreSQL)   |      gRPC/RPC      | (MongoDB)        |
                     +----------------+                    +------------------+
                          |   ^                                  |
                          |   |                                  |
                          v   |                              Logging
                     +----------------+                      +-----------+
                     | Mail Service   |<--- AMQP/RabbitMQ ---| Listener  |
                     | (Email Sender) |                      | Service   |
                     +----------------+                      +-----------+
                           ^                                        |
                           |                AMQP Messages           |
                           +----------------------------------------+

```

---

## 📌 Service Contracts

### REST

**Auth Service**

```http
POST /api/authenticate
```

### gRPC

**UserService**

```proto
POST /api/log-grpc
```

### AMQP

**Mail Event**

```jsonc
{
  "from": "me@example.com",
  "to": "user@example.com",
  "subject": "Welcome",
  "message": "Hello from microservices!",
}
```

---

## 🧪 Testing

Unit & integration tests are included with mocked DB for Auth Service.
CD into api folder inside authentication-service.

```sh
go test -v .
```

> 100% coverage - time of completion: TBD

---

## 📦 Deployment

### Docker Swarm

```sh
docker swarm init
docker stack deploy -c swarm.yml myapp
```

### Kubernetes

```sh
kubectl apply -f k8s
minikube tunnel
```

If you do not have ingress addon enabled:

```sh
minikube addons enable ingress
```

---

## 🔍 Observability

- **Health Checks**
  `/healthz` on each service
- **Metrics**
  Prometheus instrumented handlers (`/metrics`)
- **Structured Logging**
  JSON logs with correlation IDs
- **Tracing**
  OpenTelemetry ready

> Time of completion: TBD

---

## 🧠 Best Practices Enforced

✔ Idempotent services
✔ Shared nothing architecture
✔ Fail fast & retry policies
✔ Backpressure via RabbitMQ QoS
✔ Config driven (12-factor)
✔ Canary releases supported

---

MIT Licensed ©
