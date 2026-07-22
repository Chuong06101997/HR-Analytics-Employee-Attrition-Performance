# Internal QA Review — Part 2 (Sections 5-7)

**Section 5 (Predictive Modeling):** This is where required improvement #2 lands directly. The original phrasing ("chosen because it is interpretable") is too shallow — it doesn't explain *what* interpretability means in practice (coefficients, odds ratios, direction of association) or connect it to *why* that matters for this audience. Also needs to state clearly that predicted probabilities are not read literally, and why — calibration was insufficient, not just "a limitation to note."

**Section 6 (Business Recommendations):** Mostly consistent, but needs to explicitly reflect the Predictive Feature vs. Business Action distinction just introduced in Part 1 — right now it's implicit rather than stated. Also this is where improvement #5 (ROI clarification) belongs: the original mentions the ROI framework exists but doesn't spell out the three specific missing inputs (intervention effectiveness, intervention cost, organizational cost data) as clearly as the brief requires.

**Section 7 (Governance Highlights):** Content is solid and doesn't need new findings — but the original reads as a flat list with reasons bolted on. Tightening flow so each governance practice reads as "why it exists" rather than "what it is + why" as two disconnected clauses.

No evidence tier, statistic, or Decision ID is being changed — only clarity, connective tissue back to Part 1, and the required additions.

---

# Project Summary — Part 2

## 5. Predictive Modeling

A model was built to estimate relative attrition risk among currently employed staff — not to make decisions, but to help HR know where to look first.

Two modeling approaches were evaluated, and their performance came out close enough that performance alone didn't settle the choice. What did settle it was communication. The selected model's coefficients, odds ratios, and direction of association can be explained directly to a business audience in plain terms — "this factor increases risk, that one decreases it, by roughly this much" — in a way the alternative approach could not offer as clearly. For a tool meant to inform HR conversations, that clarity carried real weight.

One limitation was identified during evaluation and is treated as a hard constraint on how this model should be used: its raw predicted probabilities are not well-calibrated. In practice, that means a prediction like "80% risk" should not be read literally as an 80% chance of leaving — the underlying calibration wasn't tight enough to support that interpretation. What the model *does* support reliably is relative ranking: telling you that one employee's risk is meaningfully higher than another's, even when the exact percentage attached to either can't be taken at face value.

That distinction shapes how the model is meant to be used. It's a prioritization tool — a way to decide who HR should look at first — not an automated verdict on any individual, and not a source of literal probabilities to quote in a report.

---

## 6. Business Recommendations

Recommendations below are tiered directly to the evidence behind them, following the same logic introduced in Section 4: a factor being useful inside the model is not the same as a factor being ready for a standalone business decision.

**Action Now (Strong Evidence)**
- Build a proactive monitoring and support mechanism for employees in their first 12 months — this is where attrition risk is most concentrated, and the evidence behind it is the strongest in the project.
- Review overtime allocation for new hires, with particular attention to the teams where the effect is most pronounced. Any specific policy change should be validated through a small pilot with a predefined success measure before being rolled out more broadly — the evidence supports concern, not yet a specific fix.

**Monitor (Moderate / Weak Evidence)**
- Continue tracking business travel frequency for new hires as a contributing factor, without changing travel policy on this basis alone. It plays a useful role in the predictive model — helping rank who's at higher risk — but the underlying subgroup is small enough that treating it as a standalone justification for policy change would outrun what the evidence actually supports.
- Track pay positioning and job satisfaction for new hires on an ongoing basis. Neither currently warrants standalone action, but both are worth continued observation as more data accumulates.

**Further Investigation Required**
- A structured framework exists for evaluating the return on investment of a retention intervention, but it cannot produce a real number today. Three specific inputs are missing: how effective any given intervention actually is, what it would cost to run, and what the organization's true cost of losing an employee is. Until at least these three exist, ROI stays a framework to be filled in, not a figure to act on.
- No recommendation is made for a combined overtime-and-satisfaction intervention. The data did not support treating these as a compounding risk, so they should continue to be addressed as two separate, independent signals rather than one combined program.

---

## 7. Governance Highlights

What separates this project from a one-off analysis is a set of practices that exist specifically to keep its conclusions honest over time — not just at the moment they were written.

A **Decision Log** exists because conclusions are only as trustworthy as the reasoning behind them. Every material choice in this project — how "early attrition" was defined, which features were built or rejected — is recorded so that later readers, including a future version of this same analysis, can trace *why* a decision was made, not just *what* was decided.

An **Evidence Hierarchy** exists because not every finding deserves the same level of trust. Sorting findings into Strong, Moderate, and Weak — and holding that line even when a Moderate finding would have made for a punchier headline — is what keeps the recommendations in Section 6 honest.

A **Risk Register**, maintained from the first phase through the last, exists because risks to an analysis' validity are easier to manage if they're tracked continuously rather than discovered at the end.

**Full traceability** connects each business question to the analysis that addressed it and the recommendation that followed — so the entire chain of reasoning can be audited, not just accepted on faith.

**Explicit assumption management** exists because proxies are sometimes unavoidable. Where JobLevel was used to stand in for something the data couldn't measure directly, that substitution — and its specific risk of misclassifying people — is documented openly rather than presented as if it were the real thing.

A **Calibration Assessment** was run on the predictive model for one reason: to prevent its output from being misread as a literal probability by anyone who wasn't there for the modeling work.

Together, these practices are what let this project's conclusions be reused and trusted later, rather than simply taken at face value now.

---
