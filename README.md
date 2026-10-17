# DigitorAssets

This public repository publishes validated, **data-only** transition/effect/filter
recipes for [DigitorAndroid](https://github.com/Tajuli/DigitorAndroid).
The native Android renderers and shaders are compiled into the app; uploading random
shaders, binaries, model files or executable scripts here **does not install new engines**.

## Mirrored editor categories

The directories match the tabs in the Android editor exactly:

- `effects/` (13): `Video Effect`, `Image Effect`, `Basic`, `Glitch`, `Retro`,
  `Lens`, `Motion`, `Body`, `Eyes`, `Funny Faces`, `Glowing Lines`,
  `Stroke`, `Clone`
- `filters/` (2): `Looks`, `Beauty`
- `transitions/` (3): `Basic`, `Camera`, `Effect`

Each folder has either a `presets.json` catalog or an empty-folder
`.gitkeep` placeholder. The preexisting top-level
`effects/presets.json`, `filters/presets.json`, and
`transitions/presets.json` are kept for compatibility with early client builds;
**the new manual-download client discovers only the per-category files.**

### Publish a downloadable preset

1. In the chosen editor category folder, create or edit **`presets.json`**.
2. Use `{"schemaVersion":1,"presets":[...]}`. Every entry must declare the
   correct `category` (effects/transitions) or `group` (filters), matching its folder.
3. Commit to `main`. Android can then discover a new file SHA in the **public GitHub
   tree metadata** without downloading the actual file.
4. The user opens that category in DigitorAndroid, sees **Download** or **Update**
   and taps it, then confirms. Only this explicit action downloads the JSON.
5. Once validated (size, schema, whitelisted algorithms and SHA), the presets
   appear alongside built-in options. Approved downloads are cached for offline use.

If a folder only has `.gitkeep`, the app shows **No online assets**.
If new assets are committed while the editor is open, tap **Refresh** to check
GitHub metadata again. GitHub availability/rate limits can affect this check.

Catalog restrictions: at most 256 KiB and 200 entries per folder; all numeric
parameters are bounded. Only supported native effect vectors,
`BEAT_CIRCLE_V1` animated motion, color `LOOKS`, whitelisted `BEAUTY`
operations and existing V22 transition styles are supported. A folder name
does not itself enable new ML, face tracking, custom shaders or new 3D engines.
Unsupported recipes are rejected, not run.

### Example: Test effect

[effects/Motion/presets.json](effects/Motion/presets.json) contains **Test**,
a validated `BEAT_CIRCLE_V1` recipe:

- Clear an initial blur over 2s
- Small continuous 10s zoom oscillation
- Slight shakes at detected strong audio onsets (no artificial beat on silence)
- Subtle expanding circular ripple about every 4.8s

This animated recipe requires the updated Android native renderer from
[DigitorAndroid PR #108](https://github.com/Tajuli/DigitorAndroid/pull/108).

Raw GitHub base URL: `https://raw.githubusercontent.com/Tajuli/DigitorAssets/main`.
No GitHub token is embedded in the application.
