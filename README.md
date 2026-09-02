# Spatial Incident Analysis with PCA

An R-based geospatial data science project analysing the spatial concentration of incidents across urban wards and investigating whether neighbourhood characteristics help explain the observed pattern.

## Project overview

The analysis combines point-pattern methods, spatial joins, ward-level incident densities and principal component analysis (PCA). It identifies geographic hotspots, summarises neighbourhood characteristics into lower-dimensional components and uses those results to motivate evidence-based priority areas.

## Methods

- Spatial data handling with `sf`
- Coordinate-to-polygon spatial joins
- Point-pattern analysis and kernel-smoothed intensity estimation
- Ward-level incident counts and density calculations
- Choropleth mapping with `ggplot2`
- PCA on standardised neighbourhood-profile variables
- Interpretation of PCA loadings and ward scores
- Correlation analysis between incident density and principal components
- Evidence-based prioritisation using both incident burden and neighbourhood profiles

## Selected findings

- Incident locations were highly concentrated rather than evenly distributed across the city.
- The five highest-count wards accounted for approximately 70% of recorded incidents, while the top ten accounted for approximately 86%.
- PCA reduced several neighbourhood characteristics into interpretable dimensions associated with social pressure, safety infrastructure and population density.
- The first two principal components explained most of the variation in the selected neighbourhood-profile variables, but their correlations with incident density were only moderate. This suggests that neighbourhood characteristics provide a partial rather than complete explanation of the spatial hotspot.
- The analysis identified Maple Cross and Saffron Lea as priority areas and recommended investigation of local response coverage and lighting infrastructure while avoiding causal claims from observational data.

## Repository structure

- `coursework_02.qmd` — source analysis in Quarto/R
- `coursework_02.md` — rendered GitHub-friendly report
- `coursework_02_files/` — generated figures and supporting render files
- `data/` — spatial and tabular datasets used by the analysis
- `coursework_02.Rproj` — RStudio project file

## Tools

R, sf, spatstat, tidyverse, ggplot2, patchwork, knitr

## Notes

This project was originally developed as university data science coursework and has been cleaned for portfolio presentation. The recommendations are prioritisation hypotheses based on observational evidence, not causal conclusions.
