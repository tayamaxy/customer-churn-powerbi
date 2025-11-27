# Databel Customer Churn Analysis in Power BI

This repository contains my Power BI solution for the **Databel customer churn** case study.  
The report is built as a set of analytical dashboards (slides) that quantify **how many customers churn**, **who they are**, and **which factors drive churn**.

All visuals are powered by custom **DAX measures** and **calculated columns** that I created specifically for this analysis (see **Key Metrics & DAX Logic** below).

---

## 1. Business Context

Databel is a fictitious telecom provider with a subscription-based model. The key business questions are:

- What is the overall **churn rate**?
- Which **customer segments** are most likely to churn?
- How do **contracts, pricing, usage, extra charges, payment methods and customer service calls** relate to churn?
- How much **revenue is at risk**, and where should Databel focus retention efforts?

The analysis is based on the public Databel churn dataset used in the DataCamp case study.

---

## 2. Power BI Report: Pages / Slides

The Power BI file is structured into thematic pages. Each page is driven by specific metrics and segmentation logic.

### 2.1 Churn Overview: Key Metrics and Drivers

**Slide:** `Churn Overview: Key Metrics and Drivers`  

Core KPIs:

- **Churn Rate %**
- **Churned Customers**
- **Total Customers**

Main visuals:

- Bar chart of **Churn Reasons** (% of total customers)
- Donut chart of **Customers by Contract Type**
- Pie chart of **Churn by Category** (Competitor, Attitude, Dissatisfaction, Price, Other)
- Map of **Churn Rate by State**

All these visuals use custom measures for total customers, churned customers, churn rate, and percentage contribution.

---

### 2.2 Who Is Churning and Why?

**Slide:** `Who Is Churning and Why?`  

Focus:

- Matrix combining **Senior / Under 30** flags with **Churn Rate**
- Global KPI cards:
  - **Churn Rate %**
  - **Churned Customers**
  - **Total Customers**
- Combination chart:
  - **Number of Customers and Churn Rate by Age (bins)**
- Bar chart of detailed **Churn Reasons**

Key modeling elements:

- **Age Bins** (calculated column to group customers by age)
- **Churn Rate by Age Bin** (measure)
- **% of Total Customers by Churn Reason** (measure)

---

### 2.3 Churn Drivers: Contracts, Group Size & Reasons

**Slide:** `Churn Drivers: Contracts, Group Size & Reasons`  

Focus:

- **Average Monthly Charge and Churn Rate by Group Size**
- **Churn Rate by Contract Category (Monthly vs Yearly) and Gender**
- **Churn by Category** (Competitor, Attitude, Dissatisfaction, Price, Other)
- **Customers by Contract Type** (Month-to-Month, One Year, Two Year)

Key metrics:

- **Avg Monthly Charge**
- **Churn Rate by Group Size**
- **Churn Rate by Contract Category & Gender**
- **Share of Customers by Contract Type**
- **Churn Share by Churn Category**

---

### 2.4 Impact of Unlimited Data Plans and Usage on Churn

**Slide:** `Impact of Unlimited Data Plans and Usage on Churn`  

Focus:

- Matrix with **Churn Rate** and **Number of Customers** by **Unlimited Data Plan (Yes/No)**
- Bar chart of **Churn Rate by Grouped Consumption and Unlimited Data Plan**

Key modeling elements:

- **Grouped Consumption** (calculated column: e.g. `<5 GB`, `5–10 GB`, `10+ GB`)
- Measures:
  - **Churn Rate by Unlimited Data Plan**
  - **Churn Rate by Grouped Consumption and Plan**
  - **Customer Count by Plan**

---

### 2.5 International Plan & Geographic Churn Patterns

**Slide:** `International Plan & Geographic Churn Patterns`  

Focus:

- Matrix showing churn patterns for **International Plan Active (Yes/No)** and churn label
- Map with **Churn Rate by State**

Key metrics:

- **Churn Rate by Intl Plan (Yes/No)**
- **Customer Count by Intl Plan**
- **Churn Rate by State**

---

### 2.6 Churn by Tenure, Contract Type and Payment Method

**Slide:** `Churn by Tenure, Contract Type and Payment Method`  

Focus:

- Line chart: **Churn Rate by Account Length (months)**
- Pie chart: **Number of Customers and Churn Rate by Payment Method**
- Line chart: **Churn Rate by Account Length and Contract Type**

Key metrics and modeling:

- **Account Length in Months** (tenure field used as continuous axis)
- **Churn Rate by Tenure**
- **Churn Rate by Tenure and Contract Type**
- **Customer Count by Payment Method**
- **Churn Rate by Payment Method**

---

### 2.7 Age and Group Size Patterns in Churn

**Slide:** `Age and Group Size Patterns in Churn`  

Focus:

- **Number of Customers and Churn Rate by Age (bins)**
- **Average Monthly Charge and Churn Rate by Number of Customers in Group**
- **Account Length (in months)** slicer to filter visuals

