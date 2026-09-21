# Code for "How Does the Number of Source Countries Affect Cross-Country Crop-Yield Transfer Performance?"

This repository contains the R scripts used for the analysis reported in the paper.

## Data

The eight crop panel files (`panelv7_<crop>.xlsx`, for wheat, barley, oats, rye, rice,
maize, soybean, and sorghum) are provided directly in this repository. **Step 0 (data
preparation from raw monthly climate and FAOSTAT/World Bank sources) is not included
and does not need to be run.** Download the panel files, place them in your working
directory, and start from Step 1.

## Scripts

| Step | Purpose |
|------|---------|
| Step 1 | Builds the source/target country sampling plan (which countries are drawn as source countries for each target country and source-country size N) |
| Step 2 | Pilot runs to validate the modeling pipeline (5 models) on a small subset before scaling up |
| Step 3 | Stability test: compares 50, 100, and 200 replicates to choose the final replicate count |
| Step 4 | Full run: fits all 5 models across all 8 crops and all source-country sizes, using climate + GDP predictors. This is the main result reported in the paper. |
| Step 5 | Summarizes the Step 4 results into the tables and values reported in the paper |
| Step 6 | Produces the main learning-curve figures (pooled and per-crop) |
| Step 7 | Computes Mahalanobis distance between each target country and its source-country set, and merges it with the Step 4 results |
| Step 8 | Produces the distance-vs-error figure from the Step 7 results |
| Step 9 | Checks whether the distance-error association in Step 7 holds within each fixed source-country size N |
| Step 10 | Full run using climate-only predictors (no GDP), for comparison with Step 4. **Note: this comparison was ultimately not used in the paper** due to a difference in the sample of observations used by the two runs; it is included here for transparency. |
| Step 11 | Robustness check: repeats the Step 5 summary using normalized RMSE (NRMSE) instead of raw RMSE |
| Step 12 | Pilot version of the temporal-trend robustness check (2 crops only), used to estimate runtime before Step 13 |
| Step 13 | Full temporal-trend robustness check: repeats Step 4 after removing each country's own linear time trend from yield |

## Notes

- Scripts use fixed random seeds, so results are exactly reproducible.
- Steps 4, 10, and 13 are the most computationally expensive (each takes on the order
  of hours to days depending on hardware) and use checkpointing: if interrupted, simply
  re-run the script and it will resume from the last completed crop.
