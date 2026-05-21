# Kima — /apis render-loop guardrail

- **Date:** 2026-05-21
- **Scope:** `src/aipolicyengine-ui/src/pages/Apis.tsx`
- **Root cause:** The page bootstrapping effect depended on `loadInitialData`, and `loadInitialData` depended on `operationsByApi` even though it also reset `operationsByApi` to a fresh object. That changed the callback identity after every fetch and re-triggered the effect indefinitely.
- **Decision / convention:** Callbacks invoked by mount or refresh effects must depend only on stable values. When they need the latest map/array state for reconciliation, read it through a ref or derive stable IDs first.
- **Why it matters:** This keeps admin pages from self-triggering fetch loops when they reset cached child collections during refresh.
