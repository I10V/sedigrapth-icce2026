# Long-term sediment flow monitoring in the Baksan River catchment: challenges and flood-event dynamics

This repository contains the R analytical pipeline and visualization code for the research presented at the **International Commission on Continental Erosion (ICCE 2026) Conference** in Como, Italy.

## Overview

The codebase implements a hydrograph/sedigraph separation model designed to isolate sediment transport mechanisms in high-mountain, glacierized catchments (Baksan River Basin, Central Caucasus). The script decomposes continuous time-series sediment load data into three distinct runoff and transport components:

* **Baseline Glacial Ablation:** Background sediment yield driven by seasonal ice and snowmelt.
* **Sediment Reworking:** In-channel bed and bank sediment remobilization post-flood.
* **Rainstorm / Debris-Flow Peaks:** High-magnitude, short-duration pulse events caused by heavy rainfall or debris flows.

## Catchment & Monitoring Gauges

The script analyzes multi-year monitoring datasets across three key gauging stations:
* **Djankuat:** Headwater glacier basin (2015–2025 multi-year series).
* **Baksan, Tyrnyauz:** Middle reach monitoring gauge.
* **Baksan, Zayukovo:** Lower catchment outlet gauge.

## Repository Structure

| File / Folder | Description |
| :--- | :--- |
| `sediment_analysis.Rmd` | Main R Markdown file containing separation functions, hydrograph plots, and pie-chart proportion grids. |
| `sedigraph_smooth.qs` | Preprocessed continuous hydro-meteorological and sediment transport data (stored via `qs2`). |
| `presentation.pptx` | Slides for the ICCE 2026 conference presentation. |
| `output/` | Generated high-resolution plots (`.png`) for publication and presentation slides. |

## Methodological Workflow

1. **Diurnal Envelope Separation:** Uses moving median windows (`zoo::rollapply`) across specific time-of-day groups to separate diurnal ablation signals (`win_long = 90` days) from event-scale adaptation windows (`win_short = 10` days).
2. **Component Quantification:** Calculates proportional sediment mass contributions (in metric tons) for the main ablation season (June 1 – September 15).
3. **Visualization:** Generates stacked hydrograph time series (`ggplot2::geom_area`) and regional comparative pie-chart matrices (`ggplot2::coord_polar`).

## Requirements & Dependencies

To execute the R Markdown analysis, install the following required packages in R:

```r
install.packages(c("dplyr", "lubridate", "ggplot2", "tidyverse", "zoo"))
# For fast binary data deserialization:
install.packages("qs2")
