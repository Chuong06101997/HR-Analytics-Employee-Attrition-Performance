# Full-Document QA Review (Read as One Continuous Report)

Reading start to finish, four issues surfaced that wouldn't have been visible reviewing sections in isolation:

1. **Repetition:** The BusinessTravel / small-subgroup point is fully explained four separate times (Section 4 finding, Section 4 clarification, Section 6 Monitor bullet, Section 8 limitation). A reader going straight through notices the same explanation recurring. Trimming to one full explanation (Section 4) with brief references elsewhere.
2. **Terminology drift:** Section 4 calls the evidence system the "Evidence Strength Summary," Section 7 calls it the "Evidence Hierarchy." These name the same underlying artifact — unifying to one term throughout.
3. **Redundant proxy explanation:** Section 7 and Section 8 both explain the JobLevel misclassification risk in full, in different words. Per the brief, Section 8 is where the *expanded* rationale belongs — trimming Section 7 to a pointer rather than a second full explanation.
4. **Thin transitions:** Several section breaks (4→5, 5→6, 7→8, 10→table) cut abruptly. Adding one bridging sentence at each, without adding new content.

No finding, evidence tier, statistic, or Decision Log reference is changed. Below is the complete, publication-ready document.

---

# Project Summary

## 1. Executive Overview

Employee attrition is expensive under any circumstances, but it is particularly costly when it happens early — before a new hire has had the chance to become fully productive. When that happens, organizations often respond with intuition rather than evidence: raise pay, cut overtime, run an engagement survey. These responses may or may not be correct, and without verification, there is no way to know which.

This project was built to close that gap. The goal was not simply to build a model, but to establish which factors are genuinely associated with early attrition, to be explicit about how confident we can be in each one, and to turn that into guidance HR could act on without overstating what the data actually supports.

The analysis was conducted on a dataset of 1,470 employees, using a structured 13-phase process designed specifically to prevent two common failure modes in this kind of work: treating a plausible-sounding pattern as proven fact, and quietly narrowing the scope of the analysis to avoid dealing with inconvenient gaps in the data.

---

## 2. Business Questions

The investigation was organized around four categories of questions, moving from description to action:

- **Descriptive** — How does attrition differ between new hires and longer-tenured employees, and what does the profile of early leavers actually look like?
- **Diagnostic** — Which factors — overtime, pay, satisfaction, business travel, promotion history — are associated with early attrition, and which of those hold up once other factors are accounted for?
- **Predictive** — Can attrition risk be estimated for currently employed staff, to help prioritize where retention effort should go?
- **Prescriptive** — Once drivers are identified, what interventions would be realistic, and how should limited retention effort be prioritized?

Two prescriptive questions — estimating a real return on investment for retention programs — could not be fully answered, because the cost data required to answer them does not exist in this dataset. Rather than force an answer or drop the question, both were kept explicitly open. That distinction matters: a project that quietly avoids hard questions is easy to mistake for a project that has already answered them.

---

## 3. Analytical Journey

The project followed a fixed sequence of stages. Each one existed to close a specific gap before the next stage was allowed to begin — not as a checklist, but because skipping any of them would have let a weaker conclusion pass as a stronger one.

**Business Understanding** started the project by defining terms that were originally left vague — "early attrition" and "valuable employee" — before any data was examined.

**Data Audit** established what the available data could actually support, rather than assuming it was sufficient because it looked complete.

**Exploratory Analysis** surfaced candidate patterns, but every pattern was tested against at least one alternative explanation before being taken seriously.

**Feature Engineering** turned raw data into business-meaningful variables — including one clearly labeled proxy, used only where no direct measure existed.

**Hypothesis Testing** formally tested each candidate pattern, and was treated as exploratory evidence rather than confirmed fact, since the hypotheses came from the same data being tested.

**Predictive Modeling** combined the strongest signals into a tool for ranking risk, once the individual factors behind it had already been evaluated on their own merit.

**Business Recommendation** converted findings into guidance, with each recommendation's confidence explicitly tied to the strength of the evidence behind it.

