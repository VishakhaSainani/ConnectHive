# ConnectHive — Architecture & Technical Decisions Record

This document records all architectural, technical, and product design decisions made for the ConnectHive platform. Every key decision is documented with its context, rationale, and consequences to ensure clarity and continuity throughout the development lifecycle.

---

## Decision Index

| ID | Title | Date | Status |
| :--- | :--- | :--- | :--- |
| **ADR-001** | [Core Technology Stack](#adr-001-core-technology-stack) | 2026-10-28 | **Accepted** |

---

## ADR-001: Core Technology Stack

- **Date:** 2026-10-28
- **Status:** Accepted
- **Deciders:** Project Lead / Architectural Review

### 1. Context & Problem Statement
ConnectHive is a multi-tenant villa hospitality platform serving two distinct workloads:
1. **High-traffic, zero-auth public guest requests** initiated via QR code scans that demand minimal latency, high availability, and rapid rendering.
2. **Authenticated, role-based dashboards** for Superadmins, Villa Vendors, and Villa Owners requiring structured CRUD operations, granular access boundaries, audit logging, and dynamic layout/theme customization.

We need a foundational technology stack that provides:
- Strong relational data integrity with native support for tenant isolation.
- High-concurrency, low-latency, and memory-efficient backend execution.
- A modern, reactive, and component-based frontend capable of driving both the responsive guest portal and complex administrative dashboards.

### 2. Decision

We adopt the following core technology stack:

1. **Database:** **PostgreSQL**
   - **Rationale:**
     - Mature, ACID-compliant relational database ideal for strict relational boundaries (vendors -> villas -> owners -> content).
     - Powerful `JSONB` support allows structured storage of flexible, schema-less per-villa theme and layout configurations without requiring separate NoSQL data stores.
     - Robust indexing, foreign-key constraints, and potential for PostgreSQL Row Level Security (RLS) to enforce multi-tenant isolation.
     - Strong support for full-text search, audit logging, and timeseries/aggregation queries for analytics.

2. **Backend:** **Go (Golang)**
   - **Rationale:**
     - High performance, lightweight goroutine-based concurrency, and low memory footprint — ideal for handling sudden spikes in guest QR scans.
     - Statically typed and compiled into single binary artifacts, simplifying deployment and containerization.
     - Clean, idiomatic standard library and battle-tested ecosystem for building robust RESTful APIs with strict validation.
     - Strong security profile and low vulnerability surface area compared to heavy runtime environments.

3. **Frontend:** **React**
   - **Rationale:**
     - Mature component-based architecture allowing reusable UI blocks across guest pages (gallery, menu, Wi-Fi card, experiences) and dashboard preview panels.
     - Rich ecosystem of charting libraries, state management, and accessible component primitives for building administrative portals (Superadmin, Vendor, Owner).
     - Excellent mobile-first responsiveness capabilities to ensure the guest experience feels seamless on all mobile devices.

### 3. Consequences & Follow-up Technical Questions
With the core stack agreed upon, the immediate technical considerations to establish are:
1. **Go Framework & Toolkit:**
   - Lightweight idiomatic router (e.g., `chi` or `net/http`) vs. microframework (e.g., `gin`, `fiber`).
   - Database interaction layer: Type-safe SQL generator (e.g., `sqlc` + `pgx`) vs. ORM (e.g., `gorm`).
2. **React Tooling & Dialect:**
   - Single-Page Application (SPA) bundle using **Vite + TypeScript** vs. SSR framework.
   - Separate apps/routes vs. a unified SPA with role-based routing (e.g., `/v/:slug` for guests, `/app/*` for authenticated users).
3. **Repository Structure:**
   - Monorepo layout (e.g., `/backend` in Go and `/frontend` in React) to keep API schemas, documentation, and coordination unified.
