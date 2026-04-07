# KlipperVault-Online-Updates

Online macro update repository for KlipperVault clients.  
This repo **only** hosts macro update data — it is **not** the KlipperVault application repo.

---

## Repository layout

```
updates/
  manifest.json               ← index of all available macros
<vendor>/
  <model>/
    <macro_name>.cfg          ← Klipper macro file
```

### Example

```
updates/
  manifest.json
generic/
  bed_leveling/
    adaptive_mesh.cfg
  filament/
    filament_change.cfg
```

---

## manifest.json schema

KlipperVault clients fetch `updates/manifest.json` to discover available macros.

| Field | Type | Description |
|---|---|---|
| `schema_version` | string | Manifest format version (currently `"1"`) |
| `updated` | string | ISO-8601 date of the last manifest update |
| `macros` | array | List of macro descriptors (see below) |

Each entry in `macros`:

| Field | Type | Description |
|---|---|---|
| `vendor` | string | Hardware vendor identifier (e.g. `"generic"`, `"creality"`) |
| `model` | string | Printer model or macro category (e.g. `"bed_leveling"`) |
| `name` | string | Unique macro name within vendor/model |
| `version` | string | Semantic version of the macro file |
| `description` | string | Human-readable description |
| `file` | string | Repo-relative path to the `.cfg` file |

---

## Adding a new macro

1. Create the macro file at `<vendor>/<model>/<name>.cfg`.
2. Add a corresponding entry to `updates/manifest.json`.
3. Bump the `updated` field in the manifest to today's date.
4. Open a pull request.
