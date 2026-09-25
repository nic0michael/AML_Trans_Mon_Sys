# AGENTS.md

## Project Phase

Phase: `PLANNING`

This is a new project currently in the planning and design phase.

The backend application has not yet been implemented. Framework and Docker
configuration work are tracked separately using task/component states.

---

## 1. Project

* Name: AML Transaction Monitoring System
* Repository: `AML_Trans_Mon_Sys`
* Project Phase: `PLANNING`
* Purpose: Build a containerized AML transaction monitoring system using synthetic transactions, workflow orchestration, business rules and transaction monitoring.
* Primary goal: Demonstrate practical software architecture, Java/Spring Boot, Drools, Python, n8n, PostgreSQL, Docker and AI-assisted development.

---

## 2. Demonstration Objective

The system will demonstrate:

* Generation of synthetic financial transactions.
* Generation of normal and potentially fraudulent transactions.
* Workflow orchestration using n8n.
* Transaction processing using Spring Boot.
* Business-rule evaluation using Drools.
* Persistence using PostgreSQL.
* AML transaction monitoring.
* Automated testing.
* Manual API testing through Swagger/OpenAPI.

---

## 3. Ownership

### ASSIGNED TO US

"US" means the User and ChatGPT.

US is responsible for:

* Architecture decisions.
* Technology choices.
* Project structure.
* Transaction definition.
* Business rules.
* AML detection logic.
* Transaction limits.
* Design decisions.
* Project conventions.
* Deployment decisions.
* Deciding what Codex is assigned to implement.

### ASSIGNED TO CODEX

Codex is responsible only for explicitly assigned implementation tasks.

Codex may:

* Write application code.
* Write tests.
* Fix implementation defects.
* Implement approved designs.
* Add Swagger/OpenAPI where assigned.
* Run appropriate tests and report results.

### NOT ASSIGNED

Anything not explicitly assigned to Codex must not be implemented by Codex.

---

## 4. Codex Core Rule

**Codex must only do or build what is explicitly assigned to Codex.**

If a task requires a decision assigned to US:

1. Stop implementation of that decision.
2. Identify the decision required.
3. Report it to the User.
4. Do not invent a solution.

Codex must not use its own assumptions to replace an unresolved architecture, transaction or business-rule decision.

Codex may make routine implementation-level choices only when they do not conflict with an approved design, project conventions, or explicit instructions from US.

---

## 5. Project Status

The project phase describes the overall lifecycle of the project.

Task and component states describe the progress of individual work items and do not determine the project phase.

Valid task/component states:

* `PENDING`
* `IN_PROGRESS`
* `TESTING`
* `COMPLETED`

A task or component may be `COMPLETED` while the project remains in the `PLANNING` phase.

Current known component status:

| Component                          | State       | Owner |
| ---------------------------------- | ----------- | ----- |
| Project framework                  | COMPLETED   | US    |
| Docker Compose structure           | IN_PROGRESS | US    |
| PostgreSQL container configuration | IN_PROGRESS | US    |
| n8n container configuration        | IN_PROGRESS | US    |
| Transaction definition             | PENDING     | US    |
| AML business rules                 | PENDING     | US    |
| Transaction generator              | PENDING     | US    |
| Backend application                | PENDING     | CODEX |
| Drools integration                 | PENDING     | CODEX |
| Swagger/OpenAPI                    | PENDING     | CODEX |
| Backend tests                      | PENDING     | CODEX |

Status must be updated as work progresses.

---

## 6. Agreed Architecture

The target architecture is:

```text
Transaction Generator
        |
        v
      n8n
        |
        v
Spring Boot Backend
        |
        v
     Drools
      /   \
     /     \
Customer   Transaction
 Rules       Rules
        |
        v
   PostgreSQL
```

US owns all architecture decisions.

Codex must not make or change architecture decisions.

If implementation requires an architecture decision, Codex must stop and report it to US.

---

## 7. Technology Choices

Current agreed technologies:

* Python - transaction generator
* n8n - workflow orchestration
* Java / Spring Boot - backend
* Drools - business-rule engine embedded in backend
* PostgreSQL - persistence
* Docker / Docker Compose - containerisation
* Swagger/OpenAPI - manual REST API testing

US owns all technology choices.

Codex must not choose or change technologies.

If implementation requires a technology decision, Codex must stop and report it to US.

---

## 8. Important Design Decisions

### 8.1 Transaction Structure

**Owner: US**

The transaction structure has not yet been finalized.

Codex must not:

* Invent transaction fields.
* Add transaction fields because they appear useful.
* Change field names.
* Change transaction meanings.
* Define transaction status values.

The approved transaction definition will become the authoritative source for implementation.

