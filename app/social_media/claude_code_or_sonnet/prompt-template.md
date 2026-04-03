# Full-Stack Application Bootstrap Prompt

You are tasked with generating a complete, production-ready full-stack application. Follow the specifications below exactly. The application must be fully functional, well-structured, and containerized with Docker Compose.

---

## Stack

<!-- REPLACE: Define your technology choices below. Change any line independently. -->

- **Frontend:** <!-- e.g. React 18 with TypeScript, Vue 3 with TypeScript, Svelte -->
- **Backend:** <!-- e.g. Node.js with Express, Python with FastAPI, Go with Gin -->
- **Database:** <!-- e.g. PostgreSQL 16, MongoDB 7, MySQL 8 -->
- **Containerization:** Docker Compose (required for all stacks)

---

## Application

<!-- REPLACE: Define domain, entities, and features. Swap this entire section for a different app. -->

### Domain
<!-- e.g. Task Management, E-Commerce, Blog Platform -->

### Entities
<!-- List core entities with their fields and relationships.
Example:
- **User**: id, email, password_hash, name, created_at
- **Task**: id, title, description, status (enum: todo/in_progress/done), user_id (FK), created_at, updated_at
-->

### Features
<!-- List features grouped by area.
Example:
- Auth: register, login, logout, JWT-based session
- CRUD: create/read/update/delete tasks
- Filtering: filter tasks by status
- Ownership: users only see their own tasks
-->

---

## Requirements

### Project Structure
- Monorepo with top-level directories: `frontend/`, `backend/`, `docker/`
- Each directory must have its own dependency manifest and README
- Docker Compose at project root with services: frontend, backend, database
- `.env.example` with all required environment variables documented

### Backend Requirements
- Clear layered architecture: routes/controllers → services/use-cases → data-access/repositories
- Input validation on all endpoints
- Centralized error handling middleware
- Database migrations (not auto-sync) for schema management
- Environment-based configuration (no hardcoded secrets)
- Health check endpoint (`GET /health`)
- API documentation or typed API contract

### Frontend Requirements
- Component-based architecture with clear separation: pages/views, reusable components, API layer
- Centralized API client (single HTTP configuration point)
- Environment-based API URL configuration
- Proper loading and error states on all data-fetching views
- Form validation on all user inputs
- Responsive layout

### Database Requirements
- Schema defined via migrations with up/down support
- Indexes on foreign keys and frequently queried columns
- Seed script for development data
- Connection pooling configured in the backend

### Docker Compose Requirements
- All services start with a single `docker compose up`
- Database data persisted via named volume
- Backend waits for database readiness (healthcheck or wait script)
- Frontend served in production mode (built assets, not dev server)
- Environment variables via `.env` file

### Code Quality
- No TODO comments, no placeholder implementations
- Consistent naming conventions per language idiom
- No god files — each file has a single responsibility
- Reusable utilities extracted where patterns repeat 3+ times
- No over-engineering: no feature flags, no plugin systems, no abstract factories unless the domain demands it
