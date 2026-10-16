# Does Late Delivery Hurt Customer Satisfaction? An Olist Case Study

Analysis of how delivery delays relate to customer review scores, using the Brazilian e-commerce dataset from Olist.

## Question
Do orders delivered after the estimated delivery date receive lower review scores, and how large is the difference?

## Data
[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle). The CSV files are not included in this repository. Download them and place them in a `data/` folder.

Tables used so far: `orders` and `order_reviews`.

## Method
- Delay (in days) = actual delivery date - estimated delivery date. An order counts as **late** if the delay is at least 1 full day.
- Only orders with status `delivered` and a valid delivery date were analyzed.
- Some orders had more than one review. The **most recent review** per order was kept.
- Orders without a review were excluded. Final sample: 95,824 orders (89,443 on time, 6,381 late).
- Groups were compared with a **Mann-Whitney U test**, because review scores are ordinal (1-5) and skewed. Effect size is reported as the rank-biserial correlation.
- For the seller analysis, orders containing items from more than one seller (about 1.3% of orders) were excluded.

## Findings
- Mean review score: **4.29** for on-time orders vs **2.27** for late orders.
- 53.8% of late orders received a 1-star review, compared with 6.6% of on-time orders.
- The difference is statistically significant (Mann-Whitney U, p < 0.001) and the effect is large (rank-biserial r = -0.64).
- Scores drop as delays grow: 3.29 for 1-3 days late, 2.10 for 4-7 days, and about 1.7 beyond a week. The drop flattens after a week, partly because scores cannot go below 1.
- The gap is not explained by customer location alone: within each of the 12 states with at least 1,000 orders, late orders scored 1.6 to 2.3 points lower than on-time orders.

- The gap also holds within sellers: among the 285 sellers with at least 30 orders and at least 5 late orders, late orders scored lower than on-time orders for 284 of them (median gap -2.0 points).

![Score distribution](images/score_distribution.png)
![Delay vs score](images/delay_vs_score.png)

## Limitations
- This is an association, not proof of causation. Late orders may differ in other ways (distance, seller, product category) that also affect satisfaction.
- Reviews are voluntary, so customers who respond may not represent all customers.
- The seller comparison covers only larger sellers, so it may not generalize to small ones.

## Next steps
- Control for product category.
- Build a SQL analysis of the full relational dataset.

## Tools
Python, pandas, matplotlib, SciPy