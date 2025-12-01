# Predictive Delivery Management Engine

## Team Members
* **Kashinath Alias Kapil Subhash Naik** - [kashinathn@iisc.ac.in](mailto:kashinathn@iisc.ac.in)
* **Atreyee Mondal** - [atreyeem@iisc.ac.in](mailto:atreyeem@iisc.ac.in)
* **Sujith Shetty** - [sujith1@iisc.ac.in](mailto:sujith1@iisc.ac.in)
* **Pranav N** - [pranavn@iisc.ac.in](mailto:pranavn@iisc.ac.in)

## Problem Statement
The core challenge addressed by this project is the inaccuracy of Estimated Time of Arrivals (ETAs) on food delivery platforms. This inaccuracy arises from variability in driver performance, leading to reduced customer satisfaction and inefficient resource utilization. The project aims to solve this by leveraging machine learning on historical data to predict delivery duration with high accuracy and profile driver performance for data-driven operational decisions.

## Dataset Description
* **Dataset Name:** Food Delivery Time Prediction
* **Source:** Structured file (Excel Spreadsheet)
* **Volume:** 45,593 records
* **Dimensions:** 11 columns
* **Preprocessing:** The dataset underwent comprehensive cleaning, including checking for missing values (none found), calculating Geodesic distances using coordinates, clipping outliers (99th percentile), and standardizing features for neural network efficiency.

## High-Level Approach and Methods
The project utilized a multi-stage machine learning pipeline progressing from baseline statistical methods to advanced ensemble techniques.

### Feature Engineering
* **Geospatial Analysis:** Converted raw latitude/longitude into `distance_geodesic_km` using the Geopy library to account for Earth's curvature.
* **City Tier Segmentation:** Extracted city codes (e.g., 'BANG', 'MUM') from driver IDs to categorize cities into tiers (1, 2, 3) as a proxy for traffic density.
* **Interaction Features:** Created complex features like `vehicle_distance_interaction` and `traffic_adjusted_interaction` to capture non-linear dependencies.

### Modeling Strategy
* **Baselines:** Linear Regression and Random Forest Regressor.
* **Advanced Models:** XGBoost (Extreme Gradient Boosting), Multi-Layer Perceptron (MLP), and Deep ANN (Keras/TensorFlow).
* **Ensemble Techniques:** Implemented a **Stacking Regressor** (combining XGBoost and Random Forest with a Linear Regression meta-learner) and a Voting Regressor.

# Summary of Results
The project successfully replaced static averages with dynamic ML-driven predictions.

## Model Performance

The Stacking Regressor (combining XGBoost, Random Forest, and Linear Regression) proved to be the most robust model for this dataset.

* **Accuracy (R² Score)**: The model explains approximately **42%** of the variance in delivery times on unseen data. While this leaves room for improvement (likely due to unobserved factors like live traffic or weather), it is a significant improvement over baseline approaches.
* **Error Metrics**:
  - **RMSE (Root Mean Squared Error)**: The model's predictions are, on average, within ± **7.12 minutes** of the actual delivery time.
  - **MAE (Mean Absolute Error)**: The absolute error is lower, at approximately **5.60 minutes**, indicating that the model is generally accurate but penalized by a few extreme outliers.

## Key Drivers of Delivery Time

Feature importance analysis from the tree-based models revealed critical operational insights:

* **Delivery_person_Ratings (23.8%)**: This was the single most important predictor after distance. Higher-rated drivers consistently deliver faster, validating the correlation between efficiency and customer satisfaction.
* **Delivery_person_Age (15.4%)**: Age plays a significant role, with specific age groups tending to have different delivery time patterns, likely due to experience, risk tolerance, or physical agility.
* **Distance Features (20.6% combined)**: Geodesic distance and its transformations remain primary constraints, with non-linear relationships captured through log and squared transformations.

## Operational Use Case of Driver Efficiency Score: 
* Driver Efficiency Score allows fleet managers to objectively identify underperforming drivers for targeted training (route optimization coaching) and reward high-performing drivers, moving beyond simple "average speed" metrics which fail to account for difficult routes.

## Limitations

The R² score of 0.42 indicates that **58% of the variance** in delivery time remains unexplained, mainly due to missing real-world factors:

* **Coordinate Accuracy**: Distance outlier handling was required, indicating GPS/coordinate accuracy issues
* **Missing Environmental Data**: No weather conditions, live traffic, detailed time-of-day effects
* **Limited Contextual Signals**: No rush hour patterns, local events, or road closure information
* **Data Quality Issues**: Potential driver reporting inconsistencies affecting ground truth

## Highlights

* **Geodesic Distance**: Real-world route accuracy over Euclidean approximation
* **Driver Efficiency System**: Novel performance scoring beyond simple prediction
* **Data Leakage Prevention**: Corrected critical training contamination issue
* **Business-First Features**: Every engineered feature has clear operational meaning

## Future Scope

Clear opportunities for enhancement:

* **Real-time Data Integration**: Live traffic and weather APIs can directly address the 25-58% unexplained variance
* **Automated Geofencing**: Replace manual driver updates with GPS timestamps for accurate ground truth
* **Real-time Dashboard**: Scale driver efficiency monitoring with distributed computing architecture
* **Dynamic Optimization**: Use efficiency scores for route optimization and resource allocation

## Requirements
- Requires Python 3.12.3 or higher
- List of requirements can be found (requirements.txt)   

## Setup and Installation
1. Clone this repository 
2. Install required packages: `pip install -r requirements.txt`
3. Run Jupyter notebooks in the `Code/` directory

## License
MIT License