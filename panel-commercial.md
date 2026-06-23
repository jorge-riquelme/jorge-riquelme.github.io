# Cross-Industry / Commercial — Panel

## Caso: Adidas US — Sales & Pricing Analysis

**Etiqueta:** Live Power BI · Pricing Strategy · Python / Kaggle

Women's Apparel leads in both price per unit ($413) and operating margin, while Men's Street Footwear dominates in volume at a lower price — and Amazon extracts the highest revenue per unit across retailers, exposing a clear pricing gap by channel. Built by reconverting a Kaggle EDA dataset into an actionable BI dashboard.

### Context

Public Kaggle dataset of 9,648 rows covering Adidas US sales across 2020–2021. The original dataset exists as exploratory data analysis (EDA) in Python notebooks — descriptive visualizations with no analytical framework or business decision orientation. This project was deliberately developed outside the primary domain of post-secondary education to demonstrate the transferability of the same BI analytical framework to a commercial retail context.

### The Problem

No analytical questions guiding interpretation. No pricing analysis — revenue per unit, seasonal price variation, and retailer pricing gaps were unexplored. No profitability lens — margin by product, region, and channel was invisible. No interactivity — stakeholders could not explore by geography, channel, or product.

### The Approach

The work was structured around a set of business questions, each answered by a dedicated dashboard page — a four-page interactive report:

1. "How has operating margin evolved quarter over quarter across 2020–2021?"
2. "Which regions, states, and sales channels generate the most revenue?"
3. "Which products command the highest price per unit — and does pricing vary seasonally or by retailer?"
4. "Are the best-selling products also the most profitable, or is there a trade-off between volume and margin?"
5. "Where and what generates the most profit — not just revenue?"

Key Metrics: Total Sales, Operating Profit, AVG Operating Margin, Revenue per Unit, YOY Sales Growth, Units Sold

DAX Patterns: DIVIDE for margin calculations, MAXX + TOPN + SUMMARIZE for dynamic top performers, SELECTEDVALUE for context-aware narrative cards, Field Parameters for dynamic geographic granularity

iframe (Adidas BI Analisis)

> Live embed — synthetic data for portfolio purposes. Built with Power BI Publish to Web.

### Key Findings

- Women's Apparel leads in both price per unit ($413) and operating margin — the premium-margin category.
- Men's Street Footwear dominates in volume but commands a lower price per unit — a volume-versus-margin trade-off.
- Amazon extracts the highest revenue per unit across all retailers, revealing a clear pricing gap by channel.

### Transferability

The same framework — margin analysis, price-per-unit benchmarking, and channel-level revenue gaps — applies to any retail or distribution business assessing where profitability concentrates across products, regions, and sales channels.

> Note: Built on a public Kaggle dataset. No institutional or proprietary data involved.

---

## Caso: Factory OEE & Downtime — Manufacturing Performance Dashboard

**Etiqueta:** Live Power BI · Operational Efficiency · Python / Kaggle

Plant OEE of 55.3% is driven primarily by Performance loss (35.9%) — not downtime or quality — meaning the gap to the Manufacturing Standard is a structural production-speed problem, not an equipment-failure one. Built by reconverting a Kaggle predictive-maintenance dataset into an actionable operational BI dashboard.

### Context

Public Kaggle dataset (CC0 Public Domain) originally designed for predictive maintenance tutorials and machine learning feature engineering — not for operational dashboards. This project deliberately repurposed it to answer a different question: can a structured BI dashboard be built on top of a PdM-oriented dataset to deliver operational manufacturing intelligence?

### The Problem

The original dataset had no analytical framework, no business questions, and several inconsistencies that required resolution before any meaningful analysis could be produced.

### The Approach

The work was structured around a set of business questions, each answered by a dedicated dashboard page — a four-page interactive report following a diagnostic narrative arc:

- Page 1 — "What is the current OEE state of the plant?" Monthly performance summary by machine and shift.
- Page 2 — "Where is effectiveness being lost?" Loss waterfall (Availability, Performance, Quality) + Downtime Pareto analysis.
- Page 3 — "Is the machine running consistently?" Statistical Process Control (X̄ chart) with UCL/LCL to detect process instability.
- Page 4 — "What would it take to reach the 75% Manufacturing Standard?" OEE improvement scenario simulation combining downtime reduction and Performance targets.

Key Metrics: OEE, Availability, Performance, Quality, Downtime by cause, scenario-based OEE projection

### Key Findings

- Plant OEE: 55.3% — significantly below the 75% Manufacturing Standard.
- Performance loss (35.9%) is the dominant driver — not downtime (8.6%) or quality (0.2%).
- Eliminating the top 3 downtime causes (Mechanical, Changeover, Electrical) only recovers 3 OEE points — insufficient alone.
- Reaching 80% Performance efficiency combined with top 3 downtime reduction would achieve 76.9% OEE — exceeding the 75% target. The path to standard is a production-speed problem, not an equipment-failure one.

