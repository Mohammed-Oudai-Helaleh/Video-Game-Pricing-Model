# Video-Game-Pricing-Model
This project uses machine learning regression techniques to predict video game prices based on various features. The model is built using datasets from multiple sources and leverages a variety of Python libraries for data preprocessing, visualization, and modeling.

# __Datasets__
The following datasets were used in this project:
1. [games.csv](https://cdn-lfs.hf.co/repos/ea/91/ea91ddc132bbc09ba285428fb62ad8a1445f095f374365f846d0916e373ea7c6/c755572b804a5c43f4f005aacef23cadfe92ae77d03daebf908d521c81285821?response-content-disposition=attachment%3B+filename*%3DUTF-8%27%27games.csv%3B+filename%3D%22games.csv%22%3B&response-content-type=text%2Fcsv&Expires=1735972680&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTczNTk3MjY4MH19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy5oZi5jby9yZXBvcy9lYS85MS9lYTkxZGRjMTMyYmJjMDliYTI4NTQyOGZiNjJhZDhhMTQ0NWYwOTVmMzc0MzY1Zjg0NmQwOTE2ZTM3M2VhN2M2L2M3NTU1NzJiODA0YTVjNDNmNGYwMDVhYWNlZjIzY2FkZmU5MmFlNzdkMDNkYWViZjkwOGQ1MjFjODEyODU4MjE%7EcmVzcG9uc2UtY29udGVudC1kaXNwb3NpdGlvbj0qJnJlc3BvbnNlLWNvbnRlbnQtdHlwZT0qIn1dfQ__&Signature=sA38oeL7QgSgr11FrQMgjop4jqkYudUyPSNHDm4RanwRieAzXW4wr5pBkZ5Pn2XD1JhiBOgVu6UtQCE860kwAG6qXcSGinBL4u5TRsFWnJigNK4BL0JZ3VTvUgAmejsB5O06-kF9VRhYhc%7EYZNyOIMGI7GdNgMroNRDJUk9a%7E2iEp5hIh%7EYmwxyh82QELTT%7EWI3uOiBbyg-1P4uQ9xG6P3s-b6PoBNEe3lXgEsBuSjTHZ25pUaslfQH7Y4ZxofZnxZ6ht9HED-Ymh4%7EcdARQK0RUdE733LPNuDTaR6InsLZ6rLC9N5Nky7RCiG61q3hbU%7Ea45q3jrwHnCXPJIPHngg__&Key-Pair-Id=K3RPWS32NSSJCE)
2. [Top 1000 Steam Games 2023 COPY export 2025-01-06 23-42-05.csv: https://gigasheet-export-uploads.s3.amazonaws.com/97111ccf_6424_4cbb_b959_4526a4d3edf9-20250106234210.zip](https://gigasheet-export-uploads.s3.amazonaws.com/97111ccf_6424_4cbb_b959_4526a4d3edf9-20250106234210.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAXTOLCDI7G5IZZAUQ%2F20250106%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250106T234221Z&X-Amz-Expires=1800&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3D%22Top%201000%20Steam%20Games%202023%20COPY%20export%202025-01-06%2023-42-05.zip%22&X-Amz-Signature=19a9ec6605bcca9862ad64f12451f6ad71f281fc0c57adf300e75415a6784694)

# __Libraries Used__
The following Python libraries were used in this project:

 - Data Manipulation & Analysis:

   pandas

   numpy

 - Visualization:

   matplotlib.pyplot

   seaborn

 - Machine Learning:

   sklearn (including preprocessing, metrics, model_selection, ensemble, feature_selection, linear_model)

   catboost

   lightgbm

   optuna (for hyperparameter optimization)

 - Utilities:

   collections.Counter

   ast

   scipy.stats (for boxcox transformation)

   scipy.optimize (for minimize)

   joblib (for saving models)

# __Steps__
1. Data Preprocessing
 - Merged the two datasets and retained only meaningful data.

 - Visualized the data to identify patterns and outliers.

 - Noted extreme skewness in some features and applied transformations to address it.

2. Feature Engineering
 - Removed tags with low votes and ensured they did not overlap with genres.

 - Applied one-hot encoding to tags and genres columns.

 - Removed columns with values below a threshold and aggregated them into an "other" category.

 - Transformed supported_languages and full_audio_languages into their respective counts.

 - Converted windows, mac, and linux columns to binary values (dropped windows as it was always True).

 - Created new columns for review categories (positive and negative reviews) and total review counts.

 - Calculated the average of the owners column.

 - Applied logarithmic transformations to achievements, CCU, and owners columns to reduce skewness.

 - Applied a Box-Cox transformation to the price column (target variable) to handle skewness.

3. Modeling
 - Defined a function to evaluate all models.

 - Split the data into features and target variables.

 - Clipped extreme values in the target variable to handle outliers.

 - Scaled features using RobustScaler to mitigate the impact of outliers.

 - Split the data into training and testing sets.

 - Trained and evaluated the following models:

  - CatBoost

  - RandomForestRegressor

  - ExtraTreesRegressor

  - LightGBM

  - VotingRegressor (ensemble of the above models)

  - GradientBoostingRegressor (ensemble of the above models)

  - Used optuna for hyperparameter optimization.

  - Selected the GradientBoostingRegressor as the final model due to its superior accuracy and minimal error margin.

  - Saved the trained models using joblib.

4. Testing
 - Tested the final model on new data to evaluate its performance.

# __Results__
The GradientBoostingRegressor achieved the best performance with the following metrics:

 - Mean Absolute Error (MAE): [1.0874]

 - Mean Squared Error (MSE): [2.5768]

 - R² Score: [0.7282]

 - Explained Variance Score: [0.7353]
