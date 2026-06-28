# Final Recommendation

## Executive Summary

Based on regression analysis of 320 store-month records across four regions and four store types, the analysis identifies **footfall (customer traffic)** as the single most important driver of monthly sales, followed by **marketing spend**, **inventory availability**, and **customer ratings**. The final multiple regression model explains **83.2% of sales variation**, providing a robust evidence base for leadership decisions.

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

| Rank | Factor | Association | Confidence |
|---|---|---|---|
| 1 | **Footfall** | Very strong positive | Very high (p < 0.001) |
| 2 | **Marketing spend** | Positive (£1.20 per £1 invested) | Very high (p < 0.001) |
| 3 | **Inventory availability** | Meaningful positive | High (p < 0.001) |
| 4 | **Customer rating** | Positive | High (p = 0.005) |
| 5 | **Region (South/West vs East)** | ~£18K+ advantage for South/West | High (p < 0.01) |
| 6 | **Store type (Residential vs Airport)** | ~£42K disadvantage for Residential | Very high (p < 0.001) |

---

## Factors Leadership Should Focus On

### 1. Drive Footfall — The Dominant Lever
Every additional visitor is associated with approximately **£34 in monthly sales**. Footfall explains 78% of sales variation on its own. Actions to consider:
- Invest in local area marketing, events, and promotions that attract foot traffic
- Review opening hours, accessibility, and signage
- Explore loyalty programmes that encourage repeat visits

### 2. Optimise Marketing Spend — Positive ROI Confirmed
Every £1 invested in marketing is associated with **£1.20 in incremental sales**. This is a conservative return that strengthens when combined with other improvements. Actions to consider:
- Avoid cutting marketing budgets at underperforming stores — the data suggests this would reduce sales further
- Test increasing budgets at stores with high footfall potential to maximise returns

### 3. Improve Inventory Availability — Operational Quick Win
Each 1 percentage point improvement in inventory availability is associated with approximately **£3,000 in monthly sales**. Actions to consider:
- Prioritise restocking at stores with below-average inventory availability scores
- Review supply chain lead times and reorder triggers
- Share best-practice inventory management from high-performing stores

### 4. Invest in Customer Experience
A 1-point improvement in customer rating is associated with **£13,630 more in monthly sales**. Actions to consider:
- Invest in staff training, especially in stores with ratings below 3.5
- Review store layout, queuing, and checkout experience
- Act on customer feedback systematically

### 5. Investigate Regional Performance
South and West region stores outperform East stores by approximately **£18–19K per month**, even after controlling for other factors. Leadership should investigate:
- What regional conditions, demographic profiles, or competitive environments favour South/West stores?
- Are there operational practices in South/West that can be transferred to East and North?

---

## Variables That Should NOT Be Over-Interpreted

### avg_discount_pct — Do Not Use to Drive Sales
Discounting is **not statistically significant** in the full model (p = 0.211). In simple regression it is significant but explains less than 2% of variation with a negative direction. This strongly suggests that:
- Discounting is not an effective lever for increasing sales
- Stores running more promotions may already be underperforming (reverse causation)
- **Leadership should not increase discounting to drive sales** — the evidence does not support this strategy

### competitor_distance_km — Not Included
This variable had missing values and showed no strong signal in exploratory analysis. It was not selected for the final model. Competitive effects may be real but are not captured reliably in this dataset.

### monthly_profit — Not a Predictor
Monthly profit is an outcome variable correlated with sales. It should not be used as a predictor and is excluded from all models.

---

## Recommended Business Actions

| Priority | Action | Expected Impact | Based On |
|---|---|---|---|
| 🔴 High | Increase footfall through local events, signage, loyalty programmes | Highest ROI lever | Footfall coef: £34/visitor |
| 🔴 High | Maintain or increase marketing spend | £1.20 return per £1 invested | Marketing coef: 1.20, p<0.001 |
| 🟡 Medium | Improve inventory availability across all stores | ~£3,000 per % point improvement | Inventory coef: £3,002, p<0.001 |
| 🟡 Medium | Invest in customer experience (staff training, layout) | ~£13,600 per rating point | Rating coef: £13,630, p=0.005 |
| 🟢 Strategic | Investigate why South/West outperform; replicate best practices | Up to £18-19K monthly per store | Regional dummies significant |
| 🟢 Strategic | Review Residential store model — significantly lower baseline | £42K monthly gap vs Airport | type_Residential coef: −£41,880 |
| ❌ Do not pursue | Increase average discounting to drive sales | No evidence of positive effect | avg_discount p=0.211 in full model |

---

## Risks and Limitations Leadership Should Keep in Mind

### 1. This Dataset Covers Only 4 Months
The data spans January to April 2025. Seasonal patterns are not fully captured. Sales patterns in summer, back-to-school, and festive periods may be significantly different. Regression results should be validated against a full year of data.

### 2. Only 320 Observations Across 80 Stores
The dataset has 80 unique stores observed across 4 months. This limits statistical power and may not represent the full diversity of store conditions.

### 3. The Model Explains Correlation, Not Causation
Regression identifies associations — it does not prove that increasing marketing spend *causes* higher sales. For example:
- Stores that invest more in marketing may already have better management, better locations, or better products
- Footfall drives sales — but what drives footfall? This is a separate question the model does not answer
- Improvements to customer ratings may take months to affect sales

**Leadership should treat regression results as directional evidence to prioritise investigation, not as guaranteed cause-and-effect mechanisms.**

### 4. The Model Assumes Linear Relationships
The model assumes that each unit increase in a predictor has the same effect on sales regardless of the starting level. In reality, returns may diminish at high levels (e.g., doubling marketing spend from £100K to £200K may not yield the same return as doubling from £10K to £20K).

### 5. Store-Level and Manager-Level Factors Are Not Measured
The model cannot capture the impact of individual store managers, staff quality, local catchment demographics, or parking availability — all of which are likely to influence sales.

### 6. Dummy Variables Capture Averages, Not Individual Stores
The regional and store-type dummies represent group-level averages. Individual stores within a group vary significantly, as evidenced by the residual analysis. The model's prediction for any single store may be inaccurate by £90,000–£160,000 in extreme cases.

---

## Why Regression Shows Association but Not Causation

Regression measures **statistical correlation** — the degree to which one variable tends to move with another. It does not, by itself, establish that changes in variable X *cause* changes in variable Y. Several reasons why:

1. **Reverse causation**: High-sales stores may attract higher marketing budgets — not the other way around.
2. **Confounding variables**: A third factor (e.g., local population density) could drive both marketing spend and sales simultaneously.
3. **Selection effects**: Airport stores may attract higher-spending customers regardless of the store's own actions.
4. **Temporal lag**: The impact of marketing or inventory improvements may appear in future months, not the same month they are measured.

To establish true causation, leadership would need to conduct **controlled experiments** — for example, randomly assigning stores to different marketing budget levels and measuring outcomes over time.

---

*This recommendation is supported by the multiple regression model (R² = 0.8321) detailed in `analysis/regression_workbook.xlsx` and `outputs/model_equations.md`.*
