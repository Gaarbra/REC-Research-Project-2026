# ZEV Adoption and Air Quality in Southern California
### A Post-COVID Panel Analysis of NO₂ and PM₂.₅ Across 20 Cities (2021–2024)

**Gabriel Girma (CMC '28)**  
REC Spring 2026 Research Fellowship · Roberts Environmental Center  
May 4, 2026

---

## Overview

This project investigates whether localized zero-emission vehicle (ZEV) adoption rates correlate with sustained reductions in nitrogen dioxide (NO₂) and fine particulate matter (PM₂.₅) across 20 Southern California cities in the post-COVID period (2021–2024). Using a balanced panel of 80 city-year observations, four OLS models are estimated with year fixed effects and city-clustered standard errors.

The central finding: at current penetration rates of 1–7% of registered vehicles, ZEV adoption is **not associated with air quality improvement**. The dominant predictor of both pollutants is pre-existing environmental burden as measured by CalEnviroScreen 4.0, consistent with structural inequality literature pointing to heavy-duty diesel freight - not light-duty passenger vehicles - as the mechanism sustaining pollution disparities in high-burden communities.

---

## Research Questions

1. Do localized ZEV adoption rates correlate with reductions in NO₂ and PM₂.₅ across 20 Southern California cities (2021–2024)?
2. Does ZEV adoption in a given year predict air quality outcomes in the subsequent year?
3. Are any observed air quality benefits distributed equitably across communities stratified by CalEnviroScreen vulnerability quartiles?

---

## Repository Structure

```
REC-Research-Project-2026/
├── data/                  # Raw and processed datasets
│   ├── EPA AQS annual summary files (NO₂, PM₂.₅)
│   ├── CEC ZEV registration data (ZIP-to-city aggregated)
│   ├── Census ACS 2020 5-Year income estimates
│   └── CalEnviroScreen 4.0 tract-level scores
├── docs/
│   └── Girma_final_draft.pdf   # Final research paper (link below)
├── bib/                   # Bibliography / references
├── .gitattributes
└── .gitignore
```

The analysis pipeline (Jupyter Notebook) is the primary deliverable alongside the paper.

**[Read the final paper (PDF)](https://github.com/Gaarbra/REC-Research-Project-2026/blob/main/docs/Girma_final_draft.pdf)**

---

## Data Sources

| Dataset | Source | Use |
|---|---|---|
| Air quality (NO₂, PM₂.₅) | EPA AirData AQS Annual Summaries | Dependent variables |
| ZEV registrations | California Energy Commission Vehicle Population | Key independent variable |
| Median household income | U.S. Census ACS 2020 5-Year Estimates | Control variable |
| Environmental burden | CalEnviroScreen 4.0 (OEHHA) | Moderating variable |
| ZIP-to-city crosswalk | HUD USPS ZIP-to-tract crosswalk weights | Geographic aggregation |
| ZIP-to-city names | SimpleMaps | CEC aggregation |

All control and moderating variables are fixed at 2020 pre-period values to avoid endogeneity.

---

## Methods

### Sample
20 Southern California cities with continuous EPA monitor coverage for both pollutants across all four years (2021–2024), yielding a **balanced panel of 80 city-year observations**. Cities include: Anaheim, Banning, Compton, El Cajon, Fontana, Lancaster, Lompoc, Long Beach, Los Angeles, Mira Loma, Ontario, Palm Springs, Pasadena, Pico Rivera, Reseda, Rubidoux, San Bernardino, San Diego, Simi Valley, and Victorville.

### Multicollinearity Resolution
Raw VIF analysis revealed severe collinearity between ZEV adoption rate and CES score (VIF ≈ 12.4 and 8.7), driven by a shared wealth gradient. To resolve this, the **Frisch–Waugh–Lovell (FWL) theorem** is applied: ZEV adoption and CES scores are residualized with respect to income and fleet size before entering the regression. Post-residualization VIF drops to ≈ 1.1 for both variables.

### Models
Four OLS specifications are estimated for both PM₂.₅ and NO₂:

| Model | Description |
|---|---|
| **Model 1** (Baseline) | Income + year fixed effects only |
| **Model 2** (Policy) | Adds residualized ZEV rate, log fleet size, residualized CES score |
| **Model 3** (Persistence) | Replaces contemporaneous ZEV with one-year lag (N = 60, 2022–2024) |
| **Model 4** (Equity) | Adds ZEV × CES interaction to test differential effects across vulnerability quartiles |

All models include city-clustered standard errors and year fixed effects with 2021 as the reference year.

---

## Key Results

### CalEnviroScreen Burden (Strongest Finding)
The residualized CES score is **positive and highly significant** across all models and both pollutants. For PM₂.₅, the coefficient is approximately **0.20–0.22 µg/m³ per unit**; for NO₂, **0.39–0.43 ppb per unit**. Pre-existing environmental burden predicts current air quality even after controlling for income, fleet size, ZEV adoption, and year trends.

### ZEV Adoption
The residualized ZEV rate is **positive and statistically significant** - cities with unexpectedly high ZEV adoption (given income and fleet size) are associated with *worse*, not better, air quality. The lagged coefficient is larger than the contemporaneous one, ruling out a delayed-benefit explanation. The likely mechanism: high-adoption cities are also the most traffic-intensive, and post-COVID traffic rebound is outpacing electrification gains.

### Equity Interaction
The ZEV × CES interaction is **not significant** for either pollutant. High-burden communities are neither benefiting more nor less from ZEV adoption - structural inequity persists independently of local electrification levels.

### Residual Analysis
Model 3 residuals plotted against CES scores show a consistent upward slope. Ontario's NO₂ residual exceeds +10 ppb above prediction (consistent with its position at the I-10/I-15 freight interchange); Mira Loma and Fontana are the largest PM₂.₅ over-performers. This points to **heavy-duty diesel freight** as the primary mechanism sustaining the pollution premium in high-burden communities.

---

## Policy Implications

- Light-duty ZEV electrification at current penetration levels is insufficient to produce detectable ambient air quality improvements.
- Strategies targeting **heavy-duty diesel emissions** (e.g., SCAQMD Rule 2305 / WAIRE program) are likely more effective at reducing pollution disparities.
- Even if ZEVs eventually produce ambient benefits, those benefits will accrue in communities that need them least: affluent urban households still account for roughly 64% of EV owners (Wang et al., 2026).

---

## Selected References

- Garcia et al. (2023). California's early transition to electric vehicles: Observed health and air quality co-benefits. *Science of the Total Environment*, 867, 161761.
- Kerr, Goldberg & Anenberg (2021). COVID-19 pandemic reveals persistent disparities in nitrogen dioxide pollution. *PNAS*, 118(30).
- Tessum et al. (2019). Inequity in consumption of goods and services adds to racial–ethnic disparities in air pollution exposure. *PNAS*, 116(13), 6001–6006.
- Wang, Harper & Hendrickson (2026). Changing US electric vehicle owner socioeconomic characteristics. *Transportation Research Interdisciplinary Perspectives*, 35, 101788.

Full bibliography available in `bib/` and in `docs/Girma_final_draft.pdf`.

---

## Citation

> Girma, G. (2026). *ZEV Adoption and Air Quality in Southern California: A Post-COVID Panel Analysis of NO₂ and PM₂.₅ Across 20 Cities (2021–2024)*. REC Spring 2026 Research Fellowship, Roberts Environmental Center, Claremont McKenna College.