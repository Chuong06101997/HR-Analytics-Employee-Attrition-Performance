# Changelog

All notable changes made during the development and review process are documented here.

---

## v1.2 (Post-review refinements)

### Changed

- Clarified the distinction between predictive features and actionable business evidence. BusinessTravel remains in the predictive model to account for additional predictive information but is intentionally excluded from business recommendations due to limited evidence strength.

- Clarified the rationale for selecting Logistic Regression. The model was selected because its coefficients, odds ratios, and direction of association are easier to explain to business stakeholders. Predicted probabilities are used only for relative risk ranking because calibration is insufficient for literal probability interpretation.

- Expanded the business rationale for using JobLevel as a proxy for Organizational Investment.

- Renamed the Bonferroni significance column to indicate it is for reference only rather than a decision gate.

- Added a Business Question → Answer → Confidence summary table.

- Clarified that the top-30% risk threshold is a placeholder pending HR capacity and ROI optimization.

- Expanded ROI limitations by explicitly noting that intervention effectiveness cannot be estimated from observational data.

### Documentation

- Updated Decision Log.
- Updated Risk Register.
- Improved governance documentation.
