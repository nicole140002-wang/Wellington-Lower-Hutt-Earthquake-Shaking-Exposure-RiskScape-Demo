# Wellington-Lower-Hutt-Earthquake-Shaking-Exposure-RiskScape-Demo
**Building-level earthquake shaking exposure analysis using ArcGIS Pro, GeoNet MMI data, LINZ Building Outlines, and RiskScape**  

This project demonstrates a screening-level earthquake exposure workflow for Wellington City and Lower Hutt City using modelled Modified Mercalli Intensity (MMI) from the 2016 Kaikōura earthquake.

The workflow combines GIS-based hazard and building exposure analysis in ArcGIS Pro with a RiskScape model, followed by an independent cross-validation of hazard sampling results between the two workflows.

**Project scope:** This is an exposure and risk-modelling workflow demonstration. It assesses relative shaking exposure rather than structural damage or economic loss.

## Final Output

Final map to be added.

The final output will compare building-level shaking exposure across Wellington City and Lower Hutt City and summarise differences in both building counts and exposed building footprint area.

## What This Project Demonstrates
- Integrated earthquake hazard and building exposure data into a building-level risk-modelling workflow for Wellington City and Lower Hutt City.
- Quantified relative shaking exposure using MMI, exposed building counts, and building footprint area.
- Implemented a RiskScape 1.14 model with a custom consequence function to classify screening-level shaking exposure.
- Cross-validated RiskScape hazard sampling against an independent ArcGIS Pro workflow, demonstrating strong agreement between the two approaches.
- Applied spatial data QA/QC, model validation, and transparent treatment of assumptions and limitations.

## Project Question
**How did modelled shaking exposure from the 2016 Kaikōura earthquake differ between buildings in Wellington City and Lower Hutt City?**
The analysis focuses on:
- building-level MMI exposure;  
- the proportion of buildings exposed to MMI ≥ 5.6 and MMI ≥ 5.8;
- building footprint area exposed above the same thresholds; and
- consistency between ArcGIS Pro and RiskScape hazard-sampling workflows.

## Data
| Dataset | Source | Role |
|---|---|---|
| [2016 Kaikōura Earthquake MMI](https://shakinglayers.geonet.org.nz/html/quakes/2016p858000/latest) | GeoNet / Earth Sciences New Zealand | Earthquake shaking hazard |
| [NZ Building Outlines](https://data.linz.govt.nz/layer/101290-nz-building-outlines/) | LINZ | Building exposure |
| Territorial Authority boundaries | Stats NZ | Wellington City and Lower Hutt City study areas |

**Analysis CRS:** NZGD2000 / New Zealand Transverse Mercator 2000 (**EPSG:2193**)

**Final analysis population:** 134,495 buildings across Wellington City and Lower Hutt City.  

## Method  
### 1. Hazard preparation  
The 2016 Kaikōura earthquake MMI raster was projected to NZTM2000 / EPSG:2193 in ArcGIS Pro.
A TA-clipped raster was initially tested, but raster cell alignment near irregular administrative boundaries created NoData values for some boundary buildings. The final workflow therefore retained the full projected MMI surface and used the building dataset to define the Wellington–Lower Hutt analysis extent.  

### 2. Building exposure preparation
LINZ Building Outlines were:
- projected to EPSG:2193;
- checked for invalid geometry;
- repaired where required;
- assigned geometry-derived building footprint area; and
- converted to interior representative points for the ArcGIS Pro sampling workflow.

Geometry QA/QC identified several non-simple polygons, primarily self-intersections and short segments. These were repaired before further processing.
Buildings were assigned to Wellington City or Lower Hutt City using their representative point and the Territorial Authority boundaries.
Features whose representative points fell outside both study areas were excluded from the final exposure population.  
<img width="750" height="476" alt="image" src="https://github.com/user-attachments/assets/1d20f630-f730-41fc-8f4d-15db6ed4215c" />

### 3.  
