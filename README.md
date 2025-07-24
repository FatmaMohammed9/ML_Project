# ML_Project
# Property Data Cleaning and Predictive Modeling Project

## Objectives
- Combine property data from multiple sources (ATTOM and Datafiniti).
- Clean and integrate the datasets to ensure consistency in column naming and data types.
- Develop predictive models to estimate property prices based on cleaned data.
- (Challenge) Design and implement a RESTful API to expose data cleaning functionality.

## APIs Used for Data Collection
- **ATTOM Property API**: Provided detailed property and sale data.
- **Datafiniti API**: Supplemented with additional property listings and attributes.

## Data Collection and Cleaning Steps
1. Retrieved raw data from both ATTOM and Datafiniti sources.
2. Inspected and renamed columns to unify schema between datasets.
3. Converted data types for numeric columns (`price`, `size_sqft`, `num_rooms`, `year_built`).
4. Handled missing data by imputing medians or dropping rows with critical missing values.
5. Dropped duplicate or redundant columns.
6. Combined both cleaned datasets into a single DataFrame for modeling.

## Running and Interacting with the Cleaning API
*(Implemented as a challenge)*  
- Built using FastAPI framework.
- `/clean` endpoint accepts raw JSON data and returns cleaned JSON data.
- `/clean_csv` endpoint accepts raw JSON data and returns cleaned data as downloadable CSV.
- To run locally, install dependencies and run:
  ```bash
  uvicorn main:app --reload

# Property Price Prediction

## Overview
This project aims to predict real estate property prices using structured features such as size (in sqft), number of rooms, year built, and location (city, state, postal code). The dataset is a cleaned combination of property listings from different sources.

## Modeling Approach

### Data Preparation:
- Dropped rows with missing target variable (`price`).
- Split data into features (`X`) and target (`y`).
- Applied preprocessing:
  - **Numerical Columns:** Imputed missing values using median strategy.
  - **Categorical Columns:** Imputed with the most frequent value, followed by One-Hot Encoding.
- Used `train_test_split` to divide the data (80% training, 20% testing).

### Models Evaluated:
All models were embedded in a pipeline that included preprocessing and model fitting. The models tested were:
- Linear Regression
- Lasso Regression (L1 regularized)
- Decision Tree Regressor
- Random Forest Regressor

### Evaluation Metrics:
- **RMSE (Root Mean Squared Error):** Measures average prediction error.
- **R² Score:** Indicates how well the model explains the variance in the data (1.0 = perfect, 0 = no predictive power).

## Results Summary

| Model              | RMSE          | R² Score  |
|--------------------|---------------|-----------|
| Random Forest      | 7,339,773     | -0.133    |
| Linear Regression  | 7,456,869     | -0.169    |
| Lasso Regression   | 7,467,134     | -0.172    |
| Decision Tree      | 7,525,433     | -0.191    |

> **Note:** All models performed poorly, with negative R² scores, indicating that none of them were able to capture the variance in property prices effectively. A negative R² means the model performs worse than simply predicting the mean of the target.

## Observations
- **Random Forest** had the lowest RMSE and highest (least negative) R², making it the best among the tested models — but still far from acceptable performance.
- **Lasso and Linear Regression** performed similarly, suggesting limited linear relationships in the data.
- **Decision Tree** showed signs of overfitting and did not generalize well.

## Next Steps
- **Feature Engineering:** Include more relevant features (e.g., property type, neighborhood score, amenities).
- **Outlier Handling:** Investigate and remove extreme property prices that may skew results.
- **Log Transformation:** Apply log transformation to the `price` column to normalize skewed data.
- **Model Tuning:** Perform hyperparameter tuning using cross-validation.
- **Advanced Models:** Explore ensemble models like XGBoost or LightGBM for better predictive power.

---

*Project by: [Fatma Aal Abdulsalam]*
