# Day 3 — Feature Engineering and Leakage Prevention

## Dataset
- Input: `data/processed/tehran_house_prices_cleaned.csv`
- Rows: 3,256
- Input columns: 8
- Unique addresses: 193

## Target and features
- Target: `Price` (total property price in rials).
- Numeric inputs: Area, Room.
- Boolean inputs: Parking, Warehouse, Elevator.
- Categorical inputs: Address.

## Leakage prevention
- `Price(USD)` was excluded because it is derived from the target `Price`.
- `Price_per_sqm` was calculated for exploratory analysis only and excluded from model inputs because it depends on `Price`.
- Categorical encoding has not been fitted on the full dataset. Encoding and any learned preprocessing should be fitted on training data only in the modeling pipeline.

## Neighborhood analysis
- Neighborhoods were compared using median total price and median price per square meter.
- The price-per-square-meter chart includes only neighborhoods with at least 10 observations; this threshold applies to visualization only and does not filter the modeling dataset.
- Neighborhoods with small sample counts should be interpreted cautiously.

## Output files
- `data/processed/modeling_dataset.csv`
- `data/processed/model_features.csv`
- `data/processed/model_target.csv`
- `figures/day3_area_vs_price.png`
- `figures/neighborhood_price_per_sqm.png`

## Limitations and next steps
The dataset may contain unobserved differences in listing quality, property condition, exact location, and other factors. Day 2's data-cleaning judgments are documented in `reports/cleaning_report.md`. Day 4 will establish a train/test split and evaluate baseline models using leakage-safe preprocessing pipelines.
