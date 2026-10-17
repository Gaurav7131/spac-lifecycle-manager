<div align="center">

# 🏛️ SPAC Lifecycle Manager & Simulation Engine

### *Distributed FinTech Orchestration • Event-Driven Simulation Pipeline • Durable Workflows*

<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&duration=2600&pause=900&color=00F5D4&center=true&vCenter=true&width=780&lines=Distributed+FinTech+Lifecycle+Orchestrator;Durable+Temporal.io+State+Machine;Sub-50ms+Asynchronous+Decoupling+over+Kafka;Zero-CPU+Idle+Suspension+Engine;Enterprise+mTLS+Secured+Cloud+Event+Bus" alt="Typing SVG" />
</a>
<br/><br/>

<!-- Architecture Stack -->
<p align="center">
  <img src="https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white" />
  <img src="https://img.shields.io/badge/Temporal.io-Durable_Workflows-000000?style=for-the-badge&logo=temporal&logoColor=white" />
  <img src="https://img.shields.io/badge/Apache_Kafka-Aiven_mTLS-231F20?style=for-the-badge&logo=apachekafka&logoColor=white" />
  <img src="https://img.shields.io/badge/PostgreSQL-17_ACID-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" />
<!-- Live Telemetry -->
<p align="center">
  <img src="https://img.shields.io/badge/Saga_State-DURABLE_AWAIT-brightgreen?style=flat-square&logo=temporal&logoColor=white" />
  <img src="https://img.shields.io/badge/Kafka_Transport-mTLS_ENCRYPTED-blue?style=flat-square&logo=apachekafka&logoColor=white" />
  <img src="https://img.shields.io/badge/API_Response-%3C50ms-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Microservices-3_Nodes-purple?style=flat-square" />
</p>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0f172a&height=90&section=header"/>
  <div align="center">
<a href="https://spac-lifecycle-manager.netlify.app">
<img src="https://img.shields.io/badge/▶️_CLICK_HERE_TO_OPEN_LIVE_DASHBOARD-SPAC%2F%2FLIFECYCLE-00F5D4?style=for-the-badge" />
</a>
</p>

</div>

---

## 🌐 Distributed System Topology

```text
       [ External HTTP Traffic / Postman Client ]
                           │
                           ▼
 ┌──────────────────────────────────────────────────┐
 │       Spring Cloud API Gateway (Port 8080)       │  ◄── Unified Edge Router & Proxy
 └─────────────────────────┬────────────────────────┘
                           │ (Non-Blocking Reactive Netty)
                           ▼
 ┌──────────────────────────────────────────────────┐      Temporal gRPC (7233)      ┌────────────────────────┐
 │        SPAC Core Service (Port 8081)             │ ◄───────────────────────────►  │  Temporal Orchestrator │
 │   - State Machine Controller                     │                                │  - Zero CPU Suspension │
 │   - JPA Transactions & Optimistic Locking        │                                │  - Durable Event Sagas │
 │   - Kafka Producer (Command Dispatch)            │                                └────────────────────────┘
 └─────────────┬──────────────────────┬─────────────┘
               │                      │
  Async Event  │                      │ ACID State Mutation
  (JSON/mTLS)  ▼                      ▼
        ┌─────────────┐     ┌──────────────────────────────────┐
        │    Kafka    │     │      PostgreSQL 17 (Port 5432)   │
        │   Cluster   │     │      Database: spac_db           │
        └──────┬──────┘     │      - spacs (Current Stage)     │
               │            │      - simulation_results        │
     Sub-50ms  │            └─────────────────▲────────────────┘
     Consumer  ▼                              │
 ┌──────────────────────────────────┐         │
 │   Simulation Engine (Port 8082)  │         │ Batch & Transactional
 │   - Asynchronous Math Cruncher   │ ────────┘ Persist
 │   - Dilution & Valuation Compute │
 └──────────────────────────────────┘
```

---

## ⚡ Production Engineering Highlights

| | Capability | Implementation Detail |
|:--|:--|:--|
| 🕰️ | **Durable Financial Orchestration** | Models long-running SPAC lifecycles across statutory waiting windows using Temporal Workflows. The engine leverages `Workflow.await()`, persisting execution state with **zero idle CPU consumption** during multi-month pauses. |
| 🚀 | **Asynchronous Compute Offloading** | Core API latency slashed by offloading mathematical dilution modeling to Apache Kafka. The core service returns `HTTP 200` in **under 50 ms** while background workers compute scenario models asynchronously. |
| 🔐 | **mTLS Cloud Transport Encryption** | Broker communications hardened with mutual TLS via Java KeyStore (`.jks`) and PKCS12 (`.p12`) trust/key-stores on a cloud-hosted **Aiven Kafka** cluster. |
| 🧬 | **Optimistic Locking & ACID Integrity** | Database entities guarded with `@Version` and strict `@Transactional` boundaries, preventing race conditions during concurrent shareholder votes and state transitions. |

