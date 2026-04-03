# DreamJob Revised Authority Order (v2)

## Purpose
This file defines the only valid document hierarchy for rebuilding DreamJob from zero.

## Document Priority
1. `00-authority_order-v2.md`
2. `01-milestone-1-foundation-v2.md`
3. `02-milestone-2-shell-and-ux-v2.md`
4. `03-milestone-3-intake-and-listing-review-v2.md`
5. `04-milestone-4-run-progression-and-integrity-v2.md`
6. `05-milestone-5-profile-chat-and-memory-v2.md`
7. `06-milestone-6-doc-review-ready-and-submission-v2.md`
8. `07-milestone-7-company-resolution-and-network-v2.md`
9. `08-milestone-8-hardening-auth-and-beta-v2.md`
10. `09-build-brief-v2.md`
11. `10-execution-brief-v2.md`
12. `11-repo-assembly-package-v2.md`

## Auth Decision That Governs Everything
DreamJob account auth supports exactly two modes, selected by feature flag:

- `AUTH_MODE=google_oauth` (primary)
- `AUTH_MODE=password` (alternate)

Both modes use Supabase Auth and resolve to the same `user_id` ownership model.

LinkedIn companion-session auth remains separate and is never the primary DreamJob identity.

## Non-Negotiable Rules
- No fake auth mode.
- No demo-only identity shortcut.
- No parallel auth architecture.
- No route/page-specific auth branching outside the central auth adapter.
- No static export mode for authenticated app routes.
- No business logic in page components.
- No page or route entrypoint imported as reusable logic.

## How to Resolve Conflicts
- If a prior Codex doc conflicts with these revised milestone docs, these revised docs win.
- If a prior milestone implied a single auth path, reinterpret it to preserve the same ownership and security semantics under the two-mode auth model.
- If an implementation convenience conflicts with system-of-record or auth-boundary rules, implementation convenience loses.

## Explicitly Removed From the Old Direction
The following approaches are deprecated and should not appear in new implementation docs:
- ad hoc "demo auth"
- auth logic split across page files, middleware, and route handlers without a central adapter
- build steps that assume static export for authenticated routes
- legacy Next 14 request-API assumptions
- duplicated auth helper layers that can diverge
- beta-access logic coupled to LinkedIn session state
