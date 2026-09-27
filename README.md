# Beijing grey-green morphology and older adults' heat exposure

Derived data supporting the manuscript figures and supplementary analyses. The study covers 4,075 one-kilometre grids in nine Beijing districts. The outcome is daytime land-surface temperature weighted by residents aged 65 years and older (PWP), in degrees Celsius.

Repository: https://github.com/weiren2024/beijing-grey-green-older-adults-heat-exposure

## Contents

- `data/Figure1/`: the selected workflow figure's numerical grid snapshot and geometry. The CSV includes all 14 model predictors, PWP, coordinates and urban-form labels; it is not a simulated schematic dataset.
- `data/Figure2/`: mapped spatial layers in EPSG:32650.
- `data/Figure3/`: corrected PWP, grid geometry, density curves and type summaries.
- `data/Figure4/`: seven-to-four class counts and structural profiles. Spatial layers are shared with Figure 2.
- `data/Figure5/`: candidate-ranking and repeated-seed summaries. Full model-performance records are stored once under `supplementary/SupplementaryData1/`.
- `data/Figure6_Figure7/`: full SHAP rankings and relative contributions shared by both figures.
- `data/Figure8/`: partial-dependence curve coordinates and observed predictor deciles.
- `supplementary/SupplementaryData1/`: the 156-row performance ledger and its field guide.
- `supplementary/SupplementaryData2/`: complete pair screening and all 15 calculable pairs' seed-specific curves, aggregate curves and observed support. Figure 9 uses p01, p03 and p16; their files are not duplicated in a Figure 9 directory.
- `figure_data_map.csv`: exact figure-to-file mapping.
- `DATA_NOTES.md`: units, field meanings, sample definitions and limits.
- `SOURCE_PRODUCTS.md`: third-party source products and manuscript references.
- `file_manifest.csv`: relative paths, byte sizes, row counts and SHA-256 checksums. It excludes itself to avoid a circular checksum.

## Scope

This is a data-only companion to the study. It contains derived analytical data, figure-source data and recorded model outputs. The 4,075-row Figure 1 snapshot contains the numerical inputs used in the analysis, including the original missing-value pattern. Its predictor values, outcome and type membership were checked against the four archived model-input tables.

Training code, fitted models and third-party source rasters are not included. Source-product access and citation information are provided in `SOURCE_PRODUCTS.md`; the products remain subject to their original terms. No additional licence is assigned by this repository.

## Reading the files

CSV files are UTF-8 with a header row and decimal-point notation. Coordinates are projected metres (EPSG:32650). Empty numerical cells are not zeros. `DATA_NOTES.md` and the supplementary guides explain the different sample counts and units. Read the detailed conditional-analysis guide before interpreting its qualification flags or joining A-B pairs.

Use `figure_data_map.csv` to locate the files behind each figure, and `file_manifest.csv` to verify the downloaded files. Figure 9 shares its source tables with Supplementary Data 2, so those data appear only once.