---

## 🔄 SPAC Finite State Machine

```text
 [ FORMATION ] ───► POST /api/v1/spacs/init ──────────► Persist to DB & Start Temporal Workflow
       │
       ▼
 [ IPO_WAIT ]  ───► Workflow.await() ─────────────────► Zero-CPU Thread Suspension
       │
       ▼
 [ IPO_DONE ]  ───► POST /{ticker}/ipo-complete ──────► Workflow Signal Unblocks State
       │
       ▼
 [ TARGET_ID ] ───► POST /trigger-simulation/{ticker} ► Publish Event onto Kafka Topic
       │
       ▼
 [ MERGED ]    ───► POST /{ticker}/vote ──────────────► Stakeholder Sagas Concluded
```

---

## 🏢 Microservices Ecosystem

| Service Node | Port | Architectural Role | Core Technologies | Status |
|:--|:--:|:--|:--|:--:|
| `api-gateway` | **8080** | Unified edge proxy & routing | Spring Cloud Gateway, Reactive Netty | ![](https://img.shields.io/badge/live-brightgreen?style=flat-square) |
| `spac-core-service` | **8081** | Lifecycle brain & workflow coordinator | Temporal SDK, Spring Data JPA, Kafka Producer | ![](https://img.shields.io/badge/live-brightgreen?style=flat-square) |
| `simulation-engine` | **8082** | Computational dilution worker | Kafka Consumer, Dilution Math, PostgreSQL JPA | ![](https://img.shields.io/badge/live-brightgreen?style=flat-square) |

---

## 🚀 Getting Started

### 1️⃣ Start Infrastructure Backbones

Launch the orchestrator and database layers **before** the application microservices.

```bash
# Terminal 1 — Local Temporal Orchestration Engine (gRPC 7233 / Web UI 8233)
temporal server start-dev

# Terminal 2 — Ensure PostgreSQL 17 is active (Port 5432), database: spac_db
psql -U postgres -c "CREATE DATABASE spac_db;"
```

### 2️⃣ Launch Application Microservices

```bash
# Terminal 3 — Core Coordinator Service (Port 8081)
cd spac-core-service && ./mvnw spring-boot:run

# Terminal 4 — Math Simulation Worker (Port 8082)
cd simulation-engine && ./mvnw spring-boot:run

# Terminal 5 — API Gateway Front Door (Port 8080)
cd api-gateway && ./mvnw spring-boot:run
```

---

## 📡 API Flow & Signal Playbook

> All network requests target the API Gateway boundary: `http://localhost:8080`

<details open>
<summary><b>1. Register New SPAC</b> — stage <code>FORMATION</code></summary>

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

**Execution outcome —** entity saved to PostgreSQL with stage `FORMATION`; durable workflow `SPAC-ATAQ` initiated and suspended on `Workflow.await()`.

</details>

<details>
<summary><b>2. Signal IPO Completion</b> — stage <code>IPO_COMPLETED</code></summary>

```bash
curl -X POST http://localhost:8080/api/v1/spacs/ATAQ/ipo-complete
```

**Execution outcome —** delivers an external signal to Temporal, unblocking workflow execution and advancing the database record to `IPO_COMPLETE`.

</details>

<details>
<summary><b>3. Asynchronous Dilution Simulation Trigger</b></summary>

```bash
curl -X POST http://localhost:8080/api/v1/spacs/trigger-simulation/ATAQ
```

**Execution outcome —** gateway routes the request to the core service; core drops a calculation payload onto Kafka topic `spac-simulations` and returns `HTTP 200`. The `simulation-engine` consumes the message, computes scenarios, and persists output to `simulation_results`.

</details>

<details>
<summary><b>4. Shareholder Vote & Merger Close</b> — stage <code>MERGED</code></summary>

```bash
curl -X POST http://localhost:8080/api/v1/spacs/ATAQ/vote
```

**Execution outcome —** concludes the stakeholder saga; optimistic locking (`@Version`) serializes concurrent vote submissions before the terminal state transition.

</details>

---

## 🛠️ Observability & Telemetry

**Temporal Web UI** → [http://localhost:8233](http://localhost:8233) — track live workflow timers, signal execution events, and replay histories.

**PostgreSQL verification:**

```sql
-- Verify lifecycle stage progression
SELECT ticker_symbol, current_stage, trust_value, updated_at FROM spacs;

-- Inspect asynchronous background compute records
SELECT * FROM simulation_results ORDER BY id DESC;
```

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0f172a&height=90&section=footer"/>

**Built with Java 21 • Spring Boot 3 • Temporal.io • Apache Kafka • PostgreSQL 17**

</div>
