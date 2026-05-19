# 💰 Financial Dashboard

# In progress.. Will share screenshots soon or else feel free to contact me for more.

- This repository serves as a public showcase for a private codebase. The actual implementation is maintained in a private repo.
- Full-stack financial management platform — actively developed as a product

![.NET](https://img.shields.io/badge/.NET_10-512BD4?style=flat&logo=dotnet&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat&logo=nextdotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat&logo=rabbitmq&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

> 🔒 Source code is private. This repository serves as a public showcase.  
> 150+ developers have cloned this project.

---

## 🧩 Architecture Overview
Next.js 16 (Frontend)
↓ Server Actions + API Client
.NET 10 Web API (Clean/Onion Architecture)
↓ Repository + Service Pattern
PostgreSQL (EF Core 10)
↓ Event-Driven Pipeline
MassTransit v8 + RabbitMQ
↓ Consumers

Persistence Worker
SignalR Notification Worker
OpenAI Summarization Worker

---

## ✅ Key Features

### Frontend (Next.js 16)
- Server Components with server-side data fetching
- Server Actions for form handling with Zod validation
- AG Grid enterprise data grid for customer and invoice management
- Feature-based folder structure (components, hooks, services, types per feature)
- Centralized API client with shared headers and error handling

### Backend (.NET 10 Web API)
- Clean/Onion Architecture with strict layer separation
- Repository + Service pattern with interface-driven DI
- EF Core 10 with PostgreSQL — migrations, navigation properties, projections
- BFF (Backend for Frontend) pattern consolidating multiple API calls
- API versioning with Scalar documentation
- Serilog structured logging
- JWT authentication

### Event-Driven Layer
- MassTransit v8.3.x + RabbitMQ for async messaging
- Three independent consumers:
  - **Persistence Consumer** — saves events to database
  - **SignalR Consumer** — pushes real-time UI updates via Azure SignalR Service
  - **AI Consumer** — triggers OpenAI summarization of comment threads
- Redis caching with event-driven cache invalidation

### DevOps
- One-command Docker Compose local setup
- xUnit test coverage
- GitHub Actions CI pipeline

---

## 🏗️ Folder Structure
Backend/
├── CustomerAPI/          ← .NET 10 Web API
│   ├── Controllers/
│   ├── Services/
│   ├── Repositories/
│   ├── Entities/
│   ├── DTOs/
│   └── Migrations/
├── LogServiceWorker/     ← MassTransit Worker Service
├── EmailWorker/          ← Email notification worker
├── Shared.Contracts/     ← Shared enums, events, DTOs
└── AuthSolution/         ← JWT Auth
financial-dash/           ← Next.js 16 frontend
├── app/
│   ├── dashboard/
│   │   ├── customers/    ← components, hooks, services, types
│   │   └── invoices/     ← components, hooks, services, types
│   └── lib/
│       └── api/
│           └── apiClient.ts

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 16, React, TypeScript, Tailwind, AG Grid |
| Backend | .NET 10, C#, ASP.NET Core Web API |
| ORM | Entity Framework Core 10, PostgreSQL |
| Messaging | MassTransit v8, RabbitMQ |
| Realtime | Azure SignalR Service |
| Caching | Redis |
| Auth | JWT, ASP.NET Core Identity |
| AI | Azure OpenAI |
| DevOps | Docker, Docker Compose, GitHub Actions |
| Testing | xUnit, Moq |

---

## 📸 Screenshots
*Coming soon*

---

## 👨‍💻 Author
**Jasmeet Singh** — Senior Full Stack Developer, Toronto  
[Portfolio](https://jasmeetsinghwasal.netlify.app) · [LinkedIn](https://linkedin.com/in/your-profile) · [Email](mailto:jswasal@gmail.com)
