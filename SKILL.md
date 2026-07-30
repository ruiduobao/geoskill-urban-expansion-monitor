---
name: urban-expansion-monitor
description: >
  Detect and quantify urban expansion from multi-temporal built-up rasters. Use when the user wants to analyze changes, compare multi-temporal
  rasters, compute indices, or generate assessment reports.
---

# Urban Expansion Monitor

Detect and quantify urban expansion from multi-temporal built-up rasters.

## CLI Usage

```bash
python scripts/urban_expansion_monitor.py --before before.tif --after after.tif
python scripts/urban_expansion_monitor.py --before before.tif --after after.tif --threshold 0.6
python scripts/urban_expansion_monitor.py --before before.tif --after after.tif --output-dir my_output
```

## Data Download

This skill can auto-fetch a pair of Landsat Collection 2 Level-2 scenes
from the Microsoft Planetary Computer when given a bounding box + date
range. The `--date-range` is split at the midpoint: the first half is
used for `--before` and the second half for `--after`.

```bash
python scripts/urban_expansion_monitor.py \
  --bbox 116,39,117,40 \
  --date-range 2020-01-01,2024-12-31 \
  --output-dir ./expansion-output
```

The `PYTHONPATH` must include the parent of `_geoskill_data_fetcher/`
(the same directory the 50 skills live in). Set it once:

```bash
export PYTHONPATH="/path/to/行业Skill创意-20260727"
```

## Parameters

| Argument | Required | Default | Description |
|---|---|---|---|
| `--before` | Yes | — | Path to "before" built-up raster (continuous built-up index or binary mask) |
| `--after` | Yes | — | Path to "after" built-up raster (same grid as `--before`) |
| `--threshold` | No | `0.5` | Built-up classification threshold (values ≥ threshold are considered urban) |
| `--output-dir`, `-o` | No | `expansion-output` | Directory to write outputs |

## Output

| File | Description |
|---|---|
| `expansion-report.json` | Machine-readable expansion stats (areas, growth rate) |
| `report.html` | Human-readable HTML report |
| `output-manifest.json` | Run metadata + result summary |

## Exit Codes

| Code | Meaning |
|---|---|
| 0 | Success |
| 2 | Argument error (e.g. missing input file) |
| 7 | Processing failure |
