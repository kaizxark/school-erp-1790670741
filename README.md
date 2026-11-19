# 🎓 GLOBAL KIDS SCHOOL ERP

[![React](https://img.shields.io/badge/React-v19-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-v5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4.0-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![tRPC](https://img.shields.io/badge/tRPC-v11-2596BE?logo=trpc&logoColor=white)](https://trpc.io)
[![Drizzle ORM](https://img.shields.io/badge/Drizzle_ORM-v0.44-C5F74F?logo=drizzle&logoColor=black)](https://orm.drizzle.team)
[![Recharts](https://img.shields.io/badge/Recharts-v2.15-22B5BF)](https://recharts.org)
[![Vite](https://img.shields.io/badge/Vite-v7-646CFF?logo=vite&logoColor=white)](https://vitejs.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

An enterprise-grade, modern School Management and ERP platform engineered in **React 19**, **Tailwind CSS v4**, and **tRPC v11**. Built to unify academic operations, 2,400+ student profiles, fee collections, attendance logging, examinations, and transportation logistics into a fast, reactive command center.

---

## 🏛️ System Architecture

```mermaid
flowchart TD
    subgraph Frontend["Client-Side (React 19 + Vite 7)"]
        UI["Executive Dashboard & Navigation Shell"]
        Theme["Theme Engine (Dark / Light)"]
        Charts["Analytics Suite (Recharts Area/Bar/Pie)"]
        WouterRouter["Client Routing (Wouter)"]
        TRPCClient["Type-Safe tRPC Client (@tanstack/react-query)"]
    end

    subgraph Backend["Server-Side (Node.js + Express)"]
        TRPCRouter["tRPC v11 Procedure Handlers"]
        AuthMiddleware["OAuth & Session Middleware (jose JWT)"]
        FileService["AWS S3 Storage Client"]
    end

    subgraph Database["Relational Storage (Drizzle ORM)"]
        MySQL[("MySQL Database (Users, Students, Fees, Attendance, Transport)")]
    end

    UI --> WouterRouter
    UI --> Charts
    UI --> Theme
    UI --> TRPCClient

    TRPCClient <-->|End-to-End Type Safety (JSON-RPC)| TRPCRouter
    TRPCRouter --> AuthMiddleware
    TRPCRouter --> FileService
    TRPCRouter <-->|Drizzle ORM Queries| MySQL
```

---

## ✨ Core Modules & Functional Capabilities

### 1. 📊 Executive Overview & Analytics
* **Real-Time KPI Cards**: Instant visibility into total enrollment (2,486 students), active faculty, revenue collected, and daily attendance percentages.
* **Interactive Data Visualizations**: Multi-dimensional charts showing monthly attendance velocity, revenue collection pacing, and academic grade curves powered by **Recharts**.
* **Activity & Notification Feed**: Chronological stream of recent admissions, fee disbursements, and disciplinary updates.

### 2. 👨‍🎓 Student & Faculty Registry
* **Comprehensive Student Records**: Demographics, emergency guardians, medical allergies, blood groups, and previous scholastic records.
* **Staff & Department Roster**: Teacher subject allocations, qualification records, department hierarchies, and payroll categories.
* **Smart Filter & Search**: Global search overlay (<kbd>Cmd/Ctrl + K</kbd>) across student IDs, names, classes, and phone numbers.

### 3. 📝 Academics & Examinations
* **Course & Curriculum Management**: Syllabi structure, subject allocation, lesson plans, and classroom timetable grids.
* **Exams & Grading**: Term examination scheduling, mark-sheet generation, GPA calculations, and customizable report cards.
* **Assignment Tracking**: Homework distribution, submission deadlines, and student grading workflows.

### 4. 💰 Fees, Billing & Financial Management
* **Fee Structure Configuration**: Tuitions, lab fees, sports dues, and annual maintenance charges categorized by grade.
* **Indian Rupee (₹) Transactions**: Real-time payment reconciliation, outstanding balances, partial installment tracking, and printable PDF receipts.
* **Fee Status Dashboard**: Visual breakdown of Paid, Pending, and Overdue student balances with automated reminder flags.

### 5. 🚌 Transportation Logistics
* **Fleet Management**: Bus vehicle numbers, insurance validity, GPS fleet records, and driver contact rosters.
* **Route & Stoppage Coordination**: Morning pickup and evening drop schedules with assigned passenger student manifests.

---

## 📂 Project Organization

```
school-erp/
├── client/                     # Single Page React Application
│   └── src/
│       ├── pages/              # Primary route views (Home, ComponentShowcase, NotFound)
│       ├── components/ui/      # Radix UI + shadcn atomic design system
│       ├── hooks/              # Custom React hooks (theme, search, query)
│       └── lib/                # tRPC client instance, formatters, and utilities
├── server/                     # Node.js + Express Backend
│   └── _core/
│       ├── index.ts            # Server entry point & static asset serving
│       ├── trpc.ts             # tRPC procedure setup & context building
│       ├── env.ts              # Strongly-typed environment schema (zod)
│       └── oauth.ts            # OAuth callback verification & JWT cookies
├── drizzle/                    # Database Architecture
│   └── schema.ts               # Drizzle MySQL table schemas (users, students, fees)
├── shared/                     # Universal Types & Constants
│   └── const.ts                # Shared constants between client and server
└── attached_assets/            # Design mockups, assets, and branding
```

---

## 🚀 Quick Start Guide

### Prerequisites
* **Node.js**: v20.x or higher
* **pnpm**: v9.x or v10.x
* **MySQL Database**: Local instance (MySQL 8.0+) or managed provider (PlanetScale, AWS RDS)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/kaizxark/school-erp.git
   cd school-erp
   ```

2. **Install project dependencies**:
   ```bash
   pnpm install
   ```

3. **Configure Environment Variables**:
   Create a `.env` file in the project root:
   ```env
   DATABASE_URL=mysql://user:password@localhost:3306/school_erp
   JWT_SECRET=your_secure_jwt_secret_token
   AWS_ACCESS_KEY_ID=your_aws_key
   AWS_SECRET_ACCESS_KEY=your_aws_secret
   AWS_REGION=ap-south-1
   AWS_S3_BUCKET=school-erp-documents
   ```

4. **Synchronize Database Schema**:
   ```bash
   pnpm db:push
   ```

5. **Start Development Server**:
   ```bash
   pnpm dev
   ```
   Navigate to [http://localhost:5173](http://localhost:5173) in your browser.

---

## 🛠️ CLI Commands

| Command | Description |
| :--- | :--- |
| `pnpm dev` | Run full-stack development environment with HMR |
| `pnpm build` | Bundle client assets with Vite and bundle server with esbuild |
| `pnpm start` | Run production compiled server (`node dist/index.js`) |
| `pnpm check` | Type-check TypeScript across client, server, and shared |
| `pnpm format` | Auto-format codebase using Prettier |
| `pnpm test` | Run unit and integration tests with Vitest |
| `pnpm db:push` | Generate and execute Drizzle schema migrations |

---

## 📜 License & Author

Developed by **Shaik Mohammed Ehtesham** ([@kaizxark](https://github.com/kaizxark)) under the **MIT License**.
