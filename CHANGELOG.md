# Changelog

All notable changes to the KitaFix Ionic port are recorded here.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
versioning follows [Semantic Versioning](https://semver.org/) loosely
(pre-1.0.0: milestones, not production).

## [Unreleased]

### Added (Team 3 - Shop & Repair Operations)
- Service history log: technicians (or staff on their behalf) record the action performed, where, when and the details; shown per repair in the queue (`repair_service_logs`, migration 0032).
- Status timeline remarks (FSD 3.13) via `t3_update_repair_status()`; the status dialog now asks for optional remarks.
- Technician role (FSD 3.11 / 3.13): technicians see their own repairs, add notes, view history and log service actions; staff-only actions and the Portal / Services tabs are hidden for them.
- Technician names (not ids) in the technician-change history entries.
- `repair_status_events` read-only view: status-change feed for the reporting module.
- `docs/Repair_Ops_Test_Plan.md`: FSD traceability + manual test cases.

### Fixed
- Technician notes no longer try to mirror into `repairs.staff_notes` (Team 2's guard trigger would reject it).

### Changed (Team 2 - contract change, rule R10)
- New Booking is now a 4-step flow with a free-text `issue_description` instead of the six issue checkboxes.
- Migration `0021_team2_issue_description.sql` adds `repairs.issue_description` (nullable, max 500) and relaxes `repairs_at_least_one_issue`. It must be applied to the hosted project before `useMockData: false` bookings work. `libs/shared-types` was updated by hand to match; regenerate it after applying 0021.
- Dashboard redesigned to the moodboard (Poppins font now in `src/assets/fonts/poppins`).

### Planned
- Team 1 - Identity module (`libs/identity`, migration `0010_team1_identity.sql`)
- Team 3 - Repair Ops module (`libs/repair-ops`, migration `0030_team3_repair_ops.sql`)
- Team 4 - Insights module (`libs/insights`, migration `0040_team4_insights.sql`)

## [0.1.0] - 2026-09-22

### Added
- Team 2 - Booking & Scheduling module (`libs/booking`): customer Dashboard,
  New Booking form, My Repairs list.
- `repairs` booking columns, availability exclusion constraint
  (`repairs_no_double_booking`), customer RLS and the update guard trigger
  (`0020_team2_booking.sql`).
- `get_taken_slots()` database function for the "free slots only" picker.
- Supabase Realtime hook for live status updates.
- `.ts` placeholder data + mock repository so the module runs offline.
- Shared contract types (`libs/shared-types`) generated from the hosted project.
- Hosted Supabase project provisioned with migrations, demo accounts and seed data.
- CI (build) and Release (tagged builds) GitHub Actions workflows.
- Contributor documentation (`CONTRIBUTING.md`, `docs/`).

[Unreleased]: https://github.com/RN22345/KitaFix_IonicPort/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/RN22345/KitaFix_IonicPort/releases/tag/v0.1.0
