# EzLedger 
Invoice and customer management for small businesses. Create and manage customers, issue invoices, track payment status, and see updates in real time across every connected user.

Built as a working product rather than a demo - the goal was to design it the way I would design a system at work, including the parts that only matter once real traffic hits it.
Actively developed. Deployed to Azure App Service with GitHub Actions CI/CD.

**Live demo:** available on request - [email me](mailto:jswasal@gmail.com)
and I'll share the link and a demo login.

**Dashboard** - stats, insights, and recent invoices 
> Other screenshots towards the end : 

<img width="1384" alt="Dashboard" src="https://github.com/user-attachments/assets/0eccbf68-17a3-46d7-b46d-20bf5519efb6" />


> The source code is private. This repository is a public showcase of the architecture, feature set, and engineering decisions behind it.

![.NET](https://img.shields.io/badge/.NET_10-512BD4?style=flat&logo=dotnet&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat&logo=nextdotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat&logo=rabbitmq&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

---

## Architecture

```text
Next.js 16 (Frontend)
  - Server Components + Server Actions + Client components
  - Centralized API client
        |
        v
.NET 10 Web API (Onion Architecture for Auth project + N Tier for others)
  - Controllers -> Services -> Repositories
  - BFF endpoints for composed dashboard reads
        |
        +--> PostgreSQL (EF Core 10)
        |
        +--> Redis (read cache)
        |
        v
MassTransit v8 + RabbitMQ (event bus)
        |
        +--> Persistence Consumer   - writes the event/audit record
        +--> SignalR Consumer       - pushes live updates to clients
        +--> AI Consumer            - OpenAI summarization of comment threads
```

---

## Engineering notes : 

---

## Features

### Frontend - Next.js 16
- Server Components with server-side data fetching
- Server Actions for form handling, validated with Zod
- AG Grid for customer and invoice tables - sorting, filtering, pagination
- Real-time toast notifications driven by SignalR
- Centralized API client handling auth headers and error normalization

### Backend - .NET 10 Web API
- Clean / Onion architecture with strict layer separation in AuthSolution only
- Repository + Service pattern, interface-driven dependency injection, for projects other than AuthSolution
- EF Core 10 against PostgreSQL - migrations, navigation properties, projections
- API versioning with Scalar documentation
- JWT authentication via ASP.NET Core Identity
- Serilog structured logging

### Event-driven layer
- MassTransit v8 over RabbitMQ
- Persistence, SignalR, and AI summarization consumers running independently
- Redis caching with event-driven invalidation

### DevOps
- One-command local setup with Docker Compose
- xUnit and Moq test coverage
- GitHub Actions CICD pipeline, deploying frontend and API to Azure App Service via OIDC

---

## Tech stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 16, React, TypeScript, Tailwind, AG Grid |
| Backend | .NET 10, C#, ASP.NET Core Web API |
| Data | Entity Framework Core 10, PostgreSQL |
| Messaging | MassTransit v8, RabbitMQ |
| Real time | Azure SignalR Service |
| Caching | Redis |
| Auth | JWT, ASP.NET Core Identity |
| AI | Azure OpenAI |
| DevOps | Docker, Docker Compose, GitHub Actions, Azure App Service |
| Testing | xUnit, Moq |

---

## Project layout

```text
Backend/
├── CustomerAPI/          .NET 10 Web API
│   ├── Controllers/
│   ├── Services/
│   ├── Repositories/
│   ├── Entities/
│   ├── DTOs/
│   └── Migrations/
├── LogServiceWorker/     MassTransit worker - persistence
├── EmailWorker/          MassTransit worker - email notifications
├── Shared.Contracts/     Shared events, enums, DTOs
└── AuthSolution/         Onion Architecture + JWT authentication

financial-dash/           Next.js 16 frontend
├── app/
│   ├── dashboard/
│   │   ├── customers/    components, hooks, services, types
│   │   └── invoices/     components, hooks, services, types
│   └── lib/
│       └── api/
│           └── apiClient.ts
```

---

## Screenshots

**Login**

<img width="1056" alt="Login page" src="https://github.com/user-attachments/assets/c4e3632e-0a65-42ff-8ba0-949e5bae6dec" />

**Dashboard** - stats, insights, and recent invoices 

<img width="1384" alt="Dashboard" src="https://github.com/user-attachments/assets/0eccbf68-17a3-46d7-b46d-20bf5519efb6" />

**Loading state** - placeholders render immediately while the composed call is in flight

<img width="1381" alt="Dashboard loading placeholders" src="https://github.com/user-attachments/assets/c23b036e-0e9f-41dc-9473-3b2248bc07a3" />

**Real-time notifications along with invocies page** - SignalR pushes updates to every connected client

<img width="1375" alt="Real-time SignalR notifications" src="https://github.com/user-attachments/assets/3ea21ad2-4563-4224-b003-baf60840314f" />

**Customers**

<img width="1380" alt="Customers" src="https://github.com/user-attachments/assets/2e81bace-2c69-4449-953f-04333414c280" />


---

## Author

**Jasmeet Singh Wasal** - Senior Full Stack Developer, Greater Toronto Area

[Portfolio](https://jasmeetsinghwasal.netlify.app) · [LinkedIn](https://linkedin.com/in/ADD-YOUR-HANDLE) · [Email](mailto:jswasal@gmail.com)
