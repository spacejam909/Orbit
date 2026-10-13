# Orbit
Goal tracker 
# 🛰️ Orbit — Product Backlog & Engineering Roadmap

This document serves as the single source of truth for upcoming features, technical debt, user stories, and system improvements for the Orbit task management application.

---

## 📌 Epics & Status Overview

| Epic ID | Epic Name | Priority | Status | Target Completion |
| :--- | :--- | :--- | :--- | :--- |
| `EPIC-UX-01` | Core Board UX & Drag-and-Drop | High | 🟢 In Progress | Q4 2026 |
| `EPIC-AI-02` | Claude AI Assistant & Task Automation | High | 🟡 Planning | Q4 2026 |
| `EPIC-AUTH-03` | User Authentication & RLS Policies | High | 🟢 Complete | Q3 2026 |
| `EPIC-SYS-04` | Observability, Performance & Diagnostics | Medium | ⚪ Backlog | Q1 2027 |

---

## 🚀 EPIC-AI-02: Claude AI Integration & Content Generator

> **Goal:** Integrate Anthropic's Claude API to empower users to generate structured content (e.g., travel itineraries, project briefs, task breakdowns) directly in Orbit and automatically turn generated outputs into board tasks.

### `ORB-101` — Secure Claude API Proxy Route
* **Priority:** `Must Have` | **Type:** `Backend` | **Estimate:** `3 Points`
* **User Story:** As an Orbit user, I want a secure Next.js API proxy route for Claude API requests so that my Anthropic API key is never exposed on the client side.
* **Acceptance Criteria:**
  - [ ] Implement `app/api/claude/route.ts` utilizing `process.env.ANTHROPIC_API_KEY`.
  - [ ] Handle POST payloads containing user prompt strings and system parameters.
  - [ ] Return structured JSON responses with proper error status codes (`400`, `401`, `500`).

### `ORB-102` — Interactive AI Assistant Modal (Itinerary & Task Builder)
* **Priority:** `Should Have` | **Type:** `Frontend / UX` | **Estimate:** `5 Points`
* **User Story:** As a user, I want an interactive AI modal where I can prompt Claude for complex ideas (e.g., *"Design a 3-day travel itinerary"*), so I can quickly convert ideas into actionable items.
* **Acceptance Criteria:**
  - [ ] Add an AI button in the header that opens a clean slide-over or modal.
  - [ ] Stream or display formatted Markdown outputs from Claude.
  - [ ] Include a **"Convert to Tasks"** button that parses generated bullet items directly into new rows in the Supabase `issues` table.

---

## 🎨 EPIC-UX-01: Board UX & Swimlane Management

### `ORB-201` — Native Swimlane Drag-and-Drop Persistence
* **Priority:** `Must Have` | **Type:** `Frontend / Realtime` | **Estimate:** `3 Points`
* **User Story:** As a user, I want to drag cards across project swimlanes so that task categories update immediately in real time.
* **Acceptance Criteria:**
  - [x] Integrate `onDragStart` on `TriageCard` and `onDrop` on `SwimlaneRow`.
  - [x] Optimistically update local React state on drop.
  - [x] Persist category changes directly to the Supabase `issues` database table.

### `ORB-202` — Task Detail & Edit Drawer
* **Priority:** `Should Have` | **Type:** `Frontend / UX` | **Estimate:** `5 Points`
* **User Story:** As a user, I want to click on any `TriageCard` to open an editing modal, so I can update titles, priority tags, and project swimlanes without deleting the task.
* **Acceptance Criteria:**
  - [ ] Clicking a task card opens a side drawer with pre-filled task details.
  - [ ] Submitting updates pushes row modifications to Supabase and broadcasts via Realtime.

---

## ⚙️ EPIC-SYS-04: System Health & Diagnostics

### `ORB-401` — Diagnostics & Latency Health Panel
* **Priority:** `Could Have` | **Type:** `DevOps / Monitoring` | **Estimate:** `3 Points`
* **User Story:** As an admin, I want to view database connection status and API latency metrics in the right side panel, so I can monitor workspace health.
* **Acceptance Criteria:**
  - [ ] Replace static text in the Diagnostics tab with real-time ping measurements to Supabase.
  - [ ] Display active WebSocket status indicators.

---

## 📝 Definition of Done (DoD) Checklist

For any ticket in this backlog to be marked as complete (`[x]`), it must satisfy the following:
1. **Code Quality:** Written in TypeScript with zero build errors (`npm run build`).
2. **Persistence:** Tested with Supabase database state and verified in production.
3. **Responsive Design:** Verified using Tailwind CSS across desktop viewport sizes.
4. **Deployment:** Pushed to `main` branch and successfully built on Vercel.
