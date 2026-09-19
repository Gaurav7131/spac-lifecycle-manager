```markdown
<div align="center">

# 🏛️ SPAC Lifecycle Manager & Simulation Engine
### *Distributed FinTech Orchestrator & High-Compute Dilution Simulator*

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Temporal](https://img.shields.io/badge/Temporal-Orchestrator-000000?style=for-the-badge&logo=temporal&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-mTLS-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

<br/>

```text
    [ Client / Postman ]
             │ (HTTP Traffic)
             ▼
┌─────────────────────────┐
│   Spring Cloud Gateway  │  ◄── Port 8080 ("The Front Door")
└────────────┬────────────┘
             │ (Secure Routing)
             ▼
┌─────────────────────────┐       Temporal gRPC (Port 7233)
│    SPAC Core Service    │ ◄─────────────────────────────────► ┌────────────────────────┐
│  (State Machine Engine) │                                     │  Temporal Orchestrator │
└──────┬───────────┬──────┘                                     │  (Durable Workflows)   │
       │           │                                            └────────────────────────┘
       │           │ (Produce Event)
       │           ▼
       │     ┌───────────┐
       │     │   Kafka   │  Topic: spac-simulations (mTLS / SSL)
       │     └─────┬─────┘
       │           │ (Async Consumer)
       │           ▼
       │     ┌──────────────────────┐
       │     │  Simulation Engine   │  ◄── Port 8082 ("The Math Cruncher")
       │     └──────────┬───────────┘
       │ (ACID JPA)     │ (Simulation Persist)
       ▼                ▼
┌─────────────────────────────────┐
│     PostgreSQL (spac_db)        │  ◄── Port 5432 ("Source of Truth")
└─────────────────────────────────┘

```

---

## ⚡ System Highlights

* **Durable Financial Orchestration**: Tracks Special Purpose Acquisition Companies across multi-year lifecycles using **Temporal Workflows**, surviving service restarts with zero CPU idle consumption.
* **Asynchronous Compute Offloading**: Core service instantly responds to simulation requests in under 50ms while streaming heavy dilution calculations over **Apache Kafka**.
* **Enterprise Security**: Mutual TLS (mTLS / SSL) client keystore/truststore integration for secure cloud message broker transactions.
* **Optimistic Locking**: Enforced on JPA entities using `@Version` to safeguard concurrent status transitions against race conditions.

---

## 🔄 SPAC Finite State Machine

```text
 [ FORMATION ] ───► (POST /init) ───► Persist to DB & Start Temporal Workflow
       │
       ▼
 [ IPO_WAIT ]  ───► Workflow.await() ───► Zero CPU Idle Sleep
       │
       ▼
 [ IPO_DONE ]  ───► (POST /{ticker}/ipo-complete) ───► Workflow Signal Received
       │
       ▼
 [ TARGET_ID ] ───► (POST /{ticker}/simulate) ───► Kafka Offload to Simulation Engine
       │
       ▼
 [ MERGED ]    ───► Stakeholder Approval Signal ───► Final Stage Execution

```

---

## 🏢 Microservices Ecosystem

| Microservice | Internal Port | Primary Role | Key Components |
| --- | --- | --- | --- |
| **`api-gateway`** | `8080` | Reverse Proxy / Unified Front Door | Spring Cloud Gateway, Dynamic Routing |
| **`spac-core-service`** | `8081` | Workflow Brain & Database Master | Temporal Workers, Spring Data JPA, Kafka Producer |
| **`simulation-engine`** | `8082` | Computational Math Worker | Kafka Listener, Dilution Engine, Simulation Repository |

---

## 🚀 Enterprise Boot Sequence

### 1️⃣ Start Infrastructure Backbones

```bash
# Terminal 1: Launch Local Temporal Orchestrator (Port 7233 / UI 8233)
temporal server start-dev

# Terminal 2: Ensure PostgreSQL is active on port 5432
# Database: spac_db

```

### 2️⃣ Launch Application Microservices

```bash
# Terminal 3: Start Core Manager
cd spac-core-service
./mvnw spring-boot:run

# Terminal 4: Start Math Compute Worker
cd simulation-engine
./mvnw spring-boot:run

# Terminal 5: Start API Gateway
cd api-gateway
./mvnw spring-boot:run

```

---

## 📡 API Flow & Signal Playbook

All calls target the API Gateway entry point (`http://localhost:8080`).

### 1. Register New SPAC (Formation Stage)

```bash
curl -X POST http://localhost:8080/api/v1/spacs/init \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Alpha Tech Acquisition",
    "tickerSymbol": "ATAQ",
    "targetSector": "FinTech",
    "trustValue": 500000000.00
  }'

```

* **Engine Response:** Saves entity to PostgreSQL with stage `FORMATION` and initiates `SPAC-ATAQ` durable workflow.

---

### 2. Complete IPO (Signal Temporal to Advance)

```bash
curl -X POST http://localhost:8080/api/v1/spacs/ATAQ/ipo-complete

```

* **Engine Response:** Wakes sleeping Temporal workflow, advancing the database state to `IPO_COMPLETED`.

---

### 3. Asynchronous Dilution Simulation

```bash
curl -X POST http://localhost:8080/api/v1/spacs/trigger-simulation/ATAQ

```

* **Engine Response:** Core produces JSON message payload to `spac-simulations` topic. `simulation-engine` consumes asynchronously, computes financial scenarios, and persists results.

---

## 🛠️ Verification & Observability

* **Temporal Web Dashboard:** [`http://localhost:8233`](http://localhost:8233?utm_source=gemini) — Inspect live workflow execution histories, timers, and signals.
* **PostgreSQL State Check:**
```sql
SELECT ticker_symbol, current_stage, trust_value, updated_at FROM spacs;
SELECT * FROM simulation_results;

```



```

```
