# E-Commerce Analytics: Shipping Cost Prediction & Customer Segment Analysis

An end-to-end data science project on an online store's data: 138K orders and 398K order line items. It's done in two parts:

| Part | Course | Question | Approach | Tools |
|---|---|---|---|---|
| **[Part 1: Shipping Cost Prediction](data601-shipping-cost-prediction/)** | DATA 601 | Can we predict what an order will cost to ship, and does delivery speed drive that cost? | EDA, feature engineering, supervised regression, feature importance | Python, pandas, scikit-learn, seaborn |
| **[Part 2: Customer Segment Analysis](data602-customer-segmentation/)** | DATA 602 (Statistical Data Analysis) | Do VIP, Premium, Business and Consumer customers spend, rate and pay for shipping differently? | Random sampling, ANOVA hypothesis tests, 95% confidence intervals | R, ggplot2, base stats |

## Presentations

- [Part 1: Predicting Shipping Prices in E-Commerce (PDF)](data601-shipping-cost-prediction/reports/presentation.pdf)
- [Part 2: Customer Segment Analysis in E-Commerce Data (PDF)](data602-customer-segmentation/reports/presentation.pdf)

---

## The Business Problem

For an online retailer, **shipping and customers drive the margins**. Shipping is one of the biggest variable costs per order and a major reason customers abandon carts. Customer segments (loyalty tiers) decide who gets perks like free shipping. To make good decisions about pricing, promotions and loyalty programs, the business needs answers to two questions:

1. **Operations:** *What drives shipping cost, and can we estimate it before an order ships?* A reliable estimate supports checkout pricing, carrier negotiation and margin forecasting.
2. **Customers:** *Are higher-tier customers actually more valuable?* If VIP and Premium customers don't spend more, the business should know what it's getting in return for the perks it gives them.

Part 1 answers the first question with machine learning. Part 2 answers the second with statistical inference.

---

## Key Findings at a Glance

### Part 1: Shipping cost prediction (DATA 601)
- A linear regression scored **R² = 1.0 and MAE ≈ $0** on held-out test data. Shipping cost turned out to be an **exact linear function of other financial columns** (net sales, gross sales, discount, tax, product cost, profit). The model wasn't overfitting; it found the formula the store uses.
- **Delivery days had zero importance** in the model, which went against our hypothesis. Faster shipping is only weakly linked to higher cost (r ≈ -0.25).
- With `net_sales` removed, R² fell to between **0.07 and 0.11**. Shipping cost is very hard to predict from non-financial features.
- **Takeaway:** You don't always need a model. If the cost can be computed from data you already have, compute it. To forecast it *before* checkout, you need different features (weight, distance, carrier).

### Part 2: Customer segment analysis (DATA 602)
- **Customer lifetime value does not differ by segment** (ANOVA p = 0.317). VIP customers aren't measurably more valuable than regular consumers.
- **Customer ratings do differ** (p ≈ 5.5×10⁻⁷). VIP (95% CI 3.77 to 3.96) and Premium (3.69 to 3.81) customers rate products higher than Consumers (3.57 to 3.65).
- **Shipping cost differs** (p ≈ 8.6×10⁻¹¹). Premium (\$15.69 to \$19.16) and VIP (\$15.38 to \$21.24) customers pay much less than Consumer (\$22.84 to \$25.55) and Business (\$24.01 to \$30.43) customers.
- **Takeaway:** Moving customers into higher tiers is linked to better product ratings, which can bring in new customers, but not to higher spending. Loyalty perks should be judged on that basis.

### How the two parts connect
Part 1 showed that **delivery speed doesn't explain shipping cost**. Part 2 showed that **customer tier does**: higher tiers pay less for shipping and leave better ratings. A natural next step is to test whether cheaper shipping itself causes the higher ratings.

---

## Repository Structure

```
ecommerce-analytics/
├── README.md                          (this page)
├── LICENSE
├── data/
│   └── README.md                      (dataset source and download steps)
├── data601-shipping-cost-prediction/  (Part 1: Python / ML)
│   ├── README.md
│   ├── notebooks/
│   │   ├── 01_shipping_eda.ipynb
│   │   ├── 02_shipping_model_full_dataset.ipynb
│   │   └── 03_final_shipping_cost_model.ipynb
│   ├── reports/                       (final report and presentation, PDF)
│   └── images/
└── data602-customer-segmentation/     (Part 2: R / statistics)
    ├── README.md
    ├── reports/                       (proposal, analysis report, presentation)
    └── images/
```

## Dataset

[E-Commerce Sales and Customer Analytics](https://www.kaggle.com/datasets/datascikhan/e-commerce-sales-and-customer-analytics) (Kaggle). It's synthetic data from a fictional online store selling electronics, automotive, sporting goods and more, covering 2021 to 2025: 138,116 orders and 397,569 order line items across tables for sales, order items, products and customers. Because the data is synthetic, the findings show the methods working, not real-world market behaviour. See [`data/README.md`](data/README.md) for setup.

## Reproducing the Results

You need the Kaggle CSVs (see [`data/README.md`](data/README.md)), **Python 3.9+** for Part 1 and **R 4.x** for Part 2. Each part's README has its own run steps. The headline numbers (327,028 delivered line items, test R² = 1.0, R² = 0.110 without `net_sales`, ANOVA p-values) were re-run and confirmed with pandas 2.3, scikit-learn 1.6 and R 4.5.

## Limitations

- **Synthetic data.** Patterns were made up by the dataset's author, so the conclusions shouldn't be applied to real retailers.
- **Course project scope.** These are graded coursework analyses, not production pipelines. The notebooks were written in Google Colab and reflect that workflow.

## Authors

**Dawson Conlon** & **Ricky Doucette**, Master of Data Science and Analytics, University of Calgary (Fall 2026)

## License

The code, notebooks and write-ups in this repository are released under the [MIT License](LICENSE). The dataset isn't included and falls under the terms on its [Kaggle page](https://www.kaggle.com/datasets/datascikhan/e-commerce-sales-and-customer-analytics).
