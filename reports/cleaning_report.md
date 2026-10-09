# Day 2 — Data Cleaning and Exploratory Data Analysis

## 1. Objective

The objective of this stage was to clean the raw Tehran housing dataset, investigate suspicious records, examine the distributions of important variables, and prepare a reproducible dataset for machine learning.

## 2. Dataset overview

- Original dataset: 3,479 rows and 8 columns.
- Cleaned dataset: 3,256 rows.
- Rows removed: 223.
- Rows retained: 93.53%.

## 3. Data cleaning

The following operations were performed:

1. Converted `Area` to a numeric format, removing thousands separators.
2. Removed missing, non-numeric, and non-positive area values.
3. Excluded area values above 1,000 m² as implausible or malformed for this dataset.
4. Removed records with missing, non-numeric, or non-positive room counts.
5. Removed records with missing, non-numeric, or non-positive prices.
6. Excluded a suspicious record at original index 136: a 160 m² property in Qarchak priced at 3,600,000 rials. This record was flagged because its price was substantially below the observed price distribution.
7. Removed exact duplicate rows.
8. Replaced missing addresses with `Unknown`.

The area threshold and suspicious-price exclusion are dataset-specific decisions and may affect model generalization. They should be reconsidered if more reliable property-level information becomes available.

## 4. Validation

After cleaning:

- Missing values: 0.
- Exact duplicate rows: 0.
- Minimum area: 32 m².
- Maximum area: 1,000 m².
- Minimum price: 55,000,000 rials.
- Maximum price: 92,400,000,000 rials.

## 5. Exploratory data analysis

The following figures were generated:

- `figures/cleaned_area_price_distributions.png`
- `figures/area_vs_price.png`

The figures show the distributions of property area and price and the relationship between area and price. The relationship should be explored further during modeling rather than assumed to be strictly linear.

## 6. Modeling considerations

`Price` is the prediction target. `Price(USD)` is a derived conversion of `Price` and must not be included among model input features, as doing so would cause target leakage.

The cleaned dataset is intended for downstream feature engineering and model development.

## 7. Limitations

The dataset does not provide enough information to independently verify every unusual property record. Some extreme observations may be genuine. The cleaning rules therefore combine numeric validation with documented, dataset-specific judgments.