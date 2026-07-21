# Out of every 100 new hires this year, about 35 won't be here next year.

You already know who left. That's sitting in the system already.

The harder question is: among the people **currently** sitting next to you, who's about to leave next — and who's actually worth fighting to keep?

That's the question this analysis tries to answer.

---

## How costly is this problem, really?

A new hire leaving within the first year doesn't just cost a rehire. It's training time that never paid off, manager hours spent coaching someone who's about to walk out, and knowledge lost before it gets passed on.

Leadership usually already has a favorite theory: "Raise pay," "Cut OT," "Improve morale." Sounds reasonable.

But targeting the wrong group with the wrong reason burns budget and fixes nothing.

---

## Confirmed findings (strong evidence)

The two findings below passed formal statistical testing (chi-square, z-test, tight confidence intervals) and are rated **Strong evidence** — solid enough to act on:

**1. New hires leave at a much higher rate than tenured employees.**
Attrition among employees with under 1 year of tenure is 34.9%, versus 8.1% among those with over 11 years — roughly a **4.3x** gap. This is a direct descriptive comparison in the raw data, not a confound-adjusted figure.

**2. Within the new-hire group, employees working heavy overtime leave at a noticeably higher rate.**
55.1% (with OT) versus 25.3% (without OT) — roughly a **2.2x** gap. We checked whether this was just a Sales-department artifact — it isn't; the effect holds both inside and outside Sales, just more pronounced in Sales.

Both numbers describe an observed difference only — **not** the added risk caused by OT or by being new — the data doesn't support a causal claim here.

---

## Hypotheses still under watch (not yet actionable)

**Frequent business travel (BusinessTravel_Frequently)** — a fairly clear signal in the observed group, but the sample is only 36 people, so the confidence interval is wide. Rated **Moderate**: worth noting, but not a solid basis for policy on its own.

**Below-market pay for the role** and **low job satisfaction** — there's a gap between leavers and stayers, but it's small and doesn't hold up strongly after adjustment. Rated **Weak/exploratory**: keep monitoring, but don't roll out a pay policy or a broad engagement survey based on these two alone.

**Interaction between OT and satisfaction** (e.g. "OT hits harder for already-unsatisfied employees") — tested directly, **no evidence found** for this compounding effect. Treat the two as independent for now.

---

## Recommended actions

1. **Prioritize retention resources in the first 12 months** — this is the highest-risk window per Finding #1, not something to spread evenly across all employees.
2. **Within the new-hire group, review OT allocation first** — this is the clearest lever HR can actually pull directly (unlike commute distance or age). Start with Sales, where the effect is most visible.
3. **Hold off on a company-wide pay policy or morale survey** — run a small pilot first, measure real impact, then scale.
4. **Use the risk-ranking tool as a prompt for who to talk to first** — not as an automated decision-maker for termination, pay, or performance calls on individuals. A human review is always required.

---

## What to be careful about before using this

- This is public sample data (IBM, via Kaggle) — not any specific company's real data. It's a demonstration of approach, not a conclusion ready for direct application to a real organization.
- It's a single point-in-time snapshot (no real hire/exit dates) — so every finding is "A and B tend to move together," not "A causes B."
- There's no real exit-interview data, and voluntary vs. involuntary attrition isn't distinguished — so the true reason employees left isn't known for certain.
- The risk-ranking tool outputs a percentage, but that number **shouldn't be read literally** ("80%" doesn't mean an actual 80% chance of leaving) — it's only reliable for ranking who's riskier than whom.
- There's no basis to claim these 1,470 employees represent any broader population — every conclusion is scoped to this dataset only.

---

**If put to real use, this analysis helps HR know who to call in for a conversation first, instead of guessing or waiting until the resignation letter is already on the desk.**

---

## Technical details (summary — full detail in the notebook)

- Data: 1,470 employees, IBM HR Attrition dataset (Kaggle), single point-in-time snapshot.
- "Early attrition" = `YearsAtCompany ≤ 1`.
- Model: Logistic Regression, chosen over Random Forest for better interpretability for HR (both models performed comparably under 5-fold CV). ROC-AUC ≈ 0.78–0.79.
- Full statistical test detail (test type, p-value, OR, CI), evidence-tier breakdown, and decision log: see the notebook and `Decision_Log.md`.
