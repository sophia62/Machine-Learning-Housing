# Housing Price Prediction

This project explores housing data to predict home prices. It demonstrates data preprocessing, exploratory analysis, and model experimentation (including feature engineering steps). The goal is to accurately forecast house prices and derive actionable insights about real estate trends.

[In depth paper](https://docs.google.com/document/d/1ClUWeWzALbtbg5AYqc63n704XW-FhzYmfPudI__XT5w/edit?usp=sharing)
---

## Table of Contents
1. [Project Overview](#project-overview)  
2. [Data](#data)  
3. [Methods](#methods)  
4. [Key Insights](#key-insights)  
5. [Limitations & Next Steps](#limitations--next-steps)  
6. [Installation & Requirements](#installation--requirements)  
7. [Usage](#usage)  

---

## Project Overview

- **Objective**: Develop a machine learning model to predict house prices using various features (e.g., square footage, bedrooms, zip code, etc.).
- **Approach**:  
  - Cleaned and preprocessed the dataset (feature extraction from dates, quintile grouping by zip code, etc.).  
  - Explored data to identify trends and insights.  
  - Trained and evaluated multiple models, including Random Forest and XGBoost, ultimately selecting **XGBoost** for the final prediction phase.

---

## Data

- **Source**:  
  The data is sourced from a course dataset (`housing.csv` & `housing_holdout_test.csv`), provided via GitHub links:
  - [Raw Data](https://raw.githubusercontent.com/byui-cse/cse450-course/master/data/housing.csv)
  - [Holdout Data](https://raw.githubusercontent.com/byui-cse/cse450-course/master/data/housing_holdout_test.csv)

- **Key Variables**:  
  - **date**: Original sale date (transformed into `year`, `month`, `day`).  
  - **sqft_living**, **sqft_lot**: Square footage of the living area and lot area.  
  - **price**: The price of the house (target variable).  
  - **grade**, **condition**, **view**, **waterfront**, etc.: Property attributes.  
  - **zipcode**: Location (transformed into a **price quintile** category).  
  - **id**: Unique house identifier (used to track resold properties).

---

## Methods

1. **Split Date**  
   - Extracted `year`, `month`, `day` from the `date` column (removing time components).

2. **Resold Boolean**  
   - Calculated whether a house was sold more than once (`resold = True` if `id` appears more than once in the data).

3. **Price Quintile by Zipcode**  
   - Calculated average prices by zip code and assigned each zip code to a **price quintile** (from 1 to 5).

4. **Modeling Steps**  
   - **Feature Engineering**: Incorporated the new columns (`year`, `month`, `day`, `resold`, `quintile`).  
   - **Model Selection**: Compared RMSE / R² scores of Random Forest vs. XGBoost.  
   - **Hyperparameter Tuning**: Used grid search-like approach to refine parameters (`max_depth`, `max_leaves`, `learning_rate`, etc.).  

5. **Planned Enhancements (To-Add)**  
   - **Normalization**: Implement data normalization (e.g., MinMax or StandardScaler) and save the scaling stats for holdout predictions.  
   - Further advanced feature engineering to capture seasonality, renovations, etc.

---

## Key Insights

1. **Price Range & Distribution**  
   - Prices range from **\$75,000** to **\$7.7 million**—a **2-order of magnitude** difference.  
   - ~90% of houses sell between **\$75,000** and **\$1 million**.

2. **Grade vs. Price**  
   - Strong, almost **exponential relationship** between `grade` and `price`. Higher grade ⇒ significantly higher average price.

3. **View Score**  
   - ~90% of homes have a **view score = 0**, indicating limited direct water/city views. Homes with a better view command higher average prices.

4. **Seasonality**  
   - **Best to sell in late spring** (higher average prices).  
   - **Worst to sell in winter** (lower overall prices).

5. **Square Footage**  
   - As **sqft_living** increases, the **% of homes sold above the average price** also increases. Larger homes tend to be above average price.

6. **Resold Properties**  
   - Houses that are **resold** typically have **lower prices** on average compared to those sold once.

7. **Geographical Concentration**  
   - Higher-value neighborhoods/zip codes appear **centralized** in certain latitude/longitude clusters near metropolitan or waterfront areas.

---

## Limitations & Next Steps

- **Data Normalization**: Current model does not normalize or standardize continuous variables.  
- **Additional Data Sources**: Incorporating external features (e.g., local economic indicators, interest rates, or local amenities) may improve model accuracy.  
- **Non-Linear & Complex Models**: While XGBoost is effective, exploring deep learning or advanced ensemble methods might capture more nuanced patterns.  
- **Seasonality & Time Effects**: Deeper investigation of time-series components (month-year seasonality) could refine predictions.

---

## Installation & Requirements

Make sure you have Python 3.7+ and the following libraries installed:

```bash
!pip install scikit-learn==1.5.2
!pip install xgboost
!pip install pandas
!pip install tqdm
!pip install lets-plot
