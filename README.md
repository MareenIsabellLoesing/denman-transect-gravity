# Denman Transect Gravity Processing

Python notebook for processing ground-based gravity observations collected during the Denman Terrestrial Campaign in East Antarctica in 2023–2024 used in 

**Lösing, M., Aitken, A., Field, M., MacKie, E., & Li, L. (2026). Gravity topography modeling of the Denman Glacier region using a geostatistical approach. The Cryosphere, 20(10), 5629-5652. https://doi.org/10.5194/tc-20-5629-2026**

The workflow ties Scintrex CG-5 relative readings to the Casey Station gravity reference and calculates gravity disturbances along the Denman Glacier transect.

## Workflow

1. Download and extract the Casey Station, Bunger Hills control, and transect data from IMAS.
2. Load gravimeter observations and GNSS-derived site coordinates and heights.
3. Estimate instrument drift from repeated observations at Casey Station and three Bunger Hills control locations.
4. Replace the internal CG-5 tidal correction with a new calculated correction.
5. Subtract WGS84 normal gravity evaluated with Boule at each observation's latitude and ellipsoidal height.
6. Estimate residual temporal drift from repeated observations at master Site 5.
7. Export site coordinates, heights, and corrected gravity disturbances to CSV.

## Getting started

Install Python, Jupyter, and the main packages used by the workflow:

```bash
pip install jupyter numpy pandas scipy matplotlib pyproj boule openpyxl
```

Open `Denman_Transect_Gravity_Processing.ipynb` and run the cells in order. The download cell retrieves the three source archives into `data/`; an internet connection is required for the initial download.

## Source data

The observations are available from the Institute for Marine and Antarctic Studies (IMAS):

**Lösing, M., & Aitken, A. (2026). Denman Terrestrial Campaign – Ground-based gravity transect [Data set]. Institute for Marine and Antarctic Studies. https://doi.org/10.25959/RM9S-KT42**

The dataset provides three archives:

- **Bunger Hills control measurements:** summary measurements, raw gravimeter files, and GNSS observations for transect d days.
- **Casey Station measurements:** summary measurements and raw gravimeter files.
- **Transect measurements:** gravity observations, site coordinates and heights, and GNSS files.

Source data are licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Cite the dataset when using these observations. 

## Output

`Gravity_Transect.csv` contains:

| Column | Description | Units |
| --- | --- | --- |
| `Easting_m` | Projected easting in the Antarctic coordinate system defined in the notebook | m |
| `Northing_m` | Projected northing in the same coordinate system | m |
| `Longitude` | Site longitude | degrees east |
| `Latitude` | Site latitude | degrees north |
| `Gravity_disturbance_mGal` | Gravity disturbance | mGal |
| `Ellipsoidal_height_m` | Site height above the reference ellipsoid | m |

## Processing conventions

- All gravity readings and corrections are expressed in **mGal**.
- The output is a **gravity disturbance**, calculated by subtracting normal gravity at the observation position.
