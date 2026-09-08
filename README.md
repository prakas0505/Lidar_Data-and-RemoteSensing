Airborne LiDAR & Point Cloud Processing in R

A complete R-based workflow for airborne LiDAR point cloud processing, terrain and canopy modeling, individual tree delineation, and forest biomass estimation
— covering everything from raw .las/.laz files to plot-level forest structure metrics.
This repository is based on the Forest Information Technology course materials originally developed by Nikolai Knapp for the University for Sustainable Development Eberswalde (HNEE), 2020.
The scripts have been reviewed and updated to run on current R versions (R 4.4+, as of 2026), since several core dependencies were retired from CRAN between 2023 and 2026.

Contents
What this project does
Repository structure
Requirements
Setup
Data
Compatibility notes (R 4.4+)
Known limitations
References
Attribution.      
The workflow takes raw airborne LiDAR point clouds (and, in a companion simulation module, synthetic point clouds generated from forest inventory data) through a full forestry-focused processing pipeline:

Read/write point clouds in .txt, .las/.laz, and .rds formats, and manage large collections of tiles with a LAScatalog.
Classify points into ground / vegetation / building classes, and flag planar surfaces (roofs) using shape-based segmentation.
Rasterize point clouds into digital terrain models (DTM), digital surface models (DSM), and canopy height models (CHM), and reason about the matrix ↔ raster coordinate-origin flip.
Filter noise and outliers, both in the point cloud (birds, sensor noise) and via raster moving window filters.
Transform point clouds shifting, rotating, and clipping them into analysis ready plots  and normalize terrain so height is measured above ground rather than above sea level.
Derive structural metrics — vertical profiles, mean/quadratic mean canopy height, height quantiles, canopy cover, gap fraction at both the pointcloud and CHM level.
Delineate individual trees — tree-top detection and four different crown segmentation algorithms (watershed, Silva 2016, Li 2012, Dalponte 2016), plus an alternative adaptive mean-shift 3D approach.
Estimate biomass by fitting and evaluating linear and power-law models relating LiDAR-derived canopy metrics to field-measured above ground biomass (AGB) and basal area.
Simulate synthetic LiDAR point clouds and waveforms from forest inventory data (tree positions, DBH, crown geometry) using a Beer-Lambert light extinction model that is useful for testing algorithms against a known "ground truth" forest.
Batch-process whole point cloud collections using the free LAStools command-line suite, called from R via system2().
