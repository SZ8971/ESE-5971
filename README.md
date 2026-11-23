# ESE 5971 — St. Louis Real Estate Project

## Project Overview

This project aims to help real estate developers and investors identify residential properties in the City of St. Louis that may be worth further investigation.

The project uses historical property assessment data from 2017 to 2025 to predict one-year changes in assessed property values and support preliminary property screening rather than final investment decisions.

## Data Source

The project uses annual parcel datasets (PAR2017–PAR2025) from the City of St. Louis Open Data website.

**Source:** [City of St. Louis Open Data](https://www.stlouis-mo.gov/data/datasets/distribution.cfm?id=189)

The original CSV files are not included in this repository.

## Milestone 2 — Initial Analysis

Milestone 2 established the initial analytical framework, including:

- Property matching across years using `HANDLE`
- Data cleaning and missing-value analysis
- One-year log appreciation target construction
- Chronological train-validation-test split
- Mean baseline and linear regression

The initial results showed limited predictive performance, with only a small improvement from linear regression.

## Milestone 3 — Updated Analysis

Milestone 3 focuses on addressing the limitations identified in Milestone 2.

The main improvements include:

- Restricting the dataset to eligible non-vacant residential properties
- Investigating the two-year reassessment cycle
- Examining unusual assessed-value changes and within-property dependence
- Introducing additional baseline models, including a cycle-aware historical baseline
- Evaluating models using rolling-origin validation
- Testing property-ranking performance using a limited screening budget
- Generating a preliminary residential property-screening list

### Main Findings

The analysis identified a clear two-year reassessment pattern. Assessed values changed more frequently in odd target years, while most properties remained unchanged in even target years.

The zero-change baseline performed best in non-reassessment years, while linear regression provided limited improvement during reassessment years.

Historical ranking sometimes outperformed linear regression in identifying high-appreciation properties, but its performance was not consistent across years.

These findings suggest that the assessment cycle plays an important role in prediction performance and that the current models are more appropriate for preliminary screening than final investment decisions.

## Prediction Target

The project continues to predict one-year log changes in recorded assessed property values:

```python
Log_Appreciation = log(Next_ASMTTOTAL / ASMTTOTAL)
```

The two-year reassessment cycle is considered in the analysis, but the prediction horizon remains one year.

## How to Run

1. Download the annual parcel CSV files (2017–2025) from the [official data source](https://www.stlouis-mo.gov/data/datasets/distribution.cfm?id=189).

2. Create a folder named `Parcels-CSV-2017-2025` in the notebook's working directory.

3. Ensure the folder contains all CSV files from `PAR2017.csv` through `PAR2025.csv`.

4. Install the required Python packages using `requirements.txt`, if available:

   ```bash
   pip install -r requirements.txt
   ```

5. Open either notebook in Jupyter Notebook or VS Code:
   - `Milestone2.ipynb`
   - `Milestone3_Code.ipynb`

6. Run the notebook cells in order.

**Note:** If a notebook is stored in a subfolder, ensure that its relative data path points to the correct CSV directory.

## Limitations

The project predicts changes in recorded assessed property values rather than actual market prices or investment returns.

The results may be affected by:

- Property assessment and reassessment practices
- Missing or invalid property records
- Geographic dependence between properties
- Differences in model performance across years
- Unverified historical data availability

Property rankings require additional verification before supporting real estate investment decisions.
