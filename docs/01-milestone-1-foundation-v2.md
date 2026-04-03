# DreamJob Milestone 1 Output (Revised v2)

## Milestone Title
Canonical Foundation Lock

## Scope
This document locks the foundational product model, taxonomy, workflow, ownership model, auth architecture, schema direction, and MVP boundaries for the rebuilt DreamJob codebase.

## Core Product Rules
- DreamJob is mobile-first.
- The app should feel premium, motivating, and game-like without being childish.
- Opportunity is the target object.
- Run is the full active application process for one Opportunity.
- Chat is the guided conversational feature inside the Run.
- Only one application may be in an active preparation state at a time.
- Profile is the persistent user data and capability layer.
- Winning means submitting an application.

## Canonical Product Language
Allowed product nouns:
- Profile
- Opportunity
- Run
- Chat
- Submission
- Results
- Map

Implementation roots remain:
- `user_*`
- `job_listing_*`
- `application_*`
- `application_chat_*`

## Technical Foundation
- Primary framework: Next.js App Router.
- React version target: latest stable React 19 line.
- Next.js version target: latest stable Next.js 16 line.
- Data/auth/storage: Supabase.
- Browser companion: OpenClaw.
- Styling: Tailwind CSS latest stable v4 line.
- Language: TypeScript.

## Auth Architecture Lock
DreamJob account auth uses Supabase Auth with two supported account entry modes behind one feature flag:

- `AUTH_MODE=google_oauth` (primary)
- `AUTH_MODE=password` (alternate)

Both modes:
- authenticate the same DreamJob account system
- produce the same Supabase-authenticated user identity
- resolve to the same `user_id`
- use the same protected-route, session, and ownership logic

LinkedIn companion-session auth remains separate and is only used for LinkedIn-dependent enrichment workflows.

### Auth Non-Re-Deciding Rule
Later docs and implementation may not:
- add a third primary auth mode
- create fake/demo auth shortcuts
- collapse DreamJob account auth and LinkedIn companion-session auth
- fork ownership or authorization rules by auth mode
- treat Google and password users as different product actors

## System-of-Record Rules
Authoritative workflow state belongs to the backend system of record.
Workflow-critical writes must be transaction-safe and backend-authoritative.

This applies especially to:
- listing intake and automatic record creation
- stage advancement
- sent-state transitions
- retry-triggering corrections to company website or LinkedIn company URL

## MVP Workflow
The core Run remains:
1. Opportunity intake from listing URL
2. Automatic extraction and parse attempt
3. Automatic `job_listing` creation
4. Automatic `application` creation
5. Listing Review
6. Chat
7. Resume Review
8. Cover Letter Review
9. Interview Support
10. Submission summary
11. Mark as applied

## Routes
- `/dashboard`
- `/jobs/new`
- `/jobs/[id]`
- `/jobs/[id]/chat`
- `/jobs/[id]/resume`
- `/jobs/[id]/cover-letter`
- `/jobs/[id]/interview-support`
- `/profile`
- `/results`

## Entity Roots
Required entity families:
- `user_profiles`
- `job_listings`
- `applications`
- `application_chat_threads`
- `application_chat_messages`
- application-scoped working tables for keywords / answers / evidence / documents
- support records for company resolution and affiliated-network execution

## Removed From Prior Version
- single-path auth assumption
- implicit beta auth path tied to one login style
- any implementation leaning on static export for authenticated routes
