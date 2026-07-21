# Decision Log — HR Attrition Analysis Project

**Status:** Living document, consistent with Master Summary (Frozen v1.0). In case of conflict, the Master Summary takes precedence.
**Scope:** Records only approved, finalized decisions. Rejected alternatives, draft discussions, and review comments are intentionally excluded.

---

## Phase 1 — Business Understanding

| Field | Detail |
|---|---|
| **Decision ID** | D1.1 |
| **Phase** | 1 |
| **Decision** | "Early attrition" is operationally defined as `YearsAtCompany ≤ 1`. |
| **Reason** | Dataset has no hire/exit dates, only a tenure-in-years snapshot; a fixed threshold is required to operationalize the business question. |
| **Impact** | Governs every subsequent New Hire segmentation, hypothesis test, and model evaluation subgroup. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D1.2 |
| **Phase** | 1 |
| **Decision** | Project outcome sequence fixed as Diagnostic → Predictive → Prescriptive. |
| **Reason** | Stakeholder requirement; determines phase ordering and depth of investment in each analysis type. |
| **Impact** | Diagnostic (Phases 6-9) intentionally precedes and outweighs Predictive (Phase 10); Prescriptive (Phase 11) depends on both. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D1.3 |
| **Phase** | 1 |
| **Decision** | "Valuable employee" has no direct measure in the dataset; this is recorded as a dataset limitation, not a business limitation. |
| **Reason** | No 360-review, manager qualitative rating, or productivity measure exists in the data. |
| **Impact** | Forces a proxy-based approach, finalized in Phase 8 (D8.5). |
| **Status** | Approved |

---

## Phase 2 — Business Questions

| Field | Detail |
|---|---|
| **Decision ID** | D2.1 |
| **Phase** | 2 |
| **Decision** | Final Business Question set locked across Descriptive (D0–D4), Diagnostic (G1–G4, G7, G8), Predictive (P1), and Prescriptive (S1–S3) categories. |
| **Reason** | Each question maps to a specific analysis step and prevents unfocused exploration. |
| **Impact** | All later phases (EDA, Hypothesis Testing, Modeling, Feature Engineering) are scoped strictly to this list. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D2.2 |
| **Phase** | 2 |
| **Decision** | A question that cannot be answered with current data is marked "insufficient data" and retained — never deleted for that reason alone. |
| **Reason** | Prevents silently narrowing project scope to fit data availability (streetlight-effect bias). |
| **Impact** | S1 and S3 remain in scope through Phase 10 despite lacking cost data. |
| **Status** | Approved |

---

## Phase 3 — Data Requirement

| Field | Detail |
|---|---|
| **Decision ID** | D3.1 |
| **Phase** | 3 |
| **Decision** | Business-required data listed independently of dataset availability, including Attrition Event detail (voluntary/involuntary + dates), evaluation dates, Data Dictionary/HR Policy, and a grouped "Historical Employee Timeline." |
| **Reason** | Avoids bias from designing requirements around what the dataset already contains. |
| **Impact** | Forms the baseline against which Phase 4 measures actual data coverage and gaps. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D3.2 |
| **Phase** | 3 |
| **Decision** | Historical Employee Timeline is rated "Critical for answering temporal/causal business questions (Early Attrition, Root Cause), but not required for descriptive metrics." |
| **Reason** | Descriptive metrics can be computed from a single snapshot; temporal/causal claims cannot. |
| **Impact** | Sets expectation that Diagnostic conclusions (G-series) will remain correlational, not causal. |
| **Status** | Approved |

---

## Phase 4 — Dataset Discovery

| Field | Detail |
|---|---|
| **Decision ID** | D4.1 |
| **Phase** | 4 |
| **Decision** | Each Business Question is individually classified as Answerable / Answerable with caveats / Insufficient data, rather than issuing one blanket "dataset is/isn't sufficient" verdict. |
| **Reason** | A single overall verdict would obscure which specific conclusions are trustworthy. |
| **Impact** | S1, S3 = insufficient data; G2, G7, P1 = answerable with caveats; D0–D4, G1, G3, G4, G8 = answerable. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D4.2 |
| **Phase** | 4 |
| **Decision** | Representativeness of the dataset for any target population is undeterminable, since no sampling frame information exists. |
| **Reason** | Cannot assess how the 1470 employees were selected or what population they represent. |
| **Impact** | All conclusions are scoped to "within this dataset" only; no generalization claim is permitted. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D4.3 |
| **Phase** | 4 |
| **Decision** | Risk Register (R1–R7) formally adopted, covering mixed attrition types, no Exit Interview, low-variance PerformanceRating, small subgroup sample, no Data Dictionary, unknown representativeness, and missing cost data. |
| **Reason** | Consolidates known data risks into a single reference before proceeding to negotiation and analysis. |
| **Impact** | Each risk's mitigation is tracked and resolved (or explicitly accepted) in later phases. |
| **Status** | Approved |

