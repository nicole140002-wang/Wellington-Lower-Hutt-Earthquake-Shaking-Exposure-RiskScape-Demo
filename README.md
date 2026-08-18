# Wellington-Lower-Hutt-Earthquake-Shaking-Exposure-RiskScape-Demo

**Building-level earthquake shaking exposure analysis using ArcGIS Pro, GeoNet MMI data, LINZ Building Outlines, and RiskScape**

This project demonstrates a screening-level earthquake exposure workflow for Wellington City and Lower Hutt City using modelled Modified Mercalli Intensity (MMI) from the **2016 Kaikōura earthquake**.

The workflow combines GIS-based hazard and building exposure analysis in ArcGIS Pro with a RiskScape model, followed by an independent cross-validation of hazard sampling results between the two workflows.

**Project scope:** This is an exposure and risk-modelling workflow demonstration. It assesses relative shaking exposure rather than structural damage or economic loss.

## Final Output

<div align="center">

<img width="800" src="https://github.com/user-attachments/assets/b5833050-907b-4349-a865-c5b9bdf7041a" alt="Building-level shaking exposure comparison for Wellington City and Lower Hutt City" />

<br>

<em>Figure 1. Building-level relative shaking exposure classes for Wellington City and Lower Hutt City derived from the 2016 Kaikōura earthquake MMI surface.</em>

</div>



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

<div align="center">

<table>
  <thead>
    <tr>
      <th>Dataset</th>
      <th>Source</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://shakinglayers.geonet.org.nz/html/quakes/2016p858000/latest">2016 Kaikōura Earthquake MMI</a></td>
      <td>GeoNet / Earth Sciences New Zealand</td>
      <td>Earthquake shaking hazard</td>
    </tr>
    <tr>
      <td><a href="https://data.linz.govt.nz/layer/101290-nz-building-outlines/">NZ Building Outlines</a></td>
      <td>LINZ</td>
      <td>Building exposure</td>
    </tr>
    <tr>
      <td>Territorial Authority boundaries</td>
      <td>Stats NZ</td>
      <td>Wellington City and Lower Hutt City study areas</td>
    </tr>
  </tbody>
</table>

</div>

**Analysis CRS:** NZGD2000 / New Zealand Transverse Mercator 2000 (**EPSG:2193**)

**Final analysis population:** 134,495 buildings across Wellington City and Lower Hutt City.

## Method

### 1. Hazard preparation

The 2016 Kaikōura earthquake MMI raster was projected to **NZTM2000 / EPSG:2193** in ArcGIS Pro.

A TA-clipped raster was initially tested, but raster cell alignment near irregular administrative boundaries created NoData values for some boundary buildings. The final workflow therefore retained the full projected MMI surface and used the building dataset to define the Wellington–Lower Hutt analysis extent.

<div align="center">

<img width="750" src="https://github.com/user-attachments/assets/b4ffbba6-c526-4170-91ab-3b3812f3aa0b" alt="Projected Kaikōura earthquake MMI surface" />

<br>

<em>Figure 2. Projected Kaikōura earthquake MMI surface used for the analysis.</em>

</div>

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

<div align="center">

<img width="750" src="https://github.com/user-attachments/assets/3df61516-c218-4fdd-a6b2-dd0a7c6d5260" alt="Building footprints and representative points" />

<br>

<em>Figure 3. Building footprints and interior representative points generated for building-level MMI sampling in ArcGIS Pro.</em>

</div>

### 3. ArcGIS Pro hazard sampling

Building representative points were sampled against the MMI raster using ArcGIS Pro.

Each building received a modelled MMI value representing the shaking intensity at its representative location.

The resulting building-level MMI values ranged approximately from **5.23 to 5.98** across the study area.

Two analytical thresholds were then used to compare relatively higher shaking exposure:

- MMI ≥ 5.6
- MMI ≥ 5.8

These thresholds are used for relative comparison within this portfolio project and are not official damage or risk classifications.

### 4. Building exposure analysis

Exposure was assessed in two ways.

#### Building count exposure

For each Territorial Authority, the analysis calculated:

- total number of buildings;
- mean and median MMI;
- number and percentage of buildings with MMI ≥ 5.6; and
- number and percentage of buildings with MMI ≥ 5.8.

#### Building footprint exposure

Building footprint area was also used to avoid treating a small shed and a large commercial building as equivalent exposure units.

For each Territorial Authority, the analysis calculated:

- total building footprint area;
- footprint area exposed to MMI ≥ 5.6;
- footprint area exposed to MMI ≥ 5.8; and
- corresponding percentages of total building footprint area.

## RiskScape Workflow

The same building footprints and projected MMI hazard raster were used to construct a RiskScape 1.14 model.

The workflow consisted of:

<p align="center">
  <code>Building footprints</code><br>
  <strong>+</strong><br>
  <code>Projected Kaikōura MMI raster</code><br>
  ↓<br>
  <code>RiskScape spatial sampling</code><br>
  ↓<br>
  <code>Building-level MMI</code><br>
  ↓<br>
  <code>Custom consequence function</code><br>
  ↓<br>
  <code>Shaking exposure class</code>
</p>

A simple screening-level consequence function was used:

<div align="center">

