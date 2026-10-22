# Education Project

Exploring socioeconomic and geographic differences in U.S. high school performance and building regression models to predict school average ACT scores.

---

## Project Overview

This project combines EdGap data with NCES school information and geographic classifications. It examines how school average ACT scores vary with socioeconomic characteristics and school locale, then compares regression models for predicting ACT scores.

The analytical sample contains **7,227 high schools across 20 states**. School locales are grouped into **City, Suburban, Town, and Rural**.

- **Prediction target:** School average ACT score (`average_act`).
- **Socioeconomic predictors:** Unemployment rate, college proportion, married-couple family proportion, median household income, and free or reduced-price lunch eligibility.
- **Geographic predictor:** School locale (`locale_group`).
- **Methods:** Data preparation, exploratory data analysis, linear regression

## Project Structure

```
├── code/
│   ├── data_preparation.ipynb   # Merge, clean, and impute data
│   ├── eda.ipynb                # Explore distributions and relationships
│   └── modeling.ipynb           # Fit, compare, and interpret regression models
├── data/
│   ├── raw/                    # Raw datasets
│   └── processed/
│       └── clean_education.csv # Processed dataset
├── reports/                    # Directory reserved for reports and figures
├── requirements.txt
├── LICENSE
└── README.md
```
---

## Data Sources

- **[EdGap](https://www.edgap.org/):** School test scores and socioeconomic characteristics. The project uses the 2016 dataset.
- **[NCES Common Core of Data](https://nces.ed.gov/ccd/pubschuniv.asp):** School identifiers, state, school level, and other school characteristics.
- **[NCES EDGE School Geocodes](https://nces.ed.gov/programs/edge/geographic/schoollocation):** School geographic information and locale codes.
- **[NCES Locale Definitions](https://nces.ed.gov/surveys/annualreports/topical-studies/locale/definitions):** Definitions used to group locale codes into City, Suburban, Town, and Rural.

Source files are stored in `data/raw/`.

---

## Analysis Workflow

### 1. Data Preparation

Notebook: [data_preparation.ipynb](code/data_preparation.ipynb)

- Select and rename relevant variables.
- Standardize school identifiers and join the three datasets using left joins.
- Map NCES locale codes to four geographic groups.
- Check duplicates, missing values, and valid numerical ranges.
- Retain high schools and remove observations without ACT scores.
- Impute missing numerical socioeconomic predictors using iterative imputation.
- Export [clean_education.csv](data/processed/clean_education.csv).

### 2. Exploratory Data Analysis

Notebook: [eda.ipynb](code/eda.ipynb)

- Describe sample coverage across states and locales.
- Examine ACT and socioeconomic distributions, spread, and potential outliers.
- Explore numerical correlations and pairwise relationships.
- Compare ACT scores and socioeconomic characteristics across locales.

### 3. Regression Modeling

Notebook: [modeling.ipynb](code/modeling.ipynb)

- Fit a lunch-only linear model and compare it with a quadratic specification.
- Fit a full model with five socioeconomic predictors and a reduced model with three.
- Add school locale as a categorical predictor, using City as the reference group.
- Compare nested models using partial F-tests and summarize R², adjusted R², RMSE, and MAE.
- Examine residual plots and standardize the selected predictors to interpret coefficients on a common scale.

---

## Results

- School average ACT scores have a mean of **20.30** and a median of **20.50**. The middle 50% lie between **18.80 and 22.00**.
- Lunch eligibility has the strongest absolute Pearson correlation with ACT among the socioeconomic predictors (**r ≈ −0.78**).
- Suburban schools have the highest mean ACT score (**21.08**); city schools have the lowest (**18.91**) and the greatest variability.
- Socioeconomic characteristics differ across locales. Suburban schools generally have higher household income and college proportions and lower lunch eligibility.

---

### Model Comparison

| Model | R² | Adjusted R² | RMSE | MAE |
|---|---:|---:|---:|---:|
| Lunch only | 0.6139 | 0.6139 | 1.5585 | 1.1690 |
| Lunch quadratic | 0.6158 | 0.6157 | 1.5548 | 1.1651 |
| Socioeconomic full | 0.6280 | 0.6277 | 1.5299 | 1.1453 |
| Socioeconomic reduced | 0.6279 | 0.6278 | 1.5300 | 1.1455 |
| Full + locale | 0.6285 | 0.6281 | 1.5289 | 1.1443 |
| Reduced + locale | 0.6285 | 0.6282 | 1.5289 | 1.1443 |

RMSE and MAE are in ACT points; all values are calculated on the fitting data.

The **reduced socioeconomic model** is selected for simplicity and nearly identical in-sample fit to the full model:

```text
Predicted average ACT = 22.6400
                      − 2.1683 × rate_unemployment
                      + 1.7139 × percent_college
                      − 7.5863 × percent_lunch
```

Adding household income and married-couple family proportion does not significantly improve fit in the nested-model comparison (p ≈ 0.807). Adding locale gives a statistically significant but small improvement: the reduced model's MAE decreases from 1.1455 to 1.1443. Locale is omitted from the selected model to favor simplicity.

Lunch eligibility has the largest absolute coefficient among the standardized predictors in the selected model. Standardization changes coefficient units without changing fitted values or model fit.

The document communicating the results of this project is: `reports/Education_Project_Report.pdf`

---

## Limitations

- Performance on unseen schools has not been evaluated; in-sample metrics should not be interpreted as validated predictive accuracy.
- The sample covers 20 states with unequal geographic representation and is not established as representative of all U.S. high schools.
- Socioeconomic predictors were imputed before modeling. Regression results do not account for imputation uncertainty.
- Large residuals remain for some schools, and relevant predictors may be unmeasured.
- Results describe school-level observational associations, not causal effects or individual student relationships.

---

## Author

- [Krystal Tran](https://github.com/tuyettran15999)

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).

---

## Acknowledgements

- Tools/libraries used: Python, NumPy, pandas, Matplotlib, Seaborn, SciPy, statsmodels, and Jupyter Notebook.
- This project was completed as part of the Foundations of Data Science course at Seattle University.

See `requirements.txt` for the required software and libraries.
