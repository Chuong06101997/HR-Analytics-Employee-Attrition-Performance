# HR Attrition Analysis — Master Project Summary (Phase 1–10)

**Dataset:** `WA_Fn-UseC_-HR-Employee-Attrition` — public IBM Watson Analytics synthetic dataset (Kaggle). 1470 rows, 35 columns, 0 missing values, 0 duplicate `EmployeeNumber` (business key).

**Persona in effect throughout:** Senior Product/Data Analyst — 100% factual, no unfounded inference, neutral analytical tone, sharp pushback on subjective/unrealistic requests.

**Global framing established in Phase 1 and never overturned:** This is a public synthetic dataset, not a real company's operational data. There is no real stakeholder — all "stakeholder" dialogue in Phase 5 is a simulation. Every phase must therefore be explicit about which parts are assumptions vs. confirmed facts.

---

## PHASE 1 — BUSINESS UNDERSTANDING (locked)

**Core ambiguity resolved:** the raw question "why do valuable employees leave early" contains two unmeasurable terms and one undefined outcome.

### Locked definitions

| Term | Final definition | Type |
|---|---|---|
| "Valuable employee" | No direct measure exists in the dataset (no 360-review, no manager qualitative rating, no revenue-per-employee). This is a **dataset limitation, not a business limitation**. | Explicit limitation, not resolved with a formula until Phase 8 |
| "Early attrition" | `YearsAtCompany ≤ 1` | Stakeholder-confirmed |
| Outcome | Diagnostic → Predictive → Prescriptive (sequential) | Stakeholder-confirmed |

### Key structural facts established
- Dataset is **cross-sectional** (one snapshot per employee), not longitudinal — no hire/exit dates, so no true survival-time analysis is possible.
- Sample-size warning raised immediately: New Hire group (YearsAtCompany ≤1) = 215/1470, of which 75 Attrition=Yes. Any further split (e.g., by "valuable" segment) shrinks this further — flagged as an ongoing risk for later Predictive modeling.

---

## PHASE 2 — BUSINESS QUESTIONS (approved v2)

Organized into Descriptive / Diagnostic / Predictive / Prescriptive. Full final list:

**Descriptive**
- D0: Is Attrition actually higher for YearsAtCompany≤1 than for tenured employees? (prerequisite check — if not, the "early attrition" framing itself needs revisiting)
- D1: Overall Attrition rate vs. early-attrition rate
- D2: Distribution of "valuable employees" (**if using this proxy**) by Department/JobRole
- D3: % of early leavers who are "valuable" (**if using this proxy**)
- D4: Demographic distribution (Department, JobRole, Gender, MaritalStatus, Age) comparing early leavers vs. rest

**Diagnostic**
- G1: Heavy OT vs. Attrition within the "valuable" (proxy) early-leaver group
- G2: JobSatisfaction / EnvironmentSatisfaction / WorkLifeBalance / RelationshipSatisfaction differences between groups
- G3: Relative pay gap — MonthlyIncome percentile within same JobRole/JobLevel
- G4: DistanceFromHome, BusinessTravel
- G5: YearsSinceLastPromotion, YearsWithCurrManager — **downgraded to low priority** (near-zero variance expected within YearsAtCompany≤1 group)
- ~~G6~~: Manager-change proxy via YearsWithCurrManager=0 — **removed**, proxy judged too weak (no real ManagerID exists)
- G7: After controlling for confounders (Age, Department, JobLevel...), which factors remain associated with early attrition? (multivariable statistical analysis — explicitly NOT machine learning, kept distinct from Phase 10 Modeling)
- G8: Interaction OverTime × JobSatisfaction (not just isolated univariate effects)

**Predictive**
- P1: Can we predict which currently-employed "valuable" (proxy) employees are at risk of leaving within their first year?
- ~~P2~~: "which model to use" — **removed**, this is a Technical Question, not a Business Question; deferred to Phase 10

**Prescriptive**
- S1: If OverTime/pay gap are primary drivers, what interventions are cost-feasible?
- S2: Which group to prioritize for intervention — all new hires, or only the "valuable" (proxy) segment?
- S3: Estimated ROI of each intervention option (intervention cost vs. cost of replacing one employee)

**Explicit rule going forward:** a question unanswerable with current data is marked "insufficient data," never deleted.

---

## PHASE 3 — DATA REQUIREMENT (approved, final v3)

Business-required data listed **before** looking at the dataset (deliberately, to avoid streetlight-effect bias). Key items and criticality:

- Employee demographic — Critical (available)
- **Attrition Event detail** (voluntary/involuntary, resignation/termination dates) — **Critical**, added per user request
- Tenure / hire date — Critical
- Compensation + external market benchmark — Critical
- Performance evaluation **+ evaluation date** — Critical (evaluation date added per user request)
- OverTime / actual workload — Critical
- Satisfaction/Engagement + measurement timestamp — Critical
- Promotion history — Important
- Manager identity + relationship tenure — Important
- Distance/commute, Business travel — Important
- Exit Interview — Critical
- Cost-per-hire / replacement cost — Critical
- Conflict/incident record — Optional
- Competitor offer — Optional
- Periodic employee survey — Important
- **Data Dictionary / HR Policy / Metric Definition** — Critical, added per user request (needed to interpret every other variable correctly)
- **Historical Employee Timeline** (grouped: salary, promotion, manager, department, survey history over time) — rated: **"Critical for answering temporal/causal business questions (Early Attrition, Root Cause), but not required for descriptive metrics"** (final wording per user correction)

---

## PHASE 4 — DATASET DISCOVERY (approved, final v2)

### Technical checks
1470 rows, 35 cols, 0 missing values, **no duplicates detected on the business key (`EmployeeNumber`)**.

### Coverage table (Business Requirement vs. actual columns) — with Business Impact
Full detail preserved; headline items:
- Attrition Event detail — **Not available** (only binary Attrition Yes/No) — **Business Impact: High** (mixes voluntary/involuntary, corrupting all Diagnostic conclusions)
- Exit Interview — **Not available** — High impact (only source that could confirm true causes)
- Cost-per-hire — **Not available** — High impact for Prescriptive (blocks S3 entirely)
- Manager ID (real) — Not available, only weak proxy `YearsWithCurrManager`
- Data Dictionary — Not available — High impact (affects interpretation of every variable)
- Historical Employee Timeline — Not available — High impact for temporal/causal questions only

### Business Question feasibility (Phase 2 cross-check)
- Answerable: D0–D4, G1, G3, G4, G8
- Answerable but not causal: G2 (no measurement timestamp — cannot resolve reverse causality)
- Answerable but expected low discriminative power: G5
- Answerable partially (observed confounders only, not unobserved ones): G7
- Answerable but small-sample caveat: P1
- **Insufficient data (kept, not deleted):** S1, S3

### Representativeness / Bias
Public dataset, unknown company/industry representativeness. **No sampling frame information exists — therefore representativeness for any target population cannot be assessed at all** (final wording per user correction).

### Risk Register (final)
| # | Risk | Impact | Mitigation |
|---|---|---|---|
| R1 | Voluntary/involuntary attrition mixed together | Diagnostic conclusions may misattribute cause | Mandatory disclaimer on every Attrition-related conclusion |
| R2 | No Exit Interview → correlational only | Root-cause claims may be wrong | Use "associated with," never "causes" |
| R3 | PerformanceRating low variance (2/5 values) | "Value" proxy may be unreliable | Re-check in Phase 7 EDA; sensitivity analysis with/without this variable |
| R4 | Small subgroup sample size (New Hire ∩ value proxy) | Predictive modeling overfitting risk | Use cross-validation, report confidence intervals not point estimates |
| R5 | No official Data Dictionary | Variable meaning may be misinterpreted | Label all interpretations as assumptions |
| R6 | No sampling frame → representativeness unknown | Findings may not generalize | State as unresolvable limitation in Phase 12 |
| R7 | No cost-per-hire/intervention cost data | S1/S3 cannot use real numbers | Resolved in Phase 5 negotiation (see below) |

---

