# Amazon Marketplace Intelligence Dashboard

**Role:** Business Analyst | **Tool:** Microsoft Excel (Power Query, Pivot Tables, Advanced Formulas)
**Dataset:** [Amazon Sales Dataset — Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset) (1,351 products, real Amazon product + review data)

---

## Business scenario

Acting as a Business Analyst on Amazon's Category Management team, I was asked by the Head of Category Strategy to answer four questions ahead of a Monday executive review, within a 3–4 day turnaround:

> *"We're spending a lot on discounts, but I don't know if it's working. Where are we discounting too much without any payoff in customer satisfaction? Which products are customer favorites but not getting attention? Are there products with a lot of engagement but tanking in satisfaction? And Finance wants to know which categories offer the best value for money."*

This project simulates that real stakeholder brief end-to-end — from raw data cleaning through to a decision-ready dashboard.

---

## Objective

Turn a raw, messy Amazon product export into a clean, KPI-driven dashboard that answers four specific business questions with clear, actionable recommendations — not just charts.

---

## Tools & skills used

- **Power Query** — cleaned currency-formatted price fields, percentage text, split category hierarchy, handled null values
- **Advanced Excel Formulas** — `IF`, `AND`, `IFERROR`, `PERCENTILE`, structured table references
- **Pivot Tables** — category and product-level aggregation, value filters, custom benchmarks
- **Conditional Formatting** — formula-based highlighting to flag mismatches (e.g., high discount + low rating)
- **Slicers** — interactive category filtering connected across multiple pivot tables
- **Dashboard Design** — KPI cards, combo charts, scatter plots, bar charts, business-question-driven layout

---

## KPIs

| Metric | Value |
|---|---|
| Total products analyzed | 1,351 |
| Average rating | 4.09 / 5 |
| Average discount | 47% |
| Total reviews captured | 23,802,428 |

---

## Business questions, findings & recommendations

### 1. Which categories discount heavily without a satisfaction payoff?
**Method:** Compared each category's average discount % and average rating against marketplace-wide benchmarks (47% discount, 4.09 rating), flagging categories above the discount benchmark AND below the rating benchmark.

**Finding:** Health&PersonalCare (53% discount, 4.0 rating) and Electronics (50% discount, 4.08 rating) are discounting above average while under-delivering on satisfaction.

**Recommendation:** Reduce discount depth in these two categories and reallocate margin to categories where discounting is actually driving satisfaction and volume.

### 2. Which products are customer favorites but under-promoted?
**Method:** Defined "low visibility" as rating_count below the 25th percentile (1,106 reviews) and "high satisfaction" as rating above 4.5. Flagged with a helper column, cross-checked with COUNTIF.

**Finding:** 10 products meet both conditions — high satisfaction, minimal review volume.

**Recommendation:** Feature these 10 products in the next marketing push. Low-cost visibility gain on products that already convert customers into fans.

### 3. Which products have high engagement but poor satisfaction (red flags)?
**Method:** Defined "high engagement" as rating_count above the 75th percentile (top 25%), and "low satisfaction" as rating below 3.8.

**Finding:** 8 products combine very high review volume (18K–88K reviews) with below-average ratings — actively damaging brand trust at scale.

**Recommendation:** Prioritize these 8 listings for urgent quality/content review — high-visibility dissatisfaction carries more reputational risk than low-visibility issues.

### 4. Which categories offer the best "value for money" for Finance's marketing push?
**Method:** Built a Value Score (`rating ÷ discounted_price`) per product, averaged by category. Handled a divide-by-zero edge case (missing price data) with `IFERROR`.

**Finding:** OfficeProducts ranks highest (Value Score 52.7) — though this is partly driven by a low average price point rather than exceptional quality, a caveat flagged for Finance. Toys&Games was excluded from ranking (only 1 product, missing price data — insufficient sample).

**Recommendation:** Lead the value-for-money marketing campaign with OfficeProducts, with the price-scale caveat disclosed for transparency.

---

## Data quality notes (documented for transparency)

- Several rows had null `rating_count` values, initially causing formula errors — identified and handled before final analysis.
- One Toys&Games product had a missing/zero `discounted_price`, breaking the Value Score ratio — resolved with `IFERROR` rather than fabricating a price, and the category was excluded from the final ranking rather than reporting an unreliable single-product average.

---

## Dashboard preview

[Amazon_Marketplace_Intelligence_screenshot.png](Amazon_Marketplace_Intelligence_screenshot.png)

---

## Repository structure

```
Amazon-Marketplace-Intelligence/
├── Dataset/
│   └── amazon.csv
├── Excel/
│   └── Amazon_Marketplace_Dashboard.xlsx
├── Images/
│   └── dashboard_screenshot.png
├── Docs/
│   └── insights_and_recommendations.md
└── README.md
```

---

## Key takeaway

This project reflects a full BA workflow: translating a vague stakeholder brief into precise, benchmarked business questions; cleaning and validating real-world messy data; building defensible thresholds (percentiles, not guesses); and delivering a dashboard focused on decisions, not just numbers.
