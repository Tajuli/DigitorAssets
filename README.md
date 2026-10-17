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

## Downloadable `Test` motion effect

The effect preset `Test` is published under `effects/presets.json` in the Motion
category. It uses the versioned `BEAT_CIRCLE_V1` recipe supported by
[DigitorAndroid PR #108](https://github.com/Tajuli/DigitorAndroid/pull/108).

- First 2 seconds of the effect bar: smooth heavy blur → clean.
- Entire bar: restrained 10-second zoom in/out cycle.
- Shake: slight movement on detected **strong music amplitude onsets** (waveform-derived,
  not a fabricated fixed BPM). On silence or without detectable onsets there is no beat shake.
- After reveal: subtle circular rings expand from one off-centre point approximately every 4.8s.
- GPU preview, Media3 export and CPU fallback share the same effect-time schedule.
  The CPU fallback uses beat events only if waveform analysis has already been cached.

The `vector.blur` field is a backward-compatibility fallback for older catalog readers.
Updated Android versions suppress that static fallback and render the timed motion recipe
instead. The new motion algorithm does **not** become active until the application is built
with the corresponding renderer changes; JSON cannot ship executable code.
