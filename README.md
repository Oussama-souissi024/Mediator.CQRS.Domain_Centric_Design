# 🏗️ Mediator.CQRS – Domain-Centric Design

A reference **.NET 8** solution that showcases a clean, domain-centred architecture combining **CQRS**, **MediatR** request/response pipelines, and SOLID principles.

---

## ✨ Why this repo?

• **Domain-Centric Design** – business rules live in the *Core*; all other layers depend on it, never vice-versa.  
• **CQRS** – clear separation between **Commands** (state-changing) and **Queries** (read-only).  
• **MediatR Pipeline** – cross-cutting concerns (validation, logging, performance) are handled by pipeline behaviours, not controllers.  
• **Modular projects** – swap infrastructure (EF Core, Dapper, external APIs) without touching domain logic.

---

## 🗂️ Solution Layout

```
Mediator.CQRS.Domain_Centric_Design-main
│
├── Mediator.CQRS.DCD/            # ASP.NET Core Web API (entrypoint)
│   └── Program.cs / Controllers  # Thin controllers – just MediatR send()
│
├── Mediator.CQRS.Application/    # Use-cases (Commands, Queries, Handlers, Validators, PipelineBehaviours)
│
├── Mediator.CQRS.Core/           # Domain interfaces (e.g. IUserServices)
│
├── Mediator.CQRS.Services/       # Domain services implementations (in-memory demo)
│
├── Mediator.CQRS.Infrastructure/ # Infra concerns (DB, external systems) – currently empty / placeholder
│
├── Mediator.CQRS.Shared/         # DTOs, models, constants
└── Assets/                       # Diagrams, screenshots
```

> The *Application* layer depends on **Core** + **Shared** only.  
> Web API depends on *Application*; **Infrastructure** can be injected where persistence is required.

---

## 📐 Key Building Blocks

| Folder | Purpose |
|--------|---------|
| `Commands/` | Write operations (e.g. `AddUserCommand`) |
| `Queries/`  | Read operations (e.g. `GetUserByIdQuery`) |
| `Handlers/` | Logic executed by MediatR for each command/query |
| `PipelineBehaviour/` | Global behaviours (Validation, Logging, Performance) |
| `Validations/` | *FluentValidation* rules per command/query |

---

## 🏃‍♂️ Getting Started

### Prerequisites

* **.NET 8 SDK**

### Run the API

```bash
# Restore & build
 dotnet restore Mediator.CQRS.DCD.sln
 dotnet run   --project Mediator.CQRS.DCD

# Swagger UI
# → https://localhost:5001/swagger
```

A minimal in-memory user store is pre-seeded in `UserServices.cs`.

### Sample Endpoints

| Verb | Route | CQRS Flow |
|------|-------|-----------|
| GET | `/api/users` | `GetUsersQuery` |
| GET | `/api/users/{id}` | `GetUserByIdQuery` |
| POST | `/api/users` | `AddUserCommand` |

Controllers are intentionally thin – they forward requests to MediatR (`_mediator.Send(...)`).

---

## 🧪 Testing

Add unit tests in a separate `Mediator.CQRS.Tests` project (not included here) to verify:

* Handlers return expected results
* Pipeline behaviours invoke cross-cutting logic
* Domain services obey business rules

---

## 🚧 Roadmap / Ideas

- Replace in-memory services with **EF Core** persistence layer  
- Add **Authentication & Authorization** behaviour  
- Integrate **Serilog** sinks for structured logging  
- Dockerfile & CI pipeline (GitHub Actions)

---

## 🤝 Contributing

1. Fork → feature branch → PR.  
2. Follow conventional commits (`feat:`, `fix:` …).  
3. Keep *Application* layer free of infrastructure dependencies.

---

## 📜 License

This project is open-sourced under the **MIT License**.

---

## 👤 Author

**Oussama Souissi** – [GitHub](https://github.com/Oussama-souissi024)
