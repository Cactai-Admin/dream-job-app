# DreamJob Milestone 8 Output (Revised v2)

## Milestone Title
Hardening, Real Auth, and Controlled Beta

## Scope
This document locks stabilization, internal testing, real auth completion, beta access, and launch-governance behavior for the rebuilt architecture.

## Real Auth Model
DreamJob account auth is real from prototype onward and supports:
- Google OAuth (primary)
- email/password (alternate)

Both modes are production-valid and share:
- one middleware path
- one current-user resolver
- one ownership model
- one protected-route model
- one callback/redirect safety policy

## Auth Feature Flag
Supported values:
- `AUTH_MODE=google_oauth`
- `AUTH_MODE=password`

The feature flag must influence only:
- login UI rendering
- auth start action selection
- callback behavior where relevant
- password reset/verification surfaces when password mode is enabled

It must not fork:
- protected-route authorization
- session ownership
- data authorization
- progression logic

## Beta Access
Beta access is layered on top of DreamJob account auth and should use:
- allowlist / invitation rules
- protected account admission
- clear distinction between admitted and non-admitted users

It must not depend on LinkedIn companion-session state.

## Hardening Rules
Before beta:
- protected routes must not statically prerender request-bound auth pages
- auth callback must support Google OAuth code exchange
- password flows must support signup/signin/reset only when password mode is enabled
- redirect targets must be internal-path validated
- middleware matcher must target protected app surfaces only
- RLS and ownership checks must be in place before multi-user beta

## Critical Flow Set
- login
- logout
- protected app access
- intake
- Listing Review
- Chat
- Resume Review
- Cover Letter Review
- `ready`
- sent confirmation
- Profile
- LinkedIn companion-session recovery
- company/network assistive behavior

## Removed From Prior Version
- any proto-auth shortcut or fake login bypass
- auth mode coupled to beta access
- implementation that assumes a single account provider forever