**Risk Assessment** catalogued where the analysis could be wrong, misapplied, or trusted more than it should be.

**Documentation & Governance** recorded the reasoning behind every material decision made along the way — not just the conclusions, but why they were reached.

---

## 4. Key Findings

Findings below are presented exactly according to the project's evidence hierarchy — the same Strong / Moderate / Weak / Not Supported classification referenced throughout this report. Weaker findings are not hidden, but their confidence level is not inflated to match the stronger ones either.

**Strong Evidence**
- Attrition is meaningfully higher among employees in their first year than among longer-tenured employees.
- Heavy overtime is associated with substantially higher attrition among new hires.

**Moderate Evidence**
- Frequent business travel is associated with higher attrition among new hires. This finding rests on a small subgroup and carries real uncertainty, so it is held at a lower confidence level than the two findings above.

**Weak / Exploratory Evidence**
- A residual pay gap — beyond the general effect of simply being new — shows some association with early attrition, but not enough to justify standalone action yet.
- Job satisfaction shows some association with early attrition. The other satisfaction-related measures tested (environment, relationships, involvement) did not show a reliable relationship and are not carried forward as findings.

**Not Supported**
- No meaningful interaction was found between overtime and job satisfaction. The data does not support treating them as a compounding risk — they behave as two separate signals, not one combined effect.

One distinction is worth stating plainly here, because it shapes both the model in Section 5 and the recommendations in Section 6: evidence strength for a *business conclusion* and predictive usefulness inside a *model* are not the same thing. Business travel is the clearest example — Moderate evidence is enough to justify including it as a signal the model can use, but not enough, on its own, to justify a standalone policy decision. A factor can be useful to a model and still not be ready for a business decision on its own.

All findings above describe association, not cause. Nothing in this dataset allows us to say that any one factor *causes* attrition — only that it tends to appear alongside it.

---

## 5. Predictive Modeling

With the individual drivers above established on their own evidence, the next question was whether they could be combined into something forward-looking: an estimate of relative attrition risk among currently employed staff, built to help HR know where to look first, not to make decisions on its own.

Two modeling approaches were evaluated, and their performance came out close enough that performance alone didn't settle the choice. What did settle it was communication. The selected model's coefficients, odds ratios, and direction of association can be explained directly to a business audience in plain terms — "this factor increases risk, that one decreases it, by roughly this much" — in a way the alternative approach could not offer as clearly. For a tool meant to inform HR conversations, that clarity carried real weight.

One limitation was identified during evaluation and is treated as a hard constraint on how this model should be used: its raw predicted probabilities are not well-calibrated. In practice, that means a prediction like "80% risk" should not be read literally as an 80% chance of leaving — the underlying calibration wasn't tight enough to support that interpretation. What the model *does* support reliably is relative ranking: telling you that one employee's risk is meaningfully higher than another's, even when the exact percentage attached to either can't be taken at face value.

That distinction shapes how the model is meant to be used. It's a prioritization tool — a way to decide who HR should look at first — not an automated verdict on any individual, and not a source of literal probabilities to quote in a report.

---

## 6. Business Recommendations

The same principle from Section 4 governs how these recommendations are tiered: a factor being useful inside the model is not the same as a factor being ready for a standalone business decision.

**Action Now (Strong Evidence)**
- Build a proactive monitoring and support mechanism for employees in their first 12 months — this is where attrition risk is most concentrated, and the evidence behind it is the strongest in the project.
- Review overtime allocation for new hires, with particular attention to the teams where the effect is most pronounced. Any specific policy change should be validated through a small pilot with a predefined success measure before being rolled out more broadly — the evidence supports concern, not yet a specific fix.

**Monitor (Moderate / Weak Evidence)**
- Continue tracking business travel frequency for new hires. As noted above, it contributes useful signal to the risk model but sits on too small a subgroup to justify a travel policy change on its own.
- Track pay positioning and job satisfaction for new hires on an ongoing basis. Neither currently warrants standalone action, but both are worth continued observation as more data accumulates.

