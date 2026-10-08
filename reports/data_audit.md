# Data Audit

## Dataset

- **Source:** Tehran house price dataset
- **Number of rows:** 3,479
- **Number of columns:** 8
- **Duplicate rows:** 208

## Features

| Feature | Description | Initial Type |
|---|---|---|
| Area | Property area | String |
| Room | Number of rooms | Numeric |
| Parking | Parking availability | Numeric/Binary |
| Warehouse | Warehouse availability | Numeric/Binary |
| Elevator | Elevator availability | Numeric/Binary |
| Address | Property neighborhood/location | String |
| Price | Property price | Numeric |
| Price(USD) | Property price in USD | Numeric |

## Missing Values

Only the `Address` feature contains missing values:

- **Address:** 23 missing values (0.66%)
- Other columns: no missing values detected.

## Duplicates

The raw dataset contains:

- **208 duplicate rows**

This represents approximately **5.98%** of the dataset.

Duplicate records will be investigated during the cleaning stage rather than removed during the initial audit.

## Invalid Values

The audit identified:

- `Area <= 0`: **0**
- `Room <= 0`: **10**
- `Price <= 0`: **0**
- `Price(USD) <= 0`: **0**

Although no non-positive area values were detected, the `Area` column contains **6 non-numeric values** and therefore requires type investigation and cleaning.

## Categorical Variables

The raw dataset contains two string-based columns:

- `Area`: 243 unique values
- `Address`: 192 unique values

`Address` is the expected categorical location feature and has relatively high cardinality with 192 unique neighborhoods.

`Area` is conceptually a numerical feature, but it is currently represented as a string in the raw dataset. This must be corrected during data cleaning.

## Initial Observations

- The dataset contains **3,479 property listings and 8 features**.
- `Address` contains 192 unique neighborhood values and therefore represents a relatively high-cardinality categorical feature.
- `Address` has 23 missing observations.
- `Area` is stored as a string rather than a numerical data type.
- Six `Area` observations cannot currently be interpreted directly as numeric values.
- `Room` contains 10 non-positive observations, which are potentially invalid.
- The dataset contains 208 duplicate rows, requiring investigation before modeling.
- `Price` and `Price(USD)` contain no non-positive values.
- The binary property features (`Parking`, `Warehouse`, and `Elevator`) require consistency checks during cleaning.

## Potential Data Quality Issues

1. `Area` requires conversion to a numerical representation.
2. Six `Area` values are non-numeric and need to be investigated.
3. Ten observations have `Room <= 0` and may require removal or correction.
4. Twenty-three properties have missing `Address` values.
5. The 208 duplicate records need to be investigated.
6. Extreme values in area and price require further investigation before applying any outlier treatment.
7. The high cardinality of `Address` creates an encoding challenge for the machine-learning pipeline.
8. Any neighborhood-based feature must be constructed in a leakage-safe manner.

## Questions for Cleaning

1. What are the six non-numeric `Area` values?
2. What values occur in the ten records where `Room <= 0`?
3. Are the 208 duplicate rows exact duplicates or legitimate repeated listings?
4. Should observations with missing `Address` be removed or handled another way?
5. Which extreme values in `Area` and `Price` are genuine observations and which may be data errors?
6. How should `Address` be encoded without introducing target leakage?
7. Which transformations should be performed inside the training pipeline to ensure reproducibility and leakage safety?