### 8.2 Business Rules

**Owner: US**

Business rules are designed by US and implemented by Codex when explicitly assigned.

The following must be defined before Codex implements the AML rules:

#### 8.2.1 Normal Transaction

Define what constitutes a normal transaction.

#### 8.2.2 Money Laundering Transaction

Define the transaction characteristics and patterns that the system should identify as potentially suspicious.

#### 8.2.3 Limits

Define applicable transaction limits and thresholds.

Codex must not invent AML rules, thresholds or limits.

### 8.3 Backend Design

**Owner: US**

US owns and approves the backend design.

Codex must implement the approved backend design only after the required design decisions have been approved and the implementation task has been explicitly assigned.

---

## 9. Project Conventions

* Keep configuration separate from application code.
* Credentials must not be hard-coded.
* Docker Compose configuration belongs under `docker-compose/<container>/`.
* Each container directory contains its own `.env`, `compose.yaml` and `README.md`.
* Use local bind-mounted directories for persistent container data where appropriate.
* Do not introduce unnecessary technologies.
* Prefer simple implementations that demonstrate the agreed architecture.
* Follow existing project naming and directory conventions.
* Do not restructure the project without approval.

---

## 10. Current Implementation

The repository currently contains the initial project framework and Docker Compose configuration work.

Known Docker components:

```text
docker-compose/
├── postgres/
└── n8n/
```

Detailed implementation belongs in the actual project files.

Do not duplicate complete configuration files in this document.

---

## 11. Project Plan

The project plan describes planned work.

Listing a task in the project plan does not constitute an assignment to Codex.

Codex may begin a task only when the User explicitly assigns that task to CODEX.

### 11.1 Define Transactions

State: `COMPLETED`

Owner: US

The transaction structure has been defined and approved.

#### Transaction

| Field                   | Type      | Description                                  |
| ----------------------- | --------- | -------------------------------------------- |
| `transactionId`         | BIGINT    | Internal database primary key                |
| `externalTransactionId` | VARCHAR   | Transaction ID from external system          |
| `transactionTimestamp`  | TIMESTAMP | Date/time transaction occurred               |
| `transactionType`       | VARCHAR   | Transaction type, e.g. `TRANSFER`, `PAYMENT` |
| `amount`                | DECIMAL   | Transaction amount                           |
| `currency`              | CHAR(3)   | Currency code, e.g. `ZAR`                    |
| `reference`             | VARCHAR   | Business/external reference                  |
| `sourceAccount`         | VARCHAR   | Account sending funds                        |
| `sourceCountry`         | CHAR(2)   | Source country                               |
| `destinationAccount`    | VARCHAR   | Account receiving funds                      |
| `destinationCountry`    | CHAR(2)   | Destination country                          |
| `destinationCustomerId` | BIGINT    | Receiving customer's internal ID             |
| `channel`               | VARCHAR   | `ONLINE`, `ATM`, `BRANCH`, etc.              |
| `ipAddress`             | VARCHAR   | IP address associated with transaction       |
| `deviceId`              | VARCHAR   | Device associated with transaction           |
| `locationCountry`       | CHAR(2)   | Country where transaction originated         |
| `status`                | VARCHAR   | Processing status                            |
| `riskScore`             | DECIMAL   | Risk score calculated by monitoring          |
| `riskLevel`             | VARCHAR   | `LOW`, `MEDIUM`, `HIGH`                      |
| `ruleResults`           | JSON      | Rules triggered by monitoring                |

#### Customer

| Field                | Type    | Description                      |
| -------------------- | ------- | -------------------------------- |
| `customerId`         | BIGINT  | Internal database primary key    |
| `externalCustomerId` | VARCHAR | Customer ID from external system |
| `customerType`       | VARCHAR | `INDIVIDUAL`, `BUSINESS`         |
| `customerRiskLevel`  | VARCHAR | `LOW`, `MEDIUM`, `HIGH`          |
| `customerCountry`    | CHAR(2) | Customer's country               |

#### Identity Rules

```text
transactionId          → our database ID
externalTransactionId  → external system ID

customerId             → our database ID
externalCustomerId     → external system ID
```

#### Monitoring

Monitoring results are stored as part of the Transaction record.

This keeps the initial database design simple and avoids introducing a separate monitoring-result table.

The monitoring fields are populated by the transaction monitoring process and are not supplied as trusted values by the transaction generator.


### 11.2 Define Business Rules

State: `COMPLETED`

Owner: US

The initial business rules and risk scoring model have been defined and approved.

The rules are designed to evaluate both:

* Individual transactions.
* Customer transaction history and transaction patterns over time.