iframe (Manufacturing Performance Dashboard)

> Live embed — synthetic data for portfolio purposes. Built with Power BI Publish to Web.

### Transferability

Loss-decomposition logic — separating availability, performance, and quality to find where effectiveness is truly lost — applies to any process-driven operation: logistics throughput, service-desk resolution rates, or any system where aggregate efficiency hides the real bottleneck.

---

## Caso: Olist B2B Sales Funnel: Marketing-to-Sales Conversion

**Etiqueta:** Live Power BI · Funnel Analysis · DAX / Python / Kaggle

High-volume acquisition channels are not the best-converting ones — social drives traffic but closes worst — and deal-closing load concentrates heavily on a single rep (SR_01 alone closes 15.8% of all deals). Built by reconverting public Kaggle funnel data into an actionable B2B sales-funnel dashboard.

### Context

Olist is a Brazilian e-commerce marketplace that connects small and mid-size sellers to larger sales channels. Before a seller becomes active, it moves through a B2B sales funnel: a lead lands on a marketing page (MQL) → a Sales Development Rep (SDR) contacts and schedules a consultation → a Sales Rep (SR) runs it and closes or loses the deal → a closed deal becomes an active seller. This dashboard turns two public Olist tables into an interactive funnel analysis: 8,000 marketing qualified leads and 842 closed deals.

### The Core Constraint

The dataset records only the first stage (MQL) and the last stage (closed deal). Intermediate stages are not recorded for lost leads — so segment, lead type, behaviour profile, SDR and SR exist only for the 842 converted deals, never for the 7,158 that didn't convert. Every design decision respects this: where the data could only describe the converted population, it is presented as volume, share and velocity — never as a conversion rate that would require a denominator the data doesn't have.

### The Approach

The work was structured around a set of business questions, each answered by a dedicated dashboard page — a five-page Power BI report (the four analytical pages below plus a documentation page):

- Page 1 — Overview: "How efficiently does the funnel convert, and how does lead intake evolve against deal closure over time? Which acquisition channels bring volume, and which actually convert?"
- Page 2 — Funnel Analysis: "Among closed deals, which business segments and lead profiles predominate, and how does close time vary by segment?"
- Page 3 — Sales Team Performance: "Who closes the deals, how is load distributed across the team, and do reps specialize by industry?"
- Page 4 — Rep Efficiency: "Which reps combine high volume with fast closing, and which fall into the slow or low-volume zones?"

Built on a star schema: fact_funnel (8,000 rows) with dimensions for origin, segment, seller, SDR, SR, and a Calendar spanning both the lead and deal windows. Python (pandas) handled cleaning and feature engineering; Power Query handled typing and the date relationship.

iframe (Olist Sales Funnel)

> Live embed — public Olist data. Built with Power BI Publish to Web.

### Key Findings

- Volume ≠ conversion: the highest-volume channels are not the best converters. `social` brings high volume (1.4K leads) but the worst conversion (5.56%) — a candidate for spend review — while `organic_search` and `paid_search` lead volume with solid conversion (~11–12%).
- Load is heavily concentrated: SR_01 alone closes 15.8% of all deals (133), nearly double the second-ranked rep — a key-person dependency worth flagging.
- Fast typical close, long tail: the median deal closes in 14 days, but the mean (48.5 days) is inflated by a slow-closing subgroup. The median is the honest "typical" deal.
- Honest scope boundary: a tail of slow-closing reps exists, but each handles only 1–3 deals — too small a sample to conclude underperformance, so the analysis does not.

### DAX Patterns & Why

- USERELATIONSHIP: Two dates (lead entry vs. deal close) with a real lag. An inactive relationship lets one Calendar drive both timelines on the same axis, no duplicate date table.
- CALCULATE + ALL: Removes filter context to compute each segment's / rep's share of all closed deals — composition, explicitly not a conversion rate.
- DIVIDE: Safe division — returns blank instead of erroring on a zero denominator.
- MEDIAN: Mean close time (48.5 days) is inflated by a long tail; the median (14 days) is the typical deal.
- TOPN + CONCATENATEX + MAXX: Finds each rep's dominant segment and handles ties honestly — tied segments are listed with a flag instead of arbitrarily picking one.
- DISTINCTCOUNT: Unique counts for KPI context (e.g., 842 sellers activated = the funnel outcome).

### Transferability

Funnel composition and velocity analysis — distinguishing volume from conversion, flagging load concentration, and respecting what the data can and cannot measure — applies to any B2B sales pipeline, recruitment funnel, or multi-stage qualification process where intermediate stages are unevenly recorded.

> Note: Built with two public Olist tables — Marketing Funnel by Olist (Kaggle, CC0 Public Domain).

---

> All images are marked as "imagen <filename>" and Power BI embeds are marked as "iframe" placeholders per your requested format.
