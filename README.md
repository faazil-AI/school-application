# School Management System

A production-ready web application for managing madrasa/school operations: students, attendance, fees, reports, staff access, and organization settings.

## Project Overview

The School Management System is a self-hosted platform built for Islamic schools and madrasas. Administrators provision staff by email; users sign in with **Email OTP** or **Google Sign-In**. Role-based access control (RBAC) ensures each staff member only sees and edits what their role allows.

## Features

- **Authentication** — Email OTP (Resend or SMTP) and Google Sign-In for provisioned users only
- **User management** — Admins create staff accounts by email and assign roles
- **Students** — Student records, search, and custom fields
- **Admissions** — Register new students
- **Attendance** — Daily attendance marking, history, and monthly summaries
- **Fees** — Fee collection and status tracking
- **Reports** — Attendance and fee summaries
- **Settings** — Madrasa profile, logo, statuses, and system configuration
- **Audit-ready** — Server-side permission checks on every protected action

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript |
| Database | PostgreSQL 17 |
| ORM | Prisma |
| Auth | Auth.js (NextAuth v5) |
| Email | Resend (primary) / SMTP (fallback) |
| UI | React 19, Tailwind CSS, Radix UI |
| Validation | Zod |

## Installation

### Prerequisites

- Node.js 20+
- PostgreSQL 17
- npm

### 1. Clone and install

```bash
git clone https://github.com/faazil-AI/school-management-system.git
cd school-management-system
npm install
```

### 2. Configure environment

```bash
cp .env.example .env.local
```

Edit `.env.local` with your database URL, `AUTH_SECRET`, and email/OAuth settings (see below).

### 3. Database setup

```bash
npm run db:deploy
SEED_DEV_USERS=false npm run db:seed
```

See [docs/POSTGRESQL_SETUP.md](./docs/POSTGRESQL_SETUP.md) for detailed PostgreSQL setup on Windows.

### 4. Run locally

```bash
npm run dev
```

Open [http://localhost:3000/login](http://localhost:3000/login).

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | PostgreSQL connection string |
| `AUTH_SECRET` | Yes | Random secret (`openssl rand -base64 32`) |
| `AUTH_URL` | Yes | App URL (e.g. `http://localhost:3000`) |
| `NEXT_PUBLIC_SITE_URL` | Yes | Public site URL |
| `NEXT_PUBLIC_DEFAULT_ORG_NAME` | Yes | Organization display name |
| `SEED_ADMIN_EMAIL` | Yes (first deploy) | First admin email |
| `SEED_ADMIN_NAME` | No | Admin display name |
| `RESEND_API_KEY` | Yes* | Resend API key for OTP emails |
| `RESEND_FROM` | Yes* | Verified sender address |
| `GOOGLE_CLIENT_ID` | Recommended | Google OAuth client ID |
| `GOOGLE_CLIENT_SECRET` | Recommended | Google OAuth secret |
| `ALLOW_DEV_LOGIN` | No | `false` in production |
| `SEED_DEV_USERS` | No | `false` in production |
| `SKIP_OTP_ENFORCEMENT` | No | `false` in production |

\* Or use SMTP variables (`SMTP_HOST`, `SMTP_USER`, `SMTP_PASSWORD`, `SMTP_FROM`) instead of Resend.

Full template: [.env.example](./.env.example)

## Deployment Instructions

1. Set all production environment variables (never commit `.env.local`).
2. Run `npm run db:deploy` on the production database.
3. Run `SEED_DEV_USERS=false npm run db:seed` once for roles and the first admin.
4. Build and start:

```bash
npm ci
npm run build
npm run start
```

5. Verify `GET /api/health` returns `200`.
6. Complete the checklist in [docs/DEPLOYMENT_CHECKLIST.md](./docs/DEPLOYMENT_CHECKLIST.md).

## User Roles

| Role | Description | Access |
|------|-------------|--------|
| **Admin** | Full system control | Dashboard, admissions, students, attendance, fees, reports, settings, user management |
| **Teaching Staff** | Classroom and daily operations | Dashboard, students, attendance, fees, reports |
| **Non-Teaching Staff** | Administrative support | Dashboard, students, fees, reports (no attendance management) |

Staff accounts are created by an Admin. Users sign in only after their email has been provisioned.

## Scripts

| Command | Purpose |
|---------|---------|
| `npm run dev` | Development server |
| `npm run build` | Production build |
| `npm run start` | Production server |
| `npm run lint` | ESLint |
| `npm run type-check` | TypeScript check |
| `npm run db:deploy` | Apply migrations |
| `npm run db:seed` | Seed roles, settings, admin |
| `npm run test:rbac` | RBAC smoke tests (dev server required) |

## Documentation

- [Deployment checklist](./docs/DEPLOYMENT_CHECKLIST.md)
- [PostgreSQL setup](./docs/POSTGRESQL_SETUP.md)
- [Development login](./docs/DEV_LOGIN.md) (local only)
- [Gmail SMTP setup](./docs/GMAIL_SMTP_SETUP.md)

## License

Private — all rights reserved unless otherwise specified by the organization.
