# Contributing to NullHub

1. **Read [AGENTS.md](AGENTS.md)** and [README.md](README.md) first — the
   architecture (embedded Svelte UI, installer, supervisor) and runtime
   prerequisites are documented there.
2. One concern per PR. No drive-by refactors.
3. Build prerequisites: `npm` (UI build), `zig` 0.16.0.
4. Before every commit:
   - `bash tests/test_backend.sh` — the backend gate CI actually runs; wraps
     `zig build test` + `zig build test-integration`, both with
     `-Dembed-ui=false -Dbuild-ui=false` — 0 failures, 0 leaks
   - `zig fmt --check src/`
   - UI-touching changes: `npm --prefix ui run build` must succeed
5. Every PR runs the 4-target CI matrix (linux-x86_64, linux-aarch64,
   macos-aarch64, windows-x86_64) including backend tests and the e2e suite
   on the native Linux target. Keep it green.
6. Bug fixes must include a regression test citing the issue number.
7. Changes to instance lifecycle (install/restart/uninstall) must account for
   process-tree hygiene: the supervisor owns child processes, and restarts
   must leave exactly one process per instance (see #86).
