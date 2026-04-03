# DreamJob Milestone 5 Output (Revised v2)

## Milestone Title
Profile, Chat, and Memory Boundaries

## Scope
This document locks Profile reusable data, Chat as a guided preparation workspace, application-scoped working material, reusable-memory confirmation rules, and auth-related Profile responsibilities.

## Profile
Profile owns:
- reusable keywords
- reusable answers
- reusable evidence
- reusable strengths
- DreamJob account preferences relevant to auth/session display
- LinkedIn companion-session recovery controls

Profile does not own current Run progression.

## Chat
Chat is:
- guided
- bounded
- listing-aware
- application-scoped first

Chat is not:
- freeform assistant mode
- implicit stage advancement
- reusable-memory auto-promotion
- document approval

## Memory Promotion Rules
Nothing becomes reusable memory automatically.
Promotion requires explicit user confirmation or edit-then-confirm.

## Auth Responsibilities in Profile
Profile must present:
- current DreamJob account session status
- the active DreamJob account email/identity
- Google-vs-password account metadata only if useful, and never as the primary UX concept
- LinkedIn companion-session recovery state separately

Profile must not:
- mix DreamJob account login with LinkedIn companion-session controls
- present different capability semantics by provider

## Required Backend Contracts
- `loadChatContext()`
- `saveApplicationScopedChatWork()`
- `completeChatCheckpoint()`
- `loadReusableProfileData()`
- `saveReusableProfileData()`
- `promoteReusableMemoryItem()`

## Removed From Prior Version
- memory promotion by passive use
- chat semantics tied to one login provider
- profile surfaces that behave like settings-only pages
