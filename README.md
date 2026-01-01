
# 🎓 Moltqa Ecosystem (Multi-University Platform)

<div align="center">

<img src="assets/moltqa_logo.png" alt="Moltqa Logo" width="180" />

<br/>

> **A High-Scale Educational Platform serving 4 Universities and 3,000+ Daily Active Users.**  
> Bridging the gap between Quranic Circles (Halaqat), Students, and Administration via a unified ecosystem.

<br/>

| **Mobile App (Students & Supervisors)** | **Admin Dashboard (Management)** |
|:---:|:---:|
| <img src="https://img.shields.io/badge/Platform-Android%20%7C%20iOS-02569B?style=for-the-badge&logo=flutter" /> | <img src="https://img.shields.io/badge/Platform-Web%20%7C%20Desktop-02569B?style=for-the-badge&logo=googlechrome" /> |

<br/>

<img src="https://img.shields.io/badge/Scale-4%20Universities-orange?style=flat-square" />
<img src="https://img.shields.io/badge/Traffic-3,000+%20DAU-success?style=flat-square" />
<img src="https://img.shields.io/badge/Backend-Supabase-3ECF8E?style=flat-square&logo=supabase" />
<img src="https://img.shields.io/badge/Architecture-Clean%20Architecture-teal?style=flat-square" />
<img src="https://img.shields.io/badge/Error%20Handling-fpdart-purple?style=flat-square" />

</div>

---

## 📖 Executive Summary

**Moltqa Ecosystem** is the digital backbone of Quranic education for **4 major universities**.  
It digitizes the full workflow of:

- Quranic circles (Halaqat)
- Attendance & progress tracking
- Exam scheduling and results
- Administrative reporting

The platform reliably serves **3,000+ Daily Active Users (DAU)** through a scalable architecture focused on performance, caching, and backend-driven logic.

**System Components:**
1. **Mobile App** – Used by students & supervisors for daily operations.
2. **Admin Dashboard** – Used by university administrators for management and analytics.

---

## 🧠 Engineering Decisions for Scale

### 🔐 Multi-Tenancy Architecture
Data isolation is enforced between the **4 universities** using **Row Level Security (RLS)** in Supabase.  
Each user only accesses resources belonging to their university.

### ⚡ Aggressive Caching Strategy
To reduce database load under heavy traffic:
- Implemented local caching using **Hive**
- Cached static entities such as:
  - University Forms
  - Study Circle Metadata  
➡️ Result: **~40% reduction in server load**

### 🧩 Functional Error Handling (`fpdart`)
Errors are treated as values using `Either<Failure, Success>`, ensuring:
- No unexpected crashes
- Explicit handling of edge cases
- Production stability under poor network conditions

---

## 📂 Modular Code Structure

Both applications follow **Feature-First Clean Architecture**,  
but are structured differently based on their responsibilities and scale.

---

### 📱 1. Mobile App Structure
*Optimized for granular feature isolation and shared utilities.*