## PHASE 5 — STAKEHOLDER NEGOTIATION (approved, final v2)

Simulated negotiation (explicitly labeled as simulated — no real stakeholder exists) resolved scope:

### Decision Log (final)
| Decision | Reason |
|---|---|
| Analyze Attrition on the combined voluntary/involuntary pool, with mandatory disclaimer | No data to split; accepted trade-off |
| **S1/S3 kept in scope, but reframed from "real ROI" to "ROI Framework + list of required business inputs"** | Avoid a single illustrative number being mistaken for a real figure that could drive real investment decisions |
| Any illustrative ROI numbers go in an **Appendix only**, explicitly labeled "illustrative, not actual" | Same reason as above |
| No additional data collection (no Exit Interview, no Data Dictionary sourced) | Accept correlational limitation rather than pausing the project |
| No new dataset sought, no Business Questions removed | Full Phase 2 scope preserved |
| Conclusions limited to "within this 1470-employee dataset," not generalized | No sampling frame to justify generalization |

**Final scope statement (exact wording, per user correction):** *"Business Questions giữ nguyên; mức độ tin cậy của từng câu trả lời sẽ phụ thuộc vào dữ liệu hỗ trợ"* (Business Questions remain unchanged; the confidence level of each answer will depend on the supporting data).

---

## PHASE 6 — DATA QUALITY ASSESSMENT (approved, final)

**Purpose reminder:** assessed trustworthiness of data for answering Phase 2 questions — not data cleaning, no EDA, no modeling.

### Key quantitative findings
1. **Constant features:** `EmployeeCount`=1, `StandardHours`=80, `Over18`='Y' — irrelevant to any Business Question, excluded from analysis scope (not deleted from data).
2. **PerformanceRating:** only values 3 (n=1244) and 4 (n=226). Correlation with JobLevel = -0.021, with MonthlyIncome = -0.017 (essentially independent). **Neutral conclusion held per user correction: this shows weak apparent linkage to the other proxy components — role in the "value" concept deferred to Phase 7 discriminative-power check, not pre-judged as "noise."**
3. **Multicollinearity (identified as risk only, feature-selection decision deferred to Phase 8/9 per user correction):**
   - corr(JobLevel, MonthlyIncome) = **0.95**
   - corr(JobLevel, TotalWorkingYears) = 0.78
   - corr(MonthlyIncome, TotalWorkingYears) = 0.77
   - corr(Age, TotalWorkingYears) = 0.68
4. **Class imbalance:** Attrition No=1233 (83.9%), Yes=237 (16.1%) — flagged directly for Phase 10 metric choice (no Accuracy-only evaluation).
5. **Logical consistency checks — ALL PASSED (0 violations):** YearsInCurrentRole≤YearsAtCompany, YearsWithCurrManager≤YearsAtCompany, YearsSinceLastPromotion≤YearsAtCompany, TotalWorkingYears≥YearsAtCompany, Age-18≥TotalWorkingYears. Positive signal — the time variables are internally consistent.
6. **Small subgroup sample:** New Hire n=215, positives n=75 (quantified, reiterated from Phase 1).
7. **OverTime:** No=1054 (71.7%), Yes=416 (28.3%) — distribution fine; the limitation is conceptual (policy flag, not actual hours), not statistical.

### Confidence-by-question-group summary (from Phase 6)
Descriptive: High. Univariate Diagnostic: Medium-High. G7 (multivariable): Medium-Low (multicollinearity). G5: Low. P1: Medium-Low (imbalance + small subgroup). Value proxy foundation: Low-Medium.

---

## PHASE 7 — EDA (approved, final v2 — after self-review refinement)

**Format used per user requirement:** Evidence → Alternative Explanation → Business Implication, actionable insights prioritized, non-actionable insights shortened/dropped.

### Findings kept

**D0 (foundational):** Attrition rate by tenure bucket — monotonic decline: 0-1yr 34.9% (75/215), 2-3yr 18.4% (47/255), 4-6yr 12.8% (49/382), 7-10yr 12.4% (46/372), 11+yr 8.1% (20/246). Overall 16.1%. **Confirms the Phase 1 premise is supported by data.**

**Insight 1 (G1 — OverTime):** Within New Hire: OT=Yes 55.1% (38/69) vs OT=No 25.3% (37/146) attrition. **Alternative explanation tested and partially rejected:** OverTime rate by JobRole is fairly even (23.9%-33.2%, no dominant role); effect persists when split Sales (61.1% vs 30.2%) vs Non-Sales (52.9% vs 23.3%) — not purely a JobRole confound.

**Insight 2 (G3 — Pay gap):** New-hire-overall mean pay percentile (regardless of attrition) = 38.5 vs. non-new-hire = 51.6 (confirms a genuine "newness" effect on pay). **But within New Hire only:** leavers=31.9 vs stayers=42.0 — a residual gap exists beyond the newness effect.

**Insight 3 (G2 — Satisfaction):** All 5 satisfaction-type measures lower among leavers (0.09–0.25-point gaps); WorkLifeBalance weakest (0.09). **Alternative explanation unresolved:** no timestamp exists to distinguish "low satisfaction causes leaving" from "planning to leave causes negative survey answers" (reverse causality) — structural limitation, cannot be resolved with this data.

**Insight 4 (G8 — Interaction):** OT=Yes+LowSat=63.0%, OT=Yes+HighSat=50.0%, OT=No+LowSat=31.7%, OT=No+HighSat=20.9%. Flagged explicitly as **not yet statistically tested for true interaction** (small cells, n=27-86).

**Insight 5 (short) — G4:** DistanceFromHome (10.97 vs 8.31) — **not actionable** (HR cannot change where someone lives), shortened; BusinessTravel_Frequently 66.7% attrition (n=36, small) — checked against JobRole confound: Travel_Frequently in the early group is **not** concentrated only in Sales (also Lab Technician, Research Scientist present) — confound not fully explained away, kept but low priority pending more data.

**Insight 6 (short) — PerformanceRating discriminative power:** Overall 16.1% (rating=3) vs 16.4% (rating=4); within New Hire 34.1% vs 38.9% (n=36 for rating=4). **Evidence-based neutral conclusion: weak discriminative power** — feeds directly into the Phase 8 proxy-formula decision, not a standalone HR insight.

### Explicitly dropped from Phase 7 (per self-review)
- G5 (Years* variables) — already downgraded at Phase 2, reconfirmed via Phase 6 variance issue; not treated as a "new insight."
- G7 — not performed here (belongs to multivariable analysis in Phase 9).

### Final Phase 7 decision table
| Finding | Confidence | Send to Phase 9? |
|---|---|---|
| D0 — Early attrition higher | High | Yes |
| OverTime linked to attrition, not purely JobRole | High | Yes |
| Pay gap residual beyond newness effect | Medium | Yes |
| Satisfaction lower among leavers (4 kept, WorkLifeBalance dropped) | Medium | Yes |
| Interaction OT×JobSatisfaction | Low-Medium | Yes — needs formal interaction test |
| BusinessTravel_Frequently | Low (n=36, confound not fully ruled out) | Yes, low priority |
| DistanceFromHome | Medium evidence but not actionable | **No** — dropped |
| PerformanceRating weak discriminative power | Medium | **Not sent to Phase 9** — feeds Phase 8 proxy decision directly |

---

## PHASE 8 — FEATURE ENGINEERING (approved, final v4 — Business Analyst perspective, not ML-first)

**Rule applied throughout:** every feature must answer a specific Business Question and be something HR can understand/act on; features not tied to an active Business Question were rejected.

### Final feature set

