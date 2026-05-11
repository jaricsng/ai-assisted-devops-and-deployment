# Software Development Lifecycle

## From Ground Zero to Production

> *Nine phases — from the first conversation to a live, monitored production system.*

---

## End-to-End Flow

```mermaid
flowchart LR
    A([🔍 Discovery]) --> B([🏗️ Design])
    B --> C([⚙️ Dev Setup])
    C --> D([💻 Coding])
    D --> E([🧪 Testing])
    E --> F([🎭 Staging])
    F --> G([🚀 Deploy])
    G --> H([📊 Monitor])
    H --> I([🔄 Maintain])
    I -->|Next sprint| D
    H -->|Incident| D

    style A fill:#028090,color:#fff,stroke:none
    style B fill:#028090,color:#fff,stroke:none
    style C fill:#00a896,color:#fff,stroke:none
    style D fill:#00a896,color:#fff,stroke:none
    style E fill:#028090,color:#fff,stroke:none
    style F fill:#00a896,color:#fff,stroke:none
    style G fill:#ffc857,color:#1e2761,stroke:none
    style H fill:#028090,color:#fff,stroke:none
    style I fill:#00a896,color:#fff,stroke:none
```

---

## Phase Overview

```mermaid
timeline
    title SDLC Phases — Ground Zero to Production
    section Conceive
        01 Discovery    : Stakeholder interviews
                        : Requirements gathering
                        : Feasibility study
    section Plan
        02 Design       : High-level architecture
                        : Low-level design
                        : Security model
    section Prepare
        03 Dev Setup    : Version control
                        : CI pipeline
                        : Local environment
    section Build
        04 Development  : Agile sprints
                        : Code review
                        : Unit tests
    section Validate
        05 Testing      : Unit → Integration
                        : E2E & Performance
                        : Security & UAT
    section Release
        06 Staging      : Pre-prod validation
                        : Dry runs
                        : Go/No-Go sign-off
        07 Deployment   : CI/CD pipeline
                        : Blue/Green · Canary
                        : Feature flags
    section Operate
        08 Monitoring   : Logs · Metrics · Traces
                        : Alerting & SLOs
                        : Incident response
        09 Maintenance  : Bug management
                        : Performance tuning
                        : Iterate & repeat
```

---

## 01 — Discovery & Requirements

> Define the problem before writing a single line of code.

```mermaid
mindmap
  root((Discovery))
    Stakeholders
      Business Owners
      End Users
      Tech Leads
      Compliance
    Requirements
      Functional
        What the system does
        User stories
      Non-Functional
        Performance
        Security
        Scalability
      Constraints
        Budget
        Timeline
        Compliance
    Feasibility
      Technical
      Financial / ROI
      Timeline
    Deliverable
      SRS Document
      BRD Sign-off
```

**Key outputs:**

- Business Requirements Document (BRD)
- Software Requirements Specification (SRS)
- Signed stakeholder approval

---

## 02 — System Design

> Blueprint the architecture before building.

```mermaid
graph TD
    HLD[High-Level Design] --> ARCH[Architecture Pattern]
    HLD --> STACK[Tech Stack]
    HLD --> INFRA[Infrastructure]

    ARCH --> M[Microservices]
    ARCH --> MO[Monolith]
    ARCH --> SL[Serverless]

    LLD[Low-Level Design] --> DB[DB Schema / ERD]
    LLD --> API[API Contracts]
    LLD --> COMP[Component Diagrams]

    SEC[Security Design] --> AUTH[Auth Model — OAuth2, RBAC]
    SEC --> ENC[Encryption — at rest & in transit]
    SEC --> COMP2[Compliance — GDPR, SOC2]

    style HLD fill:#028090,color:#fff,stroke:none
    style LLD fill:#00a896,color:#fff,stroke:none
    style SEC fill:#1e2761,color:#cadcfc,stroke:#028090
    style M fill:#161d4a,color:#cadcfc,stroke:#028090
    style MO fill:#161d4a,color:#cadcfc,stroke:#028090
    style SL fill:#161d4a,color:#cadcfc,stroke:#028090
```

**Key outputs:**

- Architecture Decision Records (ADRs)
- API specs (OpenAPI / Swagger)
- Database schema

---

## 03 — Development Environment Setup

> Get every engineer productive from day one.

```mermaid
flowchart TD
    A[Initialise Repo] --> B[Branching Strategy]
    B --> B1[GitFlow]
    B --> B2[Trunk-based]

    A --> C[Local Dev]
    C --> C1[Docker / Docker Compose]
    C --> C2[Makefile one-command setup]
    C --> C3[Secrets via Vault / .env]

    A --> D[CI Pipeline]
    D --> D1[Linting & Formatting]
    D --> D2[Pre-commit Hooks]
    D --> D3[Build on every PR]

    style A fill:#ffc857,color:#1e2761,stroke:none
    style D fill:#028090,color:#fff,stroke:none
    style C fill:#00a896,color:#fff,stroke:none
    style B fill:#028090,color:#fff,stroke:none
```

