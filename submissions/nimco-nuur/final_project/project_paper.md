# StockSense AI: Smart Inventory Segmentation and Stockout Prediction System

**Author:** Nimco NOR Geesey

**Date:** July 2026

---

# 1. Problem Statement and Motivation

Inventory management is one of the most important business operations in retail stores, supermarkets, pharmacies, and warehouses. Poor inventory planning often causes products to become unavailable when customers need them, resulting in lost sales and reduced customer satisfaction. On the other hand, keeping excessive inventory increases storage costs and reduces business profitability.

The objective of this project is to develop an intelligent inventory management system that uses machine learning to improve inventory decision-making. The project combines unsupervised learning and supervised learning. First, K-Means clustering groups products according to their inventory behavior. These groups help inventory managers understand which products move quickly and which move slowly. After segmentation, supervised classification models are trained to predict stockout events. The final solution will be deployed as a Django REST Framework API that can later be integrated with a React frontend dashboard.

---

# 2. Dataset and Preprocessing

## Dataset

This project uses the **High-Dimensional Supply Chain Inventory Dataset** obtained from Kaggle.

The dataset contains more than one thousand inventory records collected from supply chain operations. It includes product information, inventory levels, supplier information, demand forecasts, reorder information, and stockout events.

### Dataset Source

https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset?.com
### Main Features

* Inventory Levels
* Units Sold
* Supplier Lead Times
* Reorder Points
* Reorder Quantities
* Forecasted Demand
* Selling Price
* Warehouse
* Supplier

### Target Variable

**Stockout Events**

The target variable indicates whether a stockout occurred for a product.

---

## Data Preprocessing

Several preprocessing techniques will be applied before model training.

### Data Cleaning

* Remove duplicate records.
* Handle missing values.
* Correct inconsistent values if necessary.

### Feature Engineering

* Encode categorical variables.
* Scale numerical features using StandardScaler.
* Select the most relevant features.

### Data Splitting

The prepared dataset will be divided into:

* Training Set (80%)
* Testing Set (20%)

The same train-test split will be used for every supervised algorithm to ensure a fair comparison.

---

# 3. Algorithms

This project compares one unsupervised learning algorithm and three supervised learning algorithms.

---

## K-Means Clustering

K-Means is an unsupervised learning algorithm that groups products based on similar inventory characteristics. It identifies hidden patterns without using target labels.

Expected inventory segments include:

* Fast Moving Products
* Medium Moving Products
* Slow Moving Products

These segments help businesses understand inventory behavior and improve inventory planning.

### Why K-Means?

K-Means is simple, efficient, and widely used for customer and product segmentation. It provides useful business insights before building predictive models.

---

## Logistic Regression

Logistic Regression is used as the baseline classification model.

### Why Logistic Regression?

It is simple, fast, interpretable, and performs well on binary classification problems.

---

## Random Forest

Random Forest combines multiple decision trees to improve prediction performance.

### Why Random Forest?

It reduces overfitting, handles complex relationships between variables, and usually performs well on structured datasets.

---

## XGBoost

XGBoost (Extreme Gradient Boosting) is an advanced ensemble learning algorithm that builds decision trees sequentially to improve prediction accuracy.

### Why XGBoost?

XGBoost is widely used in real-world machine learning applications because it provides excellent performance, handles structured data efficiently, and includes regularization techniques that reduce overfitting. It is expected to achieve the highest performance among the classification models.

---

# 4. Results and Discussion

The performance of all supervised models will be compared using the same testing dataset.

The evaluation metrics include:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix

The clustering model will be evaluated using:

* Silhouette Score
* Davies–Bouldin Index

After evaluating every algorithm, a comparison table will summarize their performance.

Example:

| Algorithm           | Accuracy | Precision | Recall | F1-Score |
| ------------------- | -------: | --------: | -----: | -------: |
| Logistic Regression |        - |         - |      - |        - |
| Random Forest       |        - |         - |      - |        - |
| XGBoost             |        - |         - |      - |        - |

The best classification model will be selected using the **highest F1-Score** because it balances Precision and Recall and is suitable for predicting stockout events.

Three sanity checks will also be performed on the best model by providing sample inventory records and verifying that the predicted results are reasonable.

---

# 5. Deployment Notes

The final application will use the following technologies:

* Backend: Django REST Framework
* Frontend: React
* Machine Learning: Scikit-learn and XGBoost
* Database: MySQL
* Model Persistence: Joblib

The trained K-Means model, the best classification model, and the preprocessing artifacts will be saved and loaded during prediction.

## Prediction Endpoint

**POST /api/predict/**

Example request:

```json
{
  "inventory_level": 150,
  "units_sold": 60,
  "supplier_lead_time": 5,
  "reorder_point": 100,
  "forecasted_demand": 75
}
```

The API workflow is:

1. Receive inventory information.
2. Preprocess the input.
3. Assign the product to an inventory cluster using K-Means.
4. Pass the processed features to the best classification model.
5. Return the predicted stockout event and prediction probability.

Example response:

```json
{
  "cluster": "Fast Moving",
  "prediction": "Stockout",
  "probability": 0.94
}
```

The React dashboard will display:

* Inventory overview
* Product segments
* Stockout predictions
* Business analytics
* Reports and charts

---

# 6. Lessons Learned

Developing this project demonstrates how unsupervised learning and supervised learning can be combined to solve a real-world business problem.

The project highlights the importance of data preprocessing, including cleaning, encoding, scaling, and feature selection before model training.

Another important lesson is that clustering helps identify hidden inventory patterns that support better business decisions. Classification models then use these insights together with historical inventory data to predict future stockout events.

Finally, deploying the trained model using Django REST Framework demonstrates how machine learning can be integrated into a practical business application that provides real-time predictions.

---

# Conclusion

StockSense AI is an intelligent inventory management system that combines product segmentation and stockout prediction to improve inventory planning and business decision-making. By integrating K-Means clustering with Logistic Regression, Random Forest, and XGBoost, the system provides meaningful inventory insights while accurately predicting stockout events. This project demonstrates the practical application of machine learning, backend development, and REST API deployment in solving real-world supply chain and inventory management challenges.




prepared By Nimco nor gesey
