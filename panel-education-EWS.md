# Education Domain — Panel

## Caso: Early Alert System (Risk Assessment): A Multilevel Business Intelligence Ecosystem

**Etiqueta:** Education Domain · Research Pilot

The name says "Early Alert System," but the alerts are the smallest part of what this is. At its core it is a multi-domain data architecture — a single Constellation Schema from which early alerts, Strategic Enrolment Management, retention and graduation reporting, and Comprehensive Program Review all emerge as outputs of the same model. The alert is one report among many, not the system itself.

### The Problem & Strategic Alignment

The Ontario postsecondary sector faces a critical barrier: functional data silos and a lack of identity-based administrative data (HEQCO 2022). Current practices—often relying on static, disconnected reports—create analytical silos and inherent bias by focusing exclusively on the student (Micro level) in isolation. This fragmented approach fails to identify systemic bottlenecks and the diverse challenges of underrepresented populations, ignoring the interplay between the learner, the curriculum, and the institution.

### The Solution: A Holistic Data Ecosystem

This ecosystem transforms limited administrative data into a comprehensive analytical engine supporting multiple institutional workstreams, bridging data gaps through a specialized Multidimensional Data Mart that integrates Historical, Real-time, and Forecast data.

+ Read more: Student Success: Early Warning Systems (EWS) and intervention tracking. Enrollment Management: Real-time monitoring and trend forecasting. Academic Quality: Identification of curricular bottlenecks and teaching performance. Equity & Access: Identity-based reporting and bias-reduced assessments aligned with provincial standards.

### Data Flow & System Architecture

The system consolidates data from institutional warehouses through an ETL process into a specialized Educational Data Mart, implemented as a Constellation Schema that integrates three types of information — historical, real-time, and forecast data — segmented into multidimensional domains covering partial grades, enrollment trends, teaching competencies, retention, and graduation outcomes. Designed for monitoring, following up, predicting, and analyzing results, the analytical layer feeds into an interactive Power BI environment where threshold-based alerts trigger early intervention workflows coordinated across advisors, faculty, and student success teams.

imagen EWS_Diagram.png

### Data Model: Constellation Schema

The Data Mart is implemented as a Constellation Schema in Power BI — multiple fact tables (enrollment, partial and final grades, teaching competencies, retention, graduation) sharing dimension tables across Student, Faculty, Course, Program, and Calendar. This structure enables cross-domain analysis without data duplication.

imagen Constellation_Schema.png

### Technical & Research Validation

The architecture is strategically designed to answer the four critical questions for equitable access:

- Who: Student Demographic Dimensions (monitoring).
- What: Academic Performance (Grades & Enrollment) (following up).
- Where/How: Structural Factors (Teaching & Curriculum) (predicting).
- Outcome: Long-term Success (Graduation & Retention) (analyzing results).

### Research Foundation

The multilevel nested analytics approach is validated by research from Politecnico di Milano, acknowledging that dropout probability is highly conditional on program-specific variables. Additional frameworks draw on UCSC-Chile's multilevel model and Purdue University's Course Signals risk predictor research.

### Scaling to Other Report Types

The same data mart that powers early alerts is, by design, a multi-domain reporting backbone — the alerts are one output among several, not the system's only purpose. Because the model shares dimensions across all fact tables, a single architecture feeds multiple institutional workstreams without duplicating data or rebuilding the schema.

**Generated natively by the core model** — no additional sources required: Strategic Enrolment Management (SEM), retention and graduation reporting, and Comprehensive Program Review (CPR) all draw on dimensions already present in the mart (Enrollment, Retention, Graduation, Program). These are not future possibilities; they are direct outputs of the same model.

**Extensible to external sources** through the shared dimensions: a Labour Market fact mapped by the Program dimension enables graduate employability analysis by program, without altering the core. The same principle opens further integrations — each connecting through a dimension the model already exposes. The architecture scales by adding facts to existing dimensions, not by redesigning the core.

> Note: Independently developed proposal based on validated research. Not institutionally adopted — the initiative and design represent original analytical work developed within an institutional reporting role at a post-secondary institution in Canada.
