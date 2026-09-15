# Optimising-Irish-Fen-Habitat-Mapping-Codes
This repository contains the source code, scripts, and analytical workflows developed for optimising the mapping and monitoring of Irish fen habitats. Fens are complex, groundwater-fed wetland ecosystems of high conservation value under the EU Habitats Directive


In all codes the date range, spectral features combos and data splits can be edited to look at different temporal windows, feature sets and data splits

  
BallyStrat
* **Data Preprocessing:** Maps string-based Fossitt habitat codes (`GM1`, `PB1`, `PF1`, etc.) to numerical targets.
* **Feature Engineering:** Generates an 8-band spectral index stack (`NDVI`, `SAVI`, `EVI`, `NDWI`, `GNDVI`, `GRVI`, `RVI`, `NRVI`) combined with Sentinel-2 optical bands.
* **Stratified Sampling:** Executes an 80/20 train/validation split per class to handle class imbalance.
* **Classification & Post-Processing:** Trains a 250-tree Random Forest model and applies 3x3 filtering to reduce pixel noise.
* **Validation:** Calculates Overall Accuracy, Kappa Coefficient, F1-Scores, Producer's/User's Accuracy, and outputs a formatted Confusion Matrix.

  
  Ballymore
* **Data Mapping:** Converts string-based Fossitt habitat codes to numeric identifiers for machine learning compatibility.
* **Spectral Feature Engineering:** Constructs a 12-band input stack combining raw optical bands with 8 vegetation and moisture indices (`NDVI`, `SAVI`, `EVI`, `NDWI`, `GNDVI`, `GRVI`, `RVI`, `NRVI`).
* **Random Forest Classification:** Trains a 250-tree Random Forest classifier using high-resolution spatial sampling (5m).
* **Spatial Post-Processing:** Reduces noise using a 3x3 and offers polygon-level majority voting (`reduceRegions`) for clean boundary outputs.
* **Model Validation:** Computes training/validation accuracy, Producer's & User's accuracy, Kappa coefficient, and full confusion matrices to evaluate model performance and overfitting.
* **Habitat Area Reporting:** Automatically calculates vector coverage metrics, outputting precise per-class spatial statistics in hectares and percentages.

  
Ballymore_5.no
* **Data Harmonization & Band Scaling:** Standardizes string-based Fossitt habitat codes to numeric identifiers and scales raw Sentinel-2 reflectance values.
* **Spectral Indices Engineering:** Builds a 12-band stack combining optical bands with 8 spectral indices (`NDVI`, `SAVI`, `EVI`, `NDWI`, `GNDVI`, `GRVI`, `RVI`, `NRVI`).
* **Random Forest Modeling:** Samples regions at 5m resolution and trains a 250-tree Random Forest classifier on an 80/20 train/validation split.
* **Spatial Smoothing & Map Display:** Uses a 3x3 filter for spatial denoising and visualizes output maps via custom color palettes.
* **Accuracy Assessment:** Evaluates model performance using internal training metrics and unseen validation metrics (Overall Accuracy, Kappa Coefficient).
* **Automated Area Analytics & UI Charts:** Dynamically calculates spatial coverage (hectares and percentages) and renders UI column/pie charts for habitat composition.
* **Spectral Distribution Profiling & CSV Export:** Generates custom 5-number summary interval boxplots (Min, P_{25}, Median, P_{75}, Max) across classes and outputs a direct CSV download URL for pixel-level data.

  
Ballymore_bestscene
* **Optimal Scene Selection:** Queries the 2019–2020 Sentinel-2 repository to programmatically select, clip, and process the single clearest scene (lowest cloud cover percentage).
* **Spectral Indices Engineering:** Generates an 8-band index stack (`NDVI`, `RVI`, `SAVI`, `EVI`, `GNDVI`, `GRVI`, `NRVI`, `NDWI`) combined with raw Sentinel-2 optical bands ($B2, B3, B4, B8$).
* **Data Harmonization:** Converts string-based Fossitt habitat codes to numeric identifiers for Random Forest compatibility.
* **Classifier Training:** Samples pixel regions at 5m resolution and trains a 250-tree Random Forest classifier across an 80/20 train/validation split.
* **Spatial Smoothing & Map Display:** Filters out spatial noise using a 3x3 filter.
* **Overfitting & Validation Diagnostics:** Calculates and compares internal training accuracy against unseen validation accuracy, Kappa coefficient, and confusion matrices.

  
Ballymore_growing
* **Growing Season Median Compositing:** Generates a cloud-free composite from summer 2020 Sentinel-2 imagery clipped to polygon bounds.
* **Feature Engineering:** Combines 4 optical bands with an 8-index spectral stack (`NDVI`, `RVI`, `SAVI`, `EVI`, `GNDVI`, `GRVI`, `NRVI`, `NDWI`).
* **Stratified Sampling:** Samples pixel regions at 5m resolution and enforces an 80/20 train/validation split per class.
* **Random Forest Modeling & Post-Processing:** Fits a 250-tree Random Forest classifier and reduces spatial noise via a 3x3 filter.
* **Detailed Accuracy Assessment:** Evaluates validation and internal training performance (Overall Accuracy, Kappa) alongside per-class Producer's and User's Accuracy metrics.
* **Formatted Diagnostics:** Outputs an aligned 8x8 confusion matrix table directly into the GEE console and prints unique vector asset codes for validation.


Ballymore_lowcloud
* **Growing Season Median Compositing:** Generates a cloud-free composite from  Sentinel-2 imagery clipped to polygon bounds.
* **Feature Engineering:** Combines 4 optical bands with an 8-index spectral stack (`NDVI`, `RVI`, `SAVI`, `EVI`, `GNDVI`, `GRVI`, `NRVI`, `NDWI`).
* **Stratified Sampling:** Samples pixel regions at 5m resolution and enforces an 80/20 train/validation split per class.
* **Random Forest Modeling & Post-Processing:** Fits a 250-tree Random Forest classifier and reduces spatial noise via a 3x3 filter.
* **Detailed Accuracy Assessment:** Evaluates validation and internal training performance (Overall Accuracy, Kappa) alongside per-class Producer's and User's Accuracy metrics.
* **Formatted Diagnostics:** Outputs an aligned 8x8 confusion matrix table directly into the GEE console and prints unique vector asset codes for validation.


Ballymore_stats
* **Band Scaling & Feature Engineering:** Scales raw Sentinel-2 bands to properly calculate clamped vegetation and water indices (`NDVI`, `RVI`, `GNDVI`, `SAVI`, `EVI`, `GRVI`, `NRVI`, `NDWI`).
* **Feature Integration:** Stacks 4 optical bands (B2, B3, B4, B8) with the 8 calculated spectral indices into a 12-band classification image.
* **Random Forest Classification:** Samples regions at 5m resolution and splits data 80/20 into training and validation sets for a 250-tree Random Forest model.
* **Accuracy Validation & Binary Scoring:** Classifies unseen test pixels and programmatically generates a binary correctness indicator (`is_correct`) comparing actual vs. predicted habitat IDs.
* **Direct CSV Export:** Dynamically generates and prints a direct download link for the validation results CSV (`habitat_num`, `is_correct`), enabling rapid external performance auditing.