Key metrics:

- **Churn Rate by Age Bin**
- **Customer Count by Age Bin**
- **Avg Monthly Charge by Group Size**
- **Churn Rate by Group Size**

---

### 2.8 Churn by Payment Method, Contract Category and Service Calls

**Slide:** `Churn by Payment Method, Contract Category and Service Calls`  

Focus:

- Scatter chart: **Average Account Length and Churn Rate by Payment Method and Contract Category**
- Cards:
  - **Total Customer Service Calls**
  - **Average Customer Service Calls**

Key metrics:

- **Total Customer Service Calls**
- **Average Customer Service Calls per Customer**
- **Average Account Length by Payment Method & Contract Category**
- **Churn Rate by Payment Method & Contract Category**

---

### 2.9 Usage, Extra Charges and Churn Risk

**Slide:** `Usage, Extra Charges and Churn Risk`  

Focus:

- KPI cards for:
  - **Average Extra International Charges**
  - **Average Extra Data Charges**
- Bar chart: **Churn Rate by Grouped Consumption and Unlimited Data Plan**

Key metrics:

- **Avg Extra International Charges**
- **Avg Extra Data Charges**
- **Churn Rate by Usage Band and Plan Type**

---

### 2.10 Customer Service Calls and State-Level Churn

**Slide:** `Customer Service Calls and State-Level Churn`  

Focus:

- KPI cards:
  - **Customer Service Calls (total)**
  - **Avg Customer Service Calls**
  - **Avg Extra International Charges**
  - **Avg Extra Data Charges**
- Map: **Churn Rate by State**
- Line chart: **Avg Customer Service Calls by State and Churn Label**

Key metrics:

- **Average Service Calls by State**
- **Average Service Calls by Churn Status (Yes/No)**
- Combination of **extra charges metrics** with geographic churn.

---

## 3. Key Metrics & DAX Logic (Conceptual)

Most insights in the report are driven by the following custom measures and calculated fields:

### 3.1 Core Churn KPIs

- **Total Customers** – distinct count of customer IDs  
- **Churned Customers** – count of customers where churn label = "Yes"  
- **Churn Rate %**  

  > churn rate = churned customers / total customers  

- **Retention Rate %**

  > retention rate = 1 – churn rate  

These measures are reused on almost every slide as KPI cards and in segment-level comparisons.

### 3.2 Segmentation Fields (Calculated Columns)

- **Age Bin** – groups customers into age ranges (e.g. `<20`, `20–30`, `30–40`, …, `80+`).
- **Grouped Consumption** – usage bands based on data consumption (`<5 GB`, `5–10 GB`, `10+ GB`).
- **Contract Category** – `Monthly` vs `Yearly` grouping based on detailed contract types.
- **Senior Flag / Under 30 Flag** – Boolean fields used in the senior vs under-30 matrix.

These columns enable the layered analysis of churn across age, usage, and contract structures.

### 3.3 Revenue and Charges Metrics

- **Avg Monthly Charge**
- **Avg Total Charges / Lifetime Charges** (where applicable)
- **Avg Extra International Charges**
- **Avg Extra Data Charges**

These are used to understand how pricing and additional charges relate to churn, and to highlight where revenue is at risk.

### 3.4 Usage, Plans and Contract Metrics

- **Churn Rate by Unlimited Data Plan**
- **Churn Rate by International Plan Active**
- **Churn Rate by Group Size (Number of Customers in Group)**
- **Churn Rate by Contract Type / Contract Category**

These metrics explain how plan structure and usage intensity influence the likelihood of churn.

### 3.5 Customer Service & Payment Metrics

- **Total Customer Service Calls**
- **Average Customer Service Calls per Customer**
- **Average Service Calls by State and Churn Status**
- **Churn Rate by Payment Method**
- **Average Account Length by Payment Method & Contract Category**

These measures connect operational behavior (support interactions, payment channel, tenure) with churn outcomes.

### 3.6 Geographic Metrics

- **Churn Rate by State**
- **Customer Count by State**
- **Average Service Calls by State**

Used on map visuals and line charts to reveal regional differences.

---

## 4. How to Use the Report

1. Open `Taisiia_Starchenko_pbi_case_study.pbix` in **Power BI Desktop**.
2. Navigate through the pages described above:
   - Start with **“Churn Overview: Key Metrics and Drivers”**.
   - Explore detail pages for contracts, age, usage, extra charges, payment methods, and service calls.
3. Use slicers (e.g. **Account Length**, **Contract Category / Payment Method**) to filter the dashboards.
4. Compare segments against the global **churn rate** to identify high-risk groups and drivers.

---

## 5. Repository Structure

```text
.
├── Taisiia_Starchenko_pbi_case_study.pbix   
├── README.md                                
└── data/
    └── Databel - Data.csv                   
