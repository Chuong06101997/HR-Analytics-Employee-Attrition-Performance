# Internal QA Review — Part 3 (Sections 8-10 + new Business Question Summary)

**Section 8 (Limitations):** This is where two required improvements land. Improvement #3 (expanded JobLevel proxy rationale) belongs here in full — the earlier mention in Section 7 was appropriately brief for a governance overview, but the brief specifically asks for expanded business reasoning plus an explicit acknowledgment of its limitation, which deserves its own treatment rather than a repeated one-liner. Improvement #4 (subgroup sample size) is currently implicit — it's alluded to via the BusinessTravel finding in Section 4/6, but never stated as a standalone, general limitation of the project. Needs its own bullet.

**Section 9 (Future Roadmap):** Consistent, no factual issues. Slight tightening for executive pace.

**Section 10 (Final Reflection):** Consistent. Keeping the core message but trimming overlap with what Section 7 already said, so it doesn't feel repeated.

**New section (Business Question Summary):** Building this table now. One deliberate exclusion: I'm not including a row for "after controlling for other factors, which drivers remain associated with attrition" (the multivariable question) — the project's own governance record shows this was deliberately left unresolved as a standalone finding rather than formally answered, and adding a confident-sounding row for it here would overclaim past what the project actually settled. Also excluding the "valuable employee distribution" descriptive questions, since those were formally retired rather than answered — including them would risk resurrecting a closed item. The table only includes questions with a real, traceable answer.

No evidence tier, statistic, or Decision ID is being changed — only the two required expansions and the new closing table.

---

# Project Summary — Part 3

## 8. Limitations

This project's conclusions come with real boundaries, and they're worth stating plainly rather than tucking into a footnote.

**The dataset is synthetic and publicly available** (IBM Watson Analytics, via Kaggle), not a live company's operational HR data. Everything here demonstrates a method, not a fact about any specific real-world workforce.

**The data is cross-sectional** — a single snapshot in time, not a timeline. There's no way to build a genuine before-and-after picture for any one employee.

**No causal inference is possible.** Every relationship identified is an association. This project can tell you what tends to travel together with attrition — it cannot tell you what causes it.

**No exit interview data exists**, so the actual reason any given employee left is unknown; the analysis works from correlated factors, not stated causes.

**External validity is limited.** There's no information on how these 1,470 employees were sampled, so nothing here is claimed to generalize to another company or industry.

**Several findings rest on much smaller subgroups than the headline number suggests.** The dataset contains 1,470 employees, but once the analysis narrows to new hires — and further, to specific combinations like new hires who travel frequently — the working sample can shrink to a few dozen people. That's not a flaw in the method, but it is a real constraint: smaller subgroups carry wider uncertainty, which is exactly why findings like business travel are held at Moderate confidence rather than Strong, regardless of how the underlying pattern looks on the surface.

**The `Organizational Investment Segment` proxy carries a specific, acknowledged risk.** No variable in this dataset directly measures how much an organization has invested in an employee, so JobLevel was used as the closest available stand-in. That choice wasn't just a statistical convenience — it reflects a real business reality that there often isn't a clean, single number for "investment" in a person. But the substitution has a real cost: an employee who is highly capable but hasn't yet been promoted could be misclassified as "low investment" simply because JobLevel hasn't caught up with their actual value. This proxy should be read as a reasonable approximation, not a precise measure.

**The predictive model is not deployment-ready on its raw output.** As covered in Section 5, its probabilities are not well-calibrated — it supports relative risk ranking, not literal percentage claims, without further calibration work.

---

## 9. Future Roadmap

If this project were extended inside a real organization, the natural next steps would be:

- **Validate against real HR data**, rather than relying solely on this public dataset, to confirm whether the same patterns hold in a live operational setting.
- **Collect exit interview data**, to get closer to actual stated reasons for departure rather than relying on associated factors alone.
- **Run a pilot** for the overtime and onboarding-related recommendations, with a control group and a predefined success metric, before any wider rollout.
- **Estimate intervention effectiveness properly**, using pilot or experimental data — the observational data used here simply cannot answer that question on its own.
- **Improve probability calibration** on the model, so its output can be used more literally if that ever becomes operationally necessary.
- **Build a monitoring dashboard**, so HR can track these risk indicators on an ongoing basis instead of treating this as a one-time analysis.

---

## 10. Final Reflection

The most valuable thing this project produced isn't a model score. It's a habit of letting evidence — not intuition, and not how convincing something sounds — decide what gets recommended and how confidently.

Correlation was used throughout to decide where to look further, never as proof of why something happens. Where the evidence held up, the recommendations say so directly. Where it didn't, they say that too, instead of dressing up a hunch as a finding.

A model is only as useful as the honesty of its limitations. Used well, it supports the judgment of the person making the call — it doesn't replace them. And a project willing to document its own uncertainty, rather than hide it, ends up more trustworthy than one that claims more certainty than the evidence can actually carry.

---

## Business Question Summary

| Business Question | Answer | Evidence Strength |
|---|---|---|
| Is attrition higher among new hires than longer-tenured employees? | Yes — attrition is meaningfully higher in the first year of tenure. | **Strong** |
| Is heavy overtime associated with attrition among new hires? | Yes — overtime shows a substantial association with early attrition. | **Strong** |
| Is frequent business travel associated with attrition among new hires? | Yes, directionally — but based on a small subgroup with real uncertainty. | **Moderate** |
| Is there a pay gap associated with early attrition, beyond the general "new hire" pay effect? | A residual gap exists, but not strongly enough to justify standalone action. | **Weak / Exploratory** |
| Is job satisfaction associated with early attrition? | Some association found for job satisfaction specifically; other satisfaction measures did not hold up. | **Weak / Exploratory** |
| Does overtime combine with low satisfaction to compound attrition risk? | No — no meaningful interaction was found; the two behave as separate signals. | **Not Supported** |
| Can attrition risk be estimated for currently employed staff? | Yes, for relative risk ranking — not for literal probability, due to calibration limits. | **Supported (ranking only)** |
| What is the return on investment of a retention intervention? | Cannot be estimated with current data; a framework exists but requires real cost and effectiveness data to complete. | **Insufficient Data** |

---

