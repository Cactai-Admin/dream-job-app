# DreamJob Milestone 3 Output (Revised v2)

## Milestone Title
Opportunity Intake and Listing Review Foundation

## Scope
This document locks URL intake, automatic forward movement, create-or-resolve behavior, Listing Review, and the minimum query/save contracts for the new build.

## Intake Rules
A valid listing URL submission must:
1. normalize the URL
2. check preparation gate
3. create-or-resolve the existing listing/application context
4. transition into Listing Review automatically

No separate scrape button is allowed.

## Minimum Required Parsed Fields
Listing Review becomes completion-eligible when these are usable:
- company name
- role title
- role description

Supporting fields may continue hydrating:
- minimum requirements
- nice-to-have requirements
- company website
- company LinkedIn URL
- location
- workplace type
- employment type
- compensation
- affiliated-network support state

## Listing Review Rules
- Listing Review is editable.
- Writes must update the authoritative stored listing record.
- Save behavior may be explicit or autosave, but must not fork state.
- Continue to Chat is enabled only when the required completion threshold is satisfied.
- Company website and company LinkedIn URL must be visible and editable.

## Backend Contract Rules
Required server-side contracts:
- `createOrResolveIntakeContext()`
- `loadListingReviewContext(applicationId | jobListingId)`
- `saveListingReviewFields()`
- `advanceListingReviewToChat()`

## Auth Interaction Rules
Authenticated ownership is always based on `user_id`, regardless of auth mode.
No intake or Listing Review behavior may vary by Google-vs-password account type.

## Security Rules
- authorize every load/save against `user_id`
- validate redirect targets to internal paths only
- do not trust client route changes as proof of progression

## Removed From Prior Version
- prototype shortcuts that assume single-user auth
- intake flows dependent on one login style
- page-owned business logic for create-or-resolve
