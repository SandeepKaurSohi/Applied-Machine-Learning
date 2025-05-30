# Assignment 2
## Predictive Model for Payment Default Risk

### Overview-
This code implements a predictive model to predict payment default risk using a logistic regression classifier. It handles missing values, performs feature preprocessing, balances the dataset using SMOTE (Synthetic Minority Over-sampling Technique), and evaluates the model's performance.

### Code Explanation

Importing Libraries: The necessary libraries for data manipulation, model building, and evaluation are imported at the beginning.

Data Loading: The dataset is loaded using pandas.read_csv() function. The dataset is assumed to be in tab-separated format (\t).
	
Dataset Exploration: The first few rows, data types, and summary statistics of the dataset are displayed to understand its structure and characteristics.

Missing Value Handling: The code checks for missing values and replaces any '?' values with NaN. Categorical missing values are filled with 'Unknown', and numerical missing values are filled with the median.

Data Preprocessing:
Binary categorical columns are label-encoded (converted to numerical values).

Categorical features with more than two categories are target encoded (replaced with the mean of the target variable CLASS for each category).

Feature and Target Variable Split: The dataset is split into features (X) and target (y), where CLASS is the target variable.

SMOTE (Synthetic Minority Over-sampling Technique): To handle class imbalance, SMOTE is applied to generate synthetic samples for the minority class.

Train-Test Split: The data is split into training and testing sets with an 80-20 ratio.

Feature Scaling: Numerical features are scaled using StandardScaler to ensure that all features have the same scale.

Model Training: A logistic regression model is trained on the preprocessed data.

Prediction: Predictions are made using a threshold of 0.4 (instead of the default 0.5), which helps to adjust the classification decision boundary.
Evaluation: The model's performance is evaluated using a classification report and confusion matrix.


Outputs
Classification Report: This includes precision, recall, F1-score, and support for each class.
Confusion Matrix: Displays the number of true positives, false positives, true negatives, and false negatives.

Confusion Matrix Data Results:The confusion matrix is a 2x2 array representing the performance of a classification model:

The first row ([5333, 312]) represents the true negatives and false positives:

o	5333: True Negatives (TN) – correctly predicted "No Default."
o	312: False Positives (FP) – incorrectly predicted as "Default" when it's actually "No Default."

The second row ([155, 5502]) represents the false negatives and true positives:
o	155: False Negatives (FN) – incorrectly predicted as "No Default" when it's actually "Default."
o	5502: True Positives (TP) – correctly predicted "Default."

Created a Heatmap: This line creates a new figure for the plot with a size of 6x5 inches.

Ceated a Bar chart to Visualize the Classification Report clearly.

Calculated Misclassification Costs: Misclassification costs are calculated based on the number of false positives and false negatives:

false_positive_cost = cm[0, 1] * 50  # False Positive * 50
false_negative_cost = cm[1, 0] * 5   # False Negative * 5

False Positive Cost: The cost of a false positive is the number of false positives (cm[0, 1] which is 312) multiplied by the cost per false positive, which is 50.
False Negative Cost: The cost of a false negative is the number of false negatives (cm[1, 0] which is 155) multiplied by the cost per false negative, which is 5.

Total Misclassification Cost
total_cost = false_positive_cost + false_negative_cost
total_cost: This variable stores the total misclassification cost, which is the sum of the false positive and false negative costs.

Plotting the Misclassification Costs
labels = ['False Positive', 'False Negative']
cost_values = [false_positive_cost, false_negative_cost]

Adding Text Annotations to the Bars
plt.text(0, false_positive_cost + 500, f'{false_positive_cost:.0f}', ha='center', va='bottom', fontsize=12)
plt.text(1, false_negative_cost + 500, f'{false_negative_cost:.0f}', ha='center', va='bottom', fontsize=12)
plt.text(): This function adds text annotations above the bars to display the exact misclassification cost values.

The 0 and 1 correspond to the position of the bars (0 for the first bar, "False Positive," and 1 for the second bar, "False Negative").

The +500 adds a vertical offset to position the text above the bars.

f'{false_positive_cost:.0f}' and f'{false_negative_cost:.0f}' format the numbers to display them as integers with no decimal places.

This combines the false positive and false negative costs to show how much the misclassification has cost based on the provided costs per type.

