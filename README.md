# Washington-Wildfires-Wolf-Pack-Impact-QGIS
Spatial overlay analysis in QGIS quantifying historical wildfire perimeter overlap and habitat impact across 49 Washington State wolf pack territories.
# Washington State Wildfires & Wolf Pack Territory Impact Analysis (QGIS)

## Project Overview
This spatial overlay analysis evaluates historical wildfire exposure across **2025 Washington Department of Fish and Wildlife (WDFW) wolf pack territories** using **QGIS** (`EPSG:2285` / `EPSG:2927` Washington State Plane, US Survey Feet). By intersecting historical Washington large-fire perimeters (1973–2022) with **49 active wolf pack polygons** (**6,496,365.4 total acres**; 22 Breeding Pairs and 27 Nonbreeding Packs), this study identifies **254 distinct fire-pack intersection events** and quantifies exact overlap acreage (`Overlap_Ac`) and percentage of territory burned (`Pct_Burned`).

## Data Sources
* **Wolf Pack Territories:** Washington Department of Fish and Wildlife (WDFW) 2025 Wolf Pack Polygons (`Wolf_Pack_Polygons`, 49 active territories totaling 6,496,365.4 acres).
* **Wildfire Perimeters & Centroids:** Washington DNR / NIFC Historical Large Wildfire Perimeters (`1973–2022`) and `Wildfire_Centroid` point layer.
* **Ecological Context:** Pacific Northwest Ecoregions (`Ecoregions_Counts in Polygons`) for regional fire frequency comparison.

## Geoprocessing Methodology (QGIS)
1. **CRS Standardization:** Reprojected wolf pack polygons, wildfire perimeters, and ecoregion boundaries into Washington State Plane (`EPSG:2285` / `EPSG:2927`) to ensure accurate planar area calculations in square feet and acres (`ShapeSTAre / 43560`).
2. **Spatial Overlay (`Intersect`):** Executed a vector **Intersect** between `Wolf_Pack_Polygons` and historical wildfire perimeters (`Wolf_Fire_Intersect`, generating 254 overlap polygons).
3. **Impact Quantification (`Field Calculator`):**
   * **Intersected Area (`Overlap_Ac`):** `$area / 43560`
   * **Percent Territory Burned (`Pct_Burned`):** `("Overlap_Ac" / ("Pack_Acres")) * 100`
4. **Regional Aggregation:** Summarized historical wildfire counts across Pacific Northwest Ecoregions (`Count Points in Polygon`) and compared breeding vs. nonbreeding pack exposure.

## Highlighted High-Impact Fire-Pack Intersections

| Wolf Pack | Pack Status | Fire Year | Ignition Cause | Total Fire Size (Acres) | Intersected Area (`Overlap_Ac`) | % Pack Territory Burned (`Pct_Burned`) |
| :--- | :--- | :---: | :--- | :---: | :---: | :---: |
| **Sullivan Creek** | Breeding Pairs | 2014 | Lightning | 143,748.9 | **8,193.70** | **6.55%** |
| **Chewuch** | Breeding Pairs | 2006 | Unknown | 166,977.8 | **5,824.29** | **4.31%** |
| **Chewuch** | Breeding Pairs | 2021 | Lightning | — | **5,411.29** | **2.50%** |
| **Navarre** | Breeding Pairs | 2014 | Lightning | 143,748.9 | **5,002.72** | **3.69%** |
| **Nason** | Breeding Pairs | 2021 | — | — | **4,163.30** | **3.09%** |
| **Reed** | Breeding Pairs | 2015 | Lightning | 134,161.6 | **4,091.89** | **8.42%** |
| **Tucannon** | Breeding Pairs | 2021 | — | — | **2,987.75** | **2.66%** |
| **Chewuch** | Breeding Pairs | 2014 | Lightning | 143,748.9 | **2,798.53** | **2.07%** |
| **Teanaway** | Breeding Pairs | 2017 | Lightning | 81,862.4 | **2,477.94** | **1.83%** |
| **Navarre** | Breeding Pairs | 2013 | Unknown | 107,596.0 | **2,442.84** | **1.80%** |

## Key Findings
* **Concentrated Breeding Pack Exposure:** High-severity lightning-driven megafires in the North Cascades and Okanogan highlands (such as the 2006, 2014, 2015, and 2021 fire seasons) drove the largest single-event habitat overlaps across **Breeding Pair** territories including **Sullivan Creek**, **Chewuch**, **Navarre**, **Nason**, and **Reed**.
* **Disproportionate Impact on Compact Territories:** Smaller wolf pack territories face acute single-fire vulnerability—for example, the **Reed** pack (`48,597.1` total acres) saw **8.42%** (`4,091.89` acres) of its territory intersect a single 2015 lightning fire.
* **Chronic Multi-Decade Fire Return:** Territories such as **Navarre** and **TupShin** experienced repeated wildfire intersections across multiple decades (1994–2021), highlighting the importance of post-fire ungulate forage recovery and denning/rendezvous site resilience.

## Repository Structure
```text
├── data/
│   └── [Clipped Wolf Pack & Wildfire GeoPackage (.gpkg)]
├── docs/
│   ├── Wolf_Wildfire_README.pdf
│   ├── Vector_Overlay_Methodology.pdf
│   └── Pack_Impact_Summary_Worksheet.pdf
├── outputs/
│   └── [Final QGIS Print Layout Map PNG]
├── stats/
│   ├── wolf_fire_intersect_stats.csv
│   └── wolf_pack_territories.csv
└── README.md
```
