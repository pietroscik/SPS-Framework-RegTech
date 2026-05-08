# 📊 SPS FRAMEWORK - FINAL SUBMISSION REPORT
**Innovation Data Challenge 2026 - NayaOne Sandbox**
**Candidate:** Pietro Maietta (ID: 0273000007)
**Institution:** University of Naples "Parthenope"

---

## 1. Executive Summary

The project presents a "Bi-Focal" supervisory framework (SPS - Supervisory Prioritisation Score) that integrates **technical risk** (DORA) and **social risk** (PSD2). The execution is based on a two-stage complementary architecture:
1.  **Actuarial Diagnosis (Notebook V2):** Empirical validation of assumptions on raw data to justify modeling choices.
2.  **Operational Pipeline (Master Notebook):** Execution of the complete model with data imputation, AutoML, and Time-Series forecasting.

---

## 2. Part 1: Diagnostic Analysis (Notebook V2)

The `V2 - ACTUARIAL APPROACH` notebook analyzed raw data *without imputation* to identify structural biases in the dataset and demonstrate the need for advanced statistical techniques.

### 🔍 Key Empirical Evidence
| Detected Phenomenon | Statistical Evidence | Implication for the Model |
|-------------------|---------------------|-----------------------------|
| **"Small Numbers" Effect** | Exploded variance for PSPs with <1000 tx (Funnel Plot) | Adoption of **Credibility Theory** (Bühlmann) to stabilize scores for small operators. |
| **Extreme Sparsity** | **93.8%** of hourly windows have ≤3 transactions | Need for hourly aggregation + 24h rolling windows (instead of pure real-time). |
| **Social Dependence** | Positive correlation between ADZ (Rural) and Fragility | Social risk requires an interaction term (not linear sum) between geography and user profile. |

> **Methodological Note:** In this phase, data imputation was *not* applied to preserve visibility of data quality issues (e.g., 34.19% missing latency).

---

## 3. Part 2: Operational Execution (Master Notebook)

The `MASTER EXECUTION NOTEBOOK` implements the production pipeline, applying corrections justified by phase V2 and generating final outputs.

### 🛠️ Data Engineering & Imputation
- **Dataset:** 414,108 transactions (January 2024) across 698 PSPs.
- **Imputation:** Applied to **34.19%** of missing values on `processing_time_ms`.
- **Method:** Median conditioned on payment instrument (Chi-Square Test confirms MCAR - Missing Completely At Random).

### 🤖 AutoML Optimization (Stage V3)
Genetic optimization calibrated SPS Score weights to maximize discriminative capacity:
- **Alpha (Tech Risk):** 0.2404
- **Beta (Social Risk):** 0.2404
- **Ratio:** 1.00:1 (Perfect Bi-Focal Balance)
- **Result:** The model confirms that technical and social risks are equally relevant for systemic stability in the NayaOne dataset.

### 🏆 Vigilance Matrix (Final Classification)
The 698 PSPs were classified into 4 action quadrants based on SPS and NCR scores:

| Class | PSP | % | Supervisory Action |
|--------|-----|---|--------------------|
| **🔴 CRITICAL_FAILURE** | **201** | **28.8%** | Immediate DORA inspection (Unstable Hubs) |
| **🟠 SOCIAL_RISK** | **167** | **23.9%** | PSD2 inclusion audit (Fragile rural zones) |
| **🟡 SYSTEMIC_WATCH** | **159** | **22.8%** | Continuous monitoring (Stress test) |
| **🟢 STANDARD** | **171** | **24.5%** | Standard reporting |

### 📈 Dual Time-Series Architecture
The framework covers the entire temporal spectrum required by supervision:
1.  **Phase 7 - ARIMA (Hourly):** 744 hourly periods. Detects operational micro-shocks (24-48h) for Early Warning.
2.  **Phase 8 - SARIMA (Monthly):** 12 monthly periods. Validates structural stability and absence of critical seasonal trends.

---

## 4. Conclusions

The SPS framework demonstrates statistical robustness and operational relevance. The strategic separation between **diagnosis (V2)** and **production (Master)** ensures methodological transparency, while the hybrid temporal architecture offers Supervisory Authorities a complete predictive tool, capable of transitioning from real-time monitoring to annual strategic planning.

**Status:** ✅ READY FOR DEPLOYMENT

© 2026 Pietro Maietta. Tutti i diritti riservati. Documentazione tecnica depositata presso Canale Fintech - Banca d'Italia (Rif. Invio Maggio 2026).
