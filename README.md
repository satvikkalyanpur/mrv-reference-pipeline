# Sensitivity of Smallholder Agroforestry Carbon Credits under VM0047 (ARR)

A reproducible, open-data pipeline quantifying how much **issued carbon credits vary with defensible methodology choices** for a single arecanut agroforestry parcel in Chikkamagaluru (Malnad), Karnataka, India — computed under **VM0047 v1.1** (Verra's Afforestation, Reforestation and Revegetation standard, successor to CDM AR-ACM0003), with India's **CCTS** discussed as context.

> **Scope.** This is a reference-implementation demonstration on open/proxy data. It is **not** a field-validated measurement and does **not** issue real credits. Tree diameter, height, count, and species are assumed inputs (measured in operational deployment); equation forms, coefficients, and methodology rules are cited. Soil organic carbon is excluded under VM0047's optional-pool provision. India's CCTS is treated as context and is **not** used to compute credits.

## Key result

For an identical 1.27 ha parcel, issued credits range from **0.51 to 0.98 tCO₂e/yr** across **36 defensible parameter combinations** — a **1.94× spread** (CV 17.9%) — driven entirely by methodology choices that India's CCTS does not yet specify for agroforestry.

## Parameters varied (the 36 combinations)

The sensitivity analysis runs the full credit calculation across every combination of the values below (2 × 2 × 3 × 3 = 36). Each value is individually defensible and cited.

| Parameter | Values compared | Source |
|---|---|---|
| Carbon fraction | 0.47 / 0.50 | IPCC 2006 Vol.4 default / palm-carbon literature |
| Root-to-shoot ratio (BGB) | 0.15 / 0.24 | Pragasan 2025 (arecanut) / IPCC 2006 tropical default |
| Uncertainty deduction | 10% / 15% / 20% | VM0047 v1.1 (10% minimum, higher permitted) |
| Permanence buffer | 10% / 20% / 40% | VCS AFOLU Non-Permanence Risk Tool (risk-rated) |

Stand parameters (tree diameter, height, count) are held fixed — they are measurement inputs, not methodology choices — so the reported spread reflects methodology choice alone.

## What the pipeline does

| Step | Method | Source |
|---|---|---|
| Vegetation confirmation | NDVI from a cloud-filtered dry-season composite | Sentinel-2 (ESA Copernicus) |
| Above-ground biomass | Species-specific allometric equation (annual increment) | Prayogo et al. 2018 |
| Below-ground biomass | Root-to-shoot ratio applied to AGB | IPCC 2006 / Pragasan 2025 |
| Credit estimate | (AGB + BGB) − uncertainty deduction − permanence buffer | VM0047 v1.1 |
| Sensitivity | Issued credits across all 36 parameter combinations | — |
| Integrity | SHA-256 hash chain over key results | — |

## Methodology basis

**VM0047 v1.1** (active since May 2025): credits above- and below-ground biomass; soil organic carbon optional; minimum 10% uncertainty deduction at the 90% confidence interval; permanence via the VCS AFOLU Non-Permanence Risk Tool.

**India CCTS (offset):** agroforestry is a Phase-1 offset sector (Detailed Procedure, March 2025), but no agroforestry methodology is yet approved and no numeric quantification rules are published — so a CCTS agroforestry credit outcome is currently indeterminate.

## Repository contents

- `mrv_sensitivity.ipynb` — the full pipeline (runs top to bottom in Google Colab).
- `provenance.txt` — every data source, equation, coefficient, citation, and parameter value.
- `results-log.txt` — the recorded output numbers.
- `explanation.txt` — plain-language guide to what each output means and what is and is not claimed.
- `figure_sensitivity.png` — the sensitivity (tornado) figure.
- `site_map.png` — the study-parcel map (true colour, NDVI, boundary).
- `README.md` — this file.
- `LICENSE` — MIT.

## Figures

<img width="1085" height="602" alt="figure_sensitivity" src="https://github.com/user-attachments/assets/de603828-7eeb-49d3-82c4-08b23467278e" />

<img width="1917" height="862" alt="site_map" src="https://github.com/user-attachments/assets/6008d006-e921-4577-b135-bb06badc159c" />


## How to run

1. Open `mrv_sensitivity.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Register a free (noncommercial) Google Earth Engine project and paste your own project ID into Cell 2.
3. Run all cells (Runtime → Run all).

No local installation or data download is required; all data is streamed from Earth Engine.

## Key reference

Prayogo, C. et al. (2018). "Allometric Equation for Pinang (*Areca catechu*) Biomass and C Stocks." *AGRIVITA Journal of Agricultural Science*, 40(3): 381–389. DOI: 10.17503/agrivita.v40i3.1124

## License

MIT License (see `LICENSE`).
