# Releasing `patina-ai-child-slate-manager`

## Versioning

- Follow SemVer (`MAJOR.MINOR.PATCH`).
- Keep `Cargo.toml` version aligned with release tag (`vX.Y.Z`).
- Record end-user changes in `CHANGELOG.md` under `Unreleased`, then cut a release entry.

## Local preflight

Run before tagging:

```bash
cargo fmt --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test --all-targets
cargo component build --release
```

## Release steps

1. Update `Cargo.toml` version.
2. Move `CHANGELOG.md` entries from `Unreleased` to the new version/date section.
3. Commit release changes.
4. Create and push a tag matching the version:

```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

## CI/CD behavior

- Local pre-commit Tier 0 runs via `.githooks/pre-commit` (installed with `scripts/install-hooks.sh`) and executes `scripts/ci-tier0.sh`.
- `.github/workflows/ci.yml` runs on pushes (non-tag) and enforces Tier 1 + Tier 2 (fmt/clippy/test).
- `.github/workflows/pr-main.yml` runs for pull requests targeting `main`/`master` and enforces Tier 1 + Tier 2 + Tier 3 (fmt/clippy/test/component build).
- `.github/workflows/release.yml` runs on `v*` tags and publishes:
  - `patina_ai_child_slate_manager.wasm`
  - `patina_ai_child_slate_manager.wasm.sha256`