```text
lib/
├── core/                 # Shared Kernel & Utilities
│   ├── adapters/         # External Adapters (e.g. JSON Parsing)
│   ├── cache/            # Local Caching Logic
│   ├── di/               # Dependency Injection Setup (GetIt)
│   ├── errors/           # Custom Failures & Exceptions
│   ├── models/           # Shared Data Models (e.g. Pagination)
│   ├── router/           # GoRouter Configuration
│   ├── services/         # Global Services (Connectivity, FCM, LocalStorage)
│   ├── theme/            # App Theme & Design Tokens
│   ├── utils/            # Helper Functions & Extensions
│   └── widgets/          # Reusable Shared UI Components
│
├── features/             # Feature-Based Modules
│   ├── auth/             # Authentication & Session
│   │   ├── data/
│   │   │   ├── datasources/
│   │   │   ├── models/
│   │   │   └── repositories/
│   │   └── presentation/
│   │       ├── cubit/
│   │       └── screens/
│   │
│   ├── student/          # Student Ecosystem
│   │   ├── data/         # Exam & Result Repositories
│   │   └── presentation/ # Booking, Results & Profile Screens
│   │
│   ├── moderator/        # Admin & Supervisor Dashboard
│   │   ├── data/         # Management Data Layers
│   │   └── presentation/ # Admin Controls & Statistics
│   │
│   ├── guest/            # Public Access & Onboarding
│   │   └── presentation/ # Landing & Info Screens
│   │
│   └── more/             # Settings & Static Pages
│
└── main.dart             # App Entry Point & Initialization
````

---

### 🖥️ 2. Admin Dashboard Structure

*Optimized for complex workflows and data-heavy operations.*

```text
lib/
├── core/
│   ├── config/           # Environment & App Configuration
│   ├── di/               # Dependency Injection (GetIt)
│   ├── network/          # Network Layer (Supabase Client)
│   ├── router/           # App Navigation (GoRouter)
│   ├── storage/          # Local Storage (Secure Storage/SharedPrefs)
│   ├── theme/            # App Theme & UI Styles
│   └── utils/            # Helper Methods & Constants
│
├── features/
│   ├── auth/             # Authentication
│   │   ├── data/
│   │   │   ├── models/       # Auth Models
│   │   │   └── repositories/ # Auth Repository Implementation
│   │   └── presentation/
│   │       ├── bloc/         # LoginCubit
│   │       └── screens/      # LoginScreen
│   │
│   ├── dashboard/        # Dashboard & Analytics
│   │   ├── data/
│   │   └── presentation/
│   │
│   ├── exams/            # Examination System
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   │
│   ├── halaqat/          # Study Circles Management
│   │   ├── data/
│   │   └── presentation/
│   │
│   ├── users/            # User Management
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   │
│   ├── about_app/        # App Info & Settings
│   ├── content/          # Content Management
│   ├── student_suggestions/ # Student Feedback
│   ├── suggestions/      # General Suggestions
│   └── university_forms/ # University Related Forms
│
└── main.dart             # Application Entry Point
```

---

## 📱 Ecosystem Showcase

### Part 1: Student Experience (Mobile)

*Focused on speed, offline support, and clarity.*

<img src="assets/placeholders/mobile_1.png" width="220" />
<img src="assets/placeholders/mobile_2.png" width="220" />
<img src="assets/placeholders/mobile_3.png" width="220" />

* Smart exam booking with DB constraints
* Attendance & academic progress tracking
* Real-time updates via Supabase Realtime

---

### Part 2: Administration Hub (Web Dashboard)

*Focused on analytics and bulk operations.*

<img src="assets/placeholders/web_1.png" width="350" />
<img src="assets/placeholders/web_2.png" width="350" />
<img src="assets/edge_functions.png" width="350" />

* Real-time analytics for 4 universities
* Advanced filtering & data export
* Server-side monitoring via Edge Functions

---

## 🏗️ Architecture & Quality Assurance

### Robust Error Handling

Using **fpdart**, runtime exceptions are minimized by enforcing explicit failure handling at compile-time.

### Testing Strategy

* Unit tests for critical repository layers
* Ensures data integrity for thousands of concurrent users

<p align="center">
  <img src="assets/testing_structure.png" width="600" />
</p>

---

---

## ☁️ Backend Infrastructure (Supabase)

The backend is built on **Supabase (PostgreSQL)** and acts as the **single source of truth** for the entire ecosystem.

Rather than relying on client-side validation, **business rules, security boundaries, and data consistency are enforced directly at the database level**.

### This design guarantees:
- Strong consistency under concurrent usage
- Predictable behavior during peak exam periods
- Secure multi-university isolation by default

---

## 🗄️ Relational Schema (Production-Grade)

The production database consists of **20+ relational tables**, designed around real-world academic workflows:

- Quranic halaqat management
- Attendance & daily progress tracking
- Exam scheduling, booking, and grading
- Announcements, suggestions, and feedback
- Secure multi-university operations

---

## 📦 Core Domain Tables

| Domain | Tables |
|------|-------|
| **Universities** | `universities` |
| **Users & Identity** | `users`, `user_devices` |
| **Halaqat System** | `halaqat`, `halaqa_members`, `halaqa_posts` |
| **Academic Tracking** | `attendance`, `daily_progress` |
| **Exams** | `exam_slot_templates`, `exam_bookings`, `exam_results` |
| **Content & Communication** | `announcements`, `about_app`, `suggested_texts` |
| **Forms & Feedback** | `university_forms`, `suggestions`, `excuse_requests` |

---

## 🔗 High-Level Domain Relationships

> The diagram below represents a **simplified view** of the core domain relationships.

<p align="center">
  <img src="assets/db_schema_overview.png" width="700" alt="Database Schema Overview" />
</p>

> **Note:**  
> The actual production schema includes additional constraints, enums, and indexes optimized for scale and security.

---

## 🛡️ Database-Enforced Business Rules

Unlike typical CRUD applications, **critical business rules are enforced directly at the database level**, eliminating entire classes of bugs.

### 🚫 Exam Overbooking Prevention
- Exam slots are defined using `exam_slot_templates`
- Database constraints ensure:
  - Capacity limits cannot be exceeded
  - Race conditions are prevented during concurrent bookings

### 🚻 Gender Isolation (Hard Constraint)
Enforced across:
- `halaqat`
- `exam_slot_templates`
- `exam_bookings`
- `announcements`
- `about_app`

➡️ Prevents **any cross-gender data access**, even if the client is compromised.

### 🏢 Multi-Tenancy by Design
- Every major table includes `university_id`
- **Row Level Security (RLS)** guarantees:
  - Complete isolation between universities
  - Zero accidental data leakage
  - Secure shared infrastructure

---

## ⚙️ Server-Side Logic (Edge Functions)

Sensitive workflows are handled using **Supabase Edge Functions**, keeping authority off the client.

| Function | Responsibility |
|--------|----------------|
| `create_user` | Secure user creation & role assignment |
| `notfi_send` | High-priority FCM notifications |
| `delete_user` | Safe user deletion with auth cleanup |

---

## 🔄 Event-Driven Automation

To reduce client-side complexity and ensure reliability:

- Database triggers automatically:
  - Dispatch notifications
  - React to attendance, exam, and post events
- Fully backend-driven
- No polling
- No fragile client orchestration

---

## 🧠 Architectural Rationale

By pushing **validation, security, and business logic into PostgreSQL**, the system achieves:

- Higher reliability under load
- Safer concurrency handling
- Simpler client code
- Clear separation between UI and domain logic

---

## 📬 Contact & Portfolio

**Hashem Soud**
Software Engineer | Flutter & Supabase Expert

<p align="left">
  <a href="LINKEDIN_URL">LinkedIn</a> •
  <a href="mailto:YOUR_EMAIL">Email</a>
</p>

> **Note:**
> This repository is a portfolio demonstration.
> Source code is private due to proprietary logic.

```
