# Updating this FlexGate repository

Do **not** develop the plugin here. Build and verify in the private µGulp™ main project, then copy the checked distribution into this public repo.

## Repeatable flow

1. In the private main project, produce or confirm a verified marketplace pack, e.g.  
   `packages/marketplace/microgulp-flexbar_marketplace_V<version>.flexplugin`
2. Run the official check there:  
   `flexcli plugin validate --path <extracted-plugin-folder>`  
   Record SHA-256 of that `.flexplugin` before any FlexGate-specific edits.
3. Extract the pack into a clean staging folder (plugin root = `manifest.json` + `backend/` + `ui/` + `resources/`).
4. Set `manifest.json` → `repo` to:  
   `https://github.com/mamekudz/microGulpFlexBar`  
   (FlexGate / FlexDesigner expect this GitHub URL; product marketing stays on https://microgulp.dev.)
5. Replace the contents of this repository root with that plugin tree (plus `LICENSE`, `README.md`, `NOTICE.md`, `THIRD_PARTY/`, `UPDATE.md`, `.gitignore`). Do not copy main-project sources, maps, logs, tokens, or other plugins.
6. Re-validate the **folder** with FlexCLI. Zip a new `.flexplugin` from that folder and validate again. Document the new SHA-256 (do not reuse old proofs after the `repo` edit).
7. Commit and push **only** this repository (no force-push). Create a GitHub Release whose **tag equals** `manifest.json` `version`, and attach the new `.flexplugin` as a release asset.

## Do not

- Rebuild from scratch in this repo without the main-project verify step
- Dual-maintain TypeScript/Vue sources here
- Add CI secrets or extra cloud accounts unless FlexGate later requires them
- Claim hardware acceptance when only schema validation passed
