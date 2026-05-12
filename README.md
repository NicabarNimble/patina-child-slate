# patina-child-slate

Standalone Slate manager child for Patina.

Slate is a project-living build/refactor/fix workbench. This repository packages
Slate as an app-like Patina child with a strict WIT/WASI boundary:

- host owns authority;
- child owns Slate behavior;
- WIT owns the contract;
- declared toys/WASI capabilities own access.

## Build

Requires Rust, `cargo-component`, and the `wasm32-wasip1` target when prompted by
`cargo component`.

```bash
cargo component build --release
```

The component is written to:

```text
target/wasm32-wasip1/release/patina_ai_child_slate_manager.wasm
```

## Install into Patina

From this repository:

```bash
patina child install . \
  --wasm target/wasm32-wasip1/release/patina_ai_child_slate_manager.wasm \
  --force
```

For local development against a Patina checkout before the installed `patina`
binary has the latest command surface, run the same command through the Patina
source checkout:

```bash
cargo run --manifest-path /path/to/patina/Cargo.toml -- child install . \
  --wasm target/wasm32-wasip1/release/patina_ai_child_slate_manager.wasm \
  --force
```

The installed manifest may need a project-local writable filesystem scope, for
example:

```toml
[needs.scopes.filesystem.project]
path = "/path/to/patina/project"
mode = "read-write"
```

Patina's installer preserves existing local scope additions by default when
reinstalling.

## Use

```bash
patina slate next
patina slate show <work-id>
patina slate check <work-id>
```

Child skill help is exposed through Mother when installed:

```bash
patina mother skills show slate-manager
patina mother skills help slate-manager slate-code
```

## Package contents

- `src/lib.rs` — Slate manager child behavior
- `child.toml` — Patina child manifest
- `wit/` — WIT world and package-style dependency contracts
- `wit-contract/` — Slate control interface contract copy
- `skills/` — child-owned agent skill packages

## License

MIT
