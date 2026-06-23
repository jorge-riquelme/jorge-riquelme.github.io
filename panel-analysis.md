# Data Analysis & Auditing — Panel

## Caso: Disaggregated Failure Rate Analysis: Beyond Demographics

**Etiqueta:** Data Analysis & Auditing · Python

### The Problem

Class failure rates were tracked institutionally, but reported as aggregate figures — masking the underlying factors driving student underperformance. The question was not just *how many* students were failing, but *which conditions* were most strongly associated with failure.

+ Read more: Existing reports did not disaggregate failure rates by demographic, engagement, or support dimensions, making it difficult to design targeted interventions. Funding Code was treated carefully — subcategories were aggregated to avoid overidentification of specific demographic groups while still capturing the financial dimension of student risk.

### The Approach

Using Python, I cross-referenced Cognos reports to build a multi-dimensional dataset spanning three indicator groups: Demographic Insights, Educational Engagement, and Background and Support. The analysis combined descriptive statistics, clustering, correlation analysis, and linear regression — with a deliberate bias reduction strategy that avoided individual identifiers and program-specific data.

+ Read more: The dataset was built by cross-referencing multiple Cognos reports — not a single extract. Each indicator group required separate data preparation before the dimensions could be combined for analysis. This foundation also serves as the dimensional structure for a future Power BI implementation, where each indicator group becomes a slicer enabling dynamic filtering.

### The Visual

The chart shows average failed classes per metric across three indicator groups — offering a balanced view among indicators, metrics, and submetrics.

*In this recreation using synthetic data, the following patterns can be observed:*

- **Trend:** Steady increase from Residency (2.39) to Funding Code (3.37) across all three groups.
- **Demographics:** Age Range (2.52) emerges as the most significant demographic factor.
- **Engagement:** Shaped primarily by Semester (2.74) and Previous Standing (2.89).
- **Background & Support:** Funding Code (3.37) and Catchment Area (2.95) show the highest average failure rates.

imagen average_class_failure_rates.png

### The Finding

Financial circumstances, represented by Funding Code, emerged as the strongest predictor of class failure — stronger than gender, age, or residency status. This challenges assumptions that demographic identity is the primary risk factor, and points toward financial support systems as a higher-leverage intervention point.

### Transferability

This analytical framework applies directly to healthcare (readmission risk), HR (employee turnover), and credit risk modeling — any domain where disaggregated risk analysis can identify systemic factors behind individual outcomes.

> Analysis developed independently within an institutional reporting role at a post-secondary institution in Canada. Recreated with synthetic data for portfolio purposes.

---

## Caso: Retention Dataset Audit & ETL Transformation: From Wide Format to BI-Ready Structure

**Etiqueta:** Data Analysis & Auditing · Python

### The Audit

Wide-format datasets are the standard output of legacy administrative systems — efficient for storage and transactional reporting, but structurally limited for dynamic BI analysis. This case documents the audit and transformation of a retention dataset typical of Ontario post-secondary institutions: 985 rows and 33 columns, where semester-retention values are embedded directly in column names rather than stored as rows.

+ Read more: The audit process began by mapping the dataset composition: five descriptive columns (academic year, cohort term, program, campus, ministry codes) followed by 18 retention columns encoding both the semester number (1-6) and student type within the column name itself. This wide structure, while readable as a static report, prevents dynamic filtering by semester or student type without creating individual measures for each column.

### Dataset Structure — Original Format

Wide-format structure where each semester and student type occupies a separate column — 18 retention columns embedded in column names, making dynamic slicing in Power BI impractical.

*(Tabla: encabezados y ejemplo de fila presente en la página — omito la tabla visual y conservo la descripción)*

> 985 rows x 33 columns — 18 of which are semester-retention values embedded in column names (SEM1-SEM6 x Total / DOM / INT)

### The Transformation

Using Python, the dataset was unpivoted from wide to long format — extracting the semester number from column names into a dedicated field. The result reduces 33 columns to 6, making the data natively compatible with Power BI slicers and DAX measures. Demographic dimensions are added separately via foreign key joins.

*(Ejemplo de la tabla resultante: academic_year, cohort_term, program_name, campus, semester, students — un ejemplo de fila: 2026 | 202508 | [Program] | Campus A | 1 | 26)*

> Long format — one row per program, campus, and semester. What previously required 18 static measures becomes a single Students field.

### Second Transformation — Adding Dimensions

A foreign key was constructed to enable joins with dimension tables — adding demographic, program, and enrollment context without embedding it in the base retention structure. This separation of concerns keeps the retention layer clean and scalable as additional data sources are connected.

### A Note on Cohort Tracking

Institutional enrollment data is typically aggregated at the program-cohort level, not at the individual student level. To support cohort tracking across semesters, the dataset was restructured using enrollment data as the foundation — making it possible to distinguish organic retention from other enrollment movements that aggregate reporting does not capture by default. Cohort-level program tracking is developed further in Case 2.

### The Result

A long-format structure ready to calculate institutional and program-level retention rates dynamically — with a foundation that scales to include additional dimensions as data sources are connected via foreign keys. What previously required 18 static measures becomes a single analytical layer adaptable to any reporting need.

> Analysis developed independently within an institutional reporting role at a post-secondary institution in Canada. Dataset structure illustrated with synthetic data for portfolio purposes.

---

## Caso: Cohort Attribution Audit: Resolving Hidden Bias in Retention Metrics

**Etiqueta:** Data Auditing · Strategic BI

### The Audit

Institutional retention is often reported as an aggregate figure, assuming a linear progression where "Semester 1" represents the same starting point for all records. This audit identified a critical **Attribution Bias**: the mixing of true freshmen with internal transfer students within program-level cohorts.

