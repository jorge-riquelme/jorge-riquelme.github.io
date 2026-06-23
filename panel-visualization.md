# Visualization & Dashboards — Panel

## Caso: Student Retention Analysis: From Static Reports to Interactive Dashboards

**Etiqueta:** Live Power BI · Retention Analysis · Deneb / Vega

A consistent visual language across three iterations — each preserving the same reading logic: rows as cohorts, columns as semesters, attrition visible inline. What changes is the level of interactivity, not the structure. A stakeholder familiar with the static table can read the interactive dashboard without relearning the format.

### The Problem

Retention reports existed but were not fully actionable — visuals were static screenshots embedded in Word documents, making year-over-year comparison difficult and limiting accessibility for non-technical stakeholders. The underlying dataset added complexity: over 20,000 rows, nearly 50 columns, and unidentified transfer students that distorted program-level metrics.

+ Read more: The source dataset combined dimensions and calculated fields with coding conventions that evolved over time. Records could not be reliably linked back to the original cohort, and transfer students were not separately identified — making it impossible to distinguish institutional retention from program-level retention without first resolving these structural issues.

### The Approach

Rather than rebuilding from scratch, I first understood the existing calculation logic — how retention rates were computed, how cohorts were tracked, and critically, how institutional retention differed from program-level retention. From there, I redesigned the visualization applying churn analysis principles: the student as the equivalent of a customer, semester-to-semester retention as the equivalent of churn.

+ Read more: Transfer students needed to be identified and separated from the original cohort to produce meaningful program-level metrics. The redesign was iterative — each version tested against the question: can a non-technical stakeholder act on this?

### Iteration 1 — Program Retention Table (Static)

An improved tabular view tracking cohort progression across semesters on the horizontal axis, with retention percentages segmented by domestic (RES) and international (NRES) students. The staircase effect makes attrition patterns immediately readable — newer cohorts have fewer semesters of data, while older cohorts show the full retention trajectory.

+ Read more: This format represented a significant improvement in accessibility over previous reports, though it remained static. It served as the analytical and visual foundation for the subsequent implementations.

imagen Mock Data_Retention - Excel.png

### Iteration 2 — Interactive Power BI Matrix

The second version migrated the static table into Power BI with a responsive matrix and a Deneb-powered retention heatmap. The goal was to preserve the same cohort-semester reading logic while adding interactive filtering and visual cues for risk.

- Cohort selector by intake term.
- Semester slider showing the number of semesters available per cohort.
- Color-coded retention percentages with conditional formatting for low-performance cells.
- Drill-through to a detail page that compares domestic vs. international retention and highlights cohort outliers.

+ Read more: The visualization kept the same row/column arrangement so stakeholders who had used the static report could transition immediately. The interaction layer added direct access to program and campus filters, which previously required manual report preparation.

imagen PowerBI_Retention_Heatmap.png

### Iteration 3 — Operational Dashboard

The final implementation combined the retention matrix with a cohort flow summary and a narrative KPI strip. Instead of relying on a single table, the dashboard presented three coordinated views:

1. Retention matrix by cohort + semester.
2. Cohort attrition stream showing drop-off and persistence trends.
3. KPI cards for first-year retention, transfer-adjusted retention, and domestic/international divergence.

This version also introduced a “What changed?” panel that explained the difference between institutional and program-level retention, making the report self-explanatory for executive sponsors.

+ Read more: The dashboard was designed to answer two questions at once: “Which cohorts are at risk?” and “Why is the retention rate different for this program?” The answer was visible in the same page, with no extra training required.

imagen Dashboard_Retention_Interactive.png

### The Result

The final visualization package delivered:

- A reusable Power BI / Deneb template for retention analysis.
- A stakeholder-ready dashboard that preserved the original static reading logic while enabling dynamic slicing by program, campus, and student type.
- Faster decision cycles: enrollment managers could identify at-risk cohorts immediately, rather than waiting for monthly report updates.

> The iterative design preserved the mental model of the original report while unlocking interactivity and auditability for operational use.

---