---

## Phase 5 — Stakeholder Negotiation

| Field | Detail |
|---|---|
| **Decision ID** | D5.1 |
| **Phase** | 5 |
| **Decision** | Attrition analysis proceeds on the combined voluntary/involuntary pool, with a mandatory disclaimer on every Attrition-related conclusion. |
| **Reason** | No data field distinguishes attrition type; pausing the project to source it was rejected. |
| **Impact** | All Diagnostic/Predictive conclusions carry a standing disclaimer (see "Standing Disclaimers" below). |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D5.2 |
| **Phase** | 5 |
| **Decision** | S1/S3 (cost/ROI questions) are reframed from "produce a real ROI figure" to "present an ROI framework plus the list of business inputs required." Any illustrative numbers are confined to an Appendix, explicitly labeled "illustrative, not actual." |
| **Reason** | Prevents a placeholder number from being mistaken for a real figure and misused in an actual investment decision. |
| **Impact** | Phase 11 recommendations must not present computed ROI as fact. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D5.3 |
| **Phase** | 5 |
| **Decision** | No additional data collection (Exit Interview, Data Dictionary, cost data) is pursued; project proceeds with documented correlational limitations instead. |
| **Reason** | Simulated stakeholder accepted the trade-off rather than delaying the project indefinitely. |
| **Impact** | All causal-sounding claims are restricted to "associated with" language throughout. |
| **Status** | Approved |

---

## Phase 6 — Data Quality Assessment

| Field | Detail |
|---|---|
| **Decision ID** | D6.1 |
| **Phase** | 6 |
| **Decision** | Constant columns (`EmployeeCount`, `StandardHours`, `Over18`) are excluded from analysis scope (not deleted from the dataset). |
| **Reason** | They carry no variance and answer no Business Question. |
| **Impact** | Simplifies later EDA/Feature Engineering without loss of information. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D6.2 |
| **Phase** | 6 |
| **Decision** | PerformanceRating's low variance and near-zero correlation with JobLevel/MonthlyIncome are recorded neutrally; no conclusion is drawn about its role in the "value" proxy until Phase 7 tests its discriminative power directly. |
| **Reason** | Correlation with other proxy components does not, by itself, prove or disprove predictive relevance to Attrition. |
| **Impact** | Final proxy formula decision deferred to Phase 8, informed by Phase 7 evidence. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D6.3 |
| **Phase** | 6 |
| **Decision** | Multicollinearity among JobLevel, MonthlyIncome, TotalWorkingYears, and Age (r=0.68–0.95) is logged as a risk only; feature-selection action is deferred to Phase 8/9. |
| **Reason** | Phase 6 assesses data trustworthiness, not feature/model design. |
| **Impact** | Directly resolved in Phase 8 (Organizational Investment Segment uses JobLevel alone; see D8.5). |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D6.4 |
| **Phase** | 6 |
| **Decision** | Class imbalance (16.1% Attrition=Yes) is flagged to prohibit Accuracy-only evaluation in later modeling. |
| **Reason** | A model predicting "No" for everyone would already reach 84% accuracy without any predictive value. |
| **Impact** | Phase 10 evaluates models using ROC-AUC, PR-AUC, Precision/Recall/F1, and Brier Score instead. |
| **Status** | Approved |

---

## Phase 7 — Exploratory Data Analysis

