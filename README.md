# Land Cover Classification for Deforestation Detection

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)
![USGS](https://img.shields.io/badge/Data-USGS%20Landsat-4CAF50?style=flat&logo=nasa&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat)
![Status](https://img.shields.io/badge/Status-Portfolio-8A2BE2?style=flat)

Multispectral satellite imagery pipeline for land cover classification and deforestation detection using Landsat 7 and Landsat 8. Designed for regional-scale analysis across Colombia's diverse ecosystems — from Amazonian forest to Andean transition zones. The pipeline is region-agnostic: any area of interest with available Landsat coverage can be analyzed by adjusting the spatial bounding box and retraining the classifier on locally annotated labels.

---

## Problem Statement

Colombia's forests face persistent pressure from illegal land clearing, cattle ranching expansion, and extractive activities. Ground-based monitoring is logistically unfeasible at national scale and prohibitively expensive for local environmental authorities. Freely available multispectral data from the USGS Landsat archive enables reproducible, cost-effective monitoring with sufficient spatial resolution (30m/pixel) to detect meaningful land cover transitions over time.

---

## Methodology

### 1. Data Acquisition
- **Source:** USGS Earth Explorer — Landsat 7 ETM+ and Landsat 8 OLI/TIRS collections
- **Region definition:** Configurable bounding box per area of interest
- **Selection criteria:** Cloud cover < 20%, dry season acquisition window to minimize atmospheric interference

### 2. Preprocessing
- Radiometric calibration: DN → Top-of-Atmosphere (TOA) reflectance
- Band stacking and spatial alignment across sensor dates
- Cloud masking using QA_PIXEL band

### 3. Spectral Analysis
- **True Color Composite:** Bands 4-3-2 (Landsat 8) for visual baseline
- **NDVI (Normalized Difference Vegetation Index):** Quantifies vegetation density and health
  ```
  NDVI = (NIR - Red) / (NIR + Red)
  ```
- **False Color Composites:** Near-infrared combinations to enhance vegetation/bare soil contrast across different ecosystem types

### 4. Classification Model
- **Algorithm:** Decision Tree Classifier (scikit-learn)
- **Training labels:** Manually annotated land cover classes (forest, degraded forest, bare soil, water)
- **Features:** Per-pixel spectral band values + derived indices (NDVI)
- **Output:** Classified raster identifying deforested and at-risk areas

### 5. Visualization
- Side-by-side comparison of true color imagery vs. classified land cover output
- Spatial mapping of land cover change at pixel level

---

## Case Study — Guaviare Department

Guaviare was selected as the primary validation region given its status as one of the Amazon basin's most actively deforested frontiers. The department sits at the ecological boundary between Andean foothills and lowland rainforest, making land cover transitions particularly detectable through spectral contrast.

**Context:** The Colombian Amazon loses tens of thousands of hectares annually to illegal land clearing, with Guaviare consistently ranking among the most affected departments (IDEAM, annual deforestation reports). Remote sensing provides the only scalable tool for monitoring transitions in this region.

**Imagery acquired:** Landsat 8 OLI, dry season, cloud cover < 15%

<p align="center">
  <strong>True Color Composite (Bands 4-3-2)</strong><br>
  <img src="img/True-Color-Guaviare.PNG" alt="True Color Composite">
</p>

<p align="center">
  <strong>Predicted Land Cover — Decision Tree Classification</strong><br>
  <img src="img/Deforestación-Guaviare.PNG" alt="Deforestation Classification">
</p>

<div align="center">

| Output | Description |
|---|---|
| True Color (4-3-2) | Baseline visual reference — forest appears dark green, cleared areas in pale tones |
| Decision Tree classification | Binary land cover map — forest vs. deforested/degraded areas |

</div>

**Replicating for other regions:** Replace the bounding box coordinates in the data acquisition notebook, download corresponding Landsat scenes from USGS Earth Explorer, annotate training labels for the new region, and rerun the classification pipeline.

---

## Stack

<div align="center">

| Layer | Tools |
|---|---|
| Language | Python 3 |
| Data processing | NumPy, Pandas, Rasterio |
| ML / Classification | scikit-learn |
| Visualization | Matplotlib, GDAL |
| Data source | USGS Landsat Archive (public domain) |

</div>

---

## Repository Structure

```
Satellite-Imagery/
├── SatImegery-DataScience/   # Jupyter notebooks (preprocessing, analysis, modeling)
├── img/                      # Output visualizations
└── README.md
```

---

## Potential Extensions

- Multi-temporal analysis to quantify deforestation rate (ha/year) across multiple regions simultaneously
- Replace Decision Tree with Random Forest or CNN for improved classification accuracy
- Integration with Google Earth Engine for scalable, cloud-based processing without local download
- Automated alert pipeline for near-real-time deforestation detection and reporting

---

## Context

Developed as an independent exploration of remote sensing applications in environmental monitoring. Landsat imagery is in the public domain and freely accessible through the [USGS Earth Explorer](https://earthexplorer.usgs.gov/) platform.

---

## Author

**Juan Sebastián Henao**
[GitHub](https://github.com/jshenaop) · [LinkedIn](https://www.linkedin.com/in/juan-sebastian-henao-parra-50783088/)
