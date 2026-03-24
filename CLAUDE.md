# Lead Scoring Tool — AI Development Brief

This is an intelligent multi-channel lead scoring system that consolidates leads from HubSpot, ads platforms, and phone systems into a unified scoring and routing engine for sales teams.

## Tech Stack
- Next.js 15 (App Router, Server Components)
- Supabase (PostgreSQL, Auth, Real-time)
- TypeScript (strict mode)
- Tailwind CSS
- Integrations: Slack, ChatGPT, Replicate, Gmail, HubSpot, Facebook/Google Ads, Glowcom

## Project Structure

app/
├── (auth)/              # Login, signup, password reset
├── (protected)/         # All dashboard pages require auth
│   ├── dashboard/       # Main overview dashboard
│   ├── leads/          # Lead management and detail views
│   ├── scoring/        # Scoring rules and configuration
│   ├── validation/     # Email/phone validation tools
│   ├── enrichment/     # Lead enrichment management
│   ├── reports/        # Analytics and reporting
│   ├── integrations/   # API integration management
│   ├── teams/          # Team and user management
│   └── settings/       # System configuration
└── api/                # API routes for integrations

components/
├── ui/                 # Shadcn/ui base components
└── features/           # Business logic components

db/                     # Database access functions only
lib/                    # Business logic, utilities, validation
actions/                # Server actions for mutations
integrations/           # External API clients
types/                  # TypeScript definitions
supabase/               # Database schema and migrations


## Coding Conventions
- **TypeScript strict mode** — no `any` types
- **Server Components by default** — use 'use client' only when needed
- **Data access layer** — all database queries in `/db` directory
- **Business logic** — keep in `/lib` and `/actions`, never in components
- **No secrets in client components** — use server actions for sensitive operations
- **Component organization** — feature-specific components in `/components/features`
- **Conventional commits** — feat:, fix:, docs:, refactor:, etc.

## Database Schema (15 tables)
- **users, organizations, user_organizations** — Auth and team structure
- **lead_sources, leads, lead_activities** — Lead data and tracking
- **scoring_criteria, lead_scores, lead_total_scores** — Scoring engine
- **validations, enrichment_jobs** — Processing workflows
- **routing_rules, lead_assignments** — Lead routing
- **api_integrations, reports** — System management

## Current State: Initial Scaffold
The project has been scaffolded with:
- ✅ Complete database schema with RLS policies
- ✅ Authentication system with role-based access (Manager, Analyst, Sales Rep)
- ✅ Route stubs for all 25 pages from sitemap
- ✅ Integration stubs for all external APIs
- ✅ Basic UI components and layout structure
- ✅ TypeScript types for all database entities

## What to Build Next: v1 Features

### 1. Multi-channel Lead Ingestion API
Build API endpoints (`/api/leads/import`) that connect to HubSpot, Facebook Ads, Google Ads, and Glowcom to automatically capture and centralize all incoming leads into the `leads` table.

### 2. Configurable Lead Scoring Engine
Implement scoring logic in `/lib/scoring.ts` with weighted criteria for email domain validation, phone verification, company size, industry classification, and lead source quality. Store criteria in `scoring_criteria` table.

### 3. Real-time Email and Phone Validation
Integrate third-party validation services that check email deliverability, phone format correctness, and flag disposable contacts. Store results in `validations` table.

## Never Touch (Without Explicit Instruction)
- `.env` files — these contain secrets
- Migration files — database changes need careful review
- RLS policies — security implications need audit
- Authentication middleware — security-critical code

## How to Work on This Project

1. **Always read this file first** before making changes
2. **Run `npm run build`** before committing to catch TypeScript errors
3. **Commit small and often** with conventional commit messages
4. **Document technical debt** explicitly in TECHNICAL_DEBT.md
5. **Test integrations** against real APIs in development
6. **Follow the data flow:** API → validation → scoring → routing → assignment
7. **Security first:** validate all inputs, use server actions for mutations
8. **Performance matters:** use proper indexing, cache API responses

## Integration Priority Order
1. HubSpot (primary CRM)
2. Email/phone validation services
3. Facebook Ads API
4. Google Ads API
5. Glowcom phone system
6. Slack notifications
7. ChatGPT for lead analysis

## Key Workflows to Implement
1. **Lead Import:** External source → validation → scoring → storage
2. **Real-time Scoring:** Criteria change → recalculate all affected leads
3. **Lead Routing:** Score threshold met → assign to sales rep → Slack notification
4. **Enrichment:** Lead created → background job → append data → update score

Remember: This is a production system handling real business leads. Prioritize data integrity, security, and reliability over feature velocity.