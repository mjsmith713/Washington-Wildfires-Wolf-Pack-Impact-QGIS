# Washington State Wildfires & Wolf Pack Territory Impact Analysis (1973–2022)

## Project Overview

![Washington Wildfires and Wolf Pack Territory Overlap Map](outputs/Washington_Wildfire_Wolf_Pack_Map_II.png)

📄 **[Download Full-Resolution Cartographic Layout (PDF)](outputs/Washington_Wolf_Wildfire_Map.pdf)**

This geospatial analysis evaluates historical wildfire exposure across active gray wolf (*Canis lupus*) territories in Washington State. By intersecting 50 years of large wildfire perimeter records (**1973–2022**) with **2025 Washington Department of Fish and Wildlife (WDFW)** wolf pack polygons in **QGIS** (`EPSG:2927` / NAD83(HARN) Washington South ftUS), this study quantifies overlapping burned acreage (`Overlap_Ac`), territory burn percentages (`Pct_Burned`), and wildfire frequency across Pacific Northwest ecoregions.

## Primary Spatial Datasets
* **2025 WDFW Wolf Pack Polygons (`Wolf_Pack_Polygons_(current_year)`):** 49 active territories totaling **6,496,365.4 acres** (22 Breeding Pairs; 27 Nonbreeding Packs).
* **Washington Large Fires (`1973–2022`):** Historical wildfire perimeter polygons (`FIRENAME`, `YEAR`, `CAUSE`, total `ACRES`) repaired via *Fix Geometries*.
* **EPA Level III Pacific Northwest Ecoregions:** Regional ecological zones aggregated via fire perimeter centroids (`Wildfire_Centroid`).

## Geoprocessing Workflow (QGIS)
1. **CRS Standardization:** Reprojected all vector inputs into **NAD83(HARN) / Washington South (ftUS) (`EPSG:2927`)** for uniform planar area measurements.
2. **Topology Validation:** Executed *Fix Geometries* on historical wildfire perimeters to resolve self-intersections before overlay operations.
3. **Spatial Intersection:** Ran *Vector → Geoprocessing Tools → Intersect* between wolf pack territories and repaired wildfire perimeters, generating **254 fire-pack overlap polygons** (`Wolf_Fire_Intersect`).
4. **Field Calculator Metrics:** Computed exact intersected footprint (`Overlap_Ac = $area / 43560`) and relative territory burn share (`Pct_Burned = (Overlap_Ac / Pack_Acres) * 100`).
5. **Ecoregion Aggregation:** Converted fire perimeters to centroids and ran *Count Points in Polygon* across Pacific Northwest Ecoregions.

## Key Territory & Fire Overlap Highlights
* **Statewide Territory Footprint:** **6,496,365.4 acres** across **49 active packs** (`22` Breeding Pairs [44.9%]; `27` Nonbreeding Packs [55.1%]).
* **Largest Mapped Territories:** **Napeequa** (`575,780.6` ac), **Billy Goat** (`216,912.8` ac), **Dollar Mountain** (`184,944.5` ac), **Lookout** (`177,442.9` ac), and **Naneum** (`173,318.5` ac).
* **Notable 2021 Fire-Pack Overlaps:** **Chewuch** (`5,411.29` overlap ac; `2.50%` burned), **Nason** (`4,163.30` overlap ac; `3.09%` burned), **Tucannon** (`2,987.75` overlap ac; `2.66%` burned), **Couse** (`2,435.31` overlap ac; `2.17%` burned), and **Napeequa** (`2,042.30` overlap ac; `1.51%` burned).

## Repository Structure
```text
├── data/
│   └── washington_wolf_fire_analysis.gpkg
├── docs/
│   ├── Washington_Wolf_Wildfire_Final_README.pdf
│   ├── Washington_Wolf_Wildfire_Methodology.pdf
│   └── Washington_Wolf_Pack_Summary_Report.pdf
├── outputs/
│   ├── Washington_Wolf_Wildfire_Map.png
│   └── Washington_Wolf_Wildfire_Map.pdf
├── stats/
│   ├── Wolf_Fire_Intersect_Stats.csv
│   ├── Wolf_Pack_Territories.csv
│   └── Ecoregion_Fire_Counts.csv
└── README.md
```
