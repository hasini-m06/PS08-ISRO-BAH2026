# PS08 — Lunar Subsurface Ice Exploration Pipeline
## Bharatiya Antariksh Hackathon 2026

**Problem Statement PS08**: Detection and Characterization of Subsurface Ice 
in Lunar South Polar Regions Using Chandrayaan-2 Radar and Imagery Data 
for Landing Site and Rover Traverse Planning.

## Key Results
| Stage | Output |
|-------|--------|
| Ice Detection | 29 confirmed pixels, Haworth–Shoemaker complex |
| Landing Site | 87.2596°S, 19.2198°E — Score: 92.6/100 |
| Rover Traverse | 20.16 km, 40.3 h (next-gen rover 0.5 km/h) |
| Ice Volume | 9,062 m³ best estimate — 9.06 million litres |
| Mission Impact | 69–276 years supply for 6-person lunar base |

## Data Sources
- Chandrayaan-2 DFSAR West + East mosaics — ISRO PRADAN/ISDA
- Chandrayaan-2 OHRC strips (9 polar strips, 2.9 GB) — ISRO PRADAN
- LOLA DEM ldem_75s_60m.img — NASA PDS

## Method
Dual-criteria CPR+DOP filter (CPR > 1.0 AND DOP < 0.13) directly from:
> Sinha R.K. et al. (2026). "Subsurface ice in doubly shadowed craters
> as revealed by Chandrayaan-2 dual frequency synthetic aperture radar."
> npj Space Exploration 2, Article 22.

## Pipeline Stages
1. Doubly-shadowed crater ID — geometric horizon model + PSR mask
2. CPR + DOP extraction — full-resolution targeted DFSAR windows
3. Dual-criteria ice detection — 29 confirmed pixels georeferenced
4. Landing site selection — 12,615 candidates, multi-criteria scoring
5. Dijkstra rover traverse — slope + PSR cost raster, 7 named waypoints
6. Ice volume estimation — literature ice fraction method (5–20%)
7. Instrument payload recommendation — NS, GPR, Drill+TDR, MS

## Tools
`rasterio` `pyproj` `numpy` `scipy` `skimage` `PIL` `matplotlib`

## Reproducibility
Run all 27 cells top to bottom on Google Colab with Drive mounted.
Full pipeline runtime: ~45 minutes.
All data from open-access archives (ISRO PRADAN, NASA PDS).
