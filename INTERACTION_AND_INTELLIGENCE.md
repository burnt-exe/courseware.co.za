# DizzyOps interactive experience and intelligence requirements

## Design objective
Build a responsive, animated, highly interactive operations platform for AfrodizzyActs. The existing AfrodizzyActs website is the design reference; audit its actual fonts, colors, imagery, spacing and navigation before final visual sign-off.

## Dashboard intelligence
- Role-aware views: management, bookings coordinators, finance, contractors and performers.
- Interactive KPI cards: upcoming bookings, unfilled roles, performer availability, revenue, outstanding invoices, event profitability and expense approvals.
- Filter by date, event, performer, status and client; filters must update all related charts and tables.
- Drill down from charts and KPI cards into the underlying records; show source, calculation basis and last-updated timestamp.
- Event staffing conflict warnings, double-booking detection, expiring documents, overdue invoices, cost overruns and missing approvals.
- Actionable recommendations: suggest available performers based on skills, location, availability, booking requirements and prior assignments; show why each match is recommended.
- Forecasts for revenue, utilization and cash flow must state assumptions and confidence; never display fabricated predictive values as real data.
- Search, saved views, quick actions, status transitions and inline editing where authorized.

## Animation and interaction
- Subtle page transitions, expanding detail panels, animated but accurate KPI updates, chart transitions, drag-and-drop scheduling with accessible button alternatives.
- Skeleton loading, success/error feedback, confirmations for destructive actions, helpful empty states and undo where practical.
- Respect prefers-reduced-motion; never let animation delay critical tasks.
- Keyboard operability, visible focus, WCAG AA contrast, minimum 44px mobile targets and no horizontal overflow at 320px.

## Functional integrity
- Distinct routes for all 15 sections in DIZZYOPS_SPEC.md; no dead navigation or decorative controls pretending to work.
- Responsive sidebar/drawer, breadcrumbs, route highlighting and consistent navigation hierarchy.
- Use clearly labeled demonstration data until a real backend exists.
- AI suggestions must be distinguishable from verified records; explain recommendations and allow human override.
- Sage and Google Workspace require secure server-side integrations and authorization before presenting live sync.

## Acceptance tests
1. All 15 routes load directly and via navigation, including browser back/forward.
2. Desktop, tablet and mobile navigation and content remain usable.
3. Filters, drilldowns, actions, charts and forms work with actual state or are explicitly marked unavailable.
4. Animation and reduced-motion settings are both tested.
5. No claims of live data, AI forecasts, or external integration without working verified sources.
