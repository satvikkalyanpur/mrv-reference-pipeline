# Open Reproducible MRV Reference Pipeline for Agroforestry Carbon

A reproducible, open-data reference implementation of a Measurement, Reporting, and
Verification (MRV) pipeline for agroforestry carbon, demonstrated on an arecanut
(*Areca catechu*) agroforestry parcel in Chikkamagaluru (Malnad), Karnataka, India.

The pipeline takes a field boundary (polygon) and produces a conservative, uncertainty-
deducted carbon-credit estimate across three pools — above-ground biomass (AGB),
below-ground biomass (BGB), and soil organic carbon (SOC) change — with a tamper-evident
audit trail, using only free and open satellite and soil datasets.

> **Scope and honesty statement.** This is a *reference-implementation demonstration on
> open/proxy data*. It is **not** a validated carbon measurement and does **not** issue
> real credits. There is no field validation, no physical soil cores, and no ground-truth
> tree inventory. Species, tree diameter, height, and count are supplied inputs. Two
> components are explicitly provisional and flagged in the code and in `provenance.txt`:
> the soil-carbon change rate (a conservative literature value, not a calibrated model)
> and the palm below-ground ratio (a tree-derived default, as no palm-specific value was
> found). Producing real credits would require field baseline data and a calibrated soil
> model, verified by an accredited third party.

## What the pipeline does

| Step | Method | Data source |
|---|---|---|
| Parcel + vegetation | NDVI from a cloud-filtered dry-season composite | Sentinel-2 (COPERNICUS/S2_SR_HARMONIZED) |
| AGB | Species-specific allometric equation (increment, not standing stock) | Prayogo et al. 2018 (areca) |
| BGB | Root-to-shoot ratio applied to AGB (provisional palm proxy) | IPCC 2006 GL Vol.4 default |
| SOC baseline | Soil organic carbon concentration + stratification | SoilGrids, SRTM, ESA WorldCover |
| SOC change | Conservative literature-based rate (placeholder for calibrated RothC) | CHIRPS + ERA5-Land forcing |
| Credit estimate | AGB + BGB + ΔSOC − leakage − uncertainty buffer | — |
| Integrity | SHA-256 hash chain over daily records (no blockchain required) | — |
| Sensitivity | Issued credits vs uncertainty deduction | — |

## The organizing idea

Soil carbon has two separable parts. The **stock** (how much carbon is in the ground) is
spatially heterogeneous and is handled by stratification and sampling. The **change**
(the credited quantity) is driven by climate forcing, which is spatially smooth and is
handled by satellite and reanalysis data. The pipeline keeps these decoupled: the number
of soil samples scales with stock heterogeneity (strata), while the environmental forcing
is drawn from smooth satellite/reanalysis inputs.

## Repository contents

- `mrv_poc.ipynb` — the full pipeline (runs top to bottom in Google Colab).
- `provenance.txt` — every data source, equation, coefficient, citation, caveat, and
  final result, for full reproducibility.
- `README.md` — this file.
- `LICENSE` — see below.

## How to run

1. Open `mrv_poc.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Register a free (noncommercial) Google Earth Engine project and paste your project ID
   into Cell 2.
3. Run all cells top to bottom (Runtime → Run all).

No local installation or data download is required; all data is streamed from Earth Engine.

## Data sources (all free / open)

Sentinel-2 (ESA Copernicus), SoilGrids (ISRIC), SRTM (USGS/NASA), ESA WorldCover,
CHIRPS (UCSB Climate Hazards Group), ERA5-Land (ECMWF). Full asset IDs, date ranges,
and parameters are in `provenance.txt`.

## Key reference

Prayogo, C. et al. (2018). "Allometric Equation for Pinang (*Areca catechu*) Biomass and
C Stocks." *AGRIVITA Journal of Agricultural Science*, 40(3): 381–389.
DOI: 10.17503/agrivita.v40i3.1124

## Citation

If this reference pipeline is useful, please cite the accompanying paper (details to be
added on publication) and this repository.

## License

Released under the MIT License (see `LICENSE`) — permissive, standard for reproducible
research code, and compatible with the open datasets used.
