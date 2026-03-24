# Google Merchandise Store Analysis

**E-commerce Conversion & Customer Behavior Study**

This project examines three months of transactional data from the Google Merchandise Store (November 2020 through January 2021) to identify conversion bottlenecks and revenue optimization opportunities. The analysis combines funnel diagnostics, path comparison, RFM segmentation, and cohort retention to deliver actionable recommendations.

---

## Context

The Google Merchandise Store sells branded Google products online. Despite steady traffic, conversion rates remain below industry benchmarks. This analysis was conducted to understand where and why potential customers drop off, and what interventions could improve performance.

| Metric | Value |
|--------|-------|
| Analysis Period | Nov 2020 to Jan 2021 |
| Total Sessions | 354,857 |
| Unique Users | 287,359 |
| Transactions | 4,848 |
| Conversion Rate | 1.4% |
| Total Revenue | €362K |

---

## Data Sources

All data was extracted from Google Analytics 4 via BigQuery. The dataset includes event-level tracking (4.3M events) aggregated at session and user levels. Four primary tables were constructed for analysis.

| Table | Description | Grain |
|-------|-------------|-------|
| Conversion Funnel | Drop-off rates across purchase stages | Aggregate |
| Promo Efficiency | Exposure vs. click vs. conversion by promo segment | Session |
| Navigation Paths | Search vs. direct browse behavior comparison | Session |
| User Profiles | RFM scoring and segmentation | User |

---

## Key Findings

### Funnel Performance

The conversion funnel reveals that 98% of session losses occur before checkout begins. The transition from session start to product view loses 78% of traffic. Among those who view a product, 80% leave without adding to cart. These two stages represent the primary optimization opportunity.

### Path Analysis

Users who engage with the search function convert at 4.14%, compared to 1.22% for direct browsers. However, search users exhibit higher abandonment at the payment stage (62% vs 21%) and longer session durations (21 minutes median vs 13 minutes). This suggests search facilitates product discovery but introduces comparison behavior that delays purchase commitment.

### Promotion Impact

Promotion exposure correlates strongly with revenue. Users who saw a promotion (without necessarily clicking) represent 33% of sessions but generate 81% of revenue. Click-through on promotions shows weaker correlation with purchase, indicating that visibility matters more than direct engagement.

### Customer Segmentation

RFM analysis reveals extreme value concentration. The "Need Attention" segment (22% of users) generates 57% of total revenue. Meanwhile, 98% of users have never made a purchase, and retention drops below 1% by week four post-acquisition.

---

## Recommendations

Three strategic priorities emerged from the analysis.

| Priority | Focus Area | Expected Impact |
|----------|------------|-----------------|
| 1 | Improve product discovery through UX optimization and search promotion | +€200K to €300K annually |
| 2 | Reduce cart abandonment via free shipping integration and recovery emails | +€400K to €500K annually |
| 3 | Activate CRM segments with targeted campaigns for high-value users | +€200K to €350K annually |

The combined revenue opportunity ranges from €650K to €1.4M per year depending on execution.

---

## Repository Structure

```
google-merchandise-analysis/
    data/
        raw/                     Original BigQuery exports
        processed/               Cleaned datasets for analysis
    notebooks/
        macro_analysis.ipynb     Primary analysis notebook
    outputs/
        figures/                 Visualization exports (PNG)
        presentation.pptx        Final slide deck
    docs/
        speaker_notes.md         Presentation talking points
    README.md                    Project documentation
    requirements.txt             Python dependencies
```

---

## Methodology Notes

**Funnel Construction**: Events were sequenced using GA4 event naming conventions (session_start, view_item, add_to_cart, begin_checkout, add_shipping_info, add_payment_info, purchase). The shipping step was excluded from friction analysis due to auto-fire behavior for logged-in Google users.

**Path Classification**: Sessions were classified by dominant behavior. A session was tagged as "search" if the user engaged with site search, "promo_engaged" if they clicked a promotion, "promo_exposed" if they viewed but did not click, and "direct" otherwise.

**RFM Scoring**: Recency, Frequency, and Monetary values were calculated at user level and scored 1 to 5 using quintile distribution. Segment labels follow standard RFM conventions (Champions, Loyal, At Risk, etc.).

**Clustering**: K-means was applied to raw RFM values. Although silhouette scoring favored k=2, this merely separates buyers from non-buyers. A business-driven choice of k=4 was adopted to create actionable segments.

---

## Limitations

The analysis period includes Black Friday and holiday seasonality, which may inflate conversion expectations. Self-selection bias affects path comparisons, as users who search may inherently have higher purchase intent. Promo attribution is correlational rather than causal. The three-month window limits retention analysis robustness.

---

## Technical Requirements

The analysis was conducted in Python 3.10 with the following primary dependencies.

| Package | Version | Purpose |
|---------|---------|---------|
| pandas | 1.5+ | Data manipulation |
| numpy | 1.24+ | Numerical operations |
| matplotlib | 3.7+ | Visualization |
| seaborn | 0.12+ | Statistical graphics |
| scikit-learn | 1.2+ | Clustering and scaling |

Install dependencies with `pip install -r requirements.txt`.

---

## Author

**Eliott Barat-Chabeauti**

ebaratchabeauti@gmail.com

linkedin.com/in/eliott-barat-chabeauti

---

*Analysis completed March 2025*
