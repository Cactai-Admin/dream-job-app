# DreamJob Milestone 6 Output (Revised v2)

## Milestone Title
Resume Review, Cover Letter Review, Ready State, and Submission

## Scope
This document locks controlled document review, explicit acceptance, `ready`, Interview Support, and sent-state confirmation.

## Rules
- Resume Review is the first controlled approval stage after Chat.
- Cover Letter Review is the final blocking stage before `ready`.
- `ready` means preparation complete and unsent.
- `sent` means the user explicitly marked the application as applied.
- Opening submission UI is not sent-state.
- Interview Support is available only after `ready` and remains non-blocking.

## Required Backend Contracts
- `loadResumeReviewContext()`
- `saveResumeDraft()`
- `acceptResumeReview()`
- `loadCoverLetterContext()`
- `saveCoverLetterDraft()`
- `acceptCoverLetterReview()`
- `enterInterviewSupport()`
- `exitInterviewSupport()`
- `markAsApplied()`

## Auth Rules
Submission and document review semantics do not vary by auth provider.
Protected ownership is always validated against `user_id`.

## Removed From Prior Version
- any provider-specific sent-state semantics
- any auth shortcut that bypasses document review