| Field | Detail |
|---|---|
| **Decision ID** | D7.1 |
| **Phase** | 7 |
| **Decision** | D0 confirmed: Attrition rate declines monotonically with tenure (34.9% at ≤1yr down to 8.1% at 11+yr); the Phase 1 "early attrition" framing is supported by the data. |
| **Reason** | Direct descriptive evidence across five tenure buckets. |
| **Impact** | Validates continuing the project on its original premise. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D7.2 |
| **Phase** | 7 |
| **Decision** | Every EDA insight is checked against at least one alternative explanation using available data (e.g., OverTime effect checked against JobRole/Department confound; pay gap checked against a general "newness" effect) before being carried forward. |
| **Reason** | Prevents overclaiming causal or unconfounded relationships from simple bivariate comparisons. |
| **Impact** | OverTime effect confirmed to persist across Sales/Non-Sales; a residual pay-percentile association remained between leavers and stayers beyond the general "newness" effect — described as an association, not a confirmed causal gap. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D7.3 |
| **Phase** | 7 |
| **Decision** | Non-actionable or already-resolved items (DistanceFromHome, YearsSinceLastPromotion/G5) are dropped or shortened rather than presented as full insights. |
| **Reason** | HR cannot act on where an employee lives; G5's non-informativeness was already established in Phase 6. |
| **Impact** | Keeps the finding set focused on decision-relevant patterns only. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D7.4 |
| **Phase** | 7 |
| **Decision** | Findings routed to Phase 9 for formal testing: Early Attrition, OverTime, Pay Percentile gap, 4 satisfaction variables (WorkLifeBalance excluded), OT×JobSatisfaction interaction, BusinessTravel_Frequently. PerformanceRating routed directly to Phase 8 (not Phase 9), since it is a feature-formula input, not a business hypothesis. |
| **Reason** | Separates statistical hypothesis testing from feature-engineering decisions. |
| **Impact** | Defines the exact test list executed in Phase 9. |
| **Status** | Approved |

---

## Phase 8 — Feature Engineering

| Field | Detail |
|---|---|
| **Decision ID** | D8.1 |
| **Phase** | 8 |
| **Decision** | `New Hire` (YearsAtCompany ≤ 1) adopted as a derived binary feature. |
| **Reason** | Operationalizes the Phase 1 "early attrition" definition for segmentation, hypothesis testing, and modeling. |
| **Impact** | Used across EDA, Hypothesis Testing, Segmentation, Dashboard, and as a model feature. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.2 |
| **Phase** | 8 |
| **Decision** | `Heavy OT` (raw OverTime, relabeled) adopted as-is. |
| **Reason** | Most actionable lever identified in Phase 7 (G1); management can directly adjust workload allocation. |
| **Impact** | Used in EDA, Hypothesis Testing, Dashboard, and modeling. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.3 |
| **Phase** | 8 |
| **Decision** | `Pay Percentile within JobRole` created as a continuous feature (MonthlyIncome percentile-ranked within JobRole); no cutoff/threshold is assigned at this stage. |
| **Reason** | Enables fair relative-pay comparison within the same role; a cutoff would require justification beyond what Phase 8 evidence supports. |
| **Impact** | Cutoff decision explicitly deferred (confirmed still open in Phase 9, D9.5). |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.4 |
| **Phase** | 8 |
| **Decision** | JobSatisfaction, EnvironmentSatisfaction, RelationshipSatisfaction, and JobInvolvement are kept as four separate raw variables; no composite/combined score is created. |
| **Reason** | No statistical or business evidence supports treating them as a single construct; combining risks diluting the signal of the strongest variable. |
| **Impact** | Phase 9 testing later shows only JobSatisfaction reaches even raw significance — validating the decision not to combine. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.5 |
| **Phase** | 8 |
| **Decision** | `Organizational Investment Segment` created using `JobLevel` as the closest available operational proxy for organizational investment — explicitly not a direct measure of investment and not a measure of individual capability or value. |
| **Reason** | No variable directly measures organizational investment; JobLevel/MonthlyIncome collinearity (r=0.95) means JobLevel alone retains most of the available information. |
| **Impact** | Used in EDA, Segmentation, Dashboard; carries a standing risk note (may misclassify high performers not yet promoted). |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.6 |
| **Phase** | 8 |
| **Decision** | Interaction feature `OT + Low Engagement` is not created in Phase 8; its creation is contingent on a positive interaction test result in Phase 9. |
| **Reason** | Phase 7 could not confirm a true interaction effect versus two additive independent effects. |
| **Impact** | Phase 9 interaction test later returns non-significant (D9.6) — feature is never created. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.7 |
| **Phase** | 8 |
| **Decision** | `Promotion Stagnation` is not created. |
| **Reason** | YearsSinceLastPromotion has ~94% zero-values within the New Hire population, providing no discriminative capacity for the active analysis scope. |
| **Impact** | G5 remains permanently low priority. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D8.8 |
| **Phase** | 8 |
| **Decision** | Age Group, company-wide Salary Band, Satisfaction Composite, and Total Working Years Band are intentionally not created. |
| **Reason** | Respectively: no active Business Question needs age banding (plus discrimination-risk concern); redundant with and less accurate than Pay Percentile within JobRole; no evidence supports a composite; high collinearity with existing features adds no new coverage. |
| **Impact** | Keeps the feature set minimal and business-question-driven. |
| **Status** | Approved |