<table>
  <thead>
    <tr>
      <th>Consequence</th>
      <th>MMI range</th>
      <th>Interpretation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">0</td>
      <td align="center">&lt; 5.6</td>
      <td>Lower relative shaking exposure</td>
    </tr>
    <tr>
      <td align="center">1</td>
      <td align="center">5.6 to &lt; 5.8</td>
      <td>Elevated relative shaking exposure</td>
    </tr>
    <tr>
      <td align="center">2</td>
      <td align="center">≥ 5.8</td>
      <td>Higher relative shaking exposure</td>
    </tr>
  </tbody>
</table>

</div>

These values represent **relative shaking exposure classes only**. They are **not structural damage states**.

## Model Validation

RiskScape hazard sampling was independently compared with the ArcGIS Pro raster-extraction workflow across all **134,495 buildings**.

The comparison used: MMI difference = RiskScape MMI − ArcGIS Pro MMI

### Validation Summary

<div align="center">

<table>
  <thead>
    <tr>
      <th align="left">Metric</th>
      <th align="center">Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Buildings compared</td>
      <td align="center">134,495</td>
    </tr>
    <tr>
      <td>Mean absolute MMI difference</td>
      <td align="center">0.000020</td>
    </tr>
    <tr>
      <td>Median absolute MMI difference</td>
      <td align="center">0.000002</td>
    </tr>
    <tr>
      <td>Standard deviation</td>
      <td align="center">0.001642</td>
    </tr>
    <tr>
      <td>Maximum absolute MMI difference</td>
      <td align="center">0.280092</td>
    </tr>
    <tr>
      <td>Absolute MMI difference &gt; 0.01</td>
      <td align="center">23 buildings</td>
    </tr>
    <tr>
      <td>Absolute MMI difference &gt; 0.05</td>
      <td align="center">18 buildings</td>
    </tr>
    <tr>
      <td>Different classification at MMI 5.6 threshold</td>
      <td align="center">8 buildings</td>
    </tr>
    <tr>
      <td>Different classification at MMI 5.8 threshold</td>
      <td align="center">2 buildings</td>
    </tr>
  </tbody>
</table>

</div>

The mean and median absolute differences were extremely small, indicating strong agreement between the two independent sampling workflows. Only **23 of 134,495 buildings** had an absolute MMI difference greater than 0.01, while classification differences were limited to **8 buildings at the MMI 5.6 threshold** and **2 buildings at the MMI 5.8 threshold**.  

## Results

### Final Results

<div align="center">

<table>
  <thead>
    <tr>
      <th>Metric</th>
      <th>Lower Hutt City</th>
      <th>Wellington City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Total buildings</td>
      <td>57,039</td>
      <td>77,456</td>
    </tr>
    <tr>
      <td>Mean MMI</td>
      <td>5.704</td>
      <td>5.557</td>
    </tr>
    <tr>
      <td>Buildings with MMI ≥ 5.6</td>
      <td>68.58%</td>
      <td>34.86%</td>
    </tr>
    <tr>
      <td>Buildings with MMI ≥ 5.8</td>
      <td>32.89%</td>
      <td>5.17%</td>
    </tr>
    <tr>
      <td>Building footprint area with MMI ≥ 5.6</td>
      <td>70.92%</td>
      <td>36.83%</td>
    </tr>
    <tr>
      <td>Building footprint area with MMI ≥ 5.8</td>
      <td>34.91%</td>
      <td>7.02%</td>
    </tr>
  </tbody>
</table>

</div>

### Exposure comparison

The percentage-based exposure metrics are visualised below to highlight differences between Lower Hutt City and Wellington City.

<div align="center">

<img width="850" src="https://github.com/user-attachments/assets/7ddac64d-b6bb-4892-a08b-632b19f123e2" alt="Shaking exposure comparison between Lower Hutt City and Wellington City" />

<br>

<em>Figure 4. Comparison of building-count and building-footprint-area exposure at MMI ≥ 5.6 and MMI ≥ 5.8 in Lower Hutt City and Wellington City.</em>

</div>

The results show a clear difference in shaking exposure between the two study areas.

Lower Hutt had a substantially larger proportion of both buildings and building footprint area exposed to the higher modelled MMI ranges than Wellington City.

The RiskScape results were highly consistent with the independently derived ArcGIS Pro results, providing an independent cross-check of the hazard-sampling workflow.

## Tools & Skills Demonstrated

### ArcGIS Pro

- raster preparation and reprojection;
- vector projection and geometry QA/QC;
- geometry repair;
- Feature To Point;
- raster value extraction;
- Spatial Join;
- building footprint calculations;
- Summary Statistics;
- exposure classification and thematic mapping.

### RiskScape

- RiskScape Core Engine 1.14;
- project configuration and bookmarks;
- hazard and exposure layer configuration;
- raster hazard sampling;
- custom expression-based consequence functions;
- event-impact modelling;
- model output validation.

### Risk Modelling & QA

- hazard–exposure data integration;
- building-level exposure modelling;
- threshold-based exposure analysis;
- count- and area-based exposure metrics;
- cross-platform model validation;
- investigation of spatial-sampling outliers;
- transparent treatment of modelling assumptions and limitations.

## Limitations

- MMI represents modelled shaking intensity and does not by itself determine building damage.
- Detailed building vulnerability attributes were not available in the LINZ Building Outlines dataset.
- The MMI thresholds of 5.6 and 5.8 were defined for comparative analysis within this project and are not official risk or damage thresholds.
- Building footprint area is used as an exposure indicator and does not represent building replacement value, occupancy, floor area, or economic loss.
- Small differences between ArcGIS Pro and RiskScape results can occur because the two workflows use different spatial-sampling approaches.
