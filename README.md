## Overview: What Drives the Price of a Used Car?

This project aims to identify the key factors influencing the price of a used car. The dataset consists of 426,880 records (a subset of 3 million used cars), providing insights that will help a used car dealership understand what consumers value when purchasing a car.

Business Context: Understanding the Dealership's Needs
A car dealership aims to buy vehicles at a lower price and sell them for a profit. Accurate predictions of sale prices are crucial to maximizing profit. Additionally, faster inventory turnover is essential, which depends on the demand for particular cars. This demand is primarily driven by consumer demographics and preferences.

## Methodology: Following the CRISP-DM Framework
This analysis follows the CRISP-DM (Cross-Industry Standard Process for Data Mining) model, beginning with exploratory data analysis (EDA), followed by data cleaning, feature engineering, and model building. The process was iteratively refined, with separate analyses conducted for SUVs, Sedans, and Pickups.

## Data Exploration and Preprocessing: Cleaning the Dataset
The dataset contains 426,880 records with 18 features, but it was not clean. Key issues included missing values and irrelevant advertising content. Notably, the "model" column included non-car-related ads that were removed. Several transformations were also necessary for feature columns.

## Dropped Columns:

VIN and id: Unique identifiers with no predictive value.
region: Redundant with the state column.
model: Contained irrelevant advertising data.
Rows with missing manufacturer, year, or price equal to zero were also removed.
Missing Data Overview:

size: 71.77%
cylinders: 41.62%
condition: 40.79%
VIN: 37.73%
drive: 30.59%
paint_color: 30.50%
type: 21.75%
manufacturer: 4.13%
title_status: 1.93%
model: 1.24%
odometer: 1.03%
fuel: 0.71%
transmission: 0.60%
year: 0.28%
After cleaning and transforming the data, the missing values were reduced to 3.8% for manufacturer and 0.56% for odometer, resulting in a final dataset of 375,619 rows and 14 features.

## Data Distribution and Outliers: Identifying Key Patterns
We explored the distribution of key variables:

Price: Highly right-skewed with extreme outliers.
Year: Left-skewed.
Odometer: Right-skewed.
Outliers in price (values above $150K) and extreme readings in year and odometer were removed based on standard deviation thresholds. The cleaning process improved the dataset and helped identify key patterns for further modeling.

Correlation Analysis: Uncovering Relationships Between Variables
The analysis revealed the following correlations:

Price and Year: 0.57 (moderate positive correlation).
Price and Odometer: -0.53 (moderate negative correlation).
Year and Odometer: -0.67 (strong negative correlation).
These insights suggest that newer cars tend to have lower odometer readings, which in turn influences their price.

Model Building: Preparing Data for Machine Learning
Before building predictive models, the data underwent a transformation pipeline:

OneHotEncoder: For categorical data.
QuantileTransformer: For normalization.
StandardScaler: For scaling features.
This pipeline ensured that the data was ready for regression models. The first regression model used a linear regression approach without categorical features as a baseline.

Baseline Model Performance
The baseline Linear Regression model (without categorical data) returned an RMSE of:

11,590 (training data)
11,574 (test data)
Subsequent models with Lasso, Ridge, and Linear Regression showed improved performance:

Lasso (α = 0.5): RMSE of 8,676 (train) and 8,637 (test).
Ridge (α = 0.5): RMSE of 8,685 (train) and 8,647 (test).
Linear Regression: RMSE of 8,679 (train) and 8,641 (test).
These models significantly outperformed the baseline, suggesting the importance of feature selection.

Feature Selection with Lasso
Using Lasso for automatic feature selection, we identified the most important features:

ferrari, fuel_diesel, title_status_clean, drive_fwd, drive_unknown, type_pickup, cylinders_4, cylinders_8, year, and odometer.
Model Optimization: Grid Search and Cross-Validation
We performed GridSearchCV to fine-tune our models, testing different feature selections. The results confirmed that newer cars, lower odometer readings, and a clean title are key predictors of price. Additionally, 4-cylinder engines and front-wheel-drive (FWD) cars were penalized, suggesting a need for a more nuanced understanding of the market.

Segmenting the Market: Analyzing Car Types
To refine the models further, we separated the data into three car types: SUVs, Sedans, and Pickups. This segmentation allowed us to understand unique buyer preferences within each category.

## SUV Market Insights
For SUVs, the most influential features were:

Year, Odometer, and Cylinders.
Drive (FWD) was less important, and buyers preferred Toyota, Rover, and Tesla models.
Mitsubishi and 4-cylinder SUVs were less desirable.
Model Performance: RMSE ranged from 8,142 to 8,350 for training and test data.

## Sedan Market Insights
For Sedans, key features included:

Year, Odometer, Condition, and Engine Size (Cylinders).
Luxury brands like BMW, Audi, Mercedes-Benz, and Lexus were highly preferred, while 8 cylinders and good condition were significant factors.
Model Performance: RMSE ranged from 5,878 to 5,856 for training and test data.

## Pickup Market Insights
For Pickups, features such as diesel fuel, 4WD drivetrain, and 8 cylinders were highly valued. Additionally:

Nissan had a negative impact on price.
4-cylinder pickups were less desirable, and vehicles in excellent condition sold for higher prices, particularly in California, Arizona, and Oregon.
Model Performance: RMSE was significantly improved after segmentation.

## Deployment and Strategic Recommendations
For optimal pricing and inventory turnover, dealerships should consider the following recommendations based on vehicle type:

SUVs: Focus on newer models, lower odometer readings, and brands like Toyota, Rover, and Tesla. Avoid Mitsubishi and 4-cylinder SUVs.
Sedans: Prioritize good condition for older models, and target premium brands like BMW, Audi, and Mercedes-Benz. Engine size (e.g., 8 cylinders) is also important.
Pickups: Emphasize 4WD, diesel engines, and 8 cylinders. Avoid Nissan and 4-cylinder pickups. California, Arizona, and Oregon show higher demand.
By tailoring inventory and pricing strategies to these insights, the dealership can maximize profitability and meet consumer preferences more effectively.