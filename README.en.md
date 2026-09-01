# Clinic Workflow

> Automated patient service and workflow management platform for clinics, centered around WhatsApp communication.

[Português](README.md) | [English](README.en.md)

---

## About the project

**Clinic Workflow** is an automated patient service platform designed to centralize and organize communication between patients, clinic staff and healthcare professionals.

WhatsApp will be used as the primary communication channel, while a web dashboard will allow staff to monitor conversations, take over automated interactions, configure automations and analyze operational metrics.

The project is initially being developed as an **MVP**, while maintaining an architecture that can potentially evolve into a production-ready product.

Clinic-specific requirements are currently considered product hypotheses and must be validated before any real-world production adoption.

---

## Goals

The platform is expected to:

* answer frequently asked questions;
* interpret natural-language messages;
* execute deterministic service workflows;
* assist with appointment scheduling;
* assist with rescheduling;
* assist with cancellations;
* transfer conversations to human staff;
* allow clinic staff to take over conversations;
* send reminders;
* collect feedback;
* generate service metrics;
* maintain audit records.

AI will primarily be responsible for **intent interpretation and information extraction**.

Business rules and critical operations will remain under backend control.

The AI **must not diagnose conditions, prescribe medication or make medical decisions**.

---

## Architecture

The architecture follows the principle that business rules belong in the backend.

**n8n** will be used as an automation and orchestration layer rather than as the core of the application.

```text
WhatsApp
    │
    ▼
Webhook
    │
    ▼
n8n
    │
    ▼
Backend
 ├── PostgreSQL
 ├── LLM
 └── Scheduling / Integrations
    │
    ▼
Frontend
```

The application will initially follow a **modular monolith** architecture, keeping domains separated while avoiding the operational complexity of premature microservices.

---

## Technology stack

### Frontend

* Next.js
* TypeScript
* Tailwind CSS
* shadcn/ui

### Backend

* Python
* FastAPI
* SQLAlchemy 2
* Alembic

### Database

* PostgreSQL

### Automation

* n8n

### Infrastructure

* Docker
* Docker Compose

### CI/CD

* GitHub Actions

### Testing

* pytest
* Vitest
* Playwright later in development

### Artificial Intelligence

LLM integration will use an abstraction layer to prevent the application from becoming tightly coupled to a single provider.

---

## WhatsApp

The **Meta WhatsApp Cloud API** is currently the primary option being considered for WhatsApp integration.

The final integration strategy still needs to be validated before implementation.

---

## Human support

The bot must support transferring a conversation to clinic staff.

When a staff member takes control:

```text
Bot active
    │
    ▼
Transfer
    │
    ▼
Human support
    │
    ├── Staff handles the conversation
    │
    └── Bot remains inactive
              │
              ▼
       Support completed
              │
              ▼
       Automation can resume
```

The bot must not interfere while the conversation is under human control.

---

## Users and permissions

The initial system should support at least:

* Administrator
* Secretary / Clinic staff
* Doctor

The architecture should allow future expansion to multiple professionals and medical specialties.

The first specialties considered for the project are:

* Dermatology
* Gynecology

---

## Web dashboard

The administrative dashboard should allow users to:

* monitor conversations;
* inspect conversation status;
* take over conversations;
* return conversations to automation;
* access authorized information;
* configure bot information;
* configure automations;
* view metrics;
* manage users;
* manage permissions.

---

## Security and privacy

Because the platform may process patient-related information, security and privacy are core requirements.

The system should consider:

* LGPD compliance;
* authentication;
* authorization;
* least-privilege access;
* separation of responsibilities;
* logging;
* auditing;
* sensitive data protection;
* access control.

The bot should only receive the information required to perform its role.

Sensitive medical information should not be unnecessarily exposed to the AI model.

---

## Repository structure

The project follows a **monorepo** structure:

```text
clinic-workflow/
├── .github/
├── apps/
│   ├── backend/
│   └── frontend/
├── workflows/
├── docs/
│   ├── requirements.md
│   ├── architecture.md
│   ├── database.md
│   └── decisions/
├── docker/
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

### Main directories

`apps/backend`

API, business rules, persistence, authentication and application integrations.

`apps/frontend`

Web dashboard used by internal platform users.

`workflows`

n8n workflows and automation definitions.

`docs`

Technical documentation covering requirements, architecture and database design.

`docs/decisions`

Architecture Decision Records used to document important technical decisions.

---

## Development process

Development is being conducted incrementally.

Major architectural decisions are evaluated and documented before large implementation tasks begin.

```text
Analyze alternatives
        ↓
Compare trade-offs
        ↓
Make a decision
        ↓
Document it
        ↓
Update Issues
        ↓
Implement
```

Additional technologies and infrastructure will not be introduced without a concrete requirement.

The main priorities are:

* simplicity;
* maintainability;
* security;
* low cost;
* scalability;
* architectural quality.

---

## Current status

The project is currently focused on establishing its technical foundation.

| Stage                      | Status      |
| -------------------------- | ----------- |
| Technology stack           | Completed   |
| System architecture        | Completed   |
| Database modeling          | In progress |
| Service workflows          | Pending     |
| Initial monorepo structure | Pending     |
| Backend implementation     | Pending     |
| Frontend implementation    | Pending     |
| WhatsApp integration       | Pending     |
| MVP                        | Pending     |

The current focus is **database modeling and defining the main entities and relationships of the system**.

---

## Roadmap

### Foundation

* [x] Define technology stack
* [x] Define system architecture
* [ ] Model database
* [ ] Define service workflows

### Initial structure

* [ ] Create monorepo structure
* [ ] Configure Docker environment
* [ ] Configure PostgreSQL
* [ ] Initialize backend
* [ ] Initialize frontend

### Application core

* [ ] Configure authentication and authorization
* [ ] Implement conversation model
* [ ] Implement incoming messages
* [ ] Implement outgoing messages
* [ ] Implement conversation state machine
* [ ] Implement intent classification
* [ ] Implement bot workflows
* [ ] Implement human support handoff

### Dashboard

* [ ] Conversation interface
* [ ] Human support interface
* [ ] Dashboard
* [ ] FAQ configuration
* [ ] Automation configuration

### Automation and metrics

* [ ] Implement reminders
* [ ] Implement feedback collection
* [ ] Implement metrics
* [ ] Implement logging and auditing

### Quality and delivery

* [ ] Tests
* [ ] CI/CD
* [ ] Configure production environment
* [ ] Documentation
* [ ] Prepare MVP demonstration

---

## Architecture decisions

Important decisions are documented using **Architecture Decision Records (ADR)**.

Examples:

```text
docs/decisions/
├── ADR-001-stack-tecnologica.md
└── ADR-002-arquitetura.md
```

This process records not only **what was decided**, but also **why the decision was made** and which alternatives were considered.

---

## Branch strategy

The main branch is:

```text
main
```

Development branches follow:

```text
feature/*
fix/*
refactor/*
docs/*
```

Examples:

```text
feature/whatsapp-integration
feature/authentication
fix/duplicate-messages
refactor/auth-service
docs/update-architecture
```

---

## Commits

Commits follow the **Conventional Commits** specification:

```text
feat:
fix:
docs:
refactor:
test:
chore:
ci:
build:
```

Example:

```text
feat: add conversation state model
```

---

## Project management

Development progress is tracked using GitHub Issues and GitHub Projects.

The Kanban workflow is:

```text
Backlog
   ↓
Todo
   ↓
In Progress
   ↓
Review
   ↓
Done
```

---

## Project status

This project is currently under active development.

Features, integrations and architectural decisions may change as requirements are validated.
