# Model Equations

## Dummy Variable Approach

### What are Dummy Variables?

Categorical variables like `region` and `store_type` cannot be directly entered into a regression model as text values. Dummy variables convert each category into a binary (0 or 1) column, allowing the model to measure the sales impact of belonging to each category.

### Reference Categories

To avoid the **dummy variable trap** (perfect multicollinearity), one category per variable is dropped and used as the **reference group**. All coefficients are interpreted relative to this reference group.

| Variable | Reference Category | Reason for Choice |
|---|---|---|
| `region` | East | Largest region group (104 observations) |
| `store_type` | Airport | Distinctive location type; useful benchmark |

### Dummy Variables Created

**Region dummies** (reference = East):

| Dummy Column | Value = 1 When | Value = 0 When |
|---|---|---|
| region_North | Store is in North | Store is not in North |
| region_South | Store is in South | Store is not in South |
| region_West | Store is in West | Store is not in West |

**Store type dummies** (reference = Airport):

| Dummy Column | Value = 1 When | Value = 0 When |
|---|---|---|
| type_High Street | Store is High Street | Store is not High Street |
| type_Mall | Store is Mall | Store is not Mall |
| type_Residential | Store is Residential | Store is not Residential |

---

## Simple Regression Equations

Each model uses `monthly_sales` as the dependent variable (Y) and a single numerical predictor.

### Model 1: marketing_spend

```
monthly_sales = 568,428 + 1.64 × marketing_spend
```

- **Intercept**: £568,428 — estimated baseline sales with zero marketing spend
- **Coefficient (1.64)**: For each additional £1 of marketing spend, monthly sales are expected to increase by £1.64
- **R²**: 0.2318 — marketing spend alone explains 23% of sales variation
- **P-value**: < 0.001 — statistically significant

**Business reading**: There is a positive return on marketing investment. However, this model alone is insufficient — 77% of sales variation is unexplained.

---

### Model 2: footfall

```
monthly_sales = 62,414 + 34.04 × footfall
```

- **Intercept**: £62,414 — estimated sales if footfall is zero (theoretical baseline)
- **Coefficient (34.04)**: Each additional visitor is associated with approximately £34 more in monthly sales
- **R²**: 0.7832 — footfall alone explains 78% of sales variation
- **P-value**: < 0.001 — highly significant

**Business reading**: Driving more customers into stores is the single most powerful lever for sales growth visible in this dataset.

---

### Model 3: avg_discount_pct

```
monthly_sales = 703,218 − 1,118 × avg_discount_pct
```

- **Coefficient (−1,118)**: A 1 percentage point increase in average discount is associated with £1,118 lower sales
- **R²**: 0.0163 — explains less than 2% of variation
- **P-value**: 0.022 — technically significant but practically weak

**Business reading**: Discounting does not appear to drive sales. This could indicate that stores run more promotions when sales are already weak (reverse causation).

---

### Model 4: inventory_availability_pct

```
monthly_sales = 348,214 + 3,303 × inventory_availability_pct
```

- **Coefficient (3,303)**: Each additional percentage point of stock availability is associated with £3,303 more in monthly sales
- **R²**: 0.1187 — explains 12% of variation
- **P-value**: < 0.001 — significant

**Business reading**: Ensuring products are in stock drives meaningful sales uplift. Inventory management is an actionable operational lever.

---

### Model 5: customer_rating

```
monthly_sales = 435,126 + 43,572 × customer_rating
```

- **Coefficient (43,572)**: Each 1-point improvement in customer rating (on a 5-point scale) is associated with £43,572 higher monthly sales
- **R²**: 0.1023 — explains 10% of variation
- **P-value**: < 0.001 — significant

**Business reading**: Customer satisfaction is meaningfully associated with sales, but causation is unclear — high-performing stores may naturally generate better reviews.

---

## Multiple Regression Equation (Final Model ★)

```
monthly_sales = 91,790
    + 1.20 × marketing_spend
    + 34.00 × footfall
    − 45,710 × avg_discount_pct
    + 3,002 × inventory_availability_pct
    + 13,630 × customer_rating
    + 6,185 × region_North
    + 18,690 × region_South
    + 18,110 × region_West
    − 23,790 × type_High Street
    − 12,790 × type_Mall
    − 41,880 × type_Residential
```

### Coefficient Explanations

| Variable | Coefficient | P-Value | Significant? | Business Meaning |
|---|---|---|---|---|
| Intercept | £91,790 | 0.055 | Marginal | Baseline when all variables = 0 (theoretical only) |
| marketing_spend | £1.20 | < 0.001 | **Yes** | Each £1 extra marketing → £1.20 in sales |
| footfall | £34.00 | < 0.001 | **Yes** | Each extra visitor → £34 in sales (dominant driver) |
| avg_discount_pct | −£45,710 | 0.211 | No | Discounting not a significant predictor in full model |
| inventory_availability_pct | £3,002 | < 0.001 | **Yes** | Better stock availability → higher sales |
| customer_rating | £13,630 | 0.005 | **Yes** | Higher satisfaction scores → significantly more sales |
| region_North | £6,185 | 0.380 | No | North vs East — no significant difference |
| region_South | £18,690 | 0.009 | **Yes** | South stores outperform East by ~£18.7K per month |
| region_West | £18,110 | 0.004 | **Yes** | West stores outperform East by ~£18.1K per month |
| type_High Street | −£23,790 | 0.011 | **Yes** | High Street underperforms Airport by ~£23.8K per month |
| type_Mall | −£12,790 | 0.187 | No | Mall vs Airport — not statistically significant |
| type_Residential | −£41,880 | < 0.001 | **Yes** | Residential underperforms Airport by ~£41.9K per month |

---

## Final Model Selected

**Model 6 (Multiple Regression)** is selected as the final model.

**Reason**:
- R² of 0.8321 vs best simple model (footfall) R² of 0.7832
- Captures multiple actionable business drivers simultaneously
- Includes both operational variables (marketing, footfall, inventory) and strategic variables (region, store type)
- All key variables are statistically significant
- Provides specific, quantified guidance for business decisions
