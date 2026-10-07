# Education Project

> This project addresses inequality of educational opportunity in U.S. high schools. We will see whether school performance is associated with socioeconomic factors and school locale.

---

## Project Overview

This project investigates factors associated with academic performance among U.S. high schools, using average ACT scores as a measure of school performance. The analysis examines socioeconomic characteristics such as unemployment rate, educational attainment, family structure, median household income, and eligibility for free or reduced-price lunch.

In addition, the project explores whether average ACT performance differs across school locales (City, Suburban, Town, and Rural) after accounting for socioeconomic characteristics.

- **Objective:** Determine whether school performance is associated with socioeconomic factors and school locale.
- **Domain:** Education Analytics
- **Key Techniques:** Data collection, Data processing, Exploratory data analysis, Statistical hypothesis testing

---

## Project Structure

```
├── data/                 # Raw and processed data
├── code/                 # Jupyter notebooks and Python scripts
├── reports/              # Generated reports and visualizations
├── requirements.txt      # Dependencies
└── README.md             # Project documentation
```

---

## Data
### EdGap data:
- **Source:** https://www.edgap.org/#5/37.875/-95.999 
- **Description:** This data set from 2016 includes information about average ACT or SAT scores for schools and several socioeconomic characteristics of the school district.
### School information data:
- **Source:** https://nces.ed.gov/ccd/pubschuniv.asp
- **Description:** This data set consists of basic identifying information about schools. 
### School geogrạphy data:
- **Source:** https://nces.ed.gov/programs/edge/geographic/schoollocation
- **Description:** This dataset from NCES EDGE provides geographic information for U.S. public schools. The `LOCALE` variable is used to classify schools by geographic setting, including City, Suburban, Town, and Rural areas.
- **Locale definitions:** https://nces.ed.gov/surveys/annualreports/topical-studies/locale/definitions

The raw datasets used in the project are located in the `data/raw/` folder.

---

## Data Preparation

- Selecting variables relevant to the research questions.
- Renaming columns to improve readability and consistency.
- Standardizing the school ID data types across the datasets to ensure accurate matching.
- Grouping the NCES locale codes into four geographic categories: City, Suburban, Town, and Rural.
- Joining the EdGap, school information, and school geography datasets using left joins to retain all observations from the EdGap dataset.
- Checking data quality, including missing values and the validity of school and socioeconomic variables.
- Restricting the analysis to high schools.
- Handling missing values and preparing the variables for analysis.

The Jupyter notebook used to clean and prepare the data is: `code/Education.ipynb`
The cleaned data file is: `data/processed/clean_education.csv`

---
## Analysis

The data analysis used the data science methodology. Here are main steps included:

- 

The Jupyter notebook used to clean and analyze the data is: `code/Education.ipynb`
The cleaned data file is: `data/processed/clean_education.csv`

---

## Results

The results show that

The document communicating the results of this project is: `reports/`

---

## Authors

- [Krystal Tran](https://github.com/tuyettran15999)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Tools/libraries used: Python, NumPy, pandas, Matplotlib, Seaborn, SciPy, statsmodels, and Jupyter Notebook.
- This project was completed as part of the Foundations of Data Science course at Seattle University.

See `requirements.txt` for the required software and libraries.
