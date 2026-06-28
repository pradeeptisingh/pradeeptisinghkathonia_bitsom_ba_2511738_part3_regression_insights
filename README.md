# Part 3: Regression Insights — Retail Chain Sales Analysis

## Business Problem Summary

A retail chain operating across four UK regions and four store formats wants to understand what factors drive monthly sales performance. Leadership is considering actions such as increasing marketing spend, improving inventory availability, adjusting discounting strategy, reallocating staff, and prioritising certain store types or regions. Regression analysis is used to identify which factors are most strongly associated with monthly sales and to quantify their relationship.

---

## Dataset Description

**File**: `data/business_regression_data.xlsx`  
**Records**: 320 (80 stores × 4 months: January–April 2025)  
**Source**: Provided dataset

### Variables

| Column | Type | Role | Description |
|---|---|---|---|
| store_id | Categorical (ID) | Identifier | Unique store identifier |
| month | Date | Time dimension | Month of observation |
| region | Categorical | Independent | East, West, North, South |
| store_type | Categorical | Independent | Airport, High Street, Mall, Residential |
| marketing_spend | Numerical | Independent | Monthly marketing expenditure (£) |
| footfall | Numerical | Independent | Monthly store visitors (count) |
| avg_discount_pct | Numerical | Independent | Average discount percentage applied |
| staff_count | Numerical | Not used | Number of staff (not significant) |
| inventory_availability_pct | Numerical | Independent | % of SKUs in stock |
| competitor_distance_km | Numerical | Not used | Distance to nearest competitor (6 nulls; weak signal) |
| holiday_flag | Binary | Not used | Whether month contains a holiday |
| customer_rating | Numerical | Independent | Average customer rating (out of 5; 8 nulls imputed) |
| monthly_sales | Numerical | **Dependent** | Total monthly revenue (£) — TARGET VARIABLE |
| monthly_profit | Numerical | Not used | Outcome variable; excluded to avoid data leakage |

### Data Quality Issues Addressed

- `competitor_distance_km`: 6 missing values → imputed with column median
- `customer_rating`: 8 missing values → imputed with column median
- No other missing values or obvious data quality issues

---

## Regression Approach

### Simple Regression Models (5 models)
Each uses `monthly_sales` as the dependent variable and one numerical predictor at a time:
1. marketing_spend
2. footfall
3. avg_discount_pct
4. inventory_availability_pct
5. customer_rating

### Multiple Regression Model (Final Model)
Combines all five numerical predictors plus dummy variables for `region` and `store_type`.

**Software**: Python (statsmodels OLS), results exported to Excel workbook.

---

## Dummy Variable Approach

| Variable | Reference Category | Dummy Columns Created |
|---|---|---|
| region | East (largest group) | region_North, region_South, region_West |
| store_type | Airport (distinctive benchmark) | type_High Street, type_Mall, type_Residential |

The reference category is the baseline against which all other groups are compared. Dropping one category per variable prevents the dummy variable trap (perfect multicollinearity).

---

## Model Comparison Summary

| Model | Variables | R² | Status |
|---|---|---|---|
| Model 1 | marketing_spend | 0.2318 | Simple baseline |
| Model 2 | footfall | 0.7832 | Best simple model |
| Model 3 | avg_discount_pct | 0.0163 | Weak |
| Model 4 | inventory_availability_pct | 0.1187 | Moderate |
| Model 5 | customer_rating | 0.1023 | Moderate |
| **Model 6** | **All 5 numerics + dummies** | **0.8321** | **✓ Final Model** |

---

## Final Model Selected

**Model 6 — Multiple Linear Regression**

Chosen because:
- R² of 0.8321 (83.2% of sales variation explained)
- Statistically significant coefficients for: footfall, marketing_spend, inventory_availability_pct, customer_rating, region_South, region_West, type_Residential
- Provides actionable, multi-dimensional view of sales drivers

### Final Model Equation

```
monthly_sales = 91,790
    + 1.20 × marketing_spend
    + 34.00 × footfall
    − 45,710 × avg_discount_pct (not significant in full model)
    + 3,002 × inventory_availability_pct
    + 13,630 × customer_rating
    + 6,185 × region_North (not significant)
    + 18,690 × region_South
    + 18,110 × region_West
    − 23,790 × type_High Street
    − 12,790 × type_Mall (not significant)
    − 41,880 × type_Residential
```

---

## Business Recommendation

1. **Prioritise footfall growth** — every additional visitor is worth ~£34 in monthly sales
2. **Maintain and increase marketing spend** — £1.20 return per £1 invested
3. **Improve inventory availability** — each percentage point improvement yields ~£3,000 in sales
4. **Invest in customer experience** — higher satisfaction scores are associated with significantly higher revenue
5. **Do not increase discounting** — no evidence that avg_discount_pct drives sales
6. **Investigate South/West outperformance** — regional best practices should be identified and shared

See `outputs/final_recommendation.md` for the full strategic recommendation.

---

## Assumptions and Limitations

- The dataset covers only 4 months; seasonal patterns are not captured
- Regression identifies correlation, not causation — controlled experiments are needed to confirm causal relationships
- The model assumes linear relationships between all variables and monthly sales
- Individual store performance varies significantly; the model provides group-level averages
- Staff count, holiday flag, and competitor distance were not significant predictors and were excluded from the final model
- Missing values were imputed using medians — a simple approach that may introduce small biases

---

## Screenshots Included

| Screenshot | Description |
|---|---|
| `screenshots/simple_regression_output.png`  |
| `screenshots/multiple_regression_output.png` |
| `screenshots/residuals_preview.png` |
| `screenshots/model_comparison_preview.png` | 
