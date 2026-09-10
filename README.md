# 📊 Data-Driven Improvements in Secondary Education
### A Comprehensive National Case Study & Power BI Analytics Architecture Across 28 States

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)
![Power Query](https://img.shields.io/badge/ETL-Power_Query-0078D4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Author](https://img.shields.io/badge/Author-Shubham_Gadekar-orange?style=for-the-badge)

---

## 📌 Executive Summary

This project presents a nationwide, census-scale educational analytics case study conducted for the **Ministry of Education**. The initiative focuses on evaluating secondary school student performance in core disciplines (Mathematics) across **28 Indian States**, and identifying how educator capacity, school infrastructure, student attendance, and socio-economic backgrounds drive educational outcomes.

Using enterprise data covering **500,000 students, 50,000 secondary schools, and 100,000 teachers**, an interactive 5-page **Power BI Command Center** was engineered along with a 3-pronged policy framework to guide evidence-based resource allocation.

---

## 🎯 Key Performance Indicators (National Baselines)

| Metric | Baseline Value | Strategic Context |
| :--- | :--- | :--- |
| **Total Students Assessed** | **500,000** | Full secondary cohort across 28 states |
| **National Average Score** | **65.92 / 100** | Median: 68.0, Standard Deviation: 20.58 |
| **National Pass Rate (>= 40)** | **87.34%** | 436,700 passing students; 12.66% remedial |
| **Exemplary Performance (>= 80)** | **27.59%** | 137,900 high-achieving students |
| **Average Attendance Rate** | **50.01%** | 49.52% in Critical Attendance (<50%) tier |
| **Teacher Training Rate** | **70.22%** | 70,220 teachers with completed in-service training |
| **School Internet Coverage** | **79.91%** | 39,954 schools connected; 10,046 in connectivity gap |
| **Functional Library Coverage** | **70.19%** | 35,093 schools equipped with libraries |

---

## 🏗️ Data Architecture & Star Schema Model

The data model is structured in a high-performance **Star Schema** to enable sub-second cross-filtering and drill-down across 500,000 records:

`
                          ┌────────────────────────┐
                          │   Dim_State (PK: State)│
                          └───────────┬────────────┘
                                      │ 1:*
                  ┌───────────────────┴───────────────────┐
                  │ 1:*                                   │ 1:*
       ┌──────────▼───────────────┐            ┌──────────▼──────────────┐
       │ Dim_SchoolInfrastructure │            │       Dim_Teachers      │
       │ (PK: School ID, State)   │            │ (PK: Teacher ID, State) │
       └──────────┬───────────────┘            └─────────────────────────┘
                  │ 1:*
       ┌──────────▼───────────────┐
       │    Dim_SocioEconomic     │
       │ (PK: Student ID, Sch ID) │
       └──────────┬───────────────┘
                  │ 1:1
       ┌──────────▼───────────────────────────────────────┐
       │             Fact_StudentPerformance             │
       │ (PK: Student ID, Subject: Math, Score: 10-100)   │
       └──────────────────────────▲───────────────────────┘
                                  │ 1:1
                       ┌──────────┴───────────────┐
                       │      Dim_Attendance      │
                       │ (PK: Student ID, Att %)  │
                       └──────────────────────────┘
`

---

## 🖥️ Interactive Dashboard Modules (5 Report Pages)

### 📄 Page 1: Executive Overview & State Benchmarking
* **Geographic Choropleth Map**: State-level visualization of student average scores and pass rates.
* **Top 5 vs Bottom 5 States**: Top performers (**Goa: 66.19**, **Mizoram: 66.16**, **Himachal Pradesh: 66.15**) vs Lagging states (**Rajasthan: 65.60**, **Bihar: 65.62**).
* **Score Tier Donut**: Proficient (35.35%), Exemplary (27.59%), Average (24.39%), Needs Remediation (12.66%).
* **State Performance Matrix**: Comprehensive multi-metric ranking table.

### 📄 Page 2: Socio-Economic Impact Analysis
* **Parental Education Gradient**: Post-Graduate parents (66.03) vs Primary education (65.87).
* **Household Income**: High Income (65.96) vs Low Income (65.88).
* **2D Matrix Heatmap**: Cross-tabulation of Parent Education x Family Income with conditional formatting.
* **Score Tier Breakdown**: 100% stacked column chart across demographic brackets.

### 📄 Page 3: School Infrastructure & Digital Enablement
* **Digital Access ROI**: Score comparison for schools with Internet (65.92) vs without Internet (65.90).
* **Computer Lab Density**: Continuous trend analysis of computer counts (0 to 49) vs student score stability.
* **Classroom Scale**: Optimal capacity isolated at 7–12 classrooms per institution (66.23 avg score).
* **State Infrastructure Matrix**: State rankings on digital connectivity and library coverage.

### 📄 Page 4: Teacher Qualifications & Training Dynamics
* **Workforce Profile**: 100,000 educators; average experience of 15.03 years.
* **Training Status Breakdown**: Donut chart tracking 70.22% Trained (70.2K) vs 29.78% Untrained (29.8K).
* **Experience Distribution**: Senior (48.44K), Mid-Career (34.31K), Novice (17.26K).
* **Qualification Mix**: Balanced degree distribution (33.5% B.Ed, 33.1% M.Ed, 33.4% Ph.D).

### 📄 Page 5: Student Attendance & Remedial Risk Matrix
* **Attendance Tiering**: Critical (<50%: 49.52%), Moderate (50-75%: 25.72%), Satisfactory (>75%: 24.76%).
* **Remedial Vulnerability**: Isolates 63,300 students scoring <40 marks; >78% exhibit chronic absenteeism.
* **High-Risk Remedial Action List**: Operational early-warning table listing specific State, School ID, Student ID, Attendance %, and Score for targeted tutoring.

---

## 🔍 Part 1: Data Understanding & Quality Audit (Dataset 1 vs Dataset 2)

As part of the case study mandate, an audit of the initial raw data (Dataset 1) was conducted:

| Feature / Defect | Dataset 1 (Raw / Corrupted) | Dataset 2 (Clean / Production) |
| :--- | :--- | :--- |
| **Attendance Scope** | 1,825 rows (<0.36% sample), text values | 500,000 rows (100% census), numerical % |
| **Relational Integrity** | Socio_economic lacks School ID FK | Socio_economic contains School ID FK |
| **Missing Values (Nulls)** | 30+ nulls across 5 sheets | 0 missing values across all entities |
| **Sheet Naming** | Trailing whitespace error ('Teacher_Data ') | Clean entity names (Teacher_Data) |

---

## 💡 Actionable Policy Recommendations (3-Pronged Framework)

1. **Pillar 1: Pedagogical Upskilling & Curriculum Modernization**
   * Enforce mandatory in-service training for all 29,780 untrained educators.
   * Shift from rote formulas to concept-based, interactive Mathematics toolkits.
   * Establish structured mentorship pairs between senior (16+ yrs) and novice teachers.
2. **Pillar 2: Infrastructure 2.0 & Digital Connectivity**
   * Connect the 10,046 unserved schools to fiber broadband within 9 months.
   * Enforce a mandatory minimum of 4 hours/week of student computer lab time.
   * Modernize secondary school libraries with cloud-accessible digital STEM resources.
3. **Pillar 3: Attendance Tracking & Targeted Social Support**
   * Deploy automated SMS alerts to parents when student attendance falls below 60%.
   * Subsidize rural transport and expand school nutrition programs in lagging districts.
   * Operationalize weekend remedial clinics for the 63.3K at-risk students.

---

## 📂 Repository Structure

`
├── Education Insights.pbix                          # Interactive 5-Page Power BI Dashboard
├── Education_Insights_Analysis_Presentation.pptx    # 15-Slide Master Executive Presentation Deck
├── Education_Insights_Case_Study_Report.docx        # Full Case Study Word Document
├── Education_Insights_Case_Study_Report.md          # Comprehensive Markdown Case Study Report
├── Dataset1- Educational Improvements Insights.xlsx # Raw Dataset (Part 1 Data Quality Audit)
├── Dataset2- Educational Improvements Insights.xlsx # Production Dataset (Part 2 BI Modeling)
├── Problem Statements.pdf                           # Official Case Study Brief & Requirements
└── README.md                                        # Project Overview & Architecture Guide
`

---

## 🚀 How to Replicate

1. Clone this repository:
   `ash
   git clone https://github.com/your-username/education-insights-analysis.git
   `
2. Open **Education Insights.pbix** in **Microsoft Power BI Desktop**.
3. Explore the 5 interactive report pages or use the slicers to filter by State, Household Income, or Parental Education.

---

## 👤 Author & Contact

**Shubham Gadekar**  
*Lead Data Analyst & BI Developer*  
*Specialization: Business Intelligence, Power BI, Advanced DAX & Data Strategy*
