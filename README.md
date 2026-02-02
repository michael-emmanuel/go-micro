# 🚀 EventMesh (Go Microservices Platform)

**Microservices architecture written in Go (Golang)**  
This project showcases a multi-service architecture using REST, gRPC, RPC, and AMQP (RabbitMQ) for inter-service communication, with PostgreSQL and MongoDB as backing data stores. It demonstrates the core building blocks of service-to-service communication in a fully containerized, orchestration-ready environment.

---

## 🧠 Overview

This repository contains a suite of loosely coupled microservices demonstrating a real distributed backend built with Go.

Each service:

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

### 2) Build & Run (Docker)

From projects folder run:

```sh
make up_build
make build_front_linux
```

Frontend GUI on localhost

---

## 📌 Service Contracts

### REST

**Auth Service**

```http
POST /api/authenticate
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
