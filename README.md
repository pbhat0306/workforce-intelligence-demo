# Workforce Retention Risk — Tableau + AI Insight Layer

A small prototype exploring what **agentic analytics** could look like for workforce data:
a Tableau dashboard you *pull*, paired with an insight layer that *comes to you*.

**Live demo → https://YOUR-USERNAME.github.io/workforce-intelligence-demo/**

---

## What it does

| Piece | What it demonstrates |
|---|---|
| **Embedded Tableau dashboard** | Built in Tableau Public on the synthetic dataset — attrition trend, division/role breakdowns, pay-model heat map, risk cohort profile |
| **Auto-detected insights** | Drivers, trends and outliers written in plain language, recomputed live |
| **Ask the data** | Natural-language questions answered from the same dataset |
| **Proactive alert** | A Slack-style card with the top finding and a recommended next action |

The two halves are **wired together**. The page uses the [Tableau Embedding API v3](https://help.tableau.com/current/api/embedding_api/en-us/docs/embedding_api_about.html)
to listen for `filterchanged` events on the embedded dashboard, reads the applied filter
values, and recomputes the narrative, the alert and the Q&A against that filtered slice.
Change a filter in Tableau and the insight panel follows.

## The analytical story

The dataset covers an entire 12,800-person workforce — Sales, Field Operations,
Monitoring & Customer Care, and Corporate (Finance, IT, Data & Analytics, Marketing,
HR, Legal, Supply Chain). The finding it surfaces:

- Company-wide attrition (~21%) looks unremarkable on its own
- But it is **not evenly spread**: Sales runs ~38% while Corporate runs ~10%
- It is **not about base pay** — the highest-paid bands are the most stable; the real
  split is variable pay vs salary
- The model's **high-risk cohort is ~20% of the company, ~81% commission-dependent**,
  and the actionable levers are quota attainment and lead conversion

That is the point of analysing the whole population rather than one team: the problem
turns out to be a *segment* problem, not a company problem.

## Data

**All data is synthetic and randomly generated. No real employee, customer or company
data is used anywhere.** The generator is seeded, so the dataset is reproducible.

Field design follows the widely used *IBM HR Analytics Employee Attrition* schema
(demographics, job, compensation, 1–4 satisfaction scales, career history), extended
with the operating model of a residential security / smart-home business (phone vs
field sales channels, districts, RMR/IR, installer productivity, contact-centre metrics)
and attrition calibrated to published industry benchmarks.

### Privacy by design
Even on synthetic data the prototype behaves the way a real people-analytics product
should:
- no individual employee records are ever displayed
- any group smaller than **5 people is suppressed** to prevent re-identification
- reporting is aggregate-only

## Pages

- **`index.html`** — the Tableau-embedded version (the main demo)
- **`standalone.html`** — a self-contained version with its own charts, no Tableau
  dependency, in case the embed is blocked on a corporate network

## Tech

Plain HTML, CSS and JavaScript — no build step, no dependencies, no server. The dataset
is embedded in a compact encoded form so all aggregation happens client-side, which is
why filtering and Q&A respond instantly.

---

*Built as a personal learning project. Conceptually inspired by Tableau Pulse, Tableau
Agent and Agentforce — this is my own lightweight take, not those products.*
