# Data

Both projects use the public **[E-Commerce Sales and Customer Analytics](https://www.kaggle.com/datasets/datascikhan/e-commerce-sales-and-customer-analytics)** dataset from Kaggle. It's synthetic data for a fictional online store, covering 2021 to 2025.

The CSVs (~90 MB in total) aren't committed. Download them from Kaggle and put them in this folder:

| File | Rows | Used by | What it holds |
|---|---|---|---|
| `ecommerce_sales_customer_analytics_150k.csv` | 138,116 | Parts 1 & 2 | One row per order (46 columns): customer segment, rating, lifetime value, warehouse, shipping method, delivery days, delivery status, order-level sales and shipping cost |
| `order_items.csv` | 397,569 | Part 1 | One row per line item: quantity, gross/net sales, discount, tax, shipping cost, product cost, profit |
| `product_catalog.csv` | 1,175 | Part 1 | Product attributes and unit prices (joined on `product_id` + `unit_price`) |
| `customer_master.csv` | 25,000 | (loaded, not analysed) | Customer demographics |

> **Note:** Despite its name, the sales file has 138,116 rows, not 150K. The notebooks also load `customer_master-selected-columns.csv`, a column subset we made from `customer_master.csv`. It isn't used in any analysis, so you can delete that `read_csv` line.

The notebooks were run in Google Colab, so they read from `/content/...`. To run them locally, change those paths to `../../data/<file>.csv`.
