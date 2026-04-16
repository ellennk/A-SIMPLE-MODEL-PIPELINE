# A-SIMPLE-MODEL-PIPELINE

### KEY OJECTIVE
 Build a simple model pipeline from data preprocessing→ training→ evaluation
using an available dataset. Deploy it as a REST API and write a brief analysis of how model performance degradation in production will be monitored.

###  CODE
1. Go to New File
 
2.  Name it train.py
 
3. Paste this code;
   
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import joblib

# Load dataset
df = pd.read_csv("housing.csv")

# Remove empty rows
df = df.dropna()

# Convert text column to numbers
df = pd.get_dummies(df, columns=["ocean_proximity"])

# Inputs
X = df.drop("median_house_value", axis=1)

# Output
y = df["median_house_value"]

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Scale
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Train model
model = LinearRegression()
model.fit(…
 Save using control + s
Go to terminal and run “python train.py
 You should see”Mean Squared Error: ....
Files saved successfully
 And desk top will have “train.py
housing.csv
model.pkl
scaler.pkl
 Open a new file again
 Name it “app.py
Paste In this code “from flask import Flask, request, jsonify
import joblib
import numpy as np

app = Flask(_name_)

model = joblib.load("model.pkl")
scaler = joblib.load("scaler.pkl")

@app.route("/")
def home():
    return "API is running"

@app.route("/predict", methods=["POST"])
def predict():
    data = request.json["features"]

    data = np.array(data).reshape(1, -1)
    data = scaler.transform(data)

    prediction = model.predict(data)

    return jsonify({
        "predicted_price": float(prediction[0])
    })

app.run(debug=True)
 Save it Control + s
 Run this in terminal “python app.py

 ### RESULT
 After running the code this is the likely result;
" Running on http://127.0.0.1:5000 AND API is running"

### SUMMARY OF WORK
Built a regression model using California Housing dataset.
Applied preprocessing with missing value removal, one-hot encoding, scaling, train/test split.
Trained Linear Regression model.
Deployed with Flask REST API




 