---

## 04 — Implementation (Coding)

> Building features iteratively with quality gates.

```mermaid
gitGraph
   commit id: "Project init"
   branch feature/auth
   checkout feature/auth
   commit id: "Add login endpoint"
   commit id: "Add JWT signing"
   checkout main
   merge feature/auth id: "PR #1 — Auth merged"
   branch feature/api
   checkout feature/api
   commit id: "REST endpoints"
   commit id: "Input validation"
   checkout main
   merge feature/api id: "PR #2 — API merged"
   branch hotfix/session-bug
   checkout hotfix/session-bug
   commit id: "Fix session expiry"
   checkout main
   merge hotfix/session-bug id: "Hotfix merged"
   commit id: "v1.0.0 🚀"
```

**Engineering practices:**

- Pull requests with mandatory peer review
- Test-driven development (TDD) encouraged
- Feature flags for safe continuous deployment
- Static analysis via SonarQube / Snyk / CodeQL
- SOLID principles and clean code conventions

---

## 05 — Testing Strategy

> Multiple layers of validation before production.

```mermaid
graph BT
    U["🧩 Unit Tests\nFast · Isolated · Mocked"] --> I["🔗 Integration Tests\nModule Boundaries · DB · APIs"]
    I --> E["🌐 E2E / System Tests\nFull User Journeys · Playwright"]
    E --> P["⚡ Performance Tests\nLoad · Stress · k6 / Locust"]
    P --> S["🔒 Security Tests\nOWASP Top-10 · Pen Testing"]
    S --> UAT["✅ UAT\nStakeholder Acceptance · Sign-off"]

    style U    fill:#1e5f74,color:#fff,stroke:none
    style I    fill:#1a7a8a,color:#fff,stroke:none
    style E    fill:#028090,color:#fff,stroke:none
    style P    fill:#00a896,color:#fff,stroke:none
    style S    fill:#02c39a,color:#fff,stroke:none
    style UAT  fill:#ffc857,color:#1e2761,stroke:none
```

| Test Type | Purpose | Tools |
|---|---|---|
| Unit | Individual functions / components | Jest, pytest, JUnit |
| Integration | Module interactions, DB, queues | Supertest, Postman |
| E2E / System | Full user journeys | Playwright, Cypress |
| Performance | Load & stress testing | k6, Locust, JMeter |
| Security | OWASP, pen testing | OWASP ZAP, Burp Suite |
| UAT | Business acceptance | Manual / stakeholders |
| Regression | No new breakages introduced | CI automated suite |

> **Target:** ≥ 80% unit test coverage minimum.

---

## 06 — Staging & Pre-Production

> Production-mirror validation before go-live.

```mermaid
flowchart LR
    DEV[Dev Branch] -->|Merge & build| STG[Staging Environment]
    STG --> SM[Smoke Tests]
    STG --> RT[Regression Suite]
    STG --> PM[Data Migration\nDry Run]
    STG --> PB[Performance\nBenchmarks]

    SM --> GO{Go / No-Go}
    RT --> GO
    PM --> GO
    PB --> GO

    GO -->|✅ Go| PROD[Production]
    GO -->|❌ No-Go| FIX[Fix & Re-deploy]
    FIX --> STG

    style STG  fill:#028090,color:#fff,stroke:none
    style GO   fill:#ffc857,color:#1e2761,stroke:none
    style PROD fill:#00a896,color:#fff,stroke:none
    style FIX  fill:#c0392b,color:#fff,stroke:none
```

**Operational readiness checklist:**

- Runbook written — step-by-step deployment procedure
- Rollback plan documented and tested
- On-call schedule and escalation path confirmed
- Estimated downtime window calculated

---

## 07 — Deployment to Production

> Getting code live safely and confidently.

```mermaid
sequenceDiagram
    participant Dev  as Developer
    participant CI   as CI/CD Pipeline
    participant Reg  as Artefact Registry
    participant Stg  as Staging
    participant Prod as Production

    Dev->>CI: git push / merge to main
    CI->>CI: Build & unit tests
    CI->>CI: Security scan (Snyk / SAST)
    CI->>Reg: Push versioned artefact
    CI->>Stg: Deploy to Staging
    Stg->>CI: Smoke tests ✓
    CI->>Prod: Canary deploy (10% traffic)
    Prod->>CI: Metrics & error rate OK ✓
    CI->>Prod: Full rollout — 100% traffic
    Prod->>Dev: Deployment notification ✅
```

### Deployment Strategies Compared

