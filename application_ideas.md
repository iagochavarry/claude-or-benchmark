# Application Ideas

A catalog of application ideas for benchmarking. Each idea will become a filled-in `prompt-template.md` on its own `app/<name>` branch.

All apps are similar in complexity: auth + 3-5 entities + relational data + one distinguishing architectural pattern.

---

## 1. Task Manager

**Branch:** `app/task-manager`
**Core pattern:** CRUD + Authentication

Standard task management app. Tests basic layered architecture, JWT auth, and ownership-based data filtering.

**Entities:**
- User: id, email, password_hash, name, created_at
- Category: id, name, color, user_id (FK)
- Task: id, title, description, status (todo/in_progress/done), priority (low/medium/high), category_id (FK), user_id (FK), due_date, created_at, updated_at

**Features:**
- Auth: register, login, logout, JWT-based session
- Tasks: full CRUD, assign to category, set priority and due date
- Filtering: by status, priority, category, due date range
- Ownership: users only see and manage their own data

---

## 2. E-Commerce Store

**Branch:** `app/ecommerce`
**Core pattern:** Stateful multi-step flow

Product catalog with cart and checkout. Tests state transitions (browse → cart → checkout → order), inventory tracking, and transactional consistency.

**Entities:**
- User: id, email, password_hash, name, address, created_at
- Product: id, name, description, price, stock_quantity, image_url, category, created_at
- Cart Item: id, user_id (FK), product_id (FK), quantity
- Order: id, user_id (FK), status (pending/paid/shipped/delivered), total, created_at
- Order Item: id, order_id (FK), product_id (FK), quantity, unit_price

**Features:**
- Auth: register, login, logout
- Catalog: list products, search, filter by category, product detail page
- Cart: add/remove/update quantities, cart summary with total
- Checkout: place order from cart, decrement stock, prevent overselling
- Orders: view order history, order detail with status

---

## 3. Blog Platform

**Branch:** `app/blog-platform`
**Core pattern:** Content management + public/private views

Multi-author blog with comments. Tests rich content handling, pagination, tag-based navigation, and mixed public/authenticated access.

**Entities:**
- User: id, email, password_hash, name, bio, created_at
- Post: id, title, slug, body, status (draft/published), author_id (FK), published_at, created_at, updated_at
- Tag: id, name, slug
- Post_Tag: post_id (FK), tag_id (FK)
- Comment: id, post_id (FK), author_name, author_email, body, created_at

**Features:**
- Auth: register, login, logout (for authors)
- Posts: create, edit, publish/unpublish, delete (authenticated authors)
- Public: list published posts with pagination, filter by tag, view single post
- Comments: public visitors can comment on published posts
- Tags: manage tags, tag-based post filtering

---

## 4. Appointment Scheduler

**Branch:** `app/appointment-scheduler`
**Core pattern:** Booking + date/time logic

Service booking system. Tests availability calculation, time-slot conflict prevention, and calendar-based queries.

**Entities:**
- User: id, email, password_hash, name, role (client/provider), created_at
- Service: id, name, description, duration_minutes, price, provider_id (FK)
- Availability: id, provider_id (FK), day_of_week, start_time, end_time
- Booking: id, service_id (FK), client_id (FK), provider_id (FK), date, start_time, end_time, status (pending/confirmed/cancelled), created_at

**Features:**
- Auth: register (as client or provider), login, logout
- Providers: define services, set weekly availability schedule
- Clients: browse providers and services, view available time slots for a given date
- Booking: book an available slot, cancel a booking, prevent double-booking
- Dashboard: providers see upcoming bookings, clients see their booking history

---

## 5. Analytics Dashboard

**Branch:** `app/analytics-dashboard`
**Core pattern:** Aggregation + read-heavy queries

Metrics dashboard with configurable widgets. Tests aggregation queries, time-range filtering, and charting-ready API responses.

**Entities:**
- User: id, email, password_hash, name, created_at
- Project: id, name, user_id (FK), created_at
- Event: id, project_id (FK), event_type, payload (JSON), timestamp
- Dashboard: id, name, project_id (FK), created_at
- Widget: id, dashboard_id (FK), title, metric (count/sum/avg), event_type_filter, time_range, position

**Features:**
- Auth: register, login, logout
- Projects: CRUD projects, each project collects its own events
- Events: ingest endpoint (POST), bulk insert support
- Dashboards: create dashboards, add/remove/reorder widgets
- Widgets: configurable metric type, event filter, and time range; API returns aggregated data ready for charting
- Time filtering: last 24h, 7d, 30d, custom range

---

## 6. Helpdesk Ticketing

**Branch:** `app/helpdesk`
**Core pattern:** Multi-role access control + status workflow

Support ticket system with customers, agents, and admins. Tests role-based permissions, status state machine, and assignment logic.

**Entities:**
- User: id, email, password_hash, name, role (customer/agent/admin), created_at
- Ticket: id, title, description, status (open/in_progress/waiting/resolved/closed), priority (low/medium/high/urgent), customer_id (FK), agent_id (FK nullable), created_at, updated_at
- Comment: id, ticket_id (FK), author_id (FK), body, is_internal (boolean), created_at
- Tag: id, name
- Ticket_Tag: ticket_id (FK), tag_id (FK)

**Features:**
- Auth: register (as customer), login, logout; admins create agent accounts
- Customers: create tickets, view own tickets, add comments
- Agents: view assigned tickets, pick unassigned tickets, add comments (public + internal notes), change ticket status
- Admins: view all tickets, assign/reassign agents, manage users and tags
- Status workflow: open → in_progress → waiting → resolved → closed (enforced transitions)
- Filtering: by status, priority, assignee, tag
