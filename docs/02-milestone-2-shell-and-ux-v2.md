# DreamJob Milestone 2 Output (Revised v2)

## Milestone Title
Mobile-First Shell and UX System

## Scope
This document locks the shell model, navigation, shared UX patterns, and shell-owned states for the rebuilt app.

## Shell Model
The shell supports these top-level destinations:
- Map (`/dashboard`)
- active Run
- Profile
- Results

The shell must:
- be mobile-native
- keep one dominant action visible at a time
- preserve continuity while background enrichment runs
- avoid desktop-dashboard density

## Shared UI Pattern Families
- Overview pattern: Map, Results
- Focused work pattern: Chat
- Controlled review pattern: Listing Review, Resume Review, Cover Letter Review
- Support/control pattern: Profile
- Status/recovery pattern: auth required, locked, stalled, failed, recovering

## Navigation Rules
- If a blocking Run exists, “continue” resolves to the earliest incomplete blocking step.
- Profile never resets the active Run.
- Results never mutates current Run state.
- `ready` is a state, not a required dedicated route.
- Interview Support is non-blocking.

## Auth UX Rules
The shell must present a single DreamJob account concept even though auth has two entry modes.

### Allowed DreamJob account entry surfaces
- Google sign-in button (primary)
- Email/password sign-in form (alternate)
- Password reset and confirmation flows when password mode is enabled

### Disallowed UX
- duplicate login pages for different auth modes
- auth mode–specific app chrome
- LinkedIn session prompts on the primary login screen
- exposing Supabase provider mechanics as product language

## Feature-Flag Rule
The active auth mode is selected centrally. Pages/components should ask the auth adapter what to render, not inspect env flags directly.

## Route Protection Rules
Protected routes live inside the authenticated app shell.
Public auth routes remain outside the protected shell.

Protected:
- `/dashboard`
- `/jobs/*`
- `/profile`
- `/results`

Public:
- `/login`
- `/auth/callback`
- password reset/confirmation routes if used

## Recovery Rules
Auth-required and support-process-required states must be visually distinct:
- DreamJob sign-in required
- LinkedIn companion-session required

They are not the same problem and must not share one message.

## Removed From Prior Version
- waitlist-as-core-auth-surface assumptions
- shell logic coupled to one login provider
- route protection implemented as page-specific ad hoc checks
