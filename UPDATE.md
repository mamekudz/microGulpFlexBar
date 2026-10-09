# Updating this FlexGate repository

Do **not** develop the plugin here. Build and verify in the private µGulp™ main project, then copy the checked distribution into this public repo.

FlexGate / FlexDesigner expect the plugin directory **`{uuid}.plugin/`** at the repository root (see [Getting Started](https://eniac-tech.github.io/FlexDocumentation/flexbar/en/sdk/getting_started.html)). For this product that folder is:

`de.amekudzi.microgulp.plugin/`

Do **not** place `manifest.json` at the Git repository root.

## Repeatable flow

1. In the private main project, produce or confirm a verified marketplace pack, e.g.  
   `packages/marketplace/microgulp-flexbar_marketplace_V<version>.flexplugin`
2. Run the official check there:  
   `flexcli plugin validate --path <plugin-folder>`  
   (in the main project the built folder is `tmp/flexbar/de.amekudzi.microgulp.plugin`).  
   Record SHA-256 of that `.flexplugin` before any FlexGate-specific edits.
3. Extract the pack into a clean staging folder. The pack itself has `manifest.json` / `backend/` / `ui/` / `resources/` at the **archive** root - that is correct for `.flexplugin`. For this **GitHub** repo, those files must live under `de.amekudzi.microgulp.plugin/`.
4. Set `de.amekudzi.microgulp.plugin/manifest.json` → `repo` to:  
   `https://github.com/mamekudz/microGulpFlexBar`  
   (FlexGate / FlexDesigner expect this GitHub URL; product marketing stays on https://microgulp.dev.)
5. Replace **only** `de.amekudzi.microgulp.plugin/` with the staged plugin tree. Keep root docs (`LICENSE`, `README.md`, `NOTICE.md`, `THIRD_PARTY/`, `UPDATE.md`, `.gitignore`). Do not leave a second `manifest.json` at the repository root. Do not copy main-project sources, maps, logs, tokens, or other plugins.
6. Re-validate:  
   `flexcli plugin validate --path de.amekudzi.microgulp.plugin`  
   A repository layout fix alone does **not** require rebuilding the GitHub Release `.flexplugin` unless the plugin payload itself changed. If you did change the payload (including `repo`), zip from the plugin subfolder contents (archive root = plugin files, not the `{uuid}.plugin` parent name), validate the package, and use a new SHA-256.
7. Commit and push **only** this repository (no force-push). Release tag must equal `manifest.json` `version` when creating or replacing a release asset.

## Do not

- Put `manifest.json` at the Git repository root
- Rebuild from scratch in this repo without the main-project verify step
- Dual-maintain TypeScript/Vue sources here
- Add CI secrets or extra cloud accounts unless FlexGate later requires them
- Claim hardware acceptance when only schema validation passed
- Claim FlexGate acceptance until Verify succeeds in the FlexGate form
