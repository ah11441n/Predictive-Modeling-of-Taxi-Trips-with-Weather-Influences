# Weather and Yellow Taxi Trip Data Analysis

## Overview

This repository contains the analysis and prediction models built using weather data and yellow taxi trip records. The main objective is to understand the impact of weather conditions on taxi trip records and predict future trips based on historical data.

## Datasets

### Weather Dataset

- **Columns:**
  - `index`: The index of the data entry.
  - `Date`: The date of the recorded weather data.
  - `Tavg`: Average Temperature in Celsius.
  - `Tmin`: Minimum Temperature in Celsius.
  - `Tmax`: Maximum Temperature in Celsius.
  - `prcp`: Total Precipitation in millimeters.
  - `snow`: Snow Depth.
  - `wdir`: Wind (From) Direction.
  - `Wspd`: Average Wind Speed in kilometers per hour.
  - `Wpgt`: Wind Peak Gust in kilometers per hour.
  - `pres`: Sea-Level Air Pressure in hectopascals (hPa).
  - `Tsun`: Total Sunshine Duration in Minutes.

- **Basic Information:**
  - The dataset contains 31 rows of weather data.
  - There are 12 columns in the dataset.
  - Columns `Tavg`, `Tmin`, `Tmax` have 3 null values each; `Wspd` and `pres` have 4 null values each.
  - Columns `prcp`, `snow`, `wpgt`, and `tsun` have 31 null values; `wdir` has 30 null values.

- **Handling Null Values:**
  - Filled `Tavg`, `Tmin`, `Tmax` null values with random numbers within their observed ranges.
  - Filled `Wspd` and `pres` null values with random numbers within their observed ranges.
  - Updated `wdir` and `prcp` columns with reference values from the instruction manual.
  - Dropped `wpgt` and `tsun` columns due to complete absence of data.

- **Handling Outliers:**
  - Retained outliers as weather data is inherently unpredictable, and their presence may impact trip data analysis.

### Yellow Taxi Trip Dataset

- **Columns:**
  - `index`, `VendorID`, `passenger_count`, `trip_distance`, `RatecodeID`, `store_and_fwd_flag`, `PULocationID`, `DOLocationID`, `payment_type`, `fare_amount`, `extra`, `mta_tax`, `tip_amount`, `tolls_amount`, `improvement_surcharge`, `total_amount`, `congestion_surcharge`, `DO_year`, `DO_month`, `DO_day`, `DO_hour`, `DO_minute`, `DO_second`, `PU_year`, `PU_month`, `PU_day`, `PU_hour`, `PU_minute`, `PU_second`.

- **Basic Information:**
  - The dataset contains 6,159,935 rows of taxi trip records.
  - Preprocessed by dropping rows with null values and splitting datetime columns into separate components.
  - A sample was taken to manage computational load and ensure representativeness.

## Merging Datasets

- The `day` column from the weather data and the `pickup day` from the yellow taxi trip records were utilized for merging both datasets.
- Weather data's `day` column was forward-filled to apply the same weather information to all subsequent rows until a new day's data appeared.
- Removed duplicate `day` column after merging.

## Regression Models

### MLPRegressor

- Utilizes a Multi-Layer Perceptron (MLP) regressor with hidden layers of sizes 64 and 32 and ReLU activation function.
- Achieved MSE of 0.1802 during training and 0.1734 during validation.

### Linear Regression

- Constructed using the Sequential API with Mean Absolute Error (MAE) as the loss function and Stochastic Gradient Descent (SGD) as the optimizer.
- Achieved a loss of 0.6067 during training and 0.542 during validation.

### Deep Neural Network (DNN)

- Constructed using the Functional API, allowing for more complex architectures.
- Utilizes the Adam optimizer, Mean Squared Error (MSE) as the loss function, and tracks the Mean Absolute Error (MAE) metric.
- Achieved a training loss of 0.0138 and a validation loss of 0.0001.
- Significantly lower losses may indicate overfitting; further evaluation or regularization techniques recommended.

## Conclusion

- The Deep Neural Network (DNN) model, although showing exceptionally low training and validation losses, does not conclusively indicate overfitting.
- Deemed the best regression deep learning model when compared with the other two models.
- Prediction losses on the validation data are recorded as MSE = 0.00011 and MAE = 0.004838, signifying the model's performance in accurately predicting yellow taxi trip records with weather data.


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

