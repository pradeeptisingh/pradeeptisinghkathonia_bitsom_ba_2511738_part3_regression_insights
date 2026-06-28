# Model Comparison Report

## Overview

This document compares all regression models built to understand the drivers of `monthly_sales` at the retail chain. Five simple regression models and one multiple regression model were developed.

---

## Model Comparison Table

| Model | Type | Variables Used | R-Squared | Significant Variables | Business Usefulness | Limitations |
|---|---|---|---|---|---|---|
| Model 1 | Simple | marketing_spend | 0.2318 | marketing_spend (p<0.001) | Useful baseline — confirms marketing ROI | Single driver; ignores footfall, inventory |
| Model 2 | Simple | footfall | 0.7832 | footfall (p<0.001) | Very strong single predictor | Does not explain what drives footfall |
| Model 3 | Simple | avg_discount_pct | 0.0163 | avg_discount_pct (p=0.022) | Very weak — discounting alone explains very little | Likely spurious or complex relationship |
| Model 4 | Simple | inventory_availability_pct | 0.1187 | inventory_availability_pct (p<0.001) | Moderate — inventory matters but needs context | R² is low; many other variables needed |
| Model 5 | Simple | customer_rating | 0.1023 | customer_rating (p<0.001) | Moderate — satisfaction is linked to sales | Cannot act on this easily in isolation |
| **Model 6 ★** | **Multiple** | **footfall, marketing_spend, avg_discount_pct, inventory_availability_pct, customer_rating, region dummies (North/South/West vs East), store_type dummies (High Street/Mall/Residential vs Airport)** | **0.8321** | **footfall, marketing_spend, inventory_availability_pct, customer_rating, region_South, region_West, type_Residential** | **BEST MODEL: Explains 83.2% of sales variance; captures store-level, regional, and operational drivers** | Assumes linear relationships; limited to 4 months of data |

---

## Detailed Analysis by Model

### Model 1: Simple Regression — marketing_spend

- **Equation**: monthly_sales = 568,428 + 1.64 × marketing_spend
- **R²**: 0.2318
- **P-value**: < 0.001
- **Interpretation**: Marketing spend explains 23% of sales variation. For every £1 increase in marketing spend, sales increase by approximately £1.64. Statistically significant but limited as a standalone model.
- **Business Usefulness**: Confirms that marketing investment has a positive return, but is not sufficient as the only lever.

### Model 2: Simple Regression — footfall

- **Equation**: monthly_sales = 62,414 + 34.04 × footfall
- **R²**: 0.7832
- **P-value**: < 0.001
- **Interpretation**: Footfall alone explains 78% of sales variation — the strongest single predictor by far. Each additional visitor is associated with £34 more in monthly sales.
- **Business Usefulness**: Driving store traffic is the single most impactful lever visible in this dataset.

### Model 3: Simple Regression — avg_discount_pct

- **R²**: 0.0163
- **P-value**: 0.022
- **Interpretation**: Discounting is technically significant but explains less than 2% of sales variation. The negative coefficient suggests higher discounting is associated with lower sales — possibly because stores running heavy promotions are already underperforming.
- **Business Usefulness**: Very limited as a standalone driver. Should not be interpreted in isolation.

### Model 4: Simple Regression — inventory_availability_pct

- **R²**: 0.1187
- **P-value**: < 0.001
- **Interpretation**: Stock availability explains 12% of variation. Stores with better inventory availability achieve higher sales. Each percentage point increase is associated with approximately £3,000 more in monthly sales.
- **Business Usefulness**: Operationally actionable — improving stock levels should boost sales.

### Model 5: Simple Regression — customer_rating

- **R²**: 0.1023
- **P-value**: < 0.001
- **Interpretation**: Customer satisfaction explains about 10% of variation. Higher-rated stores tend to sell more.
- **Business Usefulness**: A useful signal but difficult to action quickly. Likely reflects overall store quality.

### Model 6: Multiple Regression (Final Model ★)

- **R²**: 0.8321 | **Adj. R²**: 0.8262
- **Significant predictors**: footfall, marketing_spend, inventory_availability_pct, customer_rating, region_South, region_West, type_Residential
- **Interpretation**: Together, 11 predictors explain 83% of monthly sales variation. Footfall and marketing spend are the dominant drivers. Regional effects reveal that South and West stores outperform East stores even after controlling for other factors. Residential stores significantly underperform Airport stores.
- **Business Usefulness**: This is the most useful model for leadership — it identifies actionable levers across marketing, operations, and strategy.

---

## Summary Recommendation

**Model 6 (Multiple Regression) is the recommended model.** Simple models are useful for initial insights but dramatically underfit the data. The multiple regression model captures the interplay between footfall, marketing, inventory, customer experience, and store characteristics — providing leadership with a holistic view of what drives sales performance.

---

*See also: `outputs/regression_summary.xlsx` for a tabular model comparison.*
