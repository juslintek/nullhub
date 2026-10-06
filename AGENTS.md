# Repository guidance

NullHub is a Zig application with an embedded SvelteKit UI in `ui/`. Read `README.md` for setup and architecture; start backend/API work in the relevant `src/` module and UI work in the matching `ui/src/` route or component. `build.zig` builds the UI before embedding it by default.

- For backend changes, run `zig build test -Dembed-ui=false -Dbuild-ui=false --summary all`; run `zig build test-integration -Dembed-ui=false -Dbuild-ui=false --summary all` when HTTP behavior changes. CI runs `bash tests/test_backend.sh`.
- For UI changes, run `npm --prefix ui ci` when dependencies are absent, then `npm --prefix ui run build`. The UI also has a focused `npm --prefix ui run test:mission-control` check for replay automation changes.
- Keep changes focused and follow nearby Zig and Svelte patterns. Preserve local-first behavior and do not expose instance configuration, logs, or credentials. Do not claim runtime or deployment checks unless they were run.
- Do not publish or deploy unless explicitly requested.
