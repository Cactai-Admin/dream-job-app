# DreamJob Milestone 7 Output (Revised v2)

## Milestone Title
Company Resolution and Affiliated Network Connections

## Scope
This document locks company resolution, LinkedIn company-page resolution, affiliated-network scanning, compact assistive display, and the OpenClaw companion boundary.

## Core Rule
DreamJob account auth and LinkedIn companion-session auth remain distinct.

DreamJob account auth:
- protects the app
- owns records
- is required for all app access

LinkedIn companion-session auth:
- is only required for LinkedIn-dependent enrichment work
- never replaces DreamJob account access
- is recovered through Profile

## Company and Network Rules
- Company resolution is assistive and non-blocking by default.
- Listing Review remains usable if required fields are valid even when enrichment is stalled.
- Affiliated-network scanning requires a valid company identity, usable LinkedIn company page, and LinkedIn companion session.
- Results remain compact and secondary to the active Run.

## Required Contracts
- `startCompanyResolution()`
- `saveCompanyCorrection()`
- `retryCompanyResolution()`
- `startAffiliatedNetworkScan()`
- `retryAffiliatedNetworkScan()`
- `loadCompanySupportState()`

## Required Data Boundaries
User-visible canonical fields remain:
- `job_listing_company_name`
- `job_listing_company_website`
- `job_listing_company_linkedin_url`
- `job_listing_affiliated_connections`

## Removed From Prior Version
- any assumption that LinkedIn session state affects DreamJob account admission
- auth-boundary ambiguity between Google/password account access and LinkedIn session recovery
