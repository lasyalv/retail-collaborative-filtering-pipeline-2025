# Retail Collaborative Filtering Pipeline
Production‑grade retail recommendation pipeline using collaborative‑filtering and scalable data engineering

## Introduction

This project focuses on improving customer experience and sales by building a Product Recommendation System for a retail company. The goal is to suggest relevant products to shoppers based on purchase history and product similarities, driving engagement and revenue. Recommendation systems like this are widely used by companies such as Amazon and Netflix to personalize content.

## Dataset

We utilized a retail transaction dataset containing historical purchase records. Each record includes `CustomerID`, `ProductID`, `Quantity`, `Timestamp`, and `Price`. The dataset is derived from a sample e-commerce store with **~100,000** transactions and **10,000** unique customers. Product metadata (category, brand, price tier) was also used for content-based features. Data was stored in CSV and SQL tables and contained both explicit ratings (if available) and implicit feedback (purchase frequency).

## Methodology

The analysis workflow was as follows:

1. **Data Preparation:** Cleaned and transformed raw transaction logs using Python (pandas) and SQL. We aggregated purchases to create a customer-item rating matrix.  
2. **Exploratory Analysis:** Computed basic stats (e.g., most popular products, purchase frequency per user). Visualized data distributions in Tableau.  
3. **Modeling Approaches:**  
   - **Collaborative Filtering:** Implemented matrix factorization (SVD) and user-based/item-based k‑NN models. Collaborative filtering identifies similarities among user preferences to suggest items.  
   - **Content-Based Filtering:** Used product features (category, brand) to recommend items similar to those a user has liked.  
   - **Hybrid Model:** Combined both approaches and used a weighted ensemble for final recommendations.  
4. **Model Training:** Leveraged Python’s scikit-learn and Spark MLlib (for scalability) to train models. Spark was used to handle large-scale matrix operations and to accelerate computations with parallelism.  
5. **Evaluation:** Employed **RMSE** (for rating prediction accuracy) and **Precision@K/Recall@K** (for top‑N recommendation quality). We performed cross-validation and A/B tested the hybrid model against baseline popularity-based recommendations.

## Tools & Technologies

- Languages & Libraries: Python (pandas, NumPy, scikit-learn), Apache Spark (PySpark for ALS), SQL (MySQL) for data storage.
- Data Handling: SQL database for raw transactions, Jupyter notebooks for prototyping, pandas for ETL.
- Machine Learning: Spark MLlib ALS for collaborative filtering, scikit-learn for evaluation.
- Visualization: Tableau Public for interactive dashboards of recommendation coverage, and matplotlib/seaborn for metric plots.
- Collaboration: GitHub for version control, Trello for task tracking.

## Results & Insights

- The hybrid recommender achieved an **RMSE of 0.93**, outperforming a baseline model. Precision@10 was around **35%**, meaning over one-third of top-10 suggestions matched actual purchases.
- Visualizations show that collaborative filtering captures latent user preferences, while content-based adds novelty (by recommending new categories).
- Example insight: Customers who bought eco-friendly products tend to buy certain organic brands, which was captured by a strong clustering in user-feature space.
- We created a Tableau dashboard showing “Customers-to-Products” network graphs and popularity charts to communicate findings to stakeholders.

## Setup & Running Instructions

To run this project:

1. **Environment:** Install Python 3.8+, Apache Spark (3.x), and MySQL (or PostgreSQL).  
2. **Dependencies:** Run `pip install -r requirements.txt` to install needed libraries (pandas, numpy, scikit-learn, pyspark).  
3. **Database:** Import `transactions.csv` into a database using the provided SQL script `load_data.sql`.  
4. **Model Training:** Use `train_recommender.py` to execute collaborative filtering (requires Spark). Configuration in `config.yaml`.  
5. **Generating Recommendations:** Run `recommend.py` which takes a `CustomerID` or list of customers and outputs top‑N recommendations.  
6. **Evaluation:** Execute `evaluate.py` to reproduce RMSE and Precision metrics.  
7. **Visualization:** Open `Retail_Rec_Dashboard.twbx` in Tableau or run the Jupyter notebooks (`EDA.ipynb`, `Modeling.ipynb`) to visualize.


## Team & Credits

Contributors: Amit Gamot, Aarthi Sagayaraj, Daniel McGhee, Khushboo Agnihotri

Special thanks to Dr. Ashish Khandelwal for his guidance on recommender best practices.
