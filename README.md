# ❤️ Heart Disease Prediction App

A Streamlit web app that predicts the risk of heart disease from clinical
inputs, using a K-Nearest Neighbors (KNN) model trained on the Heart Failure
Prediction dataset.

> ⚠️ **Disclaimer:** This project is for educational purposes only. It is not a
> medical device and must not be used for diagnosis or treatment decisions.
> Always consult a qualified healthcare professional.

## Demo

<!-- Add a screenshot: save it as screenshot.png in the repo, then uncomment -->
<!-- ![App Screenshot](screenshot.png) -->

Live app: _add your Streamlit Cloud link here_

## Features

- Interactive form for 11 clinical features
- Same preprocessing as training (one-hot encoding, column alignment, scaling)
- Instant High Risk / Low Risk result
- Lightweight, runs locally or on Streamlit Community Cloud

## Input Features

| Feature | Description |
|---|---|
| Age | Age in years |
| Sex | M / F |
| ChestPainType | ATA, NAP, TA, ASY |
| RestingBP | Resting blood pressure (mm Hg) |
| Cholesterol | Serum cholesterol (mg/dL) |
| FastingBS | Fasting blood sugar > 120 mg/dL (1 = yes, 0 = no) |
| RestingECG | Normal, ST, LVH |
| MaxHR | Maximum heart rate achieved |
| ExerciseAngina | Exercise-induced angina (Y / N) |
| Oldpeak | ST depression induced by exercise |
| ST_Slope | Up, Flat, Down |

## How It Works

1. User inputs are collected through Streamlit widgets.
2. Categorical inputs are one-hot encoded and aligned to the training columns (`Columns.pkl`).
3. Features are scaled with the saved `StandardScaler` (`Scaler.pkl`).
4. The KNN model (`KNN_heart.pkl`) predicts the class: `1` = high risk, `0` = low risk.

## Data Preprocessing

- Zero values in `Cholesterol` and `RestingBP` (invalid readings) were replaced with the column mean
- Categorical features were one-hot encoded (`drop_first=True`)
- Features were standardized with `StandardScaler`
- The data was split 80/20 with stratification on the target (`random_state=42`)

## Model Comparison

Five models were trained on standardized features and evaluated on a held-out
20% test set:

| Model | Accuracy | F1 Score |
|---|---|---|
| **KNN** | **0.8859** | **0.8986** |
| Logistic Regression | 0.8750 | 0.8878 |
| Naive Bayes | 0.8696 | 0.8788 |
| SVM (RBF) | 0.8641 | 0.8804 |
| Decision Tree | 0.7500 | 0.7629 |

KNN performed best and was selected for the app.

## Notebook

The full exploratory data analysis and model training is in [`Heart.ipynb`](Heart.ipynb).

## Tech Stack

Python · Streamlit · pandas · scikit-learn · joblib · seaborn · matplotlib

## Run Locally

```bash
git clone https://github.com/<your-username>/heart-disease-prediction-app.git
cd heart-disease-prediction-app
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
streamlit run App.py
```

Then open http://localhost:8501.

## Project Structure

```
├── App.py            # Streamlit app
├── Heart.ipynb       # EDA and model training notebook
├── KNN_heart.pkl     # Trained KNN model
├── Scaler.pkl        # Fitted scaler
├── Columns.pkl       # Expected feature columns
├── requirements.txt
├── .gitignore
└── README.md
```

## Dataset

[Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) (Kaggle, fedesoriano), 918 records.

## Future Improvements

- Show prediction probability instead of only a label
- Hyperparameter tuning (e.g. the value of k for KNN) with cross-validation
- Add model evaluation metrics (confusion matrix, ROC curve) to the app

## Author

**Abdul Rahman Sajid**
GitHub: [@your-username](https://github.com/your-username)
