# Real Estate Portfolio & Market Intelligence Analysis

An independent Business Analyst / Data Analyst portfolio case study built on publicly available real estate project registration data. This project demonstrates an end-to-end analytical workflow — transforming raw real estate data into business insights, management KPIs, dashboards, and client-style reporting.

> **Note:** This is a practice project based on publicly available data. It is not a real client engagement.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Analyst Objective](#business-analyst-objective)
- [Business Questions](#business-questions)
- [Dataset](#dataset)
- [Data Cleaning](#data-cleaning)
- [Feature Engineering](#feature-engineering)
- [Analytical Methods](#analytical-methods)
- [Key Analysis Results](#key-analysis-results)
- [Delay Analysis Results](#delay-analysis-results)
- [Delay Rate](#delay-rate)
- [Promoter Delay Analysis](#promoter-delay-analysis)
- [Sales & Booking Results](#sales--booking-results)
- [Customer Risk Results](#customer-risk-results)
- [Key Business Insights](#key-business-insights)
- [Client Question Answerability](#client-question-answerability)
- [Data Limitations](#data-limitations)
- [Recommended Future Analysis](#recommended-future-analysis)
- [Dashboard](#dashboard)
- [Client Report](#client-report)
- [Repository Structure](#repository-structure)
- [Tools Used](#tools-used)
- [Skills Demonstrated](#skills-demonstrated)
- [Project Outcome](#project-outcome)
- [Analytical Principle](#analytical-principle)
- [Portfolio Positioning](#portfolio-positioning)
- [Author](#author)
- [Disclaimer](#disclaimer)
- [Project Status](#project-status)

---

## Project Overview

**Project Title:** Real Estate Portfolio & Market Intelligence Analysis

**Project Type:** Independent Business Analyst / Data Analyst portfolio case study, based on publicly available real estate project registration data.

The primary objective of this project is to analyze a real estate project portfolio and provide structured business insights across:

1. Project Performance
2. Project Delays
3. Sales & Apartment Booking
4. Unsold Inventory
5. Customer Complaints
6. Legal Cases
7. Promoter Performance
8. District-Level Activity
9. Project Characteristics
10. Management Reporting

The project demonstrates how a Business Analyst can translate stakeholder questions into measurable KPIs, clean and transform raw data, perform structured analysis, identify patterns, and communicate findings through dashboards and an executive-style report.

---

## Business Analyst Objective

The project follows a structured Business Analyst methodology:

```text
Business Requirements
        ↓
Understand the Dataset
        ↓
Data Cleaning
        ↓
Data Validation
        ↓
Feature Engineering
        ↓
KPI Definition
        ↓
Pivot Table Analysis
        ↓
Business Question Mapping
        ↓
Dashboard Development
        ↓
Business Insights
        ↓
Client-Style Reporting
        ↓
Recommendations / Future Analysis
```

The core objective of this project is **not** simply to create charts or pivot tables. It is to:

> Translate business questions into measurable analytical metrics and communicate the resulting insights in a management-friendly format.

---

## Business Questions asked and solved

### 1. Project Performance

- How many projects are currently completed, ongoing, delayed, or stalled?
- How many projects are delayed?
- Which districts have the highest number of active projects?
- What percentage of projects are delayed?
- Which promoters have the largest number of projects?
- What is the average delay?
- Which promoters have the best/worst project completion performance?
- How many projects have exceeded their original completion date?
- How many projects have received extensions?
- How many projects have severe delays?
- Which projects are significantly delayed?
- Which district has the most delayed projects?
- Which promoters have the highest delay rate?

### 2. Sales & Booking

- What percentage of apartments have been booked across projects?
- Which projects have the highest booking rates?
- Which districts have the strongest/weakest apartment demand?
- Are larger projects experiencing lower booking rates?
- Which promoters have the highest unsold inventory?
- How much apartment inventory remains unsold?

### 3. Customer Risk

- Which projects have the highest number of complaints?
- Which projects have the highest number of legal cases?
- Is there a relationship between project delays and complaints?
- Are projects with more complaints also more likely to have cases?
- Which promoters have consistently high complaint/case counts?

### 4. Project Characteristics

- Does project size influence completion time?
- Do projects with more floors tend to experience more delays?
- Does the number of apartments correlate with booking performance?
- How does sanctioned FSI vary across districts?
- Which districts have the largest residential developments?
- What is the average project area by district?

---

## Dataset

The project uses project-level real estate registration data, sourced from **MahaRERA Project Registration Records**. This dataset is publicly available registration data and is not an official publication by the author.

dataset source  : - https://www.kaggle.com/datasets/jhajalaj/rera-dataset-from-maharashtra-maharera?resource=download&select=mumbai-suburban-rera-dataset.csv

The dataset contains fields relating to:

- RERA/project identification
- Project name
- Promoter
- District
- PIN code
- Latitude
- Longitude
- Project status
- Proposed completion date
- Estimated completion date
- Extended completion date
- Last modified date
- Project type
- Project area
- Recreational open space
- Sanctioned FSI
- Cases
- Complaints
- Number of apartments
- Number of booked apartments
- Basements
- Plinths
- Podiums
- Sanctioned floors
- Stilts
- Open parking
- Closed parking
- Number of plots
- Plot area
- Number of plots booked/allotted/sold

---

## Data Cleaning

The dataset went through a basic data cleaning and preprocessing process in Google Sheets / Excel:

```text
Raw Dataset
      ↓
Column Review
      ↓
Column Name Standardisation
      ↓
Data Type Validation
      ↓
Duplicate Checks
      ↓
Missing Value Assessment
      ↓
Date Standardisation
      ↓
Numeric Field Validation
      ↓
Text / Category Standardisation
      ↓
Business Rule Checks
      ↓
Clean Dataset
```

Cleaning activities performed:

- Standardised column names
- Reviewed duplicate records
- Checked missing values
- Standardised date formats
- Converted numeric fields into usable numeric formats
- Reviewed project status categories
- Standardised text fields
- Validated apartment counts
- Validated booked apartment counts
- Reviewed project area values
- Reviewed latitude and longitude fields
- Reviewed complaints and legal case fields
- Checked completion-date fields
- Performed consistency checks between total and booked apartments

**Important missing-value fields identified during preprocessing:**

- `extended_date_of_completion`
- `cases_count`
- `complaints_count`

Missing values were **not** blindly converted to zero, because:

```text
Blank ≠ Automatically Zero
```

A blank may represent missing information, unavailable reporting, or a genuine zero depending on the meaning of the source field.

---

## Feature Engineering

Raw fields were converted into business-oriented metrics through the following derived metrics.

### Final Completion Date

Uses the applicable completion-date hierarchy:

```text
Extended Completion Date
        ↓ if unavailable
Estimated Completion Date
        ↓ if unavailable
Proposed Completion Date
```

The resulting field is called `Final Completion Date`. This business rule should be validated against the source definition before formal operational use.

### Delay Days

```text
Delay Days = Analysis Date - Final Completion Date
```

The analysis date must be explicitly defined for reproducibility.

### Delay Months

```text
Delay Months = Delay Days / 30.44
```

### Delay Category

The analysis uses the following management-oriented categorisation:

| Delay               | Category            |
| -------------------- | -------------------- |
| 0 days               | No Delay / On Track  |
| 1–3 months           | Minor Delay          |
| 4–6 months           | Moderate Delay       |
| 7–12 months          | Major Delay          |
| More than 12 months  | Severe Delay         |

These categories are analytical classifications created for portfolio segmentation.

### Booking / Absorption Rate

```text
Booking Rate = Booked Apartments / Total Apartments × 100
```

### Unsold Inventory

```text
Unsold Units = Total Apartments - Booked Apartments
```

### Cases per 1,000 Apartments

```text
Cases per 1,000 Apartments = Cases / Total Apartments × 1,000
```

Normalising cases by apartment inventory makes project-level exposure more comparable than raw case counts alone.

---

## Analytical Methods

### Descriptive Analysis

Used to understand:

- Portfolio size
- Project status
- Delay distribution
- Apartment inventory
- Booked inventory
- Unsold inventory
- Complaint levels
- Legal case exposure
- Promoter activity
- District activity

### Pivot Table Analysis

Pivot tables were used to analyse:

- Project status
- Delay categories
- District-wise project counts
- District-wise apartment inventory
- Promoter-wise project counts
- Promoter-wise delayed projects
- Promoter delay rates
- Booking metrics
- Inventory metrics
- Complaint metrics
- Case metrics

### KPI Analysis

Key portfolio KPIs were calculated to provide management-level visibility.

### Diagnostic Analysis

The project identifies relationships that can be tested further, including:

```text
Project Size        →  Project Delay
Number of Floors     →  Project Delay
Apartment Count      →  Booking Rate
Delay                →  Complaints
Complaints           →  Legal Cases
Delay                →  Booking / Absorption
```

These relationships are **not** claimed to be causal. They require further statistical testing using project-level data.

---

## Key Analysis Results

Reported dashboard results:

| KPI                         |   Result |
| ---------------------------- | -------: |
| Total Projects                |   5,127 |
| Delayed Projects               |   4,291 |
| Overall Delay Rate             |   83.7% |
| Severe Delay Projects          |   3,557 |
| No Delay / On Track            |     835 |
| Total Apartments               | 488,947 |
| Booked Apartments              | 253,801 |
| Unsold Units                   | 235,146 |
| Absorption Rate                |   51.9% |
| Complaint Rate                 |   1.72% |
| Cases per 1,000 Apartments     |    9.67 |

---

## Delay Analysis Results

| Delay Category        | Projects | Portfolio Share |
| ----------------------- | -------: | ---------------: |
| Severe Delay             |    3,557 |            69.4% |
| Major Delay              |      501 |             9.8% |
| Moderate Delay           |      109 |             2.1% |
| Minor Delay              |      124 |             2.4% |
| No Delay / On Track      |      835 |            16.3% |
| **Total**                |    5,126 |           100.0% |

> **Data Reconciliation Note:** The delay-severity table contains 5,126 projects compared with the headline portfolio total of 5,127 projects. One project therefore requires reconciliation before the dashboard is treated as a fully reconciled management report.

---

## Delay Rate

```text
4,291 delayed projects
---------------------- × 100  =  83.7%
5,127 total projects
```

The dashboard reports an overall portfolio delay rate of **83.7%**. This figure does not, by itself, explain *why* projects are delayed.

---

## Promoter Delay Analysis

Displayed Top 10 promoter analysis (not a complete ranking of every promoter):

| Promoter / Developer                | Delayed Projects | Total Projects | Delay Rate |
| ------------------------------------- | ----------------: | ---------------: | ----------: |
| Pranav Constructions Pvt Ltd           |                22 |               29 |       75.9% |
| Macrotech Developers Limited           |                16 |               33 |       48.5% |
| Larsen & Toubro Realty Developers      |                15 |               15 |      100.0% |
| Shraddha Landmark Private Limited      |                15 |               18 |       83.3% |
| Neepa Real Estates Private Limited     |                14 |               15 |       93.3% |
| Rare Townships Private Limited         |                14 |               16 |       87.5% |
| Arkade Developers Private Limited      |                13 |               13 |      100.0% |
| Romell Real Estate Private Limited     |                13 |               13 |      100.0% |
| Shree Krishna Properties               |                13 |               13 |      100.0% |
| Aditya Developers                      |                12 |               12 |      100.0% |
| **Top 10 Combined**                    |           **147** |          **177** |    **83.1%** |

**Analytical note:** Promoter delay rates should ideally be interpreted alongside project count, because a 100% delay rate based on a small portfolio can produce a very different interpretation from a 100% delay rate across a large portfolio. No promoter is labelled "best" or "worst" based only on this table.

---

## Sales & Booking Results

```text
Total Apartments   = 488,947
Booked Apartments  = 253,801
Unsold Units       = 235,146
Absorption Rate    = 51.9%
```

- 253,801 apartments are reported as booked.
- 235,146 apartments are reported as unsold.
- The reported portfolio absorption rate is 51.9%.

No assumptions are made about demand without project-level or district-level analysis.

---

## Customer Risk Results

| Governance Metric                    | Portfolio Value |
| -------------------------------------- | ---------------: |
| Complaint Rate                          |            1.72% |
| Cases per 1,000 Apartments              |             9.67 |
| Promoter-to-Project Concentration       |             0.68 |

Displayed benchmark / reference ranges:

| Metric                                 | Displayed Benchmark |
| ---------------------------------------- | --------------------: |
| Complaint Rate                            |                < 2.0% |
| Cases per 1,000 Apartments                |        < 10 per 1,000 |
| Promoter-to-Project Concentration         |             0.60–0.75 |

These are dashboard benchmarks/reference thresholds and should not be presented as universal industry standards unless independently validated.

---

## Key Business Insights

**Insight 1: Portfolio-Level Schedule Risk**
The dashboard reports 4,291 delayed projects out of 5,127 projects, resulting in an 83.7% reported delay rate.

**Insight 2: Severe Delay Exposure**
3,557 projects are classified as Severe Delay in the displayed delay-severity analysis.

**Insight 3: Significant Unsold Inventory**
The portfolio contains 235,146 reported unsold apartments.

**Insight 4: Moderate Overall Absorption**
The reported portfolio absorption rate is 51.9%, based on booked apartments relative to total apartments.

**Insight 5: Promoter-Level Variation**
The displayed Top 10 delayed-promoter analysis shows substantial variation in delay rates.

**Insight 6: Customer-Risk Metrics Need Segmentation**
Portfolio-level complaint and case metrics provide a high-level view, but they may conceal individual projects with elevated customer or legal exposure.

**Insight 7: Data Reconciliation Is Required**
The one-project difference between the headline portfolio count and delay-severity table should be resolved before formal management use.

---

## Client Question Answerability

Not every business question is directly answered by the current dashboard.

### Directly Supported

- Total project count
- Delayed project count
- Overall delay rate
- Severe delay count
- Delay severity distribution
- Total apartments
- Booked apartments
- Unsold inventory
- Absorption rate
- Complaint rate
- Cases per 1,000 apartments
- Displayed promoter delay rates

### Requires Additional Analysis

- Average delay
- Extension frequency
- Complete completed/ongoing/stalled segmentation
- Project-level booking rankings
- District-level demand comparison
- Promoter-level unsold inventory
- Project-level complaint rankings
- Project-level legal case rankings
- Delay versus complaints relationship
- Complaints versus legal cases relationship
- Project size versus completion time
- Floors versus delay
- Apartment count versus booking rate
- FSI by district
- Average project area by district

This distinction is a strength of the analysis — unsupported conclusions are not presented as facts.

---

## Data Limitations

1. Average delay is not currently displayed in the dashboard.
2. Extension frequency is not currently displayed.
3. Complete project-status segmentation requires additional analysis.
4. Project-level booking rankings require further aggregation.
5. Promoter-level unsold inventory requires additional calculations.
6. Project-level complaint and case rankings require additional analysis.
7. Relationships between delays, complaints, cases, project size, floors, and bookings have not been statistically established.
8. Portfolio averages may conceal individual project-level risks.
9. The displayed district analysis does not necessarily represent a complete cross-district comparison.
10. The delay-severity table contains 5,126 projects versus 5,127 in the headline portfolio.
11. Dashboard benchmarks should not automatically be treated as universal industry benchmarks.

---

## Recommended Future Analysis

### Delay Analytics

- Average delay days
- Median delay days
- Maximum delay
- Projects exceeding original completion date
- Extension frequency
- Extension duration
- Severe-delay project watchlist
- District-level delay rate
- Promoter-level delay rate with minimum project threshold

### Sales Analytics

- Project-level booking rate
- District-level absorption
- Promoter-level unsold inventory
- Inventory ageing
- Project-size versus booking-rate analysis
- Apartment inventory segmentation

### Customer Risk

- Complaints per 1,000 apartments
- Cases per 1,000 apartments
- Delay versus complaint analysis
- Complaint versus legal-case analysis
- Project-level Customer Risk Index

### Project Characteristics

- Project area versus delay
- Floors versus delay
- Apartment count versus booking rate
- FSI by district
- Average project area by district
- Project-size segmentation

### Advanced Analytics (Potential Future Methods)

- Correlation analysis
- Regression analysis
- Statistical significance testing
- Clustering
- Risk scoring
- Predictive delay modelling

*Note: These advanced methods have not yet been performed on this project — they are listed as recommended future work.*

---

## Dashboard

The project includes management-oriented dashboard views covering:

### Delay Intelligence

- Total Projects
- Delayed Projects
- On-Track Projects
- Overall Delay Rate
- Severe Delays
- Delay Severity Distribution
- Promoter Delay Analysis

### Market Intelligence

- Total Projects
- Total Promoters
- Total Apartments
- Booked Apartments
- Unsold Apartments
- Absorption Rate
- Project Status
- District Inventory
- Complaint Rate
- Cases per 1,000 Apartments
- Promoter Concentration

```markdown
![Real Estate Portfolio Delay Intelligence Dashboard](08_Visuals/delay_intelligence_dashboard.png)

![Real Estate Portfolio Market Intelligence Dashboard](08_Visuals/market_intelligence_dashboard.png)
```

*(Include these images only if the corresponding files exist in the repository.)*

---

## Client Report

A detailed client-style report was prepared, covering:

- Executive Summary
- Portfolio KPIs
- Project Performance
- Delay Intelligence
- Sales & Booking
- Customer Risk
- Project Characteristics
- Business Question Answerability
- Data Limitations
- Recommended Future Analysis
- Management-Level Conclusions

Suggested repository location: `07_Client_Report/`

---

## Repository Structure

```text
real-estate-portfolio-market-intelligence/
│
├── README.md
│
├── 01_Business_Requirements/
│   └── Client_Questions.md
│
├── 02_Data/
│   ├── README.md
│   ├── raw_data.csv
│   └── cleaned_data.csv
│
├── 03_Data_Cleaning/
│   ├── Data_Cleaning_Process.md
│   └── Data_Cleaning_Notes.xlsx
│
├── 04_Feature_Engineering/
│   ├── Feature_Engineering.md
│   └── Derived_Metrics.xlsx
│
├── 05_Pivot_Analysis/
│   ├── Pivot_Tables.xlsx
│   └── Business_Analysis.xlsx
│
├── 06_Dashboard/
│   ├── Dashboard.xlsx
│   └── Dashboard_Insights.md
│
├── 07_Client_Report/
│   ├── Real_Estate_Portfolio_Client_Analysis_Report.pdf
│   └── Real_Estate_Portfolio_Client_Analysis_Report.docx
│
├── 08_Visuals/
│   ├── delay_intelligence_dashboard.png
│   ├── market_intelligence_dashboard.png
│   └── key_insights.png
│
└── LICENSE
```

*(Only include files/folders in the actual repository that exist — remove any placeholders that do not apply.)*

---

## Tools Used

- Google Sheets
- Microsoft Excel
- Pivot Tables
- Data Cleaning
- Data Validation
- Feature Engineering
- KPI Development
- Business Analysis
- Dashboard Development
- Business Reporting

---

## Skills Demonstrated

### Business Analysis

- Requirements Analysis
- Business Question Translation
- KPI Definition
- Stakeholder-Oriented Analysis
- Business Insight Generation
- Executive Reporting
- Analytical Documentation

### Data Analysis

- Data Cleaning
- Data Validation
- Data Preprocessing
- Feature Engineering
- Pivot Table Analysis
- Descriptive Analytics
- Diagnostic Analysis
- Portfolio Analysis

### Reporting

- Dashboard Development
- KPI Reporting
- Data Storytelling
- Management Reporting
- Client-Style Documentation

---

## Project Outcome

This project demonstrates how a raw real estate dataset can be transformed into a structured business intelligence workflow:

```text
Raw Real Estate Data
        ↓
Clean Dataset
        ↓
Derived Business Metrics
        ↓
Pivot Analysis
        ↓
Portfolio KPIs
        ↓
Business Insights
        ↓
Management Dashboard
        ↓
Client-Style Report
```

The key learning outcome is that effective Business Analysis requires more than calculating numbers. It requires:

```text
Business Question
      ↓
Relevant Data
      ↓
Correct Metric
      ↓
Analysis
      ↓
Insight
      ↓
Business Interpretation
```

---

## Analytical Principle

> Good business analysis does not only explain what the data shows. It also clearly identifies what the available data cannot yet prove.

This project intentionally documents analytical gaps and reconciliation issues instead of making unsupported assumptions.

---

## Portfolio Positioning

This project is relevant to the following roles:

- Data Analyst
- Business Analyst
- BI Analyst
- Reporting Analyst
- Business Intelligence
- Real Estate Analytics
- Operations Analytics
- Data Science roles

This is an independent portfolio case study — not a claim of professional client experience.

---

## Author

### Kaustubh Narayankar

M.Sc. Data Science | Data Analyst | Business Analyst | BI & Analytics

**Areas of Interest**

- Business Analysis
- Data Analytics
- Business Intelligence
- Reporting & MIS
- Real Estate Analytics
- Financial Analytics
- Data-Driven Decision Making

**Profiles**

- GitHub: [https://github.com/KaustubhSN12](https://github.com/KaustubhSN12)
- LinkedIn: [https://www.linkedin.com/in/kaustubh-narayankar-6651a924/](https://www.linkedin.com/in/kaustubh-narayankar-6651a924/)
- Portfolio: [https://kaustubhsn12.github.io/Kaustubh_Portfolio/](https://kaustubhsn12.github.io/Kaustubh_Portfolio/)

---

## Disclaimer

This project is an independent portfolio/practice case study created for learning and professional demonstration purposes.

The analysis should not be interpreted as investment, legal, regulatory, or real estate advisory guidance.

The reported findings are based on the dataset, transformations, calculations, and dashboard used for this project.

The results should be independently validated before being used for operational, commercial, regulatory, or investment decisions.

---

## Project Status

**Completed - Portfolio Case Study**

Future iterations may extend the project with:

- Advanced delay analytics
- Statistical testing
- Project-level risk scoring
- Customer-risk segmentation
- District-level market analysis
- Promoter benchmarking
- Predictive delay analysis
- Advanced dashboarding
