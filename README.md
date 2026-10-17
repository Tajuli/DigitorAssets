# Digitor Assets

Public, data-only preset catalogs for [DigitorAndroid](https://github.com/Tajuli/DigitorAndroid).

The Android app downloads JSON recipes from the `main` branch using HTTPS and keeps the last
successfully validated download cached in private app storage. GitHub updates can add presets
implemented through existing compiled render engines; arbitrary shaders, native code,
plugins or ML models **cannot** be loaded by these JSON files.

## Catalog layout

- `transitions/presets.json`: IDs, labels, categories (BASIC/CAMERA/EFFECT), and existing V22 engine styles.
- `effects/presets.json`: effect names, categories (Basic/Glitch/Retro/Lens/Motion), and native effect vectors.
- `filters/presets.json`: color LOOKS definitions with adjustment values and optional log wheels.

Each file requires `schemaVersion: 1` and a `presets` array. Limit: 200 entries and 256 KiB
per category. The app checks allowed categories, values and schema before installing.
Built-in IDs always win on collisions. Avoid renaming previously published IDs/names
used by saved projects.

The public raw content base URL is:
`https://raw.githubusercontent.com/Tajuli/Digitor-Assets-/main`

App startup checks for updates once per six hours after success, retries on later
launches after an hour if an update fails, and uses its offline cache when needed.

Note: The repo name intentionally ends with a hyphen: `Digitor-Assets-`.
