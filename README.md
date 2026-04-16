# Walmart Sales Data Analysis: End-to-End SQL + Python Project
This end-to-end data analysis project extracts key business insights from Walmart sales data using SQL and Python. It covers a full data pipeline: cleaning and feature engineering in Python, querying with SQL, and presenting results with business-driven reasoning and visualizations.

## 🛠 Tools Used
- Python (pandas, matplotlib, seaborn)
- SQLite (via Python) — adapted from MySQL for full Colab reproducibility
- Google Colab / Jupyter Notebook

## 📊 Business Questions Solved
1. **Payment Methods & Sales Volume**
   - What are the different payment methods, and how many transactions were made with each?

2. **Top-Rated Category by Branch**
   - Which category has the highest average rating in each branch?

3. **Busiest Day by Branch**
   - What is the busiest day of the week per branch?

4. **Category Ratings by City**
   - What are the average, min, and max ratings for each category in each city?

5. **Profit by Category**
   - What is the total profit by product category, ranked?

6. **Most Common Payment Method per Branch**
   - What payment method is most frequently used in each branch?

7. **Sales Volume by Shift**
   - How many transactions occur in Morning, Afternoon, and Evening shifts?

8. **Revenue Decline Year-over-Year**
   - Which 5 branches had the largest revenue drop from 2022 to 2023?

9. **Running Revenue Total by Branch**
   - What is the cumulative revenue trajectory for each branch over time?

10. **Top 3 Profitable Categories per City**
    - Which product categories generate the most profit in each city?

11. **Category Revenue Share per Branch**
    - What percentage of each branch's total revenue comes from each product category?

## 📂 Project Structure
```text
walmart_sales/
├── data/
│   ├── Walmart.csv
├── notebook/
│   └── walmart.ipynb
└── README.md
```

## ✅ Key Insights
- **Digital payments dominate** — Credit card and Ewallet account for 82% of all transactions; cash represents only 18%
- **Two categories drive most profit** — Fashion accessories and Home and lifestyle generate ~6x more profit than any other category
- **Revenue decline is branch-specific** — The 5 highest-decline branches show individual patterns rather than a chain-wide trend, pointing to local factors
- **Ratings don't predict spend** — Customer rating has near-zero correlation with transaction revenue at the individual level
- **Peak days and shifts vary by branch** — No single day or shift dominates chain-wide; branch-level scheduling is necessary

