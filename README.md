# Machine-Learning-Tasks
Predicting House Prices Python code 
#code 
# Import necessary libraries
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
import matplotlib.pyplot as plt
import seaborn as sns

# Step 1: Load the dataset
# For this example, let's assume we have a CSV file named 'house_prices.csv'
# You can replace this with your actual dataset
df = pd.read_csv('house_prices.csv')

# Step 2: Explore the dataset
print(df.head())
print(df.info())
print(df.describe())

# Step 3: Preprocess the data
# Handle missing values, categorical variables, etc.
# For simplicity, let's drop rows with missing values
df.dropna(inplace=True)

# Convert categorical variables to dummy variables (one-hot encoding)
df = pd.get_dummies(df, drop_first=True)

# Step 4: Split the data into training and testing sets
# Assume 'Price' is the target variable and the rest are features
X = df.drop('Price', axis=1)
y = df['Price']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Step 5: Train the model
model = LinearRegression()
model.fit(X_train, y_train)

# Step 6: Evaluate the model
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f'Mean Squared Error: {mse}')
print(f'R-squared: {r2}')

# Optional: Visualize the results
plt.scatter(y_test, y_pred)
plt.xlabel('Actual Prices')
plt.ylabel('Predicted Prices')
plt.title('Actual vs Predicted Prices')
plt.show()

# Calculate residuals
residuals = y_test - y_pred

# Plotting residuals
sns.residplot(x=y_test, y=residuals, lowess=True, color="g")
plt.xlabel('Actual Prices')
plt.ylabel('Residuals')
plt.title('Residuals vs Actual Prices')
plt.show()