| Feature | Feature Source | Type | Business Question | Used In |
|---|---|---|---|---|
| **New Hire** (YearsAtCompany≤1) | Derived | Binary | D0, D1, D3 | EDA, Hypothesis Testing, Segmentation, Dashboard |
| **Heavy OT** (=OverTime, renamed) | Raw | Binary | G1 | EDA, Hypothesis Testing, Dashboard |
| **Pay Percentile within JobRole** | Derived (MonthlyIncome + JobRole) | Continuous | G3 | Hypothesis Testing, Dashboard — **no cutoff assigned; kept continuous by explicit user decision (see Phase 9)** |
| **JobSatisfaction, EnvironmentSatisfaction, RelationshipSatisfaction, JobInvolvement** | Raw | 4 separate variables | G2 | Hypothesis Testing, Dashboard — **kept separate, NOT combined into a composite** (no statistical/business evidence supported combining them) |
| **Organizational Investment Segment** (renamed from "Employee Value Proxy") | Derived — **proxy only** | Ordinal | D2, D3 | EDA, Segmentation, Dashboard |
| OT + Low Engagement (interaction feature) | — | — | G8 | **NOT created in Phase 8** — deferred pending Phase 9 interaction test |
| Promotion Stagnation | — | — | G5 | **Rejected** — YearsSinceLastPromotion has ~94% zero-values within New Hire (202/215), no discriminative capacity in the active analysis scope |

### Critical wording locked for `Organizational Investment Segment`
This feature uses `JobLevel` as **the closest available operational proxy for "organizational investment"** — explicitly **not** a direct/equivalent measure, and **not** a measure of individual capability or value. Chosen because: (a) no variable directly measures "organizational investment," and (b) JobLevel/MonthlyIncome collinearity (r=0.95) means using JobLevel alone loses little information vs. using both. **Business Risk:** may misclassify a high-performing employee not yet promoted as "low investment."

### Features Intentionally NOT Created (with reasons)
| Feature considered | Reason for exclusion |
|---|---|
| Age Group | No active Business Question needs age banding (raw Age suffices for D4); age-based HR segmentation also carries discrimination-risk concerns with no offsetting business benefit |
| Salary Band (company-wide, not by JobRole) | Redundant with and less accurate than Pay Percentile within JobRole; would reintroduce cross-role comparison unfairness |
| Satisfaction Composite | No statistical or business evidence the 4 variables measure one construct; combining would dilute the signal of the strongest variable |
| Total Working Years Band | Highly correlated with JobLevel (r=0.78) and Age (r=0.68); adds no new Business-Question coverage beyond New Hire / Organizational Investment Segment, and increases multicollinearity risk |

---

## PHASE 9 — HYPOTHESIS TESTING (approved, final v3)

**Methodological framing (final, explicit):** This project's Phase 9 is **exploratory hypothesis generation**, not confirmatory inference — hypotheses were generated from Phase 7 EDA on the same dataset now being tested (no pre-registration, no held-out set). Consequence: **effect size, confidence intervals, and business relevance are the primary basis for decisions; Bonferroni correction is reported only as a sensitivity check, never as a pass/fail gate.**

### Full statistical results (α=0.05 raw; Bonferroni-adjusted α=0.05/9=0.0056)

| Hypothesis | Test | Raw p | Adjusted p sig? | Effect size (with CI where computed) |
|---|---|---|---|---|
| H1 — Early attrition (New Hire vs. rest) | Two-proportion z-test + chi-sq (5 buckets) | z p≈6.7×10⁻¹⁶; chi² p≈1.5×10⁻¹⁵ | Yes | Risk diff=22.0pp (CI [15.3,28.6]); OR=3.61 (CI [2.61,5.00]); Cramér's V=0.227 |
| H2 — Heavy OT (within New Hire) | Chi-sq (Yates) + Fisher exact | <0.0001 | Yes | OR=3.61 (CI [1.98,6.60]); Cramér's V=0.281 |
| H3 — Pay Percentile (within New Hire) | Welch's t-test | 0.0085 | **No** | Cohen's d=-0.372 |
| H4 — JobSatisfaction (within New Hire) | Welch's t-test | 0.0286 | No | d=-0.318 |
| H4 — JobInvolvement | Welch's t-test | 0.0637 | No | d=-0.277 |
| H4 — RelationshipSatisfaction | Welch's t-test | 0.1110 | No | d=-0.235 |
| H4 — EnvironmentSatisfaction | Welch's t-test | 0.1603 | No | d=-0.212 |
| H5 — Interaction OT×JobSatisfaction | Likelihood Ratio Test (manual logistic regression, numpy/scipy — statsmodels unavailable, no internet) | 0.9475 | No | No effect found |
| H6 — BusinessTravel_Frequently (within New Hire) | Chi-sq (3x2, all expected counts ≥5) | <0.0001 | Yes | OR (Freq vs Rare)=4.70 (CI [2.17,10.18], wide due to n=36); Cramér's V=0.306 |

### Evidence Strength Summary (final — foundation carried into Phase 10/11)
- **Strong evidence:** Early Attrition (H1), Heavy OT (H2)
- **Moderate evidence:** Business Travel (H6) — significant with large point-estimate OR but very wide CI due to n=36; explicitly NOT upgraded to "strong" on p-value alone
- **Weak/exploratory evidence:** Pay Percentile (H3), JobSatisfaction (H4, 1 of 4 variables)
- **Not supported:** Interaction OT×JobSatisfaction (H5); JobInvolvement/RelationshipSatisfaction/EnvironmentSatisfaction (H4, 3 of 4 variables) — did not clear even raw p<0.05

**Business Question resolution:** Pay Percentile cutoff explicitly **NOT set in Phase 9** — statistical significance confirms group difference only, does not itself justify a business threshold. Feature remains continuous; a cutoff (if ever needed) must come from a separate method (ROC analysis, business rule, cost-benefit, or stakeholder requirement).

**Rule for Phase 10/11 carried forward:** stronger evidence tier → higher modeling/recommendation priority. Not-supported findings excluded from modeling and recommendations.

---

## PHASE 10 — MODELING (approved, final — after 3 rounds of refinement)

**Scope decision (explicit, from user):** Train on full dataset (n=1470) for stability; treat `New Hire` as a feature; evaluate overall AND specifically on the New Hire subgroup; explicitly distinguish overall vs. subgroup performance.

### Feature set used in modeling (from Phase 8, prioritized by Phase 9 evidence tier)
New Hire, Heavy OT, BusinessTravel (Frequent/Rare dummies, ref=Non-Travel), Pay Percentile within JobRole, JobSatisfaction, EnvironmentSatisfaction, RelationshipSatisfaction, JobInvolvement, Organizational Investment Segment (JobLevel). **Excluded:** Interaction feature (not supported), Promotion Stagnation (rejected in Phase 8).

### Step 1 — Single 70/30 stratified train/test split (preliminary, later shown unstable)
| | Overall Test (n=441) | New Hire Subgroup (n=67, 17 positive) |
|---|---|---|
| Logistic Regression | AUC=0.792, PR-AUC=0.498 | AUC=0.852, PR-AUC=0.698 |
| Random Forest | AUC=0.783, PR-AUC=0.457 | AUC=0.772, PR-AUC=0.600 |

Flagged explicitly as **unreliable due to tiny subgroup test set (n=67)**.

### Step 2 — 5-fold Cross-Validation, out-of-fold (primary evidence basis, n=215 for subgroup)
| | Overall (n=1470) | New Hire Subgroup (n=215, 75 positive) |
|---|---|---|
| Logistic Regression | AUC=0.785, PR-AUC=0.494, F1=0.470 | AUC=0.775, PR-AUC=0.666, F1=0.562 |
| Random Forest | AUC=0.776, PR-AUC=0.489, F1=0.482 | **AUC=0.781, PR-AUC=0.686, F1=0.616** |

**Key finding:** CV **reverses** part of the single-split conclusion — RF is actually slightly better on the subgroup under CV. This instability is presented as direct evidence of the small-subgroup risk flagged since Phase 1.

**Overall vs. subgroup distinction (explicit):** PR-AUC is higher for both models on the subgroup mainly because the subgroup's base rate (34.9%) is higher than overall (16.1%) — **not proof the model "works better" there**. ROC-AUC (less base-rate-sensitive) is roughly stable across both scopes (0.775–0.785 LR; 0.776–0.781 RF), a more trustworthy signal of consistent model behavior.

