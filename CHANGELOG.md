# Changelog

All notable changes to this plugin are documented here.

This project follows Semantic Versioning. The GitHub Release and matching `vX.Y.Z` tag are the authoritative release records.

## [0.4.0] - 2026-07-15

### Added

- `prd-replan` for plan-only, high-risk decision review before implementation.
- Replan Decision Record templates with alternatives, ADR-lite, sequential review, and verification expectations.
- Router support for `리플랜` and `replan this` requests.

### Changed

- The shared PRD workflow state now tracks Replan as an optional stage before execution handoff.
- Replan explicitly ends in `pending approval`; it cannot start `goaljaby`, `/goal`, implementation, deployment, or external updates.

## [0.3.0] - 2026-07-10

### Added

- Initial public PRD workflow plugin bundle, including PRD authoring, review, acceptance, instrumentation, and optional `goaljaby` handoff.
