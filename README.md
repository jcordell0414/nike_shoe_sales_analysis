# Nike Shoe Sales Analysis

**What drives perceived value and consumer demand in Nike's product catalog?**

A full-cycle data analysis project using Python, SQLite, and Tableau — following the Google Data Analytics six-phase structure.

---

## Project Summary

This project analyzes 555 cleaned Nike shoe records across 24 product lines to answer six business questions about pricing, consumer ratings, and review volume. The dataset originates from a public scrape of Nike product listings.

**Key findings:**
- Air Max dominates the catalog at 24.32% of all products. The top 10 lines account for 79% of catalog share.
- FlyKnit commands the highest average sale price ($182) but ranks 15th in consumer rating, showing price and satisfaction operate independently.
- Products without a listed MSRP average 12.61 reviews vs. 9.46 for listed products, and rate 0.20 points higher — suggesting price transparency creates value anchoring that works against consumer engagement.
- Mid-tier shoes ($60–$119) score highest across all price bands despite not being the most expensive.

---

## Tools

| Tool | Purpose |
|------|---------|
| Python (pandas, numpy) | Data cleaning and feature engineering |
| SQLite (in-memory) | Analytical queries across six key questions |
| Tableau | Two published dashboards |
| Jupyter Notebook | End-to-end documented workflow |

---

## Repository Structure

```
nike-shoe-sales-analysis/
├── 1_data/
│   ├── raw/
│   │   └── nike_shoes_sales_data.csv        # Original dataset (643 records)
│   └── clean/
│       └── clean_nike_shoe_sales.csv        # Cleaned dataset (555 records)
├── 2_scripts/
│   └── nike_shoe_analysis.ipynb             # Full cleaning + SQL analysis
├── 3_visualizations/
│   ├── catalog_overview_dashboard.png       
│   └── consumer_sentiment_dashboard.png     
├── 4_report/
│   └── nike_analysis_report.docx            # Written findings report
└── README.md
```

---

## Phase 1: Data Cleaning

**Raw → Clean: 643 rows to 555**

| Step | Detail |
|------|--------|
| Duplicates removed | 88 rows (13.7%) — likely scraping overlap or colorway re-listings |
| Columns dropped | `discount` (zero variance), `description`, `images` (no analytical value) |
| Price scaling | `listing_price` and `sale_price` divided by 100.0 to produce USD values |
| `is_rated` | Boolean flag — 365 products (65.8%) carry a rating above 0.0 |
| `has_msrp` | Boolean flag — 193 products (34.8%) carry a non-zero listing price |
| `shoe_line` | Keyword-extracted from `product_name`; 24 categories, priority-ordered to prevent misclassification |
| `price_tier` | Four bins: Budget (< $60), Mid ($60–$119.99), Premium ($120–$199.99), Luxury ($200+) |

Final dataset: **555 records, 11 columns, 0 nulls**

---

## Phase 2: Analysis (SQLite)

Six questions answered via SQL queries on an in-memory SQLite database.

**Q1 — Which shoe lines have the highest average sale price?**  
FlyKnit ($182), VaporMax ($153), and MX ($150) lead. Both FlyKnit and MX have fewer than 10 products, so averages reflect a narrow high-price range rather than broad catalog positioning.

**Q2 — Which shoe lines have the highest average rating?**  
Among rated products: Renew (4.70), Air Force (4.57), Jordan (4.48). FlyKnit and VaporMax — the two most expensive lines — rank 15th and 19th.

**Q3 — What is the relationship between price tier and average rating?**  
Budget (4.09), Mid (4.29), Premium (4.23), Luxury (4.18). The range is narrow. Mid-tier scores highest. No meaningful relationship between price and satisfaction.

**Q4 — Which individual products have the most reviews?**  
Air Jordan 10 Retro leads with 223 reviews. Top 10 spans six different shoe lines. Two distinct Air Force 1 '07 entries appear under different product IDs — confirmed separate colorways, not duplicates.

**Q5 — How does MSRP listing affect ratings and reviews?**  
Rated products without a listed price: avg 12.61 reviews, 4.33 rating. Listed products: 9.46 reviews, 4.13 rating. Unlisted products outperform on both metrics.

**Q6 — What percentage of products fall into each shoe line?**  
Air Max: 24.32%. Top 5 lines cover 57% of catalog. Fifteen of 24 lines hold less than 2% each.

---

## Phase 3: Visualization (Tableau)

Two dashboards published to Tableau Public.

**Catalog Overview**
- Air Max holds the largest share of the top 10 shoe lines (24.32% of total catalog)
- FlyKnit leads all shoe lines in average sale price ($182)
- FlyKnit commands a $63 premium over Air Force despite holding just 1.08% of catalog share

**Consumer Sentiment**
- Renew earns the highest average rating among top 10 rated shoe lines (4.70)
- Mid pricing earns the highest average rating across price tiers (4.29)
- Air Jordan 10 Retro leads all products in review count (223)
- Products without a listed price outperform listed products on both rating and review volume

> Tableau Public link: *(https://public.tableau.com/app/profile/jace.cordell/vizzes)*

---

## Limitations

- Dataset is a public scrape with no documented collection date. Prices and ratings may not reflect current Nike catalog conditions.
- 13.7% of raw records were duplicates; the original source of duplication cannot be verified.
- 34.2% of products carry no consumer rating. Rating analysis excludes these records, which may skew results toward more established lines.
- Small sample sizes limit reliability for FlyKnit (6 products), MX (5 products), and the Luxury price tier (10 products).
- Review counts are not date-weighted. Long-established products have a cumulative advantage over newer listings.

---

## About

Built by Jace Cordell as part of a data analyst portfolio. Background in mathematics, coaching analytics, and operational data systems. Currently seeking data analyst roles in the DFW area.

[GitHub Portfolio](https://github.com/jcordell0414) | [LinkedIn](https://www.linkedin.com/in/jcordell0414/)
