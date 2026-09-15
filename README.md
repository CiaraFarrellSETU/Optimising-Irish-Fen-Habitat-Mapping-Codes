# Optimising-Irish-Fen-Habitat-Mapping-Codes
This repository contains the source code, scripts, and analytical workflows developed for optimising the mapping and monitoring of Irish fen habitats. Fens are complex, groundwater-fed wetland ecosystems of high conservation value under the EU Habitats Directive

BallyStrat
* **Data Preprocessing:** Maps string-based Fossitt habitat codes (`GM1`, `PB1`, `PF1`, etc.) to numerical targets.
* **Feature Engineering:** Generates an 8-band spectral index stack (`NDVI`, `SAVI`, `EVI`, `NDWI`, `GNDVI`, `GRVI`, `RVI`, `NRVI`) combined with Sentinel-2 optical bands.
* **Stratified Sampling:** Executes an 80/20 train/validation split per class to handle class imbalance.
* **Classification & Post-Processing:** Trains a 250-tree Random Forest model and applies 3x3 filtering to reduce pixel noise.
* **Validation:** Calculates Overall Accuracy, Kappa Coefficient, F1-Scores, Producer's/User's Accuracy, and outputs a formatted Confusion Matrix.