+ Read more: The conflict arises from mismatched granularity. While an "Institutional Cohort" correctly tracks a student's first entry to the college, a "Program Cohort" often mislabels internal transfers as new students. This ignores the academic maturity and survival traits of transfers, who enter advanced semesters without facing the high-risk barriers of the true first year.

### The Cohort Contradiction

Comparison of data integrity status across analysis levels. The current model assumes a linear path that does not exist for 15-20% of the population.

*(Tabla comparativa: Analysis Level | Cohort Definition | Data Integrity Status — Institutional = VALID; Program-Specific = INCONSISTENT)*

### Cascading Impact

The lack of data atomicity triggers a domino effect across institutional KPIs, leading to skewed strategic decisions:

- **Retention Inflation:** Transfers (higher success probability) artificially boost averages, masking the real dropout rate of vulnerable freshmen.
- **Time-to-Degree Distortion:** Programs appear more efficient by "importing" graduates who completed 50% of their credits in other departments.
- **Resource Misallocation:** Budget for first-year support is under-prioritized because aggregated data suggests a healthy performance.

### The Solution: Atomic Architecture

I proposed a transition toward **Data Atomicity** to restore system integrity. This framework enables dynamic segmentation without losing historical context:

1. **Dual Cohort ID:** Separate identifiers for `Entry_Cohort_Institutional` and `Entry_Cohort_Program`.
2. **Origin Flags:** Mandatory classification as `First-time` or `Transfer-in`.
3. **Academic Seniority:** Normalizing semesters based on "Credits Completed" rather than calendar time.

### Transferability & Industry Parallels

The "Cohort Contradiction" is a structural data flaw applicable to any sector where aggregated reporting masks the origin or lifecycle of the subject.

+ Read more: Retail (Churn Analysis): Mixing new customers with reactivated users inflates acquisition success and masks the failure of new-user growth strategies. Finance (Accounts Receivable): Labeling refinanced old debt as "new debt" conceals long-term credit risk. Mining (Resource Recovery): Aggregating ore grade data across extraction points masks low-yield zones.

> Audit developed independently within an institutional reporting role. Findings represent original analytical work on data integrity and cross-industry logic application.

---

## Caso: From Audit to Implementation: Atomic Journey Reconstruction

**Etiqueta:** Live Power BI · Retention Analysis · Python

### Context

This case is the direct implementation of the Cohort Attribution Audit. The audit identified the structural flaw — misattributed cohort labels masking 15–20% of enrollment events. This case documents how that finding was resolved in practice: a flag pipeline built on the raw enrollment file that reconstructs every student trajectory without modifying the source data.

### The Problem

Institutional enrollment data arrives as a flat transaction file. Each row represents a student-program-semester record, but nothing in the raw data distinguishes a student who dropped out from one who transferred programs, completed their credential, or simply repeated a semester. Aggregate retention formulas — built on `Sem N − Sem N+1` subtractions — collapse these distinct events into a single number, hiding the destination.

### The Approach

Rather than filtering or removing records, the transformation was applied directly on top of the raw enrollment file. Every transaction was preserved and labeled through a flag architecture — eight boolean columns that reconstruct the full student lifecycle without altering the audit trail.

+ Read more: The flags enforce a conservation identity at every semester transition: `Started = Retained + Moving + Pathway + Incomplete`. This identity is what subtraction-based formulas cannot guarantee. A subtraction hides where a student went. A flag reveals it.

### The Flag System

Eight boolean columns reconstruct the full student lifecycle. Each flag represents a distinct institutional event: `is_transfer_in`, `is_repeating`, `is_moving`, `is_pathway`, `is_subsequent_program`, `is_program_incomplete`, `is_final_record`, `student_completed`.

*(Tabla con descripción de flags y triggers presente en la página — se conserva la lista de flags arriba.)*

### The Accounting Rule

The flags enforce an accounting rule at every semester transition. Every student that starts a semester has exactly one outcome:

This identity is what traditional retention formulas cannot guarantee. A subtraction hides the destination. A flag reveals it.

### Cohort Flow at a Glance

Applied at `Cohort + Program + Campus + Semester` level, the flags produce a flow table where every student is accounted for across the full program lifecycle.

*(Ejemplo de filas y columnas en la página — se conserva la descripción y ejemplos numéricos.)*

### One Dataset, Two Questions

The flag architecture produces two complementary views from the same source — consistent by construction, no reconciliation required:

- **Layer 1 — Macro:** Longitudinal trend reporting by program and cohort. How did cohort 202408 perform over time?
- **Layer 2 — Flag Detail:** Dimensional drill-down and audit trail. Who left, why, and where did they go?

+ Read more: In Power BI this translates to a retention map — Started → Retained → Pathway by cohort. The difference between is_moving and is_program_incomplete is not visible in a retention percentage, but it determines whether a student represents a resource allocation failure or a natural academic progression.

### Why This Matters

This is not a statistical model. It is a formula architecture: reproducible, auditable, and built to be wrong-proof. Every flag is independently verifiable, every outcome traceable to a specific row. The pipeline can be re-run on any future dataset and produce consistent results by construction — applicable to any domain where lifecycle events are currently collapsed into aggregate subtraction metrics.

### Live in Power BI

A Power BI report built on this flag layer — interact with it directly. Filter by cohort, campus, program, and demographic group to explore retention, persistence, and completion outcomes across the full student lifecycle.

iframe

> Live embed — synthetic data for portfolio purposes. Built with Power BI Publish to Web.

> Analysis developed independently within an institutional reporting role at a post-secondary institution in Canada. Dataset structure illustrated with synthetic data for portfolio purposes.
