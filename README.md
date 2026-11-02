# Interactive Web Map Generation (geoskill-web-map-generation)

> Generate interactive web maps from GeoTIFF or GeoJSON with Leaflet templates and metadata

---

## 1. Overview

Renders GeoTIFF rasters into georeferenced PNGs and embeds them in a self-contained Leaflet HTML map: open it in a browser and you can zoom, pan, and click to view the longitude/latitude. Supports two contrast stretches — percentile and min-max — and 8 matplotlib colormaps; produces a metadata JSON with the geographic extent, stretch endpoints, and statistics, as well as a reproducible rendered GeoTIFF.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-web-map-generation.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `web_map.html` | HTML | Self-contained interactive map (primary output) |
| `rendered.tif` | GeoTIFF | Stretched [0,1] rendered raster (verifiable output) |
| `map_metadata.json` | JSON | Extent/colormap/statistics metadata |

Each run also produces `output-manifest.json` (run manifest).

## 6. Technical Principle

percentile/min-max linear stretch → matplotlib colormap coloring → PIL PNG encoding (base64 embedded) → Leaflet ImageOverlay.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
