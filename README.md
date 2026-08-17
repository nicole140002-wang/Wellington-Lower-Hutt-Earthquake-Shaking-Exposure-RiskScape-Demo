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
| 2016 Kaikōura Earthquake MMI | GeoNet / Earth Sciences New Zealand | Earthquake shaking hazard |
| NZ Building Outlines | LINZ | Building exposure |
| Territorial Authority boundaries | Stats NZ | Wellington City and Lower Hutt City study areas |

**Analysis CRS:** NZGD2000 / New Zealand Transverse Mercator 2000 (EPSG:2193)

**Final analysis population:** 134,495 buildings across Wellington City and Lower Hutt City.
