# House Price Predictor – Fundamentals of AI & ML BYOP Project

## Overview

This project implements a house price prediction system as part of the **Fundamentals of AI & ML – Bring Your Own Project (BYOP)** course requirement. It uses a **Random Forest regression model** to estimate the median house value based on characteristics of a local area and its housing, using the built‑in **California Housing dataset** from scikit‑learn.[web:9]  

The Python script:

- Loads and prepares the California Housing dataset.
- Trains a Random Forest regression model on selected features.
- Evaluates the model using R‑squared and RMSE.
- Interactively asks the user for property and area details and returns an estimated house price.

---

## Dataset

The project uses the **California Housing dataset** provided by `sklearn.datasets.fetch_california_housing`, which is a real‑world regression dataset derived from the 1990 U.S. Census.[web:9]  

Key properties:

- Number of samples: 20,640.[web:62]  
- Number of original numeric features: 8.[web:9]  
- Target variable: **Median house value**, measured in units of 100,000 USD (for example, 2.0 corresponds to 200,000 USD).[web:9][web:68]  

In the script, the raw data is loaded into a pandas DataFrame and an additional `Price` column is created for the target.

---

## Features Used

To keep user input simple and intuitive, the model uses a subset of six features from the original dataset.

1. **MedInc – Median Income**  
   Median income of households in the area, measured in tens of thousands of US dollars.  
   Example: `5.5` represents an income of approximately 55,000 USD.[web:68]  

2. **HouseAge – Median House Age**  
   Median age of houses in the area, in years (how old the typical house is).[web:68]  

3. **AveRooms – Average Rooms per Household**  
   Average number of rooms per household in the area (total rooms divided by number of households).[web:68]  

4. **AveBedrms – Average Bedrooms per Household**  
   Average number of bedrooms per household in the area (total bedrooms divided by number of households).[web:68]  

5. **Population**  
   Total number of people living in the local area (block group).[web:68]  

6. **AveOccup – Average Household Occupancy**  
   Average number of people living in each household (population divided by number of households).[web:68]  

These six features are selected into `feature_columns` in the script and used as input to the Random Forest model.

---

## Model and Methodology

- **Model type:** `RandomForestRegressor` from scikit‑learn.  
- **Number of trees:** 100 decision trees (`n_estimators = 100`).  
- **Train–test split:** 80% training, 20% testing, with `random_state = 42` for reproducibility.  

Workflow:

1. Load the California Housing dataset with `fetch_california_housing()`.
2. Construct a DataFrame and select the six chosen features as input (`X`) and the `Price` column as the target (`y`).
3. Split the data into training and testing sets using `train_test_split`.
4. Train the Random Forest regressor on the training data.
5. Predict on the test data and compute:
   - **R‑squared (coefficient of determination)** using `r2_score`.
   - **RMSE (Root Mean Squared Error)** using `mean_squared_error` and the square root.

The script prints:

- The model’s R‑squared score as a percentage.
- RMSE converted back into US dollars by multiplying by 100,000 (because the target is stored in 100,000 USD units).[web:9]  

---

## Interactive Prediction

After training and evaluation, the script provides an **interactive prediction mode** in the terminal or console.

The user is prompted to enter:

1. Median household income in the area (tens of thousands of USD).  
2. Typical age of houses in the area (years).  
3. Average number of rooms per house.  
4. Average number of bedrooms per house.  
5. Total population in the local area.  
6. Average number of people per household.  

These values are assembled into a single‑row pandas DataFrame with the same feature names the model was trained on, and passed to the trained `RandomForestRegressor` for prediction.

The model output is:

- Predicted median house value in dataset units (100,000 USD).
- Predicted value converted to standard US dollars and displayed in a formatted message.

If any of the inputs are not valid numbers, the script catches a `ValueError` and prints a clear input error message.

---

## How to Run

### Requirements

- Python 3.x  
- `pandas`  
- `numpy`  
- `scikit‑learn`  

Install the required packages with:

```bash
pip install pandas numpy scikit-learn
```

### Running as a Python Script (Locally or in VS Code)

1. Save the script file (for example, as `house_price_predicter-fundamentals_of_ai_-_ml_project.py`).  
2. Save this README as `README.md` in the same folder.  
3. Open a terminal in that folder.  
4. Run:

```bash
python house_price_predicter-fundamentals_of_ai_-_ml_project.py
```

5. Wait for the dataset to load and the model to train.  
6. When prompted, enter the requested values one by one to receive the predicted property value.

### Running in Google Colab

1. Open a new notebook in Google Colab.  
2. Copy and paste the entire Python script into a single code cell.  
3. (Optional) At the top of the cell, add:

```python
!pip install pandas numpy scikit-learn
```

4. Run the cell.  
5. Provide the requested inputs in the Colab output cell when prompted.

---

## File Structure

A minimal project structure for submission can be:

```text
.
├─ house_price_predicter-fundamentals_of_ai_-_ml_project.py
└─ README.md
```

The Python file contains the full training and prediction logic, and this README explains the purpose, usage, and methodology.

---

## Limitations and Possible Improvements

- The model is trained on **California** housing data from 1990, so the predictions do not directly reflect current prices or other regions (for example, Indian cities such as Bhopal).[web:9][web:68]  
- Only six features are used to keep input simple; including additional features (such as latitude and longitude) could improve accuracy but would make user interaction more complex.  

Potential future enhancements:

- Add exploratory data analysis (EDA), such as distributions and correlations between features and price.
- Compare Random Forest with other regression models (for example, Linear Regression or Gradient Boosting) and report performance differences.
- Build a simple graphical user interface (GUI) or web interface for easier interaction (for example, using Streamlit or a lightweight web framework).