The rules, scores and thresholds are project values and may be reviewed and changed by US as the project develops.

#### 11.2.1 Business Rules

| Rule ID | Rule                              | Type                | Score |
| ------- | --------------------------------- | ------------------- | ----: |
| TR-001  | Large Transaction                 | Transaction         |   +30 |
| TR-002  | Out-of-Line Transaction           | Transaction         |   +30 |
| TR-003  | High Risk Country                 | Transaction         |   +40 |
| TR-004  | Structuring / Threshold Avoidance | Transaction Pattern |   +50 |
| TR-005  | Unusual Transaction Frequency     | Transaction Pattern |   +20 |
| CR-001  | High Risk Customer                | Customer            |   +30 |
| CR-002  | Customer Activity Pattern Anomaly | Customer            |   +30 |

#### 11.2.2 Risk Levels

| Total Score | Risk Level | Status    |
| ----------: | ---------- | --------- |
|        0–29 | LOW        | PROCESSED |
|       30–59 | MEDIUM     | REVIEW    |
|         60+ | HIGH       | FLAGGED   |

#### 11.2.3 Out-of-Line Transactions

An out-of-line transaction is a transaction or transaction pattern that differs significantly from the customer's normal or expected activity.

The system should be able to compare current activity with the customer's historical transaction behaviour.

Examples may include:

* An amount significantly higher than the customer's normal transactions.
* A sudden change in transaction frequency.
* A sudden change in transaction location or country.
* A transaction pattern inconsistent with the customer's previous activity.

#### 11.2.4 Structuring / Threshold Avoidance

The system should identify patterns where multiple transactions are made over a period of time that may be intended to avoid triggering a transaction threshold.

The rule must consider multiple transactions rather than evaluating each transaction independently.

Example:

```text
Day 1    R90,000
Day 2    R95,000
Day 3    R92,000
Day 4    R89,000
Day 5    R94,000
----------------
Total   R460,000
```

The individual transactions may not independently trigger the large-transaction rule, but the combined pattern may trigger `TR-004`.

#### 11.2.5 Rule Processing

Multiple rules may trigger for the same transaction.

The risk score is calculated by adding the scores of all triggered rules.

Example:

| Rule                      |   Score |
| ------------------------- | ------: |
| TR-001 Large Transaction  |     +30 |
| TR-003 High Risk Country  |     +40 |
| CR-001 High Risk Customer |     +30 |
| **Total**                 | **100** |

Result:

| Field      | Value     |
| ---------- | --------- |
| Risk Level | `HIGH`    |
| Status     | `FLAGGED` |

Codex must not change, add or remove business rules, scores or thresholds without explicit approval from US.


### 11.3 Deploy Existing Docker Containers

State: `COMPLETED`

Owner: US

Initial containers:

* PostgreSQL
* n8n

Codex is not responsible for deployment unless explicitly assigned.

### 11.4 Build and Test Backend Application

State: PENDING

Owner: CODEX

US owns and approves the backend design and transaction definition.

After these have been approved, Codex may implement the backend only when the User explicitly assigns the implementation task to CODEX.

Codex will implement the approved design, including where assigned:

* Spring Boot backend.
* REST API.
* Transaction processing.
* Drools integration.
* PostgreSQL integration.
* Swagger/OpenAPI.
* Unit tests.
* Integration tests where required.

Codex must implement the approved design and must not redefine it.

---

## 12. Codex Working Procedure

Before starting an assigned task:

1. Read this `AGENTS.md`.
2. Inspect the relevant existing project files.
3. Identify the explicitly assigned task.
4. Confirm that required design decisions are approved.
5. Implement only that task.
6. Do not make unapproved design decisions.
7. Run appropriate tests.
8. Report what was changed.
9. Report tests performed and their results.
10. Report any unresolved issue requiring a decision from US.

A task appearing in the Project Plan is not an assignment.

Stop and ask for clarification when implementation requires an unapproved decision.

---

## 13. Things Codex Must NOT Change

Codex must not change:

* Overall architecture.
* Technology choices.
* Project structure.
* Transaction structure.
* Transaction field definitions.
* Business rules.
* AML detection criteria.
* AML limits or thresholds.
* Docker architecture.
* Component responsibilities.
* Project conventions.
* Ownership boundaries.

Codex may suggest improvements, but must report the suggestion to US rather than implementing it.

---

## 14. Source of Truth

This file defines:

* Codex responsibilities.
* Project boundaries.
* Current high-level state.
* Agreed architectural constraints.

Detailed technical and business definitions should be maintained in dedicated documentation when created.

If another project document conflicts with an explicit Codex instruction in this file, stop and report the conflict rather than choosing an interpretation.
