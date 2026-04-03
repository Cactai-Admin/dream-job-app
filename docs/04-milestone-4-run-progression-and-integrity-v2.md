# DreamJob Milestone 4 Output (Revised v2)

## Milestone Title
Run Progression, Preparation Gate, and Integrity

## Scope
This document locks authoritative stage progression, one-active-preparation-flow enforcement, transition validity, lifecycle writes, and integrity recovery rules.

## Canonical Blocking Progression
1. `listing_review`
2. `run_chat`
3. `resume_review`
4. `cover_letter_review`
5. `ready`

Non-blocking:
- `interview_support`
- `sent`
- later outcome states

## Valid Transition Rules
Only these forward transitions are valid:
- `listing_review -> run_chat`
- `run_chat -> resume_review`
- `resume_review -> cover_letter_review`
- `cover_letter_review -> ready`
- `ready -> interview_support`
- `interview_support -> ready`
- `ready -> sent`

## Required Write Groupings
Every advancement must:
- validate source stage
- validate completion conditions
- write target stage
- write target lifecycle checkpoint
- preserve idempotency / duplicate-submit safety

## Preparation Gate
Only one Run can occupy a blocking preparation stage per user.
This is enforced by the backend, not only by shell UI.

## Auth and Ownership Integrity
The same protection rules apply to both auth modes:
- only the authenticated owner can load or mutate a Run
- progression never depends on Google-vs-password mode
- protected access is based on session validity and `user_id`, not provider type

## Required Backend Services
- `resolveCurrentRun()`
- `resolveEarliestIncompleteBlockingStep()`
- `advanceRunStage()`
- `markApplicationSent()`

## Removed From Prior Version
- route navigation interpreted as progression
- auth-mode-specific stage logic
- UI-only state as source of truth