### Logistic Regression coefficients (standardized) — direction check vs. Phase 9 evidence
Heavy OT (+0.611), BizTravel_Frequent (+0.510), New Hire (+0.510), Org Investment Segment (-0.438), JobSatisfaction (-0.362), other 3 satisfaction vars (-0.21 to -0.35), **Pay Percentile (+0.042 — surprisingly small in the multivariable context** despite a significant univariate test in Phase 9, suggesting its effect may be partly absorbed by other variables in the model).

### Random Forest feature importances
Heavy OT (0.180), New Hire (0.175), Pay Percentile (0.170), Org Investment Segment (0.166), EnvironmentSatisfaction (0.094), JobInvolvement (0.064), JobSatisfaction (0.055), RelationshipSatisfaction (0.051), BizTravel_Frequent (0.034), BizTravel_Rare (0.011).

**Explicit rule (final, per user correction):** Logistic Regression coefficients and Random Forest feature importances **measure fundamentally different concepts and must not be directly compared** — coefficients are signed log-odds effects assuming linearity; RF importances are unsigned impurity-reduction measures biased toward continuous variables with more distinct values.

### Calibration Assessment (added per user request)
| Model | Brier Score — Overall | Brier Score — New Hire subgroup |
|---|---|---|
| Logistic Regression | 0.182 | 0.281 |
| Random Forest | **0.168 (better)** | **0.230 (better)** |

