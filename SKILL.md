---
name: geoskill-web-map-generation
description: 'Generate interactive web maps from GeoTIFF or GeoJSON with Leaflet templates and metadata'
---

# 交互式Web地图生成 | Interactive Web Map Generation

Renders GeoTIFF rasters into georeferenced PNGs and embeds them into self-contained Leaflet HTML maps, so users can zoom, pan, and click to inspect coordinates right in the browser.

Supports both percentile and min-max contrast stretches and 8 matplotlib colormaps; produces a metadata JSON with the geographic extent, stretch endpoints, and statistics, plus a reproducible rendered GeoTIFF.

## Core Algorithm / 核心算法

percentile/min-max linear stretch → matplotlib colormap coloring → PIL PNG encoding (base64 embedded) → Leaflet ImageOverlay.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (Synthetic Data, Offline)

```bash
python geoskill-web-map-generation.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (Custom Color Scheme and Stretch)

```bash
python geoskill-web-map-generation.py --input dem.tif --cmap terrain --stretch percentile --output-dir ./out
```

### 示例 3（min-max 拉伸 + 高不透明度）

```bash
python geoskill-web-map-generation.py --input dem.tif --stretch minmax --opacity 1.0
```

### Example 4 (Specified Title)

```bash
python geoskill-web-map-generation.py --bbox 116 39 117 40 --synthetic --title "Beijing DEM"
```

### Example 5 (Custom Percentile Endpoints)

```bash
python geoskill-web-map-generation.py --input dem.tif --lo-pct 1 --hi-pct 99
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `web_map.html` | HTML | Self-contained interactive map (primary output) |
| `rendered.tif` | GeoTIFF | Stretched [0,1] rendered raster (verifiable output) |
| `map_metadata.json` | JSON | Extent/colormap/statistics metadata |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
