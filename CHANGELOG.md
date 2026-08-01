# Changelog

All notable changes to reasonix-cruise.

## [0.3.0] — 2026-08-01

### Changed
- **Switched to `deepseek-v4-flash`** — the flash tier now beats v4-pro in benchmarks, so `default_model` and the review/security_review subagent overrides point at `deepseek-flash/deepseek-v4-flash`. `deepseek-pro` remains defined as an alternative provider.

## [0.2.0] — 2026-08-01

### Changed
- **config.toml aligned with Reasonix 1.18.0** — `config_version` 3 → 5
- **Removed retired keys**: `[agent] max_steps` and `auto_plan` — 1.18.0 ignores and strips them during config migration (planning is now built into the executor; Plan Mode is an explicit user choice). The old "disable auto_plan" workaround is obsolete.
- **Added 1.18.0 sections/fields**: `[cli]` (update_channel), `[telemetry]`, `[environment]`, `[tools.shell]`, `[secrets]`, `[sandbox] forbid_read`, `[agent] tool_result_snip_ratio` + `recovery_model` + `max_subagent_*`, `[desktop] default_tool_approval_mode` + `update_channel`, `[bot]` queue/control/pairing + approver/admin allowlists, `[tools] mcp_call_timeout_seconds`
- **Fixed provider prices** — the previous ¥ values were stale placeholders; now match the current deepseek-v4 pricing used in the maintainer's live setup (USD, per 1M tokens), so status-bar cost estimates are consistent
- **Updated sandbox docs** for 1.18.0 semantics (enforce on macOS/Linux, forced off on Windows)

### Added
- `cruise.md`: web_fetch/`Fetch` internal-IP SSRF workaround (`curl -sS` via Bash) — backfilled from `88e3fa5`

## [0.1.0] — 2025-07-15

### Added
- `cruise.md` — self-steering agent system prompt (scope assessment, commit discipline, verification gates)
- `config.toml` — reference Reasonix configuration with inline documentation
- `.woodpecker.yml` — example CI pipeline matching cruise.md verification gates
- `spec/README.md` — convention for spec artifacts in medium/large tasks

### Fixed
- **Terminology**: cruise.md "Self-steering" no longer says "YOLO mode" — says "allow mode" matching the actual config enum (`permissions.mode = "allow"`)
- **Verification gates**: Rust verification now includes conditional `cargo deny check` for dependency auditing
- **Session handoff**: memory guidance now includes test-count delta tracking and decision-quality expectations

---

## Versioning

This repo follows [Semantic Versioning](https://semver.org/) for the cruise configuration. `config.toml` version (`config_version`) tracks Reasonix config schema compatibility independently.
