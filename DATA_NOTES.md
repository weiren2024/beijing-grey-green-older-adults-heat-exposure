# Data notes

## Grid snapshot and identifiers

`data/Figure1/workflow_map_values.csv` has one row per analytical grid. `LID` is the stable grid identifier; `FID` is an archived grid index. `Centroid_X` and `Centroid_Y` are projected coordinates in metres (EPSG:32650). `PWP_C` is the corrected older-population-weighted daytime land-surface temperature in degrees Celsius. No original or superseded PWP column is supplied.

`class4` maps to Zone1 = Compact (646 grids), Zone2 = Open mid-/high-rise (1,059), Zone3 = Open low-rise (660), and Zone4 = Green-space-dominated (1,710). `class7` retains the seven finer morphology classes; their labels and membership are supplied in `data/Figure4/class_counts.csv`. Classes 1, 2 and 3 map to type 1; classes 4 and 5 to type 2; class 6 to type 3; and class 7 to type 4.

The 14 predictors are `BuildHeight_Mean` (metres), `CanopyHeight_Mean` (centimetres), `G2_score`, `G3_score`, `B2_score`, `B3_score` (dimensionless), and green/grey `CORE_Pct`, `EDGE_Pct`, `BRDG_Pct` and `ISLET_Pct`. G2 denotes green fragmentation-extension; G3 green connectivity-interspersion; B2 grey fragmentation-boundary; B3 grey connectivity-interspersion. They are composite scores, not interchangeable with an individual landscape metric. MSPA percentages use the foreground area of the corresponding colour as denominator, not the whole grid.

MSPA was run separately for green and grey foregrounds on 10 m raster cells, using eight-neighbour foreground connectivity and an edge-width setting of 15 pixels (150 m). Classes were mapped over the study-area raster and then summarised within each analytical grid. The corresponding structural proportions were encoded as zero where a foreground was absent.

`BD_pct` and `GC_pct` are archived building-density and green-cover percentages used for stratification. Green cover was calculated as raster-tabulated green area divided by vector-grid area; forty stored estimates range from 100.08% to 100.35% and are retained without clipping. `GC_pct` is not one of the 14 final model predictors.

Building height and building density are blank for the same 70 grids in the green-space-dominated type. Blank source values must not silently be treated as zero when refitting models. The snapshot preserves source values rather than saving fitted imputation results.

## Spatial layers

JSON files retain their declared `crs` and labelled polygon collections. They are the geometric snapshots used by the study figures, not a general official-boundary distribution. The grid snapshot and grid geometries can be joined by `LID`; do not rely on row position. Figure 4 uses the shared Figure 2 geometry.

## PWP summaries (Figure 3)

`grid_data.csv` adds the published relative-exposure class to grid PWP. Low/middle/high groups use the pooled first and third quartiles; `ge35` fields refer separately to PWP at least 35 degrees Celsius. `density_curves.csv` contains the plotted density coordinates. In `type_summary.csv`, suffix `_C` indicates degrees Celsius; `_n` denotes counts and `_pct` percentages. Within-type quartiles and pooled quartile cutoffs are separate columns. `ge35_pct_within_type` uses all grids in that type as denominator; `share_of_all_ge35_pct` uses all grids meeting the 35-degree cutoff.

## Class and structural summaries (Figure 4)

`class_counts.csv` contains the fine-class counts and their four-type membership. `share_total_pct` uses all 4,075 grids. In `structural_profiles.csv`, `n_valid` is the count with an observed value of that feature; `mean_raw` retains the predictor's own unit. `pooled_mean` and `pooled_sd` describe the pooled feature, and `z_mean` is the type mean's standardised deviation from that pooled mean.

## Model performance and importance (Figures 5-7)

`candidate_ranking.csv` includes both the published rank summary and a ties-average diagnostic. `mean_rank` is the mean rank used for the displayed selection; `rank_sd_population` uses the population SD across the recorded comparison cells. `mean_rank_ties_average` is a separately stored average-rank treatment of ties, not a second model run. R2 gaps and R2 values are dimensionless; RMSE and MAE are in degrees Celsius. `seed_aggregate.csv` summarises the three seeds for each type-model combination. The complete performance CSV and its independent column guide are under SupplementaryData1.

`shap_all_models.csv` contains all 14 predictors for each type and each of the GBDT, RF and GWRF models. `mean_abs_shap` is in outcome units (degrees Celsius); `relative_pct` is its share of summed importance within that type-model combination; `rank` is the stored importance rank. `source_id` is a type-model identifier, not a file-system path. Importance alone does not encode the sign of a prediction relationship.

## Response curves (Figures 8-9)

`gbdt_pdp_points.csv` retains predictor coordinate `value` and predicted outcome `predicted_PWP` in degrees Celsius. Predictor coordinate units follow the grid snapshot above. `gbdt_pdp_deciles.csv` provides observed predictor quantiles; `n` is the available observation count.

Figure 9's shared numerical evidence is in SupplementaryData2: p01 is green-islet share by grey-core conditions in the compact type; p03 is G3 by green-islet conditions in the compact type; p16 is building height by B2 conditions in the green-space-dominated type. The included `Data_guide.txt` specifies all file roles, denominators, seeds, units, blank values and exact support-bin meanings. Pair directories p04 and p08 are absent by design because curves could not be calculated; their reasons remain in the complete screen and geometry-rejection records.
