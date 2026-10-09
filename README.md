# µGulp™ Flexbar Plugin

Public FlexGate distribution of the **µGulp™** plugin for [ENIAC Flexbar](https://eniac-tech.github.io/FlexDocumentation/flexbar/en/).

Product site: [https://microgulp.dev](https://microgulp.dev)

This repository contains only the shipped plugin layout required by FlexGate / FlexDesigner. The plugin directory is **`de.amekudzi.microgulp.plugin/`** at the repository root (FlexDesigner looks for `{uuid}.plugin` with `manifest.json` inside). The main µGulp™ product repository stays private. Publishing here is **not** an open-source release - see [LICENSE](LICENSE).

## Purpose

Control µGulp™ from an ENIAC Flexbar:

1. **µGulp Task** - assign one workspace task to a key (start/stop, optional µWatch toggle).
2. **µGulp Browser** - dynamic key (up to 16 child slots) that browses groups and tasks with live embedded icons. Opening a group never starts a task.

Live states follow the µGulp™ runtime when a local hardware-control session is available. Optional workspace colors (background / foreground, 0-2 stops) from the µGulp™ project identity tint browser key plates when configured.

## Status

**Experimental.** Windows device acceptance and macOS (Intel / Apple Silicon) hardware verification are still open. FlexCLI schema validation of this package is not a hardware acceptance test.

## Prerequisites

1. [FlexDesigner](https://eniac-tech.github.io/FlexDocumentation/flexbar/en/) with Flexbar support (see `software.minimumVersion` in `de.amekudzi.microgulp.plugin/manifest.json`).
2. µGulp™ installed (VS Code / Cursor / JetBrains) with **hardware control enabled** for the workspace. Not available in **µGulp™ Free**.
3. An active local hardware-control session for that workspace (dashboard settings or the IDE command that starts experimental hardware control).
4. Node.js is used by FlexDesigner to run the plugin backend; no separate npm install is required for this plugin folder.

There is currently no paid µGulp™ edition requirement beyond the existing Free vs. non-Free hardware gate.

## Install (after FlexGate listing)

Once the plugin is listed via FlexGate:

- In FlexDesigner, install from the catalog, **or**
- CLI: `flexcli plugin install --repo https://github.com/mamekudz/microGulpFlexBar`

Sideload for review / local test: download the `.flexplugin` asset from the matching [GitHub Release](https://github.com/mamekudz/microGulpFlexBar/releases) (tag equals `manifest.json` `version`) and import it in FlexDesigner.

## After install

### Single task key

1. Open the workspace in µGulp™ and wait until tasks are loaded.
2. Enable hardware control and confirm the session is active.
3. In FlexDesigner, drag **µGulp → µGulp Task** onto a Flexbar key.
4. Set the workspace folder, choose **Refresh**, then pick a task.
5. Key action **Start / stop the task** runs or stops the task. **Toggle µWatch** only arms/disarms the file trigger.

### Browser key

1. Drag **µGulp → µGulp Browser** once onto the bar (wide dynamic container).
2. Set the workspace folder, or enable **Follow active IDE project** when using µGulp active-project context.
3. Child keys show navigation (back / home / page) and tasks with embedded icons. Press a group to open it; press a task to start/stop it.

## Repository layout

```text
README.md
LICENSE
NOTICE.md
UPDATE.md
THIRD_PARTY/
de.amekudzi.microgulp.plugin/
  manifest.json
  config.json
  backend/
  resources/
  ui/
```

| Path | Role |
| :--- | :--- |
| `de.amekudzi.microgulp.plugin/manifest.json` | Plugin identity, version, SDK, key library (Task + Browser) |
| `de.amekudzi.microgulp.plugin/backend/` | Bundled runtime (`plugin.cjs`) + vendored `@resvg/resvg-wasm` |
| `de.amekudzi.microgulp.plugin/ui/` | FlexDesigner config pages (`task.vue`, `browser.vue`) |
| `de.amekudzi.microgulp.plugin/resources/` | Plugin logo |
| `LICENSE` | Proprietary µGulp™ license |
| `THIRD_PARTY/` | Notices for bundled third-party components |
| `UPDATE.md` | How maintainers refresh this repo from a verified main-project pack |

No development sources, source maps, CI secrets, or full product tree are published here.

## License

Proprietary - Copyright (c) 2026 Meinolf Amekudzi. See [LICENSE](LICENSE).

Bundled `@resvg/resvg-wasm` is under **MPL-2.0**; see `de.amekudzi.microgulp.plugin/backend/vendor/resvg-wasm/NOTICE.txt` and [THIRD_PARTY/MPL-2.0.txt](THIRD_PARTY/MPL-2.0.txt).

## Support

- Product: [https://microgulp.dev](https://microgulp.dev)
- FlexGate / Flexbar docs: [ENIAC FlexDocumentation](https://eniac-tech.github.io/FlexDocumentation/flexbar/en/)
