# quasar_3C_279_analysis_glmm
Request from Rodney H
the data comes from the AAVSO AID of the Quasar  3C 279  https://en.wikipedia.org/wiki/3C_279
It goes back to 2000 or so.  The issue is in the last 3 years since (2023)  there has been dimming of magnitudes,  how come?
The GLMM might help with comparing the variability in the time series before 2022 and in the data after 2023 (dimming part). 
The analysis is to be done using R and Quarto. The data is contained in the csv file rawdata_279-3C_cleaned.csv.

## Analysis

The analysis lives in **[`GLMM_3C279.qmd`](GLMM_3C279.qmd)** (Quarto/R), which renders to **[`GLMM_3C279.html`](GLMM_3C279.html)**.

📊 **Read the rendered report:** https://davidjayjackson.github.io/quasar_3C_279_analysis_glmm/

It compares 3C 279's brightness and variability before 2022 vs. from 2023 onward (2022 excluded as a transition year), using:

- a linear mixed model, `mag ~ epoch + (1 | band)`, for the change in mean brightness;
- a location-scale GLMM (`glmmTMB` with `dispformula = ~ epoch`) for the change in variability;
- a Johnson **V**-band-only sensitivity check to remove the band-composition confound.

**Finding:** since 2023, 3C 279 is both *fainter* (~1.7 mag in V) and *quieter* (V-band scatter roughly halves). The "quieter" signal only emerges once the filter is held fixed.

### Reproduce

```r
install.packages(c("tidyverse", "lubridate", "scales", "patchwork",
                   "lme4", "glmmTMB", "broom.mixed", "knitr"))
quarto::quarto_render("GLMM_3C279.qmd")
```