Both models are **overconfident at high predicted-probability bins** (e.g., LR's top decile: mean predicted ≈0.854 vs. observed rate 0.578) — caused by `class_weight='balanced'`, which improves ranking/recall but distorts probability calibration. **Practical implication for HR:** raw predicted probabilities should NOT be read literally as "X% chance of leaving" without recalibration (e.g., Platt scaling/Isotonic regression); safer interim use is relative risk ranking/percentile, not the absolute probability value.

### Final model selection — explicit final wording (per user correction)
**Random Forest is not an inferior model.** On CV evidence: classification performance is comparable between the two models (RF even edges out LR on the subgroup for PR-AUC/F1), and RF has better calibration (lower Brier Score) on both scopes. **Logistic Regression was selected because, when performance is not meaningfully different, its substantially better interpretability for the primary HR/business audience becomes the deciding factor — a trade-off decision, not a claim that Random Forest performed worse.**

### Known limitations of Phase 10 (final)
- Default 0.5 classification threshold with `class_weight='balanced'` produces high recall/low precision by construction — actual threshold choice is deferred to Phase 11 as a business decision.
- No hyperparameter grid search performed for Random Forest (reasonable defaults used: max_depth=5, min_samples_leaf=10, to limit overfitting risk given small subgroup).
- No external validation dataset exists; all Phase 4/6 representativeness limitations still apply to the model.
- Probability calibration is currently poor (see above) — must be addressed before literal probability-based business use.

---

## CARRY-FORWARD STATE FOR PHASE 11 (Recommendation) AND BEYOND

1. **ROI framing already agreed (Phase 5):** Present an ROI **framework** + list of business inputs needed (cost-per-hire, intervention cost) — do **not** put illustrative numbers in the main conclusions; illustrative numbers, if used at all, go in an Appendix labeled "illustrative, not actual."
2. **Evidence Strength Summary (Phase 9) governs recommendation confidence:** Strong (Early Attrition, Heavy OT) → confident recommendations; Moderate (BusinessTravel) → recommend with explicit caveat pending more data; Weak/exploratory (Pay Percentile, JobSatisfaction) → monitor, not act; Not supported (Interaction) → no recommendation.
3. **Model selected:** Logistic Regression (interpretability tie-break; comparable performance to Random Forest; RF has better calibration but was not chosen due to interpretability priority for HR audience).
4. **Unresolved/open items still pending explicit decision:**
   - Calibration correction (Platt/Isotonic) not yet implemented — recommended before any literal probability-based deployment.
   - Classification threshold not yet chosen — business decision for Phase 11.
   - Pay Percentile cutoff (if ever needed for dashboarding) — method not yet chosen (ROC/business rule/cost-benefit), explicitly deferred.
5. **Standing disclaimers that must accompany any Phase 11 output:**
   - All Attrition-based conclusions mix voluntary/involuntary leavers (R1, Phase 5-accepted trade-off).
   - All causal-sounding language must remain "associated with," never "causes" (no Exit Interview data, reverse-causality unresolved for Satisfaction).
   - Conclusions apply "within this 1470-employee dataset" only — no generalization claim (no sampling frame, Phase 4/5).
   - `Organizational Investment Segment` is a proxy for organizational investment via JobLevel, not a direct measure, and not a measure of individual capability.

---

## PHASE 11 — BUSINESS RECOMMENDATION

### 11.0 — Objective / Reasoning / Assumption / Limitation / Next Action (tổng thể Phase)

**Objective:** Chuyển hoá Evidence Strength Summary (Phase 9) + model output (Phase 10) thành khuyến nghị hành động cụ thể cho HR, gắn với S1–S3, có phân cấp độ tin cậy rõ ràng và framework ROI (không phải số ROI thật).

**Reasoning:** Theo Additional Review Rule #3 ("Every recommendation must trace back to a Business Question") và #8 ("Modeling exists to support business recommendations, not maximize benchmark metrics") — không đề xuất bất kỳ điều gì không truy được về Business Question hoặc Evidence Tier cụ thể.

**Assumption:** Tiếp tục thẳng vào Phase 11 theo yêu cầu, tạm gác qua nguyên tắc "dừng sau mỗi Phase" của Master Guideline gốc cho bước khởi tạo, nhưng dừng lại sau khi xong Phase 11 để review, tuân thủ ITERATIVE RULE cho các Phase sau.

**Limitation:** Không có Exit Interview, không có cost-per-hire thật (R7, D4.3) → S1/S3 không thể có số ROI thật, chỉ có framework.

**Next Action:** Sau khi review, chuyển sang Phase 12 (Limitation) và Phase 13.

### 11.1 — Recommendation Matrix (theo Evidence Tier)

| # | Finding | Evidence Tier | Recommendation | Business Question | Confidence |
|---|---|---|---|---|---|
| R-A | Early attrition tập trung ở YearsAtCompany≤1 (OR=3.61) | **Strong** | Thiết lập cơ chế theo dõi/can thiệp chủ động trong 12 tháng đầu (không phải toàn bộ vòng đời nhân viên) | S1, S2 | Cao |
| R-B | Heavy OT trong nhóm New Hire (OR=3.61) | **Strong** | Rà soát phân bổ workload/OT cho nhân viên mới, đặc biệt nhóm Sales | S1 | Cao |
| R-C | BusinessTravel_Frequently trong New Hire (OR=4.70, CI rộng do n=36) | **Moderate** | Đưa vào danh sách theo dõi, **không** ban hành chính sách travel mới chỉ dựa trên n=36 | S1 | Trung bình — kèm caveat bắt buộc |
| R-D | Pay Percentile gap còn dư sau khi trừ hiệu ứng "newness" (d=-0.372, không qua Bonferroni) | **Weak/exploratory** | Đưa vào dashboard giám sát định kỳ, **không** ra chính sách lương ngay | Monitor only | Thấp |
| R-E | JobSatisfaction thấp hơn ở nhóm rời đi (chỉ 1/4 biến satisfaction đạt raw p<0.05) | **Weak/exploratory** | Theo dõi, không hành động | Monitor only | Thấp |
| R-F | Interaction OT×JobSatisfaction | **Not supported** (LRT p=0.9475) | **Không đưa ra recommendation** — xử lý OT và Satisfaction như 2 đòn bẩy độc lập | — | Không áp dụng |

**Lưu ý bắt buộc:** R-C, R-D, R-E **không được nâng cấp** thành "Strong" trong bất kỳ bản trình bày nào cho stakeholder, kể cả khi nghe có vẻ thuyết phục về mặt định tính — đây là rule cứng từ D9.2/D9.4.

### 11.2 — S2: Prioritization — Ai được ưu tiên can thiệp trước?

**Objective:** Trả lời "nên ưu tiên nhóm nào" bằng cách kết hợp (a) risk ranking từ model Phase 10, và (b) Organizational Investment Segment (Phase 8), **không** dùng probability thô (vi phạm D10.5).

**Reasoning:** Vì model chưa được calibrate, dùng percentile rank trong nội bộ nhóm New Hire là cách an toàn duy nhất để so sánh tương đối, thay vì đọc "X% khả năng nghỉ việc."

**Assumption:** Tái sử dụng đúng frozen pipeline Phase 10 (D10.6) — Logistic Regression, cùng feature set, cùng `random_state=42`. Không train lại model mới, không đổi feature.

**Limitation:** Organizational Investment Segment là proxy qua JobLevel, có rủi ro misclassify người giỏi chưa được thăng chức (D8.5) — do đó priority tier chỉ là gợi ý cho HR review, không phải quyết định cuối.

```python
# ============================================================
# PHASE 11.2 — Risk Ranking & Priority Segmentation for HR Review
# Reuses the FROZEN Phase 10 pipeline (D10.6) — no retraining decisions here.
# ============================================================

import pandas as pd
import numpy as np
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import StratifiedKFold, cross_val_predict
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline

# --- 1. Load data (assumes df already built with Phase 8 features) ---
# df must contain: New_Hire, Heavy_OT, BizTravel_Frequent, BizTravel_Rare,
# Pay_Percentile_JobRole, JobSatisfaction, EnvironmentSatisfaction,
# RelationshipSatisfaction, JobInvolvement, Org_Investment_Segment, Attrition
#
# (Feature construction code from Phase 8 is NOT repeated here —
#  it must be the exact same code already approved, per Additional Review Rule #4:
#  "Prefer incremental refinement instead of rewriting.")

feature_cols = [
    "New_Hire", "Heavy_OT", "BizTravel_Frequent", "BizTravel_Rare",
    "Pay_Percentile_JobRole", "JobSatisfaction", "EnvironmentSatisfaction",
    "RelationshipSatisfaction", "JobInvolvement", "Org_Investment_Segment"
]
X = df[feature_cols]
y = df["Attrition"].map({"Yes": 1, "No": 0})

# --- 2. Frozen pipeline (D10.6): StandardScaler + Logistic Regression ---
pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("clf", LogisticRegression(class_weight="balanced", random_state=42, max_iter=1000))
])

cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

# --- 3. Out-of-fold predicted probabilities (NOT literal probability, see D10.5) ---
oof_proba = cross_val_predict(pipeline, X, y, cv=cv, method="predict_proba")[:, 1]
df["risk_score_raw"] = oof_proba  # DO NOT interpret as "% chance of leaving"

# --- 4. Convert to relative percentile rank WITHIN New Hire subgroup only ---
# Rationale: business focus (Phase 1) is on New Hire; comparing risk within
# this subgroup avoids conflating "New Hire effect" with "risk rank."
new_hire_mask = df["New_Hire"] == 1
df.loc[new_hire_mask, "risk_percentile_within_new_hire"] = (
    df.loc[new_hire_mask, "risk_score_raw"].rank(pct=True) * 100
)

# --- 5. Priority Tier = Risk Percentile x Organizational Investment Segment ---
# 2-axis matrix, NOT a single blended score (avoids hiding one axis inside the other).
# Business parameter — NOT a statistically derived value.
# Must be set by HR based on operational review capacity (how many cases/month
# the team can realistically investigate), not by this analysis.
priority_cutoff_percentile = 70  # <-- placeholder, PENDING HR confirmation

def assign_priority_tier(row, cutoff=priority_cutoff_percentile):
    if pd.isna(row["risk_percentile_within_new_hire"]):
        return "Not Applicable (not New Hire)"
    high_risk = row["risk_percentile_within_new_hire"] >= cutoff
    high_investment = row["Org_Investment_Segment"] >= row["Org_Investment_Segment"].__class__(2) \
        if not isinstance(row["Org_Investment_Segment"], (int, float)) else row["Org_Investment_Segment"] >= 2
    if high_risk and high_investment:
        return "P0 - Immediate HR review"
    elif high_risk:
        return "P1 - Monitor + light-touch check-in"
    elif high_investment:
        return "P2 - Retention watch (low urgency)"
    else:
        return "P3 - Routine monitoring"

df["priority_tier"] = df.apply(lambda r: assign_priority_tier(r, priority_cutoff_percentile), axis=1)

# --- 6. Output: table for HR (decision-support only, per DX.2) ---
priority_table = df.loc[new_hire_mask, [
    "EmployeeNumber", "risk_percentile_within_new_hire",
    "Org_Investment_Segment", "priority_tier"
]].sort_values("risk_percentile_within_new_hire", ascending=False)

print(priority_table.head(20))
```

### Phase 11.2 — Diễn giải bảng Priority Tier

**Cách đọc bảng:**
- `risk_percentile_within_new_hire`: xếp hạng tương đối trong nhóm New Hire, **không phải xác suất thật** (model chưa calibrate — D10.5). Ví dụ percentile=90 nghĩa là "rủi ro cao hơn 90% nhân viên mới khác," không phải "90% khả năng nghỉ việc."
- `priority_tier`: kết hợp risk rank + Organizational Investment Segment (proxy JobLevel).
  - **P0**: rủi ro cao + đầu tư tổ chức cao → ưu tiên review đầu tiên.
  - **P1**: rủi ro cao nhưng đầu tư thấp → theo dõi, không nhất thiết ưu tiên bằng P0.
  - **P2**: đầu tư cao nhưng rủi ro thấp → giữ chân dài hạn, không khẩn cấp.
  - **P3**: còn lại → theo dõi định kỳ thông thường.

**Cảnh báo bắt buộc (không được bỏ qua khi trình bày cho HR):**
1. Đây là **tín hiệu ưu tiên điều tra**, không phải quyết định tự động (DX.2). Mọi hành động cụ thể lên một nhân viên (thay đổi lương, đánh giá hiệu suất...) cần con người review, không dựa 100% vào bảng này.
2. `priority_cutoff_percentile` (mặc định minh hoạ = 70) là **tham số nghiệp vụ có thể cấu hình**, không phải giá trị thống kê tối ưu. Giá trị thật cần được HR chọn dựa trên năng lực review thực tế (số case/tháng đội HR xử lý được), không phải do phân tích này quyết định.
3. `Org_Investment_Segment` có rủi ro misclassify người giỏi chưa thăng chức (D8.5) — P2/P3 không đồng nghĩa "không quan trọng."

### 11.3 — S1: Can thiệp cụ thể theo Evidence Tier (Strong only)

**Objective:** Đề xuất intervention cho 2 finding Strong (Early Attrition framing + Heavy OT), vì đây là 2 đòn bẩy duy nhất đủ bằng chứng để hành động dứt khoát.

**Reasoning:** Theo Carry-Forward Rule #2 (Master Summary): "Strong → confident recommendations." Interaction đã bị loại (D9.6), nên OT và Satisfaction được xử lý như 2 đòn bẩy **độc lập**, không phối hợp.

| Đòn bẩy | Can thiệp đề xuất | Đối tượng | Cơ sở |
|---|---|---|---|
| Heavy OT (New Hire) | **Rà soát và thí điểm (pilot)** cơ chế phê duyệt/giới hạn OT cho New Hire, ưu tiên **điều tra trước tại** Sales (nơi hiệu ứng OT quan sát được mạnh nhất: 61.1% vs 30.2%) — **chưa có bằng chứng đây là quan hệ nhân quả**, chỉ là association | Nhóm P0/P1 có Heavy_OT=1 | H2 (Strong, correlational), Insight 1 Phase 7 |
| Early attrition nói chung | **Thí điểm** onboarding checkpoint tại mốc 3/6/9/12 tháng để **đánh giá** tác động thực tế trước khi triển khai rộng — không có cơ sở dữ liệu nào trong project này chứng minh checkpoint sẽ làm giảm attrition | Toàn bộ New Hire | H1 (Strong, correlational), D0 Phase 7 |

**Nguyên tắc triển khai:** Bất kỳ can thiệp nào ở trên đều phải được **xác thực qua một pilot program có success metrics định trước** (ví dụ: attrition rate của nhóm pilot so với nhóm đối chứng sau X tháng) trước khi triển khai toàn tổ chức — dữ liệu hiện tại chỉ là correlational (DX.1), không đủ cơ sở để triển khai đại trà ngay.

**Limitation:** Không có Exit Interview → không biết OT có phải nguyên nhân gốc hay chỉ là correlate của một biến khác chưa đo (ví dụ workload thực tế theo giờ, không phải flag Yes/No). Recommendation dừng ở mức "associated with," theo đúng DX.1.

**Next Action:** Tiếp tục sang 11.4 (ROI Framework) và 11.5 (vấn đề còn treo).

### 11.4 — S3: ROI Framework (KHÔNG phải số ROI thật — D5.2)

**Objective:** Cung cấp khung tính ROI để HR tự điền số liệu thật khi có, không tự tạo số minh hoạ trong phần kết luận chính.

```python
# ============================================================
# PHASE 11.4 — ROI FRAMEWORK (structure only — inputs are placeholders)
# Per D5.2: any illustrative numbers must be Appendix-only, labeled explicitly.
# ============================================================

def roi_framework(
    num_at_risk_employees: int,
    expected_incremental_retention_lift: float,
    # ^ Phải là INCREMENTAL treatment effect (chênh lệch attrition giữa nhóm
    #   được can thiệp và nhóm đối chứng trong một pilot/A-B test tương lai).
    #   KHÔNG được ước lượng từ dữ liệu quan sát (observational) trong project này,
    #   vì dataset không có thiết kế thực nghiệm/chuẩn hoá để tách nhân quả (DX.1).
    cost_per_hire: float,            # KHÔNG có trong dataset — cần Finance/HR cung cấp
    intervention_cost_per_employee: float,  # KHÔNG có trong dataset — cần chi phí thực tế chương trình
):
    """
    Trả về công thức ROI, KHÔNG chạy với số thật vì các input
    (expected_incremental_retention_lift, cost_per_hire, intervention_cost) đều
    KHÔNG tồn tại trong dataset này (R7, D4.3).
    """
    prevented_departures = num_at_risk_employees * expected_incremental_retention_lift
    savings = prevented_departures * cost_per_hire
    total_intervention_cost = num_at_risk_employees * intervention_cost_per_employee
    roi = savings - total_intervention_cost
    return {
        "prevented_departures": prevented_departures,
        "savings": savings,
        "total_intervention_cost": total_intervention_cost,
        "roi": roi
    }

# KHÔNG gọi hàm này với số giả định trong báo cáo chính.
# Nếu cần minh hoạ, chỉ đặt trong Appendix, ghi rõ:
# "Illustrative example only — not actual, all inputs are placeholders."
```

### Phase 11.4 — Danh sách input BẮT BUỘC phải có trước khi ROI có ý nghĩa thật

| Input | Có trong dataset? | Nguồn cần bổ sung |
|---|---|---|
| Số nhân viên rủi ro cao (P0) | Có (tính được từ 11.2) | — |
| **Incremental retention lift** kỳ vọng của can thiệp | **Không** | Phải đo bằng **pilot/A-B test tương lai có nhóm đối chứng**; không được suy ra từ correlation quan sát được trong dataset hiện tại — làm vậy sẽ vi phạm DX.1 (không claim nhân quả) |
| Cost-per-hire | **Không** | Phòng Tài chính/HR cung cấp |
| Chi phí chương trình can thiệp/nhân viên | **Không** | HR cung cấp theo chương trình cụ thể (VD: onboarding checkpoint, OT policy review) |

**Kết luận S3 (đúng D5.2):** Ở giai đoạn này, dự án **chỉ dừng ở framework**. Bất kỳ số ROI cụ thể nào xuất hiện trong bản trình bày chính là vi phạm quy tắc đã approve — nếu cần minh hoạ cho stakeholder hiểu cách tính, phải để trong Appendix và ghi rõ "illustrative, not actual."

ROI chỉ có ý nghĩa khi `expected_incremental_retention_lift` được đo từ hiệu ứng điều trị tăng thêm (incremental treatment effect) qua pilot/A-B test có nhóm đối chứng trong tương lai — không thể suy ra từ dữ liệu observational hiện có, và việc triển khai đại trà chỉ nên thực hiện sau khi pilot đó đạt các success metrics định trước.

### 11.5 — Vấn đề còn treo cần quyết định trước khi sang Phase 12

1. **Ngưỡng percentile ở mục 11.2** — đề xuất làm ví dụ minh hoạ cơ chế, **chưa phải quyết định chính thức**. Cần chốt theo capacity thực tế của HR (review được bao nhiêu case/tháng), hoặc chọn phương pháp khác (VD: theo cost-benefit khi có dữ liệu S3).
2. **Threshold phân loại của model (deferred từ Phase 10, D10 Known Limitations)** — 11.2 dùng percentile rank thay vì threshold cứng để né vấn đề calibration, nhưng nếu HR cần một con số threshold cụ thể (VD: "review tất cả nhân viên percentile ≥ X"), đây là quyết định kinh doanh cần xác nhận riêng, không phải điều tự chọn.
3. Không phát hiện mâu thuẫn nào giữa Phase 11 và Phase 1–10.

---

## PHASE 12 — LIMITATION

### 12.0 — Objective / Reasoning / Assumption / Limitation / Next Action (tổng thể Phase)

**Objective:** Liệt kê đầy đủ, không né tránh, toàn bộ Bias / Confounding / Missing Variables / Assumption / Generalization đã tích lũy xuyên suốt Phase 1–11, tổng hợp lại thành một reference duy nhất cho Phase 13.

**Reasoning:** Theo Master Guideline: "Không được né tránh." Phase này không tạo insight mới — chỉ tổng hợp và làm rõ mức độ nghiêm trọng (severity) của từng limitation đã được flag rải rác ở các phase trước (Risk Register Phase 4, Standing Disclaimers Phase 5+, D-decisions xuyên suốt).

**Assumption:** Không có limitation mới phát sinh ngoài những gì đã ghi nhận trong Master Summary/Decision Log; Phase 12 chỉ tổng hợp, không tự suy diễn thêm limitation chưa từng được nêu.

**Limitation của chính Phase 12:** Vì đây là tổng hợp, có rủi ro bỏ sót nếu Master Summary/Decision Log thiếu — đối chiếu từng mục với D-decision cụ thể để tránh việc này.

**Next Action:** Sau khi review, chuyển sang Phase 13 (Future Data Collection).

### 12.1 — Bias

| # | Bias | Mô tả | Nguồn (Decision ID) | Mức độ nghiêm trọng |
|---|---|---|---|---|
| B1 | Selection/Sampling bias — không xác định được | Không có sampling frame → không biết 1470 nhân viên này đại diện cho quần thể nào (công ty thật, ngành nào, khu vực nào) | D4.2 | Cao — ảnh hưởng toàn bộ khả năng generalize |
| B2 | Reverse causality bias (Satisfaction) | Không có timestamp đo satisfaction so với thời điểm nghỉ việc → không phân biệt được "satisfaction thấp → nghỉ việc" hay "định nghỉ việc → trả lời survey tiêu cực" | Phase 7 Insight 3 | Trung bình — chỉ ảnh hưởng nhóm finding G2/H4 (đã ở tier Weak) |
| B3 | Attrition-type conflation bias | Gộp voluntary + involuntary attrition làm một → có thể có nhân viên bị sa thải (không phải tự nghỉ) lẫn trong nhóm "attrition" | D5.1 | Cao — ảnh hưởng **mọi** kết luận có chữ "Attrition" |
| B4 | Calibration bias trong model | `class_weight='balanced'` làm probability bị lệch (overconfident ở top decile) | D10.5 | Trung bình — chỉ ảnh hưởng cách đọc probability, không ảnh hưởng ranking |
| B5 | Discrimination-risk bias (age) | Age Group cố tình không tạo làm feature vì rủi ro phân biệt tuổi tác nếu dùng trong HR decision | D8.8 | Thấp (đã được kiểm soát chủ động, không phải rủi ro tồn đọng) |

### 12.2 — Confounding

| # | Confounding | Đã kiểm tra chưa | Kết quả | Còn tồn đọng? |
|---|---|---|---|---|
| C1 | JobRole confound với Heavy OT | Đã kiểm tra (Phase 7, D7.2) | Hiệu ứng OT vẫn tồn tại khi tách Sales/Non-Sales — **không hoàn toàn giải thích bởi JobRole** | Giảm nhưng chưa loại trừ hoàn toàn (chưa kiểm soát đồng thời tất cả biến khác) |
| C2 | "Newness" confound với Pay Percentile | Đã kiểm tra (Phase 7, Insight 2) | Có gap dư ngoài hiệu ứng newness, nhưng finding này đã ở tier Weak (H3 không qua Bonferroni) | Còn tồn đọng — vì tier Weak nên chưa hành động |
| C3 | JobRole confound với BusinessTravel_Frequently | Đã kiểm tra (Phase 7, Insight 5) | Không tập trung riêng ở Sales (còn có Lab Technician, Research Scientist) — **không loại trừ được hoàn toàn** vì n=36 quá nhỏ | Còn tồn đọng, đã note trong D9.4 (CI rộng) |
| C4 | Multicollinearity (JobLevel/MonthlyIncome/TotalWorkingYears/Age, r=0.68–0.95) | Đã xử lý một phần (Phase 8: dùng JobLevel làm proxy duy nhất) | Giảm confounding trong model nhưng **không loại bỏ** — multicollinearity còn lại có thể gây **coefficient instability** (hệ số không ổn định giữa các lần refit/mẫu dữ liệu khác nhau) và **inflated standard errors**, dẫn đến khó khăn trong việc diễn giải độc lập từng hệ số (VD: Pay Percentile coefficient chỉ +0.042 trong mô hình đa biến dù kiểm định univariate có ý nghĩa thống kê — không kết luận được đây là do biến thực sự yếu hay do multicollinearity làm méo ước lượng) | Còn tồn đọng — đã ghi nhận rõ trong Phase 10 |
| C5 | Unobserved confounders (chưa đo được) | Không thể kiểm tra (không có biến) | G7 chỉ kiểm soát được confounder **quan sát được** trong dataset, không kiểm soát được confounder không đo (VD: manager quality, workload thực, career growth thực tế) | Còn tồn đọng, không thể giải quyết với dataset này (D3.2) |

### 12.3 — Missing Variables

| Biến thiếu | Business Impact | Ảnh hưởng cụ thể đến Phase 11 |
|---|---|---|
| Attrition Event detail (voluntary/involuntary, ngày nghỉ) | Cao | Không thể tách causal effect thật của OT/Pay/Travel lên từng loại attrition riêng biệt (B3) |
| Exit Interview | Cao | Không có nguồn xác nhận nguyên nhân thật → mọi recommendation ở Phase 11 dừng ở "associated with" |
| Cost-per-hire / Intervention cost thật | Cao (chặn hoàn toàn S3) | ROI Framework (11.4) không thể tính số thật |
| Real Manager ID | Trung bình | G6 đã bị loại khỏi scope từ Phase 2 vì proxy quá yếu |
| Historical Employee Timeline | Cao cho câu hỏi temporal/causal | Không thể đánh giá "diễn biến" satisfaction/pay trước khi nghỉ việc — chỉ có snapshot |
| Data Dictionary chính thức | Cao (ảnh hưởng mọi biến) | Mọi diễn giải biến (VD: JobLevel là gì thực sự) đều là **giả định**, không xác nhận |

### 12.4 — Assumption (tổng hợp toàn bộ giả định đã chấp nhận xuyên suốt project)

| # | Assumption | Được chấp nhận ở đâu | Rủi ro nếu sai |
|---|---|---|---|
| A1 | "Early attrition" = YearsAtCompany ≤ 1 | D1.1 | Nếu ngưỡng thật của business khác (VD: 6 tháng hoặc 18 tháng), toàn bộ New Hire segmentation, hypothesis test, và model đều cần làm lại |
| A2 | Organizational Investment Segment (JobLevel) ≈ "giá trị nhân viên" | D8.5 | Đây là proxy yếu — nhân viên giỏi chưa thăng chức bị misclassify là "low investment" |
| A3 | OverTime (Yes/No flag) ≈ workload thực tế | Phase 6 (R-note), Phase 7 | Flag nhị phân không phản ánh mức độ OT thực (VD: OT 2h/tuần vs 20h/tuần đều = "Yes") |
| A4 | Combined voluntary+involuntary attrition là chấp nhận được để phân tích | D5.1 | Nếu tỷ lệ involuntary cao trong data thật, toàn bộ diễn giải "nhân viên tự chọn nghỉ vì OT/pay" có thể sai một phần |
| A5 | Không có giả định nào được đưa ra về mức độ đại diện của dataset. Theo D4.2, representativeness **không thể đánh giá được** do không có sampling frame — mọi phát hiện chỉ được diễn giải **trong phạm vi 1470 bản ghi này**, không suy rộng ra bất kỳ quần thể nào, kể cả nội bộ | D4.2 | Nếu người đọc vô tình hiểu "trong phạm vi dataset" là "đại diện cho toàn bộ nhân viên công ty," mọi recommendation ở Phase 11 có thể bị áp dụng sai phạm vi |

**[Future Consideration — chưa phải canonical limitation]:** Master Summary mô tả dataset là "public IBM Watson Analytics synthetic dataset." Nếu trong tương lai cần đánh giá mức độ dữ liệu này phản ánh hành vi nhân viên thật hay được sinh ra bằng rule/thuật toán, đây là một câu hỏi cần được stakeholder/data source xác nhận riêng — không đưa vào Phase 12 chính thức vì chưa có cơ sở quyết định (D-decision) nào trong Master Summary/Decision Log về vấn đề này.

### 12.5 — Generalization

| # | Giới hạn generalization | Cơ sở |
|---|---|---|
| G-1 | Kết luận chỉ áp dụng "trong phạm vi 1470 nhân viên này" | D4.2 |
| G-2 | Không có sampling frame → không thể suy rộng ra ngành/công ty khác | D4.2 |
| G-4 | Model (Logistic Regression) chỉ được validate bằng CV nội bộ, không có external validation set | Phase 10 Known Limitations |

### 12.6 — Bảng tổng hợp Severity (để Phase 13 ưu tiên đề xuất thu thập dữ liệu)

| Nhóm limitation | Mức độ nghiêm trọng tổng thể | Có thể khắc phục bằng thu thập thêm data không? |
|---|---|---|
| B3 (attrition-type conflation) | Cao | Có — cần Attrition Event detail |
| Missing: Exit Interview | Cao | Có |
| Missing: Cost-per-hire | Cao (chặn S3) | Có |
| B1/G-2 (sampling frame) | Cao | **Không** — không thể khắc phục hồi tố, chỉ có thể tránh lặp lại ở dataset tương lai |
| C4 (multicollinearity) | Trung bình | Một phần — cần thêm biến phân biệt (VD: performance review thật thay vì chỉ JobLevel) |
| C5 (unobserved confounders) | Trung bình–Cao | Có — chính là input cho Phase 13 |

---

## PHASE 13 — FUTURE DATA COLLECTION

### 13.0 — Objective / Reasoning / Assumption / Limitation / Next Action (tổng thể Phase)

**Objective:** Đề xuất cụ thể những dữ liệu doanh nghiệp nên thu thập thêm, dựa trực tiếp trên Missing Variables (12.3) và Confounding tồn đọng (12.2) — không đề xuất chung chung, mỗi mục phải trace được về limitation cụ thể.

**Reasoning:** Theo Master Guideline Phase 13: "Giải thích tại sao" cho từng đề xuất. Map 1-1 giữa: dữ liệu thiếu → limitation nó giải quyết → business question nó mở khoá lại.

**Assumption:** Đề xuất này giả định doanh nghiệp có khả năng triển khai thu thập dữ liệu mới (không phải giới hạn kỹ thuật của riêng dataset Kaggle hiện tại) — đây là khuyến nghị cho **lần thu thập dữ liệu tiếp theo**, không áp dụng ngược lại cho dataset đang phân tích.

**Limitation:** Đây là danh sách ưu tiên hoá dựa trên logic (limitation nào chặn nhiều business question nhất → ưu tiên cao), không phải một cost-benefit analysis thật (vì không có budget/chi phí thu thập thật).

**Next Action:** Đây là điểm kết thúc chu trình 13 Phase theo Master Guideline.

### 13.1 — Danh sách dữ liệu cần thu thập, ưu tiên theo mức độ chặn Business Question

| # | Dữ liệu cần thu thập | Giải quyết Limitation nào | Business Question được mở khóa/củng cố | Ưu tiên |
|---|---|---|---|---|
| F1 | **Attrition Event detail** (voluntary/involuntary, ngày resign/terminate) | B3 (attrition-type conflation) — Cao | Tách riêng phân tích cho từng loại attrition; củng cố toàn bộ H1, H2, H6 với độ tin cậy cao hơn | **Cao nhất** |
| F2 | **Exit Interview** (structured, có category hoá lý do) | Missing Exit Interview — Cao; cung cấp bằng chứng giải thích phong phú hơn (richer explanatory evidence) và hỗ trợ điều tra nguyên nhân gốc (root-cause investigation) — **vẫn là dữ liệu observational**, chịu rủi ro self-reporting bias (nhân viên có thể không nêu lý do thật khi trả lời phỏng vấn nghỉ việc), **không** tự động nâng cấp kết luận lên mức causal | Root cause thật cho G1–G8, đặc biệt xác nhận/bác bỏ giả thuyết OT | Cao |
| F3 | **Cost-per-hire + Intervention cost thực tế** (theo từng loại can thiệp) | Chặn hoàn toàn S3 (ROI Framework 11.4) | S1, S3 — biến ROI framework thành số thật | Cao (ảnh hưởng trực tiếp Phase 11 đã làm) |
| F4 | **Pilot/A-B test program data** (nhóm can thiệp vs nhóm đối chứng, cùng thời điểm) | Không thể đo `expected_incremental_retention_lift` (11.4) từ dữ liệu quan sát | Điều kiện tiên quyết để ROI Framework (S3) và mọi recommendation ở Phase 11 chuyển từ "correlational" sang có cơ sở đánh giá hiệu quả thật | Cao |
| F5 | **OverTime dạng liên tục** (số giờ OT thực tế/tuần hoặc /tháng, không chỉ Yes/No) | A3 (OT flag không phản ánh cường độ) | Cho phép kiểm định dose-response thay vì chỉ nhị phân — củng cố hoặc bác bỏ H2 ở mức chi tiết hơn | Trung bình-Cao |
| F6 | **Historical Employee Timeline** (lương, satisfaction, promotion, manager theo thời gian, có timestamp) | Reverse causality bias (B2); Missing Historical Timeline | Giải quyết trực tiếp vấn đề "satisfaction thấp gây nghỉ việc hay ngược lại" (G2/H4) | Trung bình |
| F7 | **Real Manager ID + Manager-level metrics** (VD: manager tenure, span of control, manager turnover) | G6 (đã loại khỏi scope Phase 2 vì proxy yếu) | Mở lại G6 — một biến quan trọng trong thực tế HR nhưng hiện không đo được | Trung bình |
| F8 | **Direct performance/value measure** (360-review, manager qualitative rating, hoặc productivity metric) | D1.3 (Valuable employee không có direct measure) | Thay thế Organizational Investment Segment (proxy JobLevel, D8.5) bằng đo lường trực tiếp hơn — giảm rủi ro misclassify | Trung bình |
| F9 | **Data Dictionary / HR Policy / Metric Definition chính thức** | Missing Data Dictionary — ảnh hưởng diễn giải mọi biến | Không mở business question mới, nhưng tăng độ tin cậy diễn giải cho toàn bộ project | Trung bình (nền tảng, không cấp bách bằng F1-F4) |
| F10 | **Sampling frame / metadata nguồn dữ liệu** (công ty nào, ngành nào, thời điểm thu thập, phương pháp lấy mẫu) | B1/G-2 (representativeness không xác định) | Cho phép đánh giá generalization — hiện tại không thể làm gì nếu thiếu mục này. **Dù không mở khóa ngay bất kỳ quyết định kinh doanh cụ thể nào ở Phase 11, đây là yếu tố nền tảng quyết định external validity của mọi phân tích tương lai dùng dataset tương tự — thiếu nó, mọi kết luận (kể cả Strong tier) sẽ mãi bị giới hạn ở "trong phạm vi dataset này" mà không bao giờ có cơ sở suy rộng ra ngoài.** | Thấp-Trung bình (không ảnh hưởng phân tích nội bộ, chỉ ảnh hưởng khả năng suy rộng) |

### 13.2 — Giải thích ưu tiên hóa (tại sao F1–F4 đứng đầu)

**Objective:** Trả lời "tại sao nhóm này ưu tiên hơn nhóm kia" thay vì chỉ liệt kê.

**Reasoning:**
- F1–F3 được xếp cao nhất vì chúng **trực tiếp chặn** các quyết định đã đưa ra ở Phase 11 (S1, S3) — tức là nếu không có, Phase 11 mãi mãi chỉ dừng ở framework, không bao giờ thành hành động cụ thể.
- F4 (pilot data) đứng cao vì đây là điều kiện **duy nhất** hợp lệ về mặt phương pháp luận để đo `expected_incremental_retention_lift` — nếu không có F4, ROI Framework ở 11.4 sẽ mãi là công thức rỗng.
- F5–F8 cải thiện **độ chính xác** của các finding đã có (Strong/Moderate/Weak tier ở Phase 9) nhưng không chặn hoàn toàn business question nào — do đó ưu tiên thấp hơn.
- F9–F10 là nền tảng phương pháp luận (methodological hygiene), quan trọng về lâu dài nhưng không ảnh hưởng đến quyết định cụ thể nào đang chờ ở Phase 11.

**Assumption:** Thứ tự ưu tiên này dựa trên logic "gỡ chặn nhiều business question nhất trước," không phải một mô hình cost-benefit có trọng số thật — vì không có chi phí thu thập thật để tính.

**Limitation:** Nếu doanh nghiệp có ràng buộc ngân sách/thời gian thực tế khác với giả định "ưu tiên theo mức độ chặn," thứ tự này cần được điều chỉnh lại — đây là gợi ý logic, không phải quyết định cuối cùng.

### 13.3 — Lưu ý quan trọng: F4 không chỉ là "thu thập thêm dữ liệu"

Cần nêu rõ: F4 (pilot/A-B test) khác về **bản chất** so với F1, F2, F3, F5–F10. Các mục còn lại là *thu thập thêm dữ liệu quan sát (observational)*, trong khi F4 đòi hỏi **thiết kế thực nghiệm chủ động** (chọn nhóm can thiệp, nhóm đối chứng, đo lường trước/sau). Đây là bước bắt buộc phải có trước khi bất kỳ can thiệp nào ở Phase 11 (11.3) được triển khai đại trà, theo đúng nguyên tắc đã thống nhất: **"Bất kỳ can thiệp nào đều phải được xác thực qua một pilot program có success metrics định trước."**

### 13.4 — Vấn đề cần xác nhận

1. Thứ tự ưu tiên F1–F10 có phù hợp với constraint thực tế nào của doanh nghiệp (nếu có)?
2. Không phát hiện mâu thuẫn giữa Phase 13 và Phase 1–12.

---

*End of Master Summary — Phases 1 through 13. Governance-tracked; cross-referenced against Decision Log (see D10.7, D11.1–D11.6, D12.1–D12.4, D13.1–D13.4, DX.3).*

