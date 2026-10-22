# Google Workspace identity and integration architecture

## Decision
Use AfrodizzyActs Google Workspace as the authoritative identity provider for employees, not as the business-data database. Use Google OpenID Connect (OIDC) with Authorization Code + PKCE for sign-in. Validate issuer, audience, expiry, nonce, and the Google Workspace hosted-domain claim (hd) server-side; never rely on the email domain string alone for staff authorization.

## User classes
- Employees: organization-managed Google Workspace accounts; provision/deprovision from Google directory and authorized groups.
- External performers/contractors: separate invited external identity path (Google social login or passwordless email) with limited access; they need not have Workspace licenses.
- Service administrators: dedicated least-privilege role with audit trail and recovery access.

## Authorization
DizzyOps database owns RBAC and record-level access: admin, management, bookings, finance, performer, contractor. Google directory/group membership can inform role assignment but must not directly bypass application policy. Enforce authorization in backend and database, not just frontend navigation.

## Workspace integration scope
- Admin SDK Directory API: staff directory, group memberships and provisioning; requires Workspace admin authorization and suitable scopes.
- Gmail API: send booking confirmations, correspondence threading and optional message retrieval with per-user delegated consent; use least-privilege scopes.
- Calendar API: event scheduling, availability and conflict detection; per-user calendars and authorized shared calendars.
- Google Meet: create meeting links via Calendar conferenceData and use supported Meet APIs for eligible features; don't assume all Meet features are available.
- Drive API: approved document folders, contract links, upload and permissions.
- Contacts / People API: permitted contacts syncing, not unrestricted company directory access.
- Sheets / Docs: optional export, templates, quote generation.
- Tasks / Chat: optional future notifications or task coordination, subject to API capabilities.

## Security and consent
OAuth app configuration and appropriate verification for sensitive/restricted scopes. Keep access and refresh tokens server-side encrypted; no API secrets in GitHub or browser storage. Prefer incremental consent, short-lived sessions, refresh token rotation where supported, scope reviews, webhook validation, retry handling, and revocation/deprovisioning workflows. Respect POPIA, retention rules, and vendor terms.

## Delivery order
1. Register Google Cloud project and configure consent screen and authorized redirect URLs.
2. Implement Google OIDC staff sign-in and backend sessions.
3. Implement RBAC, staff provisioning and offboarding.
4. Integrate Calendar/Meet, then Drive and Gmail, with admin approval.
5. Add sync dashboards, audit logs, monitoring, and failure handling.

No live Google integration exists until the Workspace administrator approves OAuth and implementation/testing is completed.