---

## Phase 9 — Hypothesis Testing

| Field | Detail |
|---|---|
| **Decision ID** | D9.1 |
| **Phase** | 9 |
| **Decision** | Phase 9 is formally treated as exploratory hypothesis generation, not confirmatory inference; effect size, confidence intervals, and business relevance are the primary decision basis, with Bonferroni correction reported only as a sensitivity check. |
| **Reason** | Hypotheses were generated from Phase 7 EDA on the same dataset now being tested — no pre-registration or held-out sample exists. |
| **Impact** | No single p-value threshold is used as a pass/fail gate for any finding. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D9.2 |
| **Phase** | 9 |
| **Decision** | Evidence Strength Summary adopted as the governing framework for Phase 10/11 priority: Strong (Early Attrition, Heavy OT); Moderate (BusinessTravel); Weak/exploratory (Pay Percentile, JobSatisfaction); Not supported (OT×JobSatisfaction interaction; the other 3 satisfaction variables). |
| **Reason** | Combines raw/adjusted p-values, effect sizes, and confidence-interval width into a single actionable hierarchy. |
| **Impact** | Directly determines feature priority in Phase 10 and recommendation confidence in Phase 11. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D9.3 |
| **Phase** | 9 |
| **Decision** | Early Attrition (H1) and Heavy OT (H2) confirmed as Strong evidence — significant under both raw and Bonferroni-adjusted p, with meaningful effect sizes (Risk diff=22.0pp, OR=3.61 for H1; OR=3.61, Cramér's V=0.281 for H2). |
| **Reason** | Statistical and practical significance both hold. |
| **Impact** | Top-priority drivers carried into modeling and recommendations. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D9.4 |
| **Phase** | 9 |
| **Decision** | BusinessTravel_Frequently (H6) confirmed as Moderate evidence — significant (p<0.0001, OR=4.70) but not upgraded to Strong due to a wide confidence interval (CI [2.17,10.18]) reflecting small subgroup size (n=36). |
| **Reason** | A significant p-value alone does not justify a "strong" classification when the effect-size estimate itself is highly uncertain. |
| **Impact** | Recommendations built on this finding must include a caveat pending more data. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D9.5 |
| **Phase** | 9 |
| **Decision** | Pay Percentile cutoff is not set in Phase 9; the feature remains continuous. A future cutoff, if needed, must be derived separately (ROC analysis, business rule, or cost-benefit analysis) — never from the midpoint of two sample means. |
| **Reason** | Statistical significance of a group difference does not itself justify a business threshold. |
| **Impact** | Cutoff decision remains open for Phase 11/dashboard design. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D9.6 |
| **Phase** | 9 |
| **Decision** | Interaction OT×JobSatisfaction (H5) confirmed as Not Supported (Likelihood Ratio p=0.9475); interaction feature is never created. |
| **Reason** | No statistical evidence of a true interaction beyond two independent additive effects. |
| **Impact** | Simplifies Phase 10 feature set and Phase 11 recommendations to two independent levers. |
| **Status** | Approved |

---

## Phase 10 — Modeling

| Field | Detail |
|---|---|
| **Decision ID** | D10.1 |
| **Phase** | 10 |
| **Decision** | Model trained on the full dataset (n=1470) rather than the New Hire subgroup alone; `New Hire` is included as a feature, and performance is evaluated both overall and specifically on the New Hire subgroup. |
| **Reason** | Maximizes training stability while preserving the ability to assess performance on the primary business focus (early attrition). |
| **Impact** | Both overall and subgroup metrics are reported and interpreted separately throughout Phase 10. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D10.2 |
| **Phase** | 10 |
| **Decision** | Model evaluation relies on 5-fold cross-validated out-of-fold metrics as the primary evidence basis, not a single train/test split. |
| **Reason** | A single split's subgroup test set (n=67) was shown to produce unstable, non-reproducible conclusions compared to CV (effective subgroup n=215). |
| **Impact** | Final model comparison and selection are based on CV results only. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D10.3 |
| **Phase** | 10 |
| **Decision** | Logistic Regression is selected as the final model, on the basis that its classification performance is comparable to Random Forest (CV AUC/PR-AUC within ~0.01–0.02) while offering substantially better interpretability for the HR/business audience — not because Random Forest performed worse. |
| **Reason** | With comparable performance, interpretability is the deciding, evidence-based tie-breaker for the primary audience. |
| **Impact** | Random Forest's slightly better subgroup PR-AUC/F1 and better calibration (Brier Score) are documented but do not override the interpretability decision. Although Random Forest is better calibrated than Logistic Regression, both models remain insufficiently calibrated for direct probability interpretation (see D10.5). |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D10.4 |
| **Phase** | 10 |
| **Decision** | Logistic Regression coefficients and Random Forest feature importances are documented as measuring fundamentally different concepts and must not be directly compared. |
| **Reason** | Coefficients are signed log-odds effects under a linearity assumption; RF importances are unsigned impurity-reduction measures biased toward high-cardinality continuous variables. |
| **Impact** | Any cross-model feature-ranking claims in Phase 11 must reference each metric separately, never as a unified ranking. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D10.5 |
| **Phase** | 10 |
| **Decision** | Both models are documented as poorly calibrated (overconfident at high predicted-probability bins) due to `class_weight='balanced'`; raw predicted probabilities are not to be used as literal likelihoods in business decisions without recalibration. |
| **Reason** | Brier Score and calibration-bin analysis show predicted probabilities systematically exceed observed attrition rates at the top decile. |
| **Impact** | Phase 11 must use relative risk ranking/percentile rather than literal probability values, unless recalibration is performed first. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | D10.6 |
| **Phase** | 10 |
| **Decision** | The modeling pipeline is frozen for reproducibility: `random_state=42` throughout, the Phase 8 feature set and preprocessing (StandardScaler for Logistic Regression, no scaling for Random Forest), and the 5-fold `StratifiedKFold` cross-validation strategy are fixed as the reference configuration for any future comparison. |
| **Reason** | Phase 10 showed a single train/test split can produce unstable, non-reproducible subgroup conclusions (D10.2); without a frozen pipeline, later re-runs or model additions could silently be compared against a different, incomparable baseline. |
| **Impact** | Any future model (Phase 11 or beyond) must be evaluated against this same frozen pipeline before any performance comparison is considered valid. |
| **Status** | Approved |

---

## Cross-Cutting Decisions (apply across all phases)

| Field | Detail |
|---|---|
| **Decision ID** | DX.1 |
| **Phase** | Cross-cutting (established Phase 1–9, formalized here) |
| **Decision** | Project Scope Boundary: this project does not perform causal inference and does not estimate treatment effects. All findings are correlational, consistent with the dataset being a cross-sectional snapshot. |
| **Reason** | No Exit Interview, no timestamped survey data, and no experimental/quasi-experimental design exist to support causal claims (D3.2, D5.3). |
| **Impact** | All phase outputs, including Phase 11 recommendations, must use "associated with" language and must not claim that an intervention will cause a specific change in attrition. |
| **Status** | Approved |

| Field | Detail |
|---|---|
| **Decision ID** | DX.2 |
| **Phase** | Cross-cutting (established ahead of Phase 11) |
| **Decision** | Deployment / Intended Use: the model is intended to prioritize investigation and retention-intervention effort, not to make automated HR decisions. Predictions are decision-support only and require human review before any action is taken on an individual employee. |
| **Reason** | Consistent with DX.1 (no causal/treatment-effect claims), D10.5 (poor probability calibration), and D4.2 (unknown representativeness) — none of which support fully automated decisioning. |
| **Impact** | Phase 11 recommendations must frame model output as a triage/prioritization signal for HR review, never as a standalone basis for actions affecting an individual employee (e.g., compensation change, performance action). |
| **Status** | Approved |

---

## Standing Disclaimers (apply across all phases from Phase 5 onward)

- All Attrition-based conclusions mix voluntary and involuntary leavers (D5.1).
- All relationships are described as "associated with," never "causes" (D5.3, D3.2).
- All conclusions apply only "within this 1470-employee dataset" — no generalization claim (D4.2).
- `Organizational Investment Segment` is a proxy for organizational investment via JobLevel only, not a direct or capability measure (D8.5).
- Any ROI figures are illustrative only and confined to an Appendix (D5.2).
- No causal inference or treatment-effect claims are made anywhere in this project; all findings are correlational (DX.1).
- Model predictions are decision-support for human review only, never an automated HR decision (DX.2).

---

## Pending Decisions

*(To be populated with approved decisions from Phases 11–13.)*
