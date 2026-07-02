# Changelog

All notable changes to reasonix-cruise.

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