**Further Investigation Required**
- A structured framework exists for evaluating the return on investment of a retention intervention, but it cannot produce a real number today. Three specific inputs are missing: how effective any given intervention actually is, what it would cost to run, and what the organization's true cost of losing an employee is. Until at least these three exist, ROI stays a framework to be filled in, not a figure to act on.
- No recommendation is made for a combined overtime-and-satisfaction intervention. The data did not support treating these as a compounding risk, so they should continue to be addressed as two separate, independent signals rather than one combined program.

---

## 7. Governance Highlights

What separates this project from a one-off analysis is a set of practices that exist specifically to keep its conclusions honest over time — not just at the moment they were written.

A **Decision Log** exists because conclusions are only as trustworthy as the reasoning behind them. Every material choice in this project — how "early attrition" was defined, which features were built or rejected — is recorded so that later readers, including a future version of this same analysis, can trace *why* a decision was made, not just *what* was decided.

The **evidence hierarchy** used throughout Sections 4 and 6 exists because not every finding deserves the same level of trust. Sorting findings into Strong, Moderate, and Weak — and holding that line even when a Moderate finding would have made for a punchier headline — is what keeps the recommendations honest.

A **Risk Register**, maintained from the first phase through the last, exists because risks to an analysis' validity are easier to manage if they're tracked continuously rather than discovered at the end.

**Full traceability** connects each business question to the analysis that addressed it and the recommendation that followed — so the entire chain of reasoning can be audited, not just accepted on faith.

**Explicit assumption management** exists because proxies are sometimes unavoidable. Where a stand-in variable was used for something the data couldn't measure directly, that substitution is documented openly rather than presented as if it were the real thing — Section 8 covers the specific case and its risk in more detail.

A **Calibration Assessment** was run on the predictive model for one reason: to prevent its output from being misread as a literal probability by anyone who wasn't there for the modeling work.

Together, these practices are what let this project's conclusions be reused and trusted later, rather than simply taken at face value now.

---

## 8. Limitations

The governance practices above exist because this project has real boundaries — worth stating plainly rather than tucking into a footnote.

**The dataset is synthetic and publicly available** (IBM Watson Analytics, via Kaggle), not a live company's operational HR data. Everything here demonstrates a method, not a fact about any specific real-world workforce.

**The data is cross-sectional** — a single snapshot in time, not a timeline. There's no way to build a genuine before-and-after picture for any one employee.

**No causal inference is possible.** Every relationship identified is an association. This project can tell you what tends to travel together with attrition — it cannot tell you what causes it.

**No exit interview data exists**, so the actual reason any given employee left is unknown; the analysis works from correlated factors, not stated causes.

**External validity is limited.** There's no information on how these 1,470 employees were sampled, so nothing here is claimed to generalize to another company or industry.

**Several findings rest on much smaller subgroups than the headline number suggests.** The dataset contains 1,470 employees, but once the analysis narrows to new hires — and further, to specific combinations within that group — the working sample can shrink to a few dozen people. That's not a flaw in the method, but it is a real constraint: smaller subgroups carry wider uncertainty, which is exactly why some findings are held at Moderate confidence rather than Strong, regardless of how the underlying pattern looks on the surface.

**The `Organizational Investment Segment` proxy carries a specific, acknowledged risk.** No variable in this dataset directly measures how much an organization has invested in an employee, so JobLevel was used as the closest available stand-in. That choice wasn't just a statistical convenience — it reflects a real business reality that there often isn't a clean, single number for "investment" in a person. But the substitution has a real cost: an employee who is highly capable but hasn't yet been promoted could be misclassified as "low investment" simply because JobLevel hasn't caught up with their actual value. This proxy should be read as a reasonable approximation, not a precise measure.

**The predictive model is not deployment-ready on its raw output.** As covered in Section 5, its probabilities are not well-calibrated — it supports relative risk ranking, not literal percentage claims, without further calibration work.

---

## 9. Future Roadmap

Addressing the limitations above is largely a matter of better data and more rigorous validation. If this project were extended inside a real organization, the natural next steps would be:

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

For a fast reference, the table below summarizes each core business question, its answer, and the evidence behind it.

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
