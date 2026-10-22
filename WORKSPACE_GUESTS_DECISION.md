# Google Workspace Guests — identity decision (October 2026)

## Verified Google guidance
- Workspace Guests became generally available in 2026 and are managed under the Workspace Guests organizational unit.
- Google documents **five free guest accounts per paid Business/Enterprise license**; confirm the actual quota in the client's Admin console. Approximately 90 available guest accounts is a client-reported estimate, not verified.
- Guests can collaborate in supported Chat, Drive, Docs, Sheets, Slides and Meet workflows. They do not have Gmail, Calendar or Gemini in Workspace.
- **Crucial:** Google's documentation says third-party/custom app SSO integration options are **not supported for Workspace guests**, except apps accessing Drive files. Guest accounts are not automatically provisioned to third-party SAML applications. Therefore do not use a Workspace Guest identity as the sole required login mechanism for DizzyOps.
- Directory API user.list includes guest users and the is_guest_user flag; guests can be listed and lifecycle-managed with appropriate admin access. Guest creation API has been documented as open beta.

## Implementation decision
1. Employees: Google Workspace OIDC sign-in, staff directory sync, DizzyOps RBAC.
2. External performers: DizzyOps invitation-based authentication (passwordless email or personal Google sign-in) with role-limited access, independent of Workspace Guest SSO.
3. Optionally link a performer record to their Workspace Guest directory entry, if present, for Google Chat/Drive/Meet collaboration and guest lifecycle tracking.
4. Use the Workspace Admin Directory API only with explicit admin authorization, least-privilege scopes, secure server-side credentials and audit logging.
5. Treat guest quota, SSO behavior and API availability as integration acceptance tests, not assumptions.

## Sources
- https://workspaceupdates.googleblog.com/2026/03/introducing-guest-accounts.html
- https://knowledge.workspace.google.com/admin/users/advanced/manage-workspace-guests
- https://support.google.com/a/answer/ (Google Workspace Help: Overview: Integrate 3rd-party apps with Google Workspace; guest limitation)
- https://developers.google.com/workspace/admin/directory/reference/rest/v1/users/createGuest
