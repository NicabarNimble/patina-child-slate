# Changelog

All notable changes to this project will be documented in this file.

The format is based on Keep a Changelog and this project uses Semantic Versioning.

## [Unreleased]

### Added
- Tiered CI model across local pre-commit, push, and PR-to-main stages.
- Local git hook installer and Tier 0 pre-commit checks (`fmt` + `clippy`).
- Tag-driven release workflow that publishes wasm + sha256 artifacts.
- Initial Slate work tracking entries under `layer/slate/work/`.

## [0.1.0] - 2026-05-12

### Added
- Initial standalone `slate-manager` WIT/WASI child extraction from Patina monorepo.
