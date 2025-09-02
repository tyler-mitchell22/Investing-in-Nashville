# Real Estate Investment Analysis

## Project Overview

This project develops machine learning models to assist real estate investment firms in identifying properties with strong value opportunities in the Nashville area. The analysis focuses on predicting whether a property sells above or below its assessed market value using property characteristics, geographic variables, and timing data.

## Objective

Classify real estate transactions as either "Over" or "Under" the property's assessed market value to help investors identify undervalued properties with strong investment potential.

## Dataset Description

The dataset contains Nashville area real estate transactions with features including:
- **Structural Features:** Year built, bedrooms, bathrooms, finished area, acreage, grade, foundation type, exterior walls
- **Location Features:** City, neighborhood, tax district
- **Market Features:** Land value, building value, sale date
- **Target Variable:** Sale Price Compared to Value (Over/Under)

## Data Preprocessing

### Data Cleaning Steps:
1. **Removed non-predictive columns:** Parcel ID, Suite/Condo #, full address, legal references
2. **Handled missing values:** Eliminated rows missing critical structural information (bedrooms, bathrooms, finished area, foundation type)
3. **Feature engineering:** Combined full and half bathrooms into `total_bathrooms` to reduce collinearity
4. **Categorical encoding:** Applied label encoding to categorical variables (Grade, Foundation Type, Exterior Wall, City, Neighborhood)
5. **Target encoding:** Converted target variable to numeric labels (Over/Under)

## Models Implemented

### Model 1: Decision Tree (Structural Features Only)
- **Features:** Year built, bedrooms, total bathrooms, finished area, acreage, grade, foundation type, exterior walls
- **Performance:** 64% accuracy
  - Over class: F1-score = 0.76
  - Under class: Precision/Recall = 0.26
- **Key Insights:** Finished area, acreage, and year built were most important predictors
- **Use Case:** Baseline reference tool for investment decisions

### Model 2: Random Forest (All Features)
- **Features:** Complete feature set including structural, categorical, and location variables
- **Performance:** 73% accuracy
  - Over class: F1-score = 0.83
  - Under class: F1-score = 0.23 (Recall = 0.16)
- **Key Insights:** Building value, finished area, acreage, and land value were most important
- **Limitation:** Poor performance on identifying under-valued properties

### Model 3: XGBoost Gradient Boosting (Curated Features)
- **Features:** Curated selection including structural, location, and market-timing features
- **Performance:** 79% accuracy (Best performing model)
  - Over class: Precision = 0.81, Recall = 0.93, F1-score = 0.87
  - Under class: Precision = 0.62, Recall = 0.33, F1-score = 0.43
  - Weighted average F1-score = 0.76
- **Key Insights:** Sale Year, Year Built, Neighborhood, and City were top predictors

## Model Performance Comparison

| Model | Algorithm | Accuracy | Precision | Recall | F1-Score |
|-------|-----------|----------|-----------|---------|----------|
| Model 1 | Decision Tree | 63.7% | 0.635 | 0.637 | 0.636 |
| Model 2 | Random Forest | 72.8% | 0.670 | 0.728 | 0.684 |
| Model 3 | XGBoost | **79.4%** | **0.748** | **0.794** | **0.761** |

## Key Findings

### Important Features Across Models:
1. **Structural factors:** Finished area, year built, acreage consistently important
2. **Valuation factors:** Building value and land value crucial for prediction
3. **Temporal factors:** Sale year emerged as top predictor in XGBoost model
4. **Location factors:** Neighborhood and city showed significant predictive power

### Model Limitations:
- All models struggled with class imbalance (poor recall for "Under" category)
- 79% accuracy may not meet institutional standards for high-value investment decisions
- Models show bias toward predicting "Over" valued properties

## Recommendations

**Preferred Model:** XGBoost (Model 3) based on:
- Highest overall accuracy (79%)
- Best weighted F1-score (0.76)
- Balanced complexity vs. interpretability
- Superior feature importance extraction capabilities

**Implementation Considerations:**
- **Current readiness:** Suitable as screening tool or decision support aid
- **Not recommended for:** Ful
