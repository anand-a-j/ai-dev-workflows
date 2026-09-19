# DMRoot — MVP Architecture Skill

## Purpose

DMRoot is a SaaS product for Instagram DM automation.

Build the MVP as a **simple, maintainable ASP.NET Core modular monolith**.

Initial scope:

* Authentication
* Profile
* Settings
* Subscriptions / pricing
* Account deletion

Instagram automation comes later.

## Core Rules

* Build brick by brick.
* Prefer the simplest production-ready solution.
* Do not add abstractions before they are needed.
* Do not introduce queues, workers, event pipelines, or Instagram-specific architecture prematurely.
* PostgreSQL is the durable source of truth.
* Redis is for transient/distributed infrastructure only.
* Keep API and Worker independently deployable.

## Stack

**Backend**

* ASP.NET Core / .NET
* C#

**Database**

* PostgreSQL
* Npgsql
* Hand-written SQL
* No Entity Framework Core
* No EF migrations

**Redis**

* Cache
* Rate limiting
* Temporary state
* Distributed locks
* Idempotency
* Redis Streams when async processing is actually required

**Background Processing**

* .NET `BackgroundService`
* Separate `DMRoot.Worker` process

**Future Integrations**

* Meta Graph API
* Instagram API

Add these only when the SaaS foundation is stable.

## Repository Structure

```text
DMRoot/
│
├── src/
│   ├── DMRoot.Api/
│   ├── DMRoot.Application/
│   ├── DMRoot.Core/
│   ├── DMRoot.Infrastructure/
│   └── DMRoot.Worker/
│
├── docker/
│
├── .github/
├── .vscode/
├── .env.example
├── .gitignore
├── Directory.Build.props
├── Directory.Packages.props
├── docker-compose.yml
├── README.md
└── DMRoot.sln
```

### `src/`

Contains all application source code.

### `DMRoot.Api`

HTTP/API layer.

Responsible for:

* Controllers / endpoints
* Middleware
* Authentication configuration
* Request/response handling
* API composition

### `DMRoot.Application`

Application/use-case layer.

Responsible for:

* Business use cases
* Application services
* Commands / queries
* DTOs
* Interfaces for required infrastructure

### `DMRoot.Core`

Domain/core layer.

Responsible for:

* Domain entities
* Value objects
* Enums
* Domain rules
* Domain exceptions

Must remain independent of infrastructure.

### `DMRoot.Infrastructure`

External implementation layer.

Responsible for:

* PostgreSQL/Npgsql
* Redis
* Authentication persistence
* Email providers
* External services
* Repository implementations

### `DMRoot.Worker`

Separate background-processing process.

Use only when asynchronous processing is required.

It may depend on:

* `DMRoot.Application`
* `DMRoot.Infrastructure`
* `DMRoot.Core`

## Dependency Direction

```text
                    ┌──────────────┐
                    │ DMRoot.Api   │
                    └──────┬───────┘
                           ↓
                    ┌──────────────┐
                    │ Application  │
                    └──────┬───────┘
                           ↓
                    ┌──────────────┐
                    │     Core     │
                    └──────────────┘

Infrastructure ───────────────→ Core
     ↑
     │
Application ←── Worker
```

Rules:

* `Core` depends on nothing.
* `Application` depends on `Core`.
* `Infrastructure` implements Application abstractions and depends on `Core`.
* `Api` composes the application and infrastructure.
* `Worker` is independently deployable.
* Avoid circular dependencies.

## Data Ownership

### PostgreSQL

Source of truth for durable data:

* Users
* Profiles
* Subscriptions
* Account state
* Persistent configuration

### Redis

Transient/distributed state:

* Cache
* Rate limits
* Temporary state
* Distributed locks
* Idempotency
* Streams

Never use Redis as the primary database.

## Development Rules

When implementing a feature:

1. Start with the simplest synchronous implementation.
2. Put domain rules in `Core`.
3. Put use cases in `Application`.
4. Put external/database implementations in `Infrastructure`.
5. Keep HTTP concerns in `Api`.
6. Add Redis only when its use is justified.
7. Add `Worker`/Redis Streams only when background processing is required.
8. Do not create generic abstractions without a concrete need.

## AI Coding Rule

Before adding architecture, ask:

> "Is this required by the current feature?"

If not, do not add it.

Prefer **simple, explicit, maintainable code** over premature scalability or abstraction.
