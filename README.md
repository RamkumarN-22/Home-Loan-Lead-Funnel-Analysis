## ✅ **Project Overview**

This project analyzes the **end-to-end journey of home loan leads** across multiple stages — from initial contact to loan disbursement.

The goal is to measure:

- Stage-wise conversion
- Customer drop-offs and root causes
- Turnaround times (TAT) across the funnel
- Segment-wise performance
- Operational bottlenecks

Using **SQL** for data cleaning, validation, and transformation, and **Power BI** for interactive dashboards, this project demonstrates a strong combination of:

- Data analytics
- Business intelligence
- Funnel optimization
- BFSI domain understanding

The same framework applies to **Sales Operations, FinTech, SaaS funnel analysis, and CRM analytics.**

---

## 🎯 **Key Business Objectives**

- Evaluate how effectively leads progress through the loan funnel
- Identify major drop-off stages and root causes
- Understand customer behavior across segments (income, age, credit score, employment type)
- Measure operational efficiency using time-in-stage metrics
- Provide actionable insights to improve conversion and reduce processing delays

---

# 🗂️ **Dataset Overview**

The project uses **four core tables**:

### 1️⃣ `Lead_Master`

Customer-level data:

- Lead ID
- Customer demographics
- Income
- Loan amount requested
- Lead creation date
- Source & channel

### 2️⃣ `Stage_Tracking`

Stage movement data:

- Lead ID
- Stage name
- Stage status (Completed / Dropped)
- Stage date
- Drop reason

### 3️⃣ `Credit_Assessment`

Underwriting-related data:

- Credit score
- FOIR
- Approval/rejection indicators

### 4️⃣ `Outcome`

Final lead status:

- Sanctioned / Rejected / Withdrawn
- Disbursement date

---

# 🧹 **Step 1 — Data Cleaning & Validation (SQL)**

I performed **three layers of data quality checks**:

### ✔ Structural Integrity

- Identify missing Lead IDs
- Duplicate leads
- Invalid dates
- Null stage statuses
- Missing final outcomes

### ✔ Analytical Integrity

- Invalid age, income, loan amounts
- Wrong employment types
- Unrealistic credit scores or FOIR values
- Missing drop reasons for dropped leads

### ✔ Business Logic Validation

- Stage order validation using SQL window functions
- Negative or zero time gaps
- Disbursement before lead creation
- Credit assessment occurring before document collection

These checks ensured the dataset is **clean, accurate, and analysis-ready**.

---

# 🛠️ **Step 2 — Data Transformation (SQL)**

### ✔ **Created a Clean Stage View:**

Handles duplicates & inconsistent entries.

```sql
CREATEVIEW vw_CleanStageAS
SELECT
    Lead_ID,
    Stage_Name,
MAX(Stage_Status)AS Stage_Status,
MIN(Stage_Date)AS Stage_Date
FROM Stage_Tracking
GROUPBY Lead_ID, Stage_Name;

```

### ✔ **Created Stage Time Analysis Table:**

Calculates number of days a lead spends in each stage.

```sql
SELECT
    Lead_ID,
    Stage_Name,
    Stage_Date,
LEAD(Stage_Date)OVER (
PARTITIONBY Lead_ID
ORDERBY Stage_Date
    )AS Next_Stage_Date,
    DATEDIFF(DAY, Stage_Date, Next_Stage_Date)AS Days_In_Stage
INTO Stage_TimeAnalysis
FROM vw_CleanStage;

```

This is the backbone for TAT analysis.

---

# 📊 **Step 3 — Power BI Dashboard Development**

The report consists of **four interactive pages**, each aligned with business & operational use cases.

---

# ⭐ **PAGE 1 — Overview Dashboard**

Provides an **executive summary** of funnel performance.

<img width="755" height="432" alt="Lead funnel_Overview page" src="https://github.com/user-attachments/assets/76833cb9-2ef7-469c-b837-52d2c6fe6e8a" />


### Key Insights:

- Total Leads, Sanctioned, Dropped
- Final Conversion %
- Stage-wise funnel movement
- Completed vs Dropped leads
- Average TAT per stage

Helps leadership quickly understand overall process efficiency.

---

# ⭐ **PAGE 2 — Drop-Off Analysis**

Identifies **where and why** customers exit the funnel.
<img width="763" height="428" alt="Lead funnel_Drop-off page" src="https://github.com/user-attachments/assets/1af4e8da-5adf-41c1-8822-7209af9f1fc9" />

### Visuals Include:

- Drop count by stage
- Drop reason contribution
- Stage × Drop Reason heatmap (root cause)
- Drop % trends

### Examples of Insights:

- Document Collection had highest drop due to incomplete documents
- Credit Check failures driven by low credit score and high FOIR
- Contact stage drop caused by customer not reachable

This page provides **actionable operational insights**.

---

# ⭐ **PAGE 3 — Segment Analysis**

Analyzes **customer behavior** across key segments.

<img width="763" height="427" alt="Lead funnel_Segment page" src="https://github.com/user-attachments/assets/a611f59c-0e5c-4160-b569-349248eecd9a" />


### Segmentation Based On:

- Income range
- Age group
- Credit score bucket
- Employment type
- Lead source

### Insights:

- High-income salaried customers had highest conversion
- Poor credit scores correlated with high drop-offs
- Self-employed individuals showed higher TAT
- Builder leads converted higher than digital leads

Helps refine **marketing, targeting, and pipeline strategy**.

---

# ⭐ **PAGE 4 — TAT (Turnaround Time) Analysis**

Focuses on operational delays in the loan process.

<img width="765" height="431" alt="Lead funnel_TAT page" src="https://github.com/user-attachments/assets/88dc7828-c3c6-4570-923a-7b0ecd6a63d7" />


### Visuals Include:

- Avg Days in Each Stage
- Min / Avg / Max processing times
- TAT by segment (income, employment, credit score)
- Identification of bottleneck stages

### Insights:

- Document Collection and Legal Verification had the highest delays
- Self-employed customers required more time due to verification needs
- High credit score applicants progressed significantly faster

Improves **process efficiency and customer experience**.

---

# 🚀 **Key Skills Demonstrated**

### 🔹 SQL (Advanced)

- Data validation
- Joins & aggregations
- Window functions
- Creating views & analytical tables
- Business rule enforcement

### 🔹 Power BI

- Data modeling
- DAX measures
- Multi-page storytelling dashboard
- KPI design
- Heatmaps, funnel visuals, segmentation visuals
- Performance analysis

### 🔹 Domain Knowledge

- Lending funnel logic
- Credit assessment workflows
- Drop reason patterns
- Operational bottlenecks (TAT)
- Customer segmentation logic

### 🔹 Analytical Thinking

- Funnel optimization
- Root cause analysis
- Customer behavior patterns
- SLA and processing efficiency
- Insight generation

---

# 📌 **Final Project Outcome**

This project delivers a complete analytical solution that helps:

- Identify conversion challenges
- Reduce drop-offs
- Optimize operational performance
- Improve customer targeting
- Shorten loan processing time
- Enable decision-making with data

It reflects real-world responsibilities of:

- **Data Analysts**
- **BI Analysts**
- **Sales Operations Analysts**
- **Business Analysts**
- **FinTech Analysts**

## 👤 Author

**Ramkumar N**

Data Analyst | Data Analytics | IIT Roorkee (EPG in Data Analytics)

📧 **ramkumar.n.data@gmail.com**
