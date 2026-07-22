# Internal QA Review — Part 1 (Sections 1-4)

Before rewriting, reviewing the existing sections against the source documents:

**Section 1 (Executive Overview):** Consistent, no issues. Business framing is solid.

**Section 2 (Business Questions):** Consistent, but slightly thin — doesn't explicitly flag which questions ended up "insufficient data" (S1/S3 ROI), which is a governance point worth surfacing here rather than only in Section 9's new table.

**Section 3 (Analytical Journey):** Consistent. Wording is a bit textbook ("to pin down," "to translate") — repetitive infinitive-phrase structure across all nine stages reads mechanically. Will vary sentence construction.

**Section 4 (Key Findings):** This is where the required improvement #1 belongs — the original has no mention of BusinessTravel's dual role (predictive feature in the model vs. excluded from standalone recommendation). This distinction needs to be introduced here so Section 6 doesn't feel disconnected from it. Also, "Not Supported" finding (OT×Satisfaction interaction) is correctly stated but could be tightened for executive pace.

No evidence tier, statistic, or Decision ID is being changed — only structure, flow, and the one required clarification are being added.

---

# Project Summary — Part 1

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

Findings below are presented exactly according to the project's Evidence Strength Summary. Weaker findings are not hidden, but their confidence level is not inflated to match the stronger ones either.

**Strong Evidence**
- Attrition is meaningfully higher among employees in their first year than among longer-tenured employees.
- Heavy overtime is associated with substantially higher attrition among new hires.

**Moderate Evidence**
- Frequent business travel is associated with higher attrition among new hires. This finding is based on a small subgroup and carries real uncertainty, so it is treated with less confidence than the two findings above — worth noting, not worth acting on alone.

**Weak / Exploratory Evidence**
- A residual pay gap — beyond the general effect of simply being new — shows some association with early attrition, but not enough to justify standalone action yet.
- Job satisfaction shows some association with early attrition. The other satisfaction-related measures tested (environment, relationships, involvement) did not show a reliable relationship and are not carried forward as findings.

**Not Supported**
- No meaningful interaction was found between overtime and job satisfaction. The data does not support treating them as a compounding risk — they behave as two separate signals, not one combined effect.

One clarification worth stating plainly: evidence strength for a *business conclusion* and predictive usefulness inside a *model* are not the same thing. Business travel, for example, remains in the predictive model in Section 5 because it adds useful signal for ranking risk — but it is intentionally excluded from the standalone action items in Section 6, precisely because Moderate evidence on a small subgroup is not yet a sound basis for a policy change. A factor can be useful to a model and still not be ready for a business decision on its own.

All findings above describe association, not cause. Nothing in this dataset allows us to say that any one factor *causes* attrition — only that it tends to appear alongside it.

---

**Part 1 complete.** Say the word and I'll move to Part 2 (Predictive Modeling, Business Recommendations, Governance Highlights).