```mermaid
flowchart TD
    DS[Deployment Strategy] --> BG[Blue / Green]
    DS --> CN[Canary]
    DS --> RO[Rolling]

    BG --> BG1["Two identical envs\nInstant traffic switch\nEasy rollback"]
    CN --> CN1["Gradual traffic shift\nReal-user validation\nKill-switch ready"]
    RO --> RO1["Replace instances\none by one\nZero downtime"]

    style DS fill:#ffc857,color:#1e2761,stroke:none
    style BG fill:#028090,color:#fff,stroke:none
    style CN fill:#00a896,color:#fff,stroke:none
    style RO fill:#1e2761,color:#cadcfc,stroke:#028090
```

---

## 08 — Monitoring & Observability

> You can't improve what you can't measure.

```mermaid
graph TD
    O[Observability Platform] --> L[📋 Logs\nELK · Datadog · Loki]
    O --> M[📈 Metrics\nPrometheus · Grafana]
    O --> T[🔍 Traces\nJaeger · Zipkin · OTEL]

    L  --> AL[Alert: Error spike]
    M  --> AM[Alert: High latency / saturation]
    T  --> AT[Alert: Slow distributed query]

    AL --> IR[Incident Response\nPagerDuty · OpsGenie]
    AM --> IR
    AT --> IR

    IR --> PM[Blameless Post-Mortem\nwritten within 48h]
    PM --> FX[Fix · Deploy · Validate]
    FX --> O

    style O  fill:#ffc857,color:#1e2761,stroke:none
    style IR fill:#028090,color:#fff,stroke:none
    style PM fill:#00a896,color:#fff,stroke:none
    style FX fill:#1e2761,color:#cadcfc,stroke:#028090
```

**The three pillars of observability:**

| Pillar | What it tells you | Example tools |
|---|---|---|
| **Logs** | What happened and when | ELK Stack, Datadog, Loki |
| **Metrics** | How the system is performing | Prometheus, Grafana, CloudWatch |
| **Traces** | Where time is spent across services | Jaeger, Zipkin, OpenTelemetry |

**SLO / SLA framework:**

- Define SLIs (Service Level Indicators) per service
- Set SLOs — e.g. 99.9% uptime, p99 latency < 500ms
- Error budgets balance reliability vs. release velocity

---

## 09 — Maintenance & Iteration

> Production is not the end — it is the beginning.

```mermaid
flowchart LR
    PROD[Production] --> BUG[Bug Reports]
    PROD --> PERF[Performance Data]
    PROD --> USER[User Feedback\n& Analytics]

    BUG  --> TRIAGE[Triage by Severity\nP0 · P1 · P2 · P3]
    PERF --> OPT[Optimisation Tasks\nCaching · Queries · CDN]
    USER --> BACKLOG[Product Backlog\nRefinement]

    TRIAGE  --> SPRINT[Next Sprint]
    OPT     --> SPRINT
    BACKLOG --> SPRINT

    SPRINT --> DEV[Development]
    DEV --> TEST[Testing]
    TEST --> PROD

    style PROD   fill:#ffc857,color:#1e2761,stroke:none
    style SPRINT fill:#028090,color:#fff,stroke:none
    style DEV    fill:#00a896,color:#fff,stroke:none
```

**Ongoing cadence:**

- Monthly dependency and security audits (Dependabot / Renovate)
- Quarterly major version upgrade planning
- DORA metrics review every sprint
- Team retrospectives — no exceptions

---

## Measuring Success — DORA Metrics

```mermaid
xychart-beta
    title "DORA Metrics — Deployment Frequency vs Change Failure Rate"
    x-axis ["Low Performers", "Medium", "High Performers", "Elite"]
    y-axis "Deployments per day" 0 --> 10
    bar  [0.1, 0.5, 2, 8]
    line [0.1, 0.5, 2, 8]
```

| Metric | Elite | High | Medium | Low |
|---|---|---|---|---|
| Deployment Frequency | Multiple/day | Weekly | Monthly | 6+ months |
| Lead Time for Change | < 1 hour | 1 day | 1 week | 1+ month |
| Change Failure Rate | < 5% | < 10% | 15–30% | 45–60% |
| MTTR (restore time) | < 1 hour | < 1 day | 1 day | 1 week |

---

## The Big Picture

```mermaid
flowchart LR
    R([Requirements]) --> D([Design])
    D --> B([Build])
    B --> T([Test])
    T --> S([Stage])
    S --> DEP([Deploy])
    DEP --> MON([Monitor])
    MON --> IT([Iterate])
    IT -->|feedback loop| R

    style R   fill:#028090,color:#fff,stroke:none
    style D   fill:#028090,color:#fff,stroke:none
    style B   fill:#00a896,color:#fff,stroke:none
    style T   fill:#00a896,color:#fff,stroke:none
    style S   fill:#028090,color:#fff,stroke:none
    style DEP fill:#ffc857,color:#1e2761,stroke:none
    style MON fill:#028090,color:#fff,stroke:none
    style IT  fill:#00a896,color:#fff,stroke:none
```

> **Automate everything between commit and production.**
> Ship fast. Fail safe. Learn continuously.
