# Bike Rental Prediction

## Business Problem
The goal of this project is to predict daily bike rental demand to optimize inventory and maximize profitability for a bike rental business. Effective prediction helps the business:
1. **Minimize costs**: Reduce overstocking by keeping inventory levels closer to actual demand.
2. **Maximize revenue**: Avoid understocking, which leads to missed rental opportunities.

### Key Metrics
1. **RMSE (Root Mean Squared Error)**: Measures how well the model predicts daily demand compared to actual values.
2. **Profit**: Measures the monetary outcome based on:
   - **Rental Revenue**: Revenue earned from fulfilled bike rental demands.
   - **Overstock Cost**: Costs incurred from maintaining excess inventory.
   - **Understock Cost**: Opportunity loss due to unmet demand.

### Profit Statement
\[
\text{Profit} = \text{Rental Income} - \text{Overstock Cost} - \text{Understock Cost}
\]
Where:
- **Rental Income**: \( \text{Rental Price} \times \min(\text{Predicted Demand}, \text{Actual Demand}) \)
- **Overstock Cost**: \( \text{Holding Cost per Bike} \times \max(0, \text{Predicted Demand} - \text{Actual Demand}) \)
- **Understock Cost**: \( \text{Rental Price} \times \max(0, \text{Actual Demand} - \text{Predicted Demand}) \)

---

## Assumptions About Costs
1. **Bike Purchase Price**:
   - The cost of purchasing one bike is **£590**.
2. **Rental Price**:
   - The price for renting a bike is **£25 per rental**.
3. **Inventory Holding Cost**:
   - Annual holding cost is assumed to be **20% of the bike purchase price**, i.e., **£118 per year per bike**.
   - Daily holding cost is calculated as:
     \[
     \text{Daily Holding Cost} = \frac{\text{Annual Holding Cost}}{365} = \frac{118}{365} \approx £0.323
     \]

---

## Preprocessing Steps
1. **Dataset**:
   - Source: [Kaggle - London Bike Sharing Dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset)
   - Contains hourly data for bike rentals in London.

2. **Data Cleaning**:
   - Converted the timestamp field to a datetime object and derived the `time_of_day` feature (Morning, Afternoon, Late Evening, Night).
   - Normalized `weather_code` categories from a range of [1, 2, 3, 4, 7, 10, 26, 94] to [1, 2, 3, 4, 5, 6, 7, 8].

3. **Feature Engineering**:
   - One-hot encoded categorical features: `season` and `time_of_day`.
   - Scaled numerical features (`t1`, `t2`, `hum`, `wind_speed`) using Min-Max scaling.

4. **Data Splitting**:
   - Split the data into 50% training, 30% validation, and 20% test sets.

---

## Validation Results
These are the results for each model on the **validation set**:

| Model                       | Validation RMSE | Validation Profit (£)   | Best Hyperparameters         |
|-----------------------------|-----------------|-------------------------|------------------------------|
| **Linear Regression**       | 827.14          | 68,750,385              | N/A                          |
| **Decision Tree (RMSE)**    | 774.73          | 78,602,068              | Max Leaf Nodes: 23           |
| **Decision Tree (Profit)**  | 776.41          | 78,799,112              | Max Leaf Nodes: 25           |
| **Neural Network (RMSE)**   | 727.71          | 78,602,068              | Layers: (128, 64)            |
| **Neural Network (Profit)** | 776.41          | 85,972,722              | Layers: (64, 32)             |

---

## Models and Hyperparameter Optimization
1. **Linear Regression**:
   - Baseline model for comparison.

2. **Decision Tree (Optimized for RMSE)**:
   - Hyperparameter: Maximum number of leaf nodes.
   - Best RMSE achieved with 23 nodes.

3. **Decision Tree (Optimized for Profit)**:
   - Hyperparameter: Maximum number of leaf nodes.
   - Best Profit achieved with 25 nodes.

4. **Neural Network (Optimized for RMSE)**:
   - Hyperparameter: Number of hidden layers and neurons.
   - Best RMSE achieved with layers `(128, 64)`.

5. **Neural Network (Optimized for Profit)**:
   - Hyperparameter: Number of hidden layers and neurons.
   - Best Profit achieved with layers `(64, 32)`.

---

## Test Results
The following table summarizes the performance of all models on the **test set** using **RMSE** and **Profit** metrics:

| Model                    | Test RMSE   | Test Profit (£) |
|--------------------------|-------------|-----------------|
| Linear Regression        | 813.85      | 46,600,650      |
| Decision Tree (RMSE)     | 769.18      | 51,670,550      |
| Decision Tree (Profit)   | 771.86      | 51,641,370      |
| Neural Network (RMSE)    | 722.94      | 55,949,180      |
| Neural Network (Profit)  | 722.73      | 56,760,760      |

---

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/Bike_Rental_Prediction.git
