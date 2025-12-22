# Spatial Autocorrelation Analysis Tool

**LISA Analysis Framework for Geospatial Data**

## Overview

This codebase implements a comprehensive spatial autocorrelation analysis workflow using Local Indicators of Spatial Association (LISA) to identify statistically significant spatial clusters and outliers in geospatial data. The application demonstrates comparative analysis between different spatial weight matrix definitions.

## Features

### Core Functionality

- **Dual Spatial Weights Implementation**
  - Queen contiguity weights (boundary-based neighborhood definition)
  - K-Nearest Neighbors (KNN) weights (distance-based neighborhood definition)

- **LISA Analysis**
  - Local Moran's I calculation for cluster identification
  - Statistical significance testing (p-value < 0.05)
  - Spatial cluster categorization (HH, LL, HL, LH)

- **Comparative Analysis**
  - Side-by-side visualization of different weight matrix results
  - Change detection between neighborhood definitions
  - Detailed reporting on classification differences

- **Geospatial Data Processing**
  - Automatic CRS verification and reprojection
  - Support for GeoPackage (.gpkg) multi-layer files
  - Geographic filtering and subsetting

## Technical Stack

- **Python 3.x**
- **GeoPandas** - Geospatial data structures and operations
- **PySAL/LibPySAL** - Spatial analysis library
- **ESDA** - Exploratory Spatial Data Analysis
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical computing
- **Matplotlib** - Visualization and plotting

## Architecture

The application follows a modular 10-step workflow:

1. **Environment Setup** - Library imports and random seed initialization
2. **Data Ingestion** - Remote file loading from GitHub repositories
3. **CRS Management** - Projection verification and standardization (EPSG:5387)
4. **Geographic Filtering** - Regional subsetting capabilities
5. **Queen Weights Matrix** - Contiguity-based neighbor definition
6. **Queen LISA Analysis** - First-pass cluster identification
7. **Result Labeling** - Human-readable category assignment
8. **KNN Weights Matrix** - Distance-based neighbor definition (K=8)
9. **KNN LISA Analysis** - Alternative cluster identification
10. **Comparative Reporting** - Multi-method result comparison

## Use Case: LIMA, Peru Education Analysis

The included implementation analyzes educational attainment patterns in LIMA, Peru:

- **Dataset:** Peru distrito-level administrative boundaries
- **Variable:** `Educ_sec_comp2019_pct` (High school completion rate, 2019)
- **Region:** LIMA departamento (171 districts)
- **Projection:** Peru96 / UTM zone 18S (EPSG:5387)

### Spatial Cluster Types

The analysis identifies four types of spatial patterns:

- **HH (High-High)** - Hotspots: High-performing areas clustered together
- **LL (Low-Low)** - Coldspots: Low-performing areas clustered together
- **HL (High-Low)** - Outliers: High performance surrounded by low
- **LH (Low-High)** - Outliers: Low performance surrounded by high

## Installation & Dependencies

```python
# Core dependencies
import geopandas as gpd
import pandas as pd
import numpy as np
from libpysal.graph import Graph
from numpy.random import seed
import esda
import matplotlib.pyplot as plt
```

All dependencies are pre-installed in Google Colab environments.

## Configuration

### Data Sources

The application supports remote data loading from GitHub repositories:

```python
# Example configuration
LinkPeru = "https://github.com/YOUR-ORG/Homework_1/raw/main/PeruMaps.gpkg"
layer = 'good_geom'
```

### Spatial Parameters

- **Target CRS:** EPSG:5387 (Peru96 / UTM zone 18S)
- **KNN Neighbors:** K=8 (configurable)
- **Significance Level:** α = 0.05
- **Random Seed:** 42 (for reproducibility)

## Output & Visualization

The application generates:

1. **Diagnostic Maps**
   - Full Peru boundary visualization
   - Filtered region confirmation plots

2. **LISA Cluster Maps**
   - Queen weights spatial clusters
   - KNN weights spatial clusters
   - Side-by-side comparative visualization

3. **Statistical Reports**
   - Cluster distribution tables
   - Change detection analysis
   - District-level classification comparisons

4. **Policy Interpretation**
   - Contextual analysis of spatial patterns
   - Methodological comparison insights
   - Actionable findings for intervention

## Methodology

### Queen Contiguity Weights

Defines neighbors as geographic units sharing any boundary point (edge or vertex). Number of neighbors varies by geography.

### K-Nearest Neighbors (K=8)

Defines exactly K nearest neighbors for each unit based on centroid distance. Ensures uniform neighbor counts but may include non-contiguous units.

### LISA Calculation

Local Moran's I statistic identifies local spatial autocorrelation patterns through:
1. Row-standardization of weights matrices
2. Spatial lag calculation
3. Statistical significance testing via permutation
4. Quadrant classification

## Data Requirements

Input data must include:
- Valid geometric boundaries (polygon features)
- Numeric variable for analysis
- Geographic identifiers (e.g., district names)
- Defined coordinate reference system

## Performance Considerations

- Row-standardized weights normalization ensures equal neighbor contribution
- Random seed (42) provides reproducible significance testing
- Analysis time scales with number of spatial units and permutations

## Applications

This framework can be applied to:
- Public health outcomes analysis
- Socioeconomic disparity mapping
- Environmental pattern detection
- Urban planning assessment
- Policy intervention targeting
- Educational outcome analysis

## Extensibility

The modular design allows easy adaptation for:
- Different geographic regions
- Alternative variables (HDI, poverty, health metrics)
- Various spatial weight definitions (Rook, Distance band)
- Custom significance thresholds
- Additional visualization styles

## License

MIT License
