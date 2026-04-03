# DreamJob Build Brief (Revised v2)

## Goal
Build the smallest coherent DreamJob MVP around:
- one protected mobile-first app shell
- two-mode DreamJob account auth behind a feature flag
- the canonical Run workflow
- separate LinkedIn companion-session support
- real Supabase-backed ownership and CRUD from the beginning

## Required Stack
- Next.js App Router, latest stable Next.js 16 line
- React latest stable 19 line
- TypeScript
- Supabase Auth + Postgres + Storage
- `@supabase/supabase-js`
- `@supabase/ssr`
- Tailwind CSS latest stable v4 line
- Playwright only after core auth/build path is stable

## Auth Architecture
### Primary
`AUTH_MODE=google_oauth`

### Alternate
`AUTH_MODE=password`

### Central auth adapter responsibilities
- determine active account-entry mode
- render login page accordingly
- perform sign-in start action
- handle callback exchange for Google OAuth
- handle password sign-in / signup / reset flows when enabled
- expose current user/session retrieval
- expose logout
- expose internal-path-safe redirect rules

## Explicitly Out of Scope for v0 rebuild
- fake auth
- one-off demo login shortcuts
- multiple divergent auth helpers
- static export
- legacy Next 14 request-API assumptions
- mixing LinkedIn session into primary app auth

## Required Environment Variables
- `AUTH_MODE`
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SERVICE_ROLE_KEY` (server-only, if needed for admin tasks)
- `NEXT_PUBLIC_APP_URL`
- `GOOGLE_OAUTH_ENABLED`
- `PASSWORD_AUTH_ENABLED`
- `BETA_ACCESS_MODE`
- LinkedIn/OpenClaw env vars in a separate companion section

## Required DB Surface
Minimum tables:
- `user_profiles`
- `beta_access_allowlist` (or equivalent)
- `job_listings`
- `applications`
- `application_chat_threads`
- `application_chat_messages`
- document tables
- company/network support tables

## Security Baseline
- RLS before multi-user beta
- internal redirect validation
- middleware only on protected paths
- server-only Supabase server client
- no page/route import reuse as shared modules
