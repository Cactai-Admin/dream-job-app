# DreamJob Execution Brief (Revised v2)

## Execution Order

### Phase 0 — Foundation
1. Create repo and docs
2. Install latest stable framework stack
3. Configure TypeScript path aliases only in tsconfig
4. Configure Tailwind v4-compatible setup
5. Configure Supabase envs

### Phase 1 — Auth-first baseline
1. Build central auth adapter
2. Build Supabase browser/server/middleware clients
3. Build login page supporting auth feature flag
4. Build Google OAuth callback route
5. Build password sign-in/signup/reset surfaces as alternate mode
6. Build logout route
7. Build protected middleware matcher
8. Build current-user resolver
9. Build beta-access admission check

### Phase 2 — Protected shell
1. Build shell layout
2. Build Map / Profile / Results
3. Build shell state resolution
4. Ensure request-bound routes are dynamic and not statically exported

### Phase 3 — Run workflow
1. Intake
2. Listing Review
3. Chat
4. Resume Review
5. Cover Letter Review
6. Ready
7. Interview Support
8. Submission

### Phase 4 — Companion support
1. Company resolution
2. LinkedIn company page resolution
3. affiliated-network scan
4. Profile-managed LinkedIn recovery

### Phase 5 — Hardening
1. RLS
2. route and server tests
3. internal e2e
4. beta access controls

## Auth-Specific Execution Constraints
- Implement Google OAuth callback before expanding deep product workflow.
- Password mode must remain an alternate, not a separate app.
- All account modes must flow through the same current-user/session APIs.
- Beta access must be evaluated after account auth and before protected app entry.

## No-Go Rules
Do not proceed with deeper workflow build if:
- login/logout are not stable
- protected routes still have request-scope errors
- callback exchange is missing
- redirects are not validated
- middleware is too broad or too weak
