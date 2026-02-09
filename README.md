# Steel Melt Temperature Prediction (Industrial Optimisation)

## Project Overview

**Client**: a steelworks.

This project focuses on predicting the **final temperature of molten steel** during technological processing using machine learning.  
The model is designed to support **process simulation**, **energy optimisation**, and **data-driven decision-making** in an industrial steel production setting.

This project demonstrates a full **data science workflow**, including exploratory data analysis, preprocessing, feature engineering, model selection, and result interpretation.


## Objective
- **Task type**: Regression  
- **Target variable**: final temperature (`final_temperature`)  
- **Evaluation metric**: MAE
- - **Object of modelling:** ladle (batch, `key`)
Build and evaluate machine learning models to accurately predict the **final temperature of molten steel** based on technological parameters of the process.

**Description of the Technological Process** is provided in the project.

## Data Description
The data come from multiple heterogeneous sources related to the steelmaking process, including:

- `data_arc_new.csv` — electrode data;
- `data_bulk_new.csv` — bulk material feed data (volume);
- `data_bulk_time_new.csv` — bulk material feed data (time);
- `data_gas_new.csv` — gas purging data;
- `data_temp_new.csv` — temperature measurement results;
- `data_wire_new.csv` — wire material data (volume);
- `data_wire_time_new.csv` — wire material data (time).


Each batch (`key`) may contain multiple records corresponding to different stages of processing. The target feature is the final temperature. The initial temperature can also be used as a predictive feature. All intermediate temperature measurements can be removed, as they do not reflect the final process outcome.

## How to Run
The project is implemented as a Jupyter Notebook.
To explore the analysis and results, open and run the notebook in the `notebooks/` directory.

## Methodology

### 1. Exploratory Data Analysis (EDA)

### 2. Data Preprocessing
- Cleaning and aggregation by batch (`key`)
- Removal of non-informative datasets (feeding time tables)
- Target cleaning (removal of crystallisation-stage temperatures)
- Feature scaling and preparation for modelling

### 3. Feature Engineering
- Heating duration
- Apparent power (from active & reactive power)
- Initial temperature extraction
- Aggregated material volumes:
  - `sum_bulks`
  - `sum_wires`

### 4. Correlation Analysis
- Spearman correlation (non-normal distributions)
- Removal of multicollinear and non-informative features


## Models Evaluated
The following models were trained and compared using cross-validation:

- Linear Regression
- Random Forest Regressor
- HistGradientBoosting Regressor
- **CatBoost Regressor**  (best performance)

Hyperparameters were tuned using Randomized search within a pipeline.


## Results
The best-performing model was **CatBoostRegressor**:

- **CV MAE:** ~6.1 °C  
- **Test MAE:** ~6.3 °C  

SHAP analysis confirmed that the model relies on **physically interpretable and meaningful features**, such as:
- Heating duration
- Initial temperature
- Additive volumes
- Apparent heating power
- Gas purging intensity


## Key Insights
- Heating duration is the most influential factor.
- Initial temperature strongly affects the final outcome.
- Some additives have a cooling effect, consistent with domain knowledge.
- The model generalises well for a non-linear industrial process.


## Applications
- Technological process simulation
- Energy consumption optimisation
- Decision support for steelmaking operations
- Integration into automated process control systems


## Tech Stack
- Python
- pandas, NumPy
- scikit-learn
- CatBoost
- SHAP
- Matplotlib / Seaborn

