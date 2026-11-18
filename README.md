# Orion Quest Live Exam

A React + TypeScript + Vite starting project for the Orion Quest Live Exam platform.

## Included

- Orion deep-red and white brand system, with charcoal dark mode
- Responsive admin dashboard with Bangla-first / English language switch
- Dashboard metrics, activity chart, examination list, status filters and search
- Create-exam draft modal (currently local UI state)
- Supabase client configuration via environment variables
- Initial PostgreSQL schema and row-level security policies in `supabase/schema.sql`

## Requirements

- Node.js 20+
- npm
- A Supabase project for backend features

## Run locally

```bash
npm install
cp .env.example .env
# Set VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY in .env
npm run dev
```

Open the local URL printed by Vite.

## Build

```bash
npm run build
npm run preview
```

## Supabase setup

1. Create a Supabase project.
2. Open SQL Editor and run `supabase/schema.sql`.
3. Configure Authentication providers and email verification.
4. Add the project URL and anon key to `.env`.
5. Create server-side Edge Functions for:
   - registration approval and role assignment
   - exam approval / scheduling / publishing
   - exam start and authoritative deadline creation
   - answer autosave and idempotent submission
   - objective scoring and result publication
6. Configure private Storage buckets for question images and permitted answer attachments.
7. Test RLS with separate super-admin, controller, teacher and student accounts.

## Important production security notes

This repository is a functional frontend foundation, not a complete production examination system. The dashboard currently uses sample data and the create-exam form stores a draft in browser memory only. Do not conduct real examinations until the remaining workflows and server-side controls are implemented and independently tested.

In particular:
- Never expose a Supabase service-role key in Vite/browser code.
- Do not expose MCQ correct-answer keys to student clients.
- Enforce exam start time, deadline, attempt count and submission on the server.
- Use database transactions or server-side RPC/Edge Functions for answer saves and idempotent submissions.
- Review and penetration-test all RLS policies before launch.
- Configure backups, monitoring, rate limits, email delivery and audit retention.

## Suggested implementation sequence

1. Authentication + registration approval + profile onboarding
2. Academic hierarchy and course assignment
3. Question bank with version history and secure answer-key access
4. Exam builder, approval workflow and scheduling
5. Student exam runner with server timer, autosave and reconnect recovery
6. Written answer evaluation and result approval/publication
7. Reports, CSV/Excel import-export, notifications and audit dashboard