## Caso: Academic Standing Transition Matrix: Measuring the Real Impact of Early Alerts

**Etiqueta:** Live Power BI · Flow Analysis · Python / DAX / Matplotlib

### The Problem

Institutions implement academic alert systems but rarely have a method to measure whether those interventions actually changed student trajectories. Reports show who is at risk — but not whether the system moved them.

### The Approach

Using Python, I redesigned the academic standing dataset by assigning each student two states: their standing at the start of the semester and their standing at the end. This creates a transition matrix — borrowed from data science and actuarial modeling — that makes movement between states visible and measurable.

+ Read more: The transformation also serves as a foundation for building risk indices when enriched with campus, demographic, program, and course-level parameters — enabling contextual aggregation that reduces individual identification bias.

### The Visual

The heatmap shows student transitions across five academic standing states — Academic Intervention, Academic Probation 1-3, and Good Standing. Each cell represents the number of students who moved from one state (previous semester) to another (current semester). The diagonal represents students who maintained their standing. Off-diagonal cells reveal movement in both directions.

imagen academic_transition_heatmap.png

### Dataset Structure

The transformation produces a three-column dataset — ready to load directly into Power BI as a matrix table or Sankey chart:

- Previous_Standing
- Current_Standing
- Student_Count

+ Read more: Sample structure is synthetic and designed to illustrate the dataset shape required for visualizing academic status transitions across periods.

### Longitudinal Potential & Bias Reduction

Applying the same transformation consistently across academic periods generates historical metrics — enabling the institution to track whether recovery rates are improving and whether interventions actually shifted trajectories over time.

When results are aggregated by context — program, campus, semester, or demographic group — rather than at the individual level, the matrix reduces identification bias. Risk becomes a property of the learning environment, not a label assigned to the student.

### Next Step — Live in Power BI

This dataset structure feeds directly into Power BI as a Sankey chart, enabling dynamic filtering by campus, program, demographics, and semester.

iframe

> Live embed — mock data for portfolio purposes. Built with Power BI Publish to Web.

> Analysis developed independently within an institutional reporting role at a post-secondary institution in Canada. Recreated with synthetic data for portfolio purposes.

---

## Caso: Comprehensive Program Report: From Static Documents to BI Dashboard

**Etiqueta:** Live Power BI · Market Share Analysis · DAX

### Context

Comprehensive Program Reviews (CPR) are typically delivered as static documents with descriptive data and no analytical framework. This pilot applied a market intelligence lens to four programs, using institutional SIS data and labour market sources to assess competitive positioning, enrolment conversion, and graduate employment outcomes.

### The Problem

The existing reporting format had three core limitations: raw tables with no aggregation or contextual framing, no analytical questions guiding interpretation, and no interactivity. The result was data that described what happened but offered no insight into why it mattered or what to do next.

### The Approach

A Business Intelligence framework was applied to transform static reporting into an interactive, metrics-driven dashboard — structured around four analytical questions:

- Market Positioning — How does the institution compare against provincial competitors in confirmed applications and enrolment?
- Conversion Efficiency — What percentage of confirmed applicants actually enrol, and how does this vary by program?
- Student Profile — Who are the students, and has that profile shifted over time?
- Labour Market Alignment — What is the employment outlook and wage trajectory for graduates?

### Metrics & Patterns

Metrics were designed dynamically in Power BI using DAX patterns such as `TOPN`, `SELECTEDVALUE`, `CALCULATETABLE`, and `SWITCH` for context-aware titles. This pilot defined the analytical requirements a production data mart would need to support.

### The Dashboard

The working implementation was built on anonymized mock data and embedded via Power BI Publish to Web.

iframe

> Live embed — anonymized mock data for portfolio purposes.

### Impact

The pilot extended exploratory visualizations into a proof-of-concept dashboard, adding interactivity, analytical metrics, and a BI framework to institutional reporting.

### Transferability

The core framework — market context → conversion efficiency → customer profile → outcome alignment — applies beyond education. It is relevant to healthcare, retail, HR, and financial services where organizations need to move from descriptive reporting to analytical decision-making.

