# Subscription Manager API – Project Specification

## 📌 Project Overview
The **Subscription Manager API** is a backend system inspired by OTT platforms such as Netflix and Hotstar.

The system manages:

- Subscription plans
- User subscriptions
- Billing through invoices

This project focuses on building a production-like backend by gradually introducing persistence, authentication, and role-based access.

---

## 🎯 Objective
Build a backend system supporting:

- Browsing subscription plans
- Creating and cancelling subscriptions
- Generating invoices for billing periods
- Paying invoices through API simulation

Invoices represent stored billing data (not PDF documents).

---

## 🧩 Features

### 1️⃣ Subscription Plans
Each plan contains:

- Billing cycle (MONTHLY / YEARLY)
- Price
- Active flag

Rules:
- Only **active plans** are visible to users.
- Plans are seeded in memory for baseline implementation.
- Database integration will be added later (MySQL).

---

### 2️⃣ Subscriptions
Users can:

- Subscribe to a plan
- Cancel an active subscription
- View current subscription
- View subscription history

Rules:
- A user can have **only one active subscription** at a time.
- Subscription lifecycle and important dates must be tracked.

---

### 3️⃣ Invoices
When a subscription is created:

- An invoice is automatically generated.

Invoice states:

- `DUE` – created but unpaid
- `PAID` – marked paid via API

Scope exclusions:
- No payment gateways
- No refunds
- No reminders or discounts

---

### 4️⃣ Roles & Access (Future Design)
Baseline implementation does not enforce roles but APIs should anticipate them.

| Role | Responsibilities |
|------|------------------|
| ADMIN | Manage plans |
| SUPPORT | View subscriptions & invoices, cancel for users |
| USER | Manage own subscription & invoices |

---

## 📏 System Rules

### Plan Visibility
Only active plans are visible and subscribable.

### One Active Subscription
Users cannot hold multiple active subscriptions.

Attempting to subscribe again must return a conflict-style response.

### Invoice Creation
Creating a subscription must:

- Generate an invoice
- Set status = `DUE`
- Match invoice amount with plan price

### Paying Invoices
- Only `DUE` invoices can be paid.
- Payment sets status → `PAID`
- Payment timestamp must be recorded.

### Cancelling Subscriptions
- Only ACTIVE subscriptions can be cancelled.
- Status changes to `CANCELLED`.
- Data must not be deleted.

---

## 👤 Baseline User Identity
Baseline uses a hard-coded current user.

Future versions will introduce:
- JWT authentication
- Spring Security

---

## 🔗 Core APIs

### User APIs
- List active plans
- Subscribe to a plan
- View my subscription & history
- Cancel my subscription
- List my invoices
- Pay invoice

### Support APIs (Future)
- View user subscriptions
- View user invoices
- Cancel subscriptions on behalf of users

---

## 🧱 Baseline Implementation Approach
Before session:

- In-memory repositories
- Seeded plans
- Hard-coded user identity
- REST API endpoints implemented

Session upgrades:
- MySQL + JPA
- JWT Authentication
- Production-ready architecture

---

## 🚀 Learning Goals
- Domain modeling
- REST API design
- Business rule enforcement
- Backend architecture evolution
- Production-style development workflow
