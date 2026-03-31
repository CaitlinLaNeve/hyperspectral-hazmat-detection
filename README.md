# hyperspectral-hazmat-detection

## Overview

The `hyperspectral-hazmat-detection` repository supports a thesis study utilizing AVIRIS-3 hyperspectral imagery collected during the 2025 California wildfires to detect and map hazardous material signatures in support of the NASA Disaster Response and Coordination System (DRCS) and local disaster response teams.

Using a Spectral Angle Mapper (SAM) workflow applied to pre- and post-fire temporal pairs, this study targets six critical spectral signatures — including chrysotile asbestos and infrastructure materials (asphalt, concrete, and tar) — to characterize fire-driven spectral shifts and identify high-priority hazard hotspots for frontline personnel.

> **Key finding:** Chrysotile asbestos detections decreased significantly post-fire, suggesting chemical alteration or aerosolization during combustion — a primary inhalation risk for first responders.

---

## Repository Contents

```
aviris3-postfire-hazmat-detection/
│
├── notebooks/
│   └── 787_LaNeve_Final.ipynb       # Full SAM workflow: data loading, preprocessing,
│                                    # bad band removal, clustering, spatial analysis,
│                                    # and hazmat detection dashboard
│
├── data/
│   ├── before/                      # Pre-fire AVIRIS-3 L2A NetCDF (gitignored — see Data Access)
│   ├── after/                       # Post-fire AVIRIS-3 L2A NetCDF (gitignored — see Data Access)
│   └── spectral_library/            # Reference spectra for SAM targets (CSV)
│
├── results/
│   ├── figures/                     # Maps, spectral plots, cluster visualizations
│   └── tables/                      # Spectral shift statistics, hotspot summaries
│
├── environment.yml                  # Conda environment for full reproducibility
├── .gitignore                       # Excludes large NetCDF/HDF5 imagery files
└── README.md
```

---

## Data Access

| Scene | Filename | Acquisition Date | Period |
|---|---|---|---|
| Pre-fire | `AV320240905t181848_000_L2A_OE_f576f24d_RFL_ORT.nc` | 2024-09-05 | Pre-fire baseline |
| Post-fire | `AV320250116t193840_005_L2A_OE_f576f24d_RFL_ORT.nc` | 2025-01-16 | Post-fire |

Data are available through the NASA Earthdata portal. An Earthdata Login account is required:

1. Register at [urs.earthdata.nasa.gov](https://urs.earthdata.nasa.gov)
2. Search for AVIRIS-3 L2A Reflectance (OE) products
3. Place downloaded `.nc` files into `data/before/` and `data/after/` respectively

---

## Workflow

The notebook (`787_LaNeve_Final.ipynb`) follows a sequential pipeline:

1. **Data Identification** — Locate and inspect AVIRIS-3 pre/post-fire NetCDF files
2. **Data Loading** — Load L2A reflectance data cubes and wavelength metadata via `netCDF4` and `xarray`
3. **Preprocessing** — Bad band removal (atmospheric water vapor windows, instrument artifacts), spatial subsetting
4. **Spectral Analysis** — Spectral Angle Mapper (SAM) applied to six target material signatures
5. **Burn Severity Validation** — NDVI, NDII, and NBR calculated to validate spectral shift results
6. **Clustering** — PCA + MiniBatchKMeans, DBSCAN, Gaussian Mixture Models, and Agglomerative Clustering for land cover classification
7. **Spatial Pattern Analysis** — Patch metrics, fragmentation, and landscape connectivity pre/post-fire
8. **Hazmat Hotspot Detection** — Co-occurrence mapping of asbestos signals, structural rubble, and severe vegetation loss; ten priority hotspots identified
9. **Summary Dashboard** — Final results compiled into visualization outputs

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/caitlinlaneve/hyperspectral-hazmat-detection.git
cd aviris3-postfire-hazmat-detection
```

### 2. Set Up the Environment

Make sure you have [Anaconda](https://www.anaconda.com/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) installed. Then:

```bash
conda env create -f environment.yml
conda activate aviris3-hazmat
```

### 3. Add Data Files

Download the AVIRIS-3 scenes from NASA Earthdata (see **Data Access** above) and place them as follows:

```
data/before/AV320240905t181848_000_L2A_OE_f576f24d_RFL_ORT.nc
data/after/AV320250116t193840_005_L2A_OE_f576f24d_RFL_ORT.nc
```

### 4. Update the Base Path

In the first code cell of `787_LaNeve_Final.ipynb`, update `base_path` to match your local directory:

```python
base_path = r'your/local/path/to/hyperspectral-hazmat-detection/data'
```

### 5. Run the Notebook

```bash
jupyter notebook notebooks/787_LaNeve_Final.ipynb
```

Run cells sequentially from top to bottom.

---

## Dependencies

| Package | Purpose |
|---|---|
| `numpy` | Array operations |
| `matplotlib` | Visualization |
| `xarray` | NetCDF data handling |
| `netCDF4` | AVIRIS-3 file I/O |
| `h5py` | HDF5 file support |
| `scipy` | Spatial analysis, clustering distances |
| `scikit-learn` | PCA, KMeans, DBSCAN, GMM, clustering metrics |

See `environment.yml` for pinned versions.

---

## AI Use Disclosure

This project used [Claude.ai](https://claude.ai) to assist with code generation and debugging. All scientific ideas, analytical decisions, and interpretations originated with the author.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Acknowledgments

This study was conducted in partial fulfillment of the requirements for the degree of Master of Science at George Mason University at George Mason University.

AVIRIS-3 data were provided by NASA's Jet Propulsion Laboratory (JPL). This work was conducted in support of the NASA Disaster Response and Coordination System (DRCS).

---

## Contact

For more information, please contact [Caitlin LaNeve](https://github.com/caitlinlaneve) (claneve [ at ] gmu [ dot ] edu).

---