> Pilot presented to institutional leadership as a proof of concept. Dashboard rebuilt with anonymized mock data for portfolio purposes.

---

## Caso: Strategic Enrolment Management: From Static Reports to BI Dashboard

**Etiqueta:** Live Power BI · Enrolment Analysis · DAX

### Context

Strategic Enrolment Management (SEM) requires data-driven decisions across demand, capacity, retention, and student success. This pilot assessed institutional health using cohort data, provincial waitlist records, and regional catchment information.

### The Problem

Existing reports were disconnected, descriptive, and lacked a decision-making lens. Stakeholders could not explore program, campus, year, or student-type variation, so the reporting ecosystem described what happened without explaining why.

### The Approach

A BI framework was applied around five analytical questions:

- Unmet Program Demand — Which programs have more qualified applicants than available seats, and where do unplaced students go?
- Capacity Pressure — Are we expanding capacity at the pace of demand, and which programs face the highest competition for available seats?
- YOY Enrolment Decline — Which programs are experiencing sustained enrolment decline, and how severe is the trend?
- Student Loss by Stage — How many students never arrive after enrolling, and how many start but don’t complete their program?
- Catchment Area Analysis — How many local students are enrolling in competitor institutions for programs we offer and programs we don’t?

### Metrics & Dashboard

The pilot built seven dynamic metrics, including Waitlisted per Available Seat, Priority Loss Rate, Demand Gap, No-Show Rate, and Final Semester Attrition. A working implementation was built in Power BI on anonymized mock data.

iframe

> Live embed — anonymized mock data for portfolio purposes.

### Impact

The pilot added interactivity, analytical metrics, and a BI framework to SEM reporting, and it demonstrated how exploratory visualizations can become operational decision tools.

### Transferability

This framework applies to any domain involving demand forecasting, capacity planning, and pipeline attrition analysis. The core pattern — demand → capacity → trend → attrition → competitive positioning — is relevant to healthcare, retail, HR, and financial services.

> Visualizations adopted in institutional reports. Dashboard rebuilt with anonymized mock data for portfolio purposes.

---

## Caso: Custom Visual Explorations: Cohort Retention Tree & Temporal Sankey

**Etiqueta:** Live Power BI · Flow Analysis · Deneb / Vega-Lite

### Context

Power BI’s native visuals cover most needs, but dense cohort tables and time-aware flow diagrams expose limits. These explorations use Deneb to render Vega-Lite specs for two custom visuals with cross-industry applicability.

### Cohort Retention Tree

A clean alternative to native matrix tables for cohort tracking. Each row is an intake cohort; each column is a period. Attrition is shown inline as a red delta, retained units as a green bar. The spec is authored in Vega-Lite for maintainability and portability.

### Temporal Sankey

A time-aware alternative to a standard Sankey. The horizontal axis represents time, with flows showing retention, internal movement, and exits across periods. Each flow is traceable to individual records, making the visual suitable for cohort and mobility analysis.

### Applications

- HR & Workforce Analytics — employee mobility across departments, roles, and seniority levels.
- Customer & Subscription Analytics — cohort retention and churn flow by acquisition period.
- Healthcare — patient progression through treatment stages over time.
- Manufacturing & Operations — units or batches moving across process stages.
- Education & Training — student flow through program levels or pathways.

### Technical Considerations

- Both visuals are authored in Vega-Lite inside Deneb — maintainable and version-controlled outside Power BI.
- Deneb visuals do not support cross-filtering with native Power BI visuals on the same page.
- The Temporal Sankey requires a purpose-built dataset with previous/current state per record per time period.
- Cross-filter behavior between the Temporal Sankey and other visuals has not been fully tested — validation is required before production use.

### Live in Power BI

iframe

> Live embed — synthetic data for portfolio purposes. Built with Power BI Publish to Web.

> Explorations developed independently within an institutional reporting role at a post-secondary institution in Canada. Adapted from cross-industry frameworks and synthetic data for portfolio purposes.

*** End Patch

