# 🛰️ Jatrabari AOI — Google Earth Engine Shapefile Loader

Load a local shapefile boundary into **Google Earth Engine (GEE)** using GeoPandas, visualise it on an interactive map, and use it as an Area of Interest (AOI) for further satellite analysis.

---

## 📁 Project Structure

```
project/
├── gee_shapefile_loader.ipynb   # Main notebook (4 cells)
├── shape file/
│   ├── Jatrabari.shp
│   ├── Jatrabari.shx
│   ├── Jatrabari.dbf
│   └── Jatrabari.prj
└── README.md
```

---

## 🗺️ Study Area

| Property  | Value                          |
|-----------|-------------------------------|
| Location  | Jatrabari, Dhaka, Bangladesh  |
| CRS       | EPSG:4326 (WGS 84)            |
| Bounds    | `[90.4231, 23.6948, 90.4764, 23.7332]` |
| Features  | 1 polygon                     |

---

## ⚙️ Requirements

### Python packages

```bash
pip install earthengine-api geemap geopandas
```

### Google Earth Engine account

Sign up at [earthengine.google.com](https://earthengine.google.com) if you don't have an account.

---

## 🚀 Quick Start

### 1. Clone the repo

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Install dependencies

```bash
pip install earthengine-api geemap geopandas
```

### 3. Authenticate with GEE (first time only)

```python
import ee
ee.Authenticate()
ee.Initialize()
```

### 4. Open the notebook

```bash
jupyter notebook gee_shapefile_loader.ipynb
```

### 5. Update the shapefile path

In **Cell 2**, set `SHP_PATH` to your local `.shp` file:

```python
SHP_PATH = r'H:\gis all\test matuail land\shape file\Jatrabari.shp'
```

### 6. Run all cells

`Kernel → Restart & Run All`

---

## 🔬 Notebook Cells

| Cell | Description |
|------|-------------|
| **Cell 1** | Imports + GEE authentication (auto-triggers if not logged in) |
| **Cell 2** | Reads shapefile → reprojects to EPSG:4326 → dissolves multi-features → converts to `ee.Geometry` |
| **Cell 3** | Interactive map preview centred on the AOI with satellite basemap |
| **Cell 4** | GEE-side bounding box sanity check |

---

## 🧩 How It Works

```
Local .shp file
      │
      ▼
 GeoPandas (read + reproject to EPSG:4326)
      │
      ▼
 GeoJSON dict  ──►  ee.Geometry
      │
      ▼
 geemap interactive map preview
```

---

## 🛠️ Configuration

All tuneable options are at the top of **Cell 2**:

```python
SHP_PATH    = r'path\to\your\file.shp'
LAYER_NAME  = 'Jatrabari'     # map legend label
LAYER_COLOR = 'red'           # AOI outline colour
ZOOM_LEVEL  = 13              # initial map zoom
```

---

## 📌 Common Issues

| Error | Cause | Fix |
|-------|-------|-----|
| `NameError: name 'aoi_gdf' is not defined` | Cell 2 not run yet | Run cells in order |
| `EEException: Not signed in` | GEE session expired | Re-run Cell 1 |
| `fiona` driver error | Shapefile components missing | Ensure `.shx`, `.dbf`, `.prj` are in the same folder as `.shp` |
| Empty map layer | Wrong CRS | Confirm shapefile is in or converts to EPSG:4326 |

---

## 📄 License

MIT — free to use and modify.

---

## 🙏 Acknowledgements

- [Google Earth Engine](https://earthengine.google.com)
- [geemap](https://geemap.org) by Qiusheng Wu
- [GeoPandas](https://geopandas.org)
