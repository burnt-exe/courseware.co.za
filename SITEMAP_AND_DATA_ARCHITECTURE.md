# DizzyOps sitemap and data architecture

## Application sitemap
- Dashboard
- People
  - Performers: directory > profile > availability > documents > assignments
  - Contractors: directory > agreements > rates > compliance
- Operations
  - Bookings & Jobs: enquiries > quote > confirmation > staffing > completion
  - Calendar: month/week/day > event > conflict resolution
  - Projects & Events: overview > milestones > budget > team > profitability
- Finance
  - Finance: overview > cash flow > approvals
  - Expenses & Receipts: capture > allocate > approve
  - Invoices & Payments: draft > issue > reconcile
- Resources
  - Documents & Assets: files > inventory > check-out/check-in
  - Reports & Analytics: filters > chart > record drill-down
- Integrations
  - Sage: authorization > field mapping > sync history
  - Google Workspace: authorization > calendars/drive > sync history
- Administration
  - Settings: users > roles > permissions > audit trail
- Performer portal
  - Profile > availability > invitations > assignments > contracts > payments

## Recommended backend
PostgreSQL database behind a secure API. Supabase is a possible managed Postgres/auth/storage provider, subject to approved architecture and data residency requirements. A GitHub Pages site can host the static frontend but cannot itself host the secure database, API or secret-bearing integration services.

## Initial relational entities
users, roles, permissions, performers, performer_skills, availability, contractors, clients, contacts, enquiries, quotes, bookings, booking_assignments, events, projects, milestones, expenses, receipts, invoices, invoice_lines, payments, assets, asset_movements, documents, approvals, notifications, integration_connections, sync_runs, audit_logs.

## Relationships
clients -> bookings -> events; bookings -> booking_assignments -> performers; events -> projects and expenses; bookings -> quotes -> invoices -> payments; documents attach to authorized records; assets allocated to events via asset_movements.

## Security and rollout
- Separate production and demo data. Do not store sensitive performer or payment records in GitHub.
- Implement role-based authorization server-side, least privilege, audit logs, backups and retention controls.
- Apply South African POPIA requirements and verify hosting region, contractual safeguards and cross-border transfer basis.
- Connect Sage and Google only after authorization and API credentials are configured securely.
- Roll out incrementally: (1) responsive navigable prototype, (2) authenticated CRUD + database, (3) booking workflow, (4) finance and approvals, (5) integrations and intelligence.
