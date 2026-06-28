# Residual Analysis

## Overview

This document analyses the residuals from the final multiple regression model (Model 6). Residuals are calculated as:

**Residual = Actual Monthly Sales − Predicted Monthly Sales**

A positive residual means the store performed **better than the model predicted** (under-prediction).  
A negative residual means the store performed **worse than the model predicted** (over-prediction).

---

## Residual Statistics

| Metric | Value |
|---|---|
| Mean Residual | ~£0 (by construction of OLS) |
| Std Dev of Residuals | ~£42,700 |
| Min Residual | −£159,513 |
| Max Residual | +£112,751 |
| Model R² | 0.8321 |

---

## Top 5 Largest Positive Residuals (Model Under-Predicted)

These stores significantly **outperformed** what the model expected, given their characteristics.

| Store ID | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|
| STR-1028 | East | Mall | £713,611 | £600,860 | **+£112,751** |
| STR-1073 | East | Residential | £813,317 | £707,150 | **+£106,167** |
| STR-1019 | East | Residential | £788,088 | £695,490 | **+£92,597** |
| STR-1069 | West | High Street | £686,738 | £595,018 | **+£91,720** |
| STR-1050 | North | Residential | £735,787 | £646,314 | **+£89,472** |

### Business Interpretation of Positive Residuals

These stores are **exceptional performers** relative to their peer group. Their outperformance likely reflects factors not captured in the model, such as:

- **Local catchment quality**: The area may have above-average population density or purchasing power.
- **Strong store management**: Leadership, staff culture, or execution may be unusually effective.
- **Unique product mix**: The store may stock premium or locally popular items.
- **Loyalty effects**: Long-established stores may have a loyal customer base not visible in the current data.

**Recommendation**: These stores should be studied as **best practice examples**. Leadership should investigate what these stores are doing differently to replicate success elsewhere.

---

## Top 5 Largest Negative Residuals (Model Over-Predicted)

These stores significantly **underperformed** what the model expected.

| Store ID | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|
| STR-1017 | West | High Street | £685,379 | £844,892 | **−£159,513** |
| STR-1023 | South | Mall | £627,172 | £773,115 | **−£145,943** |
| STR-1012 | West | Residential | £595,468 | £715,299 | **−£119,831** |
| STR-1007 | West | Mall | £800,452 | £913,151 | **−£112,699** |
| STR-1014 | West | High Street | £463,534 | £563,493 | **−£99,958** |

### Business Interpretation of Negative Residuals

These stores are **underperforming** relative to what their inputs (footfall, marketing spend, etc.) would predict. Possible explanations include:

- **Execution gaps**: Poor customer service, low staff effectiveness, or inefficient store layout.
- **Local competition**: A strong nearby competitor not captured by `competitor_distance_km`.
- **Product-market mismatch**: The product range may not suit the local customer profile.
- **External factors**: Roadworks, construction, or accessibility issues near the store.
- **Data quality**: Footfall or marketing spend may be recorded inconsistently.

**Recommendation**: STR-1017 (West, High Street) and STR-1023 (South, Mall) are priority stores for investigation. Given their potential (per the model), targeted intervention could recover significant revenue.

---

## Pattern Analysis

### Regional Pattern
Three of the five most negative residuals are in the **West region**. Despite West region stores having a positive regional coefficient in the model, specific West stores are underperforming. This may indicate localised issues (competitive pressure, operational inconsistencies) within the West.

### Store Type Pattern
Residential and High Street stores appear in both tails, suggesting high variability within these categories. The model uses a single dummy variable per store type; in reality, individual store characteristics vary widely.

---

## Assessment: Under-prediction vs Over-prediction

The model does not systematically over- or under-predict for specific groups. However:

- **Airport stores** (reference category) had the fewest extreme residuals — the model fits them well.
- **West region** stores show a cluster of negative residuals, suggesting the West dummy captures an average effect but misses store-level heterogeneity.
- **Residential stores** show large residuals in both directions — the model's single dummy coefficient is too coarse for this category.

---

## Conclusion

The residual distribution is approximately symmetric around zero (as expected for OLS), confirming the model has no systematic bias. The outlier stores — both positive and negative — represent real business opportunities: either to learn from exceptional performers or to intervene in underperforming ones.

*See also: `screenshots/residuals_preview.png` for visual residual output.*
