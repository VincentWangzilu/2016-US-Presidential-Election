# Assessing the Impact of Socio-Economic Factors on the 2016 U.S. Presidential Election

## Project Overview
This project explores how various **socio-economic** and **demographic factors** may have influenced the 2016 U.S. Presidential election results at both the **county** and **state** levels. It uses official election data, coupled with U.S. Census Bureau information on income, education, racial composition, housing, and more. By merging these datasets, we investigate:

1. Which socio-economic variables are most strongly associated with an increased or decreased preference for a particular political party.
2. Whether these patterns differ between county-level and state-level aggregations.
3. How well such demographic and economic measures can **predict** the final county vote share (or the winning party at the state level).

This repository contains:
- **Final report** (`2016-US-Presidential-Election.pdf`)
- **Data files** (`PresElect2016R copy.csv`, `UScounty-facts.csv`, `UScounty-dictionary.csv`)  
- **R scripts** (`EDA and Visualisation.qmd`, `Statistical tests and Correlation.qmd`, `model-building-state.qmd`, `Model-Building-county.qmd`) for data processing, statistical analysis, visualization, and modeling.
- **EDA and visualization results** (`EDA and Visualisation.html`)

## Data Sources & Descriptions
1. **PresElect2016R.csv**  
   - **state**: Full name of the U.S. state  
   - **state.po**: Two-letter state abbreviation  
   - **county**: County name  
   - **FIPS**: Unique county identifier from the U.S. Census  
   - **candidatevotesR**: Number of votes for the Republican presidential candidate  
   - **totalvotes**: Total votes cast in the county  
   - **fracvotesR**: Fraction of total votes cast for the Republican candidate  
   - **partywonR**: Binary flag (1 if the Republican candidate won that county, 0 otherwise)

2. **UScounty-facts copy.csv**  
   - Contains demographic and socio-economic data (population size, race, age, housing, income, employment, etc.) for each county.
   - The columns correspond to numerous Census metrics, e.g., percentage of population over 65, percent of households in poverty, median household income, and so forth.

3. **UScounty-dictionary.csv**  
   - Explains each column in `UScounty-facts copy.csv` in detail.
   - Lists variable names (like `AGE775214`, `POP060210`, `INC110213`) with their descriptions (e.g., “65 years and over,” “Population per square mile,” “Median household income,” etc.).

## Main Research Questions
1. **Influential Factors**  
   - Which socio-economic or demographic factors (e.g., race, income, educational attainment) correlate most strongly with the fraction of votes received by a major party?
2. **County vs. State Differences**  
   - How do these relationships differ when data are aggregated at the state level vs. the more granular county level?
3. **Predictive Modeling**  
   - Can these socio-economic indicators be used to predict the final election outcome at the state level (i.e., which party carried the state)?  
   - How accurately do the models forecast vote share by county?

## Methodology
1. **Data Preprocessing**  
   - Merge election data (2016 results) with the Census data, keyed on FIPS (for counties) or state name.
   - Handle missing data or special cases (e.g., Alaska’s reporting).
   - Scale numeric columns for correlation analysis and model convergence.

2. **Exploratory & Statistical Analysis**  
   - Conduct **descriptive statistics** on demographic variables.  
   - Use tests such as **Welch’s t-test** or **Mann-Whitney U** to check differences in socio-economic measures between Republican-leaning and Democratic-leaning areas.  
   - Report **effect sizes** (Cliff’s Delta, Cohen’s d) and correct for multiple comparisons (e.g., Benjamini-Hochberg).

3. **Correlation Analysis**  
   - Employ **Kendall’s Tau** to handle skewed data when exploring associations between fraction of Republican votes and socio-economic indicators.

4. **Predictive Modeling**  
   - **State-Level**:  
     - Logistic regression (binary outcome: Republican vs. Democratic winner).  
     - Random forest classification for identifying top features (importance ranking).  
   - **County-Level**:  
     - Beta regression or fractional logistic to predict `fracvotesR`.  
     - Random forest regression for partial dependence plots and advanced feature importance.  
   - **Principal Component Analysis (PCA)** or stepwise selection to reduce dimensionality or tackle multicollinearity.

5. **Model Evaluation**  
   - **Classification Metrics**: Accuracy, AUC, Precision, Recall, and F1 Score.  
   - **Regression Metrics**: MSE, RMSE, R-squared.
