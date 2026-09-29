# IFEXA Healthcare Performance & Patient Analytics Dashboard

## Project Overview

The **Healthcare Performance & Patient Analytics Dashboard** is a Power BI data analytics project developed as part of the IFEXA Power BI Final Project.

The dashboard analyzes healthcare performance across Nigerian states by combining patient activity, operational performance, financial performance, patient experience, and state-level revenue targets.

The goal of the project is to transform healthcare data into an interactive decision-support dashboard that helps management understand:

* Patient demand and demographics
* Common diagnoses and patient outcomes
* Department and branch performance
* Revenue, cost, profit, and target achievement
* Waiting time and patient satisfaction
* Areas that may require further management investigation

---

## Business Problem

Healthcare organizations generate large amounts of patient, operational, and financial data. However, raw data alone does not provide management with an efficient way to identify performance patterns or areas requiring attention.

This project addresses the following business question:

> **How is our healthcare organization performing, what are our patients experiencing, and where are the major areas requiring attention?**

The dashboard provides a consolidated view of healthcare performance and allows users to interactively explore the data by date, state, branch, department, and gender.

---

## Dataset Description

The project dataset consists of three Excel tables:

### 1. Patient_Visits

The Patient_Visits table contains patient and healthcare activity information, including:

* Patient ID
* Visit Date
* State
* Branch
* Department
* Service
* Age
* Gender
* Diagnosis
* Payment Method
* Insurance Type
* Visit Count
* Revenue
* Cost
* Waiting Time
* Satisfaction Score
* Outcome

The dataset contains:

* **1,200 patients**
* **2,920 total visits**
* **4 states**
* **12 branches**
* **6 departments**
* **6 major diagnosis categories**
* Data covering **January–December 2025**

### 2. State_Targets

The State_Targets table contains annual revenue targets for the four states:

* Abuja
* Anambra
* Lagos
* Rivers

### 3. Date_Table

The Date_Table contains the calendar structure used for time-based analysis, including:

* Date
* Year
* Month Number
* Month
* Quarter

---

## Tools Used

* Microsoft Power BI Desktop
* Power Query
* DAX
* Microsoft Excel
* GitHub
* GitHub Markdown

---

## Data Cleaning and Transformation

The dataset was inspected and prepared before analysis.

The data preparation process included:

* Reviewing table structures and column names
* Checking data types
* Checking for missing values
* Checking for duplicate records
* Validating date fields
* Reviewing categorical values
* Ensuring numerical fields were stored using appropriate numeric data types
* Preparing the existing Date Table for time-based analysis
* Validating state-level revenue targets
* Preparing the data for Power BI modelling and analysis

The supplied dataset contained no blank values or duplicate complete records in the main Patient_Visits table after validation.

---

## Data Model

The project uses a simple star-style model with Patient_Visits as the central fact table.

### Model Structure

```text
                 Date_Table
                     |
                     | 1 : *
                     |
                     v
               Patient_Visits
                     ^
                     |
                     | 1 : *
                     |
                State_Targets
```

### Relationships

* Date_Table[Date] → Patient_Visits[Visit_Date]
* State_Targets[State] → Patient_Visits[State]

The relationships use the appropriate one-to-many structure, with the dimension/reference tables filtering the Patient_Visits fact table.

The existing Date_Table was used rather than creating an unnecessary duplicate date table.

---

## DAX Measures

The project includes more than 15 DAX measures covering operational, financial, patient, and time-based analysis.

Key measures include:

* Total Patients
* Total Visits
* Total Revenue
* Total Cost
* Total Profit
* Profit Margin %
* Average Revenue Per Patient
* Average Waiting Time
* Average Satisfaction
* Previous Month Revenue
* MoM Revenue Growth %
* Previous Year Revenue
* YoY Revenue Growth %
* Revenue Target
* Revenue Variance
* Achievement %
* New Patients
* Returning Patients
* Average Visits per Patient

### Example

```DAX
Total Patients =
DISTINCTCOUNT(Patient_Visits[Patient_ID])
```

```DAX
Total Visits =
SUM(Patient_Visits[Visit_Count])
```

```DAX
Total Profit =
[Total Revenue] - [Total Cost]
```

```DAX
Profit Margin % =
DIVIDE(
    [Total Profit],
    [Total Revenue],
    0
)
```

```DAX
Average Revenue Per Patient =
DIVIDE(
    [Total Revenue],
    [Total Patients],
    0
)
```

---

## Dashboard Pages

The dashboard contains five main analytical pages.

### 1. Executive Overview

Provides a high-level summary of healthcare performance through:

* Total Patients
* Total Visits
* Total Revenue
* Total Cost
* Total Profit
* Average Revenue per Patient
* Average Waiting Time
* Average Satisfaction
* Monthly Patient Visits
* Revenue by State
* Patients by Department
* Revenue vs Annual Target
* Patient Outcomes

### 2. Patient Analysis

Examines:

* Patients by Age Group
* Gender distribution
* Diagnoses
* Patient volume by State
* New vs Returning Patients
* Patient Outcomes
* Average Visits per Patient

### 3. Hospital Operations

Examines:

* Visits by Department
* Waiting Time
* Waiting Time by Department
* Patient Satisfaction by Department
* Branch Performance
* Patient Outcomes
* Monthly Patient Volume

### 4. Financial Performance

Examines:

* Revenue
* Cost
* Profit
* Profit Margin
* Revenue Target
* Revenue Variance
* Achievement %
* Revenue by State
* Revenue by Department
* Revenue by Service
* Profit by Department
* Monthly Revenue

### 5. Patient Experience

Examines:

* Average Satisfaction
* Satisfaction by Department
* Satisfaction by Branch
* Satisfaction vs Waiting Time
* Patient Outcomes
* Satisfaction Distribution

---

## Power BI Technical Features

The dashboard demonstrates the following Power BI capabilities:

* Star-style data modelling
* DAX measures
* Slicers
* Interactive visuals
* Cross-filtering
* Drill-through
* Report-page Tooltips
* Page Navigation
* Bookmarks
* Conditional formatting
* Date-based analysis

### Drill-through

A department drill-through page allows users to move from a high-level department analysis into a more detailed department performance view.

### Report-page Tooltips

A reusable Healthcare Performance tooltip provides additional information when users hover over selected visuals.

### Page Navigation

Navigation allows users to move between the five dashboard pages.

### Bookmarks

Bookmarks provide saved report states and support interactive report navigation/filter-reset functionality.

---

## Key Business Insights

### 1. Patient Age Distribution

Patients aged **31–45 years** represent the largest age group, with **361 patients**.

This identifies the 31–45 age segment as the largest patient population in the dataset.

### 2. Diagnosis Pattern

**Malaria** is the most common diagnosis, with **283 patients**, followed by Typhoid with 221 patients.

Management can use these patterns when reviewing demand for services associated with common diagnoses.

### 3. Branch Volume and Waiting Time

**Obio-Akpor recorded the highest number of visits at 303 visits**, with an average waiting time of approximately 49 minutes.

This makes the branch an area for management to investigate from a patient-flow and capacity perspective.

### 4. State Revenue Performance

**Rivers generated the highest revenue at approximately ₦12.73 million.**

However, **Abuja recorded the highest revenue-target achievement percentage at approximately 27.47%**.

This demonstrates that absolute revenue and target achievement provide different perspectives on state performance.

### 5. Department Performance

**Pediatrics recorded the highest patient volume at 221 patients and the highest departmental profit at approximately ₦3.71 million.**

Management should monitor whether operational capacity can continue supporting the department's high level of activity.

### 6. Waiting Time and Satisfaction

The dataset shows almost no linear relationship between waiting time and satisfaction.

This suggests that waiting time alone does not explain differences in patient satisfaction in this dataset. Other measurable patient-experience factors should therefore also be considered.

---

## Recommendations

Based on the analysis, management should consider:

1. **Investigating high-volume branches**, particularly Obio-Akpor, to understand patient-flow and capacity requirements.

2. **Monitoring high-demand departments**, particularly Pediatrics, to ensure operational resources remain aligned with patient demand.

3. **Reviewing state-level revenue performance against annual targets**, rather than evaluating revenue alone.

4. **Monitoring common diagnosis patterns** to support healthcare resource and service planning.

5. **Evaluating patient experience using multiple factors**, rather than assuming waiting time alone explains satisfaction differences.

---

## Important Data Definitions

The dataset contains one row per Patient_ID, while Visit_Count indicates the number of visits associated with that patient.

Therefore:

* **New Patients** = patients with Visit_Count = 1
* **Returning Patients** = patients with Visit_Count > 1

This definition was used because repeated Patient_ID records were not present in the supplied Patient_Visits table.

---

## Data Limitations

The dataset covers only **2025**.

As a result, year-over-year revenue comparisons with 2024 cannot be meaningfully interpreted because no 2024 observations are available.

The Previous Year Revenue and YoY Revenue Growth measures were created to satisfy the analytical requirements, but their interpretation is limited by the one-year dataset.

The annual state revenue targets are compared with annual 2025 revenue. No monthly target allocation was assumed because the supplied target table contains annual targets only.

---

## Screenshots

### Executive Overview

![Executive Overview](screenshots/executive-overview.png)

### Patient Analysis

![Patient Analysis](screenshots/patient-analysis.png)

### Hospital Operations

![Hospital Operations](screenshots/hospital-operations.png)

### Financial Performance

![Financial Performance](screenshots/financial-performance.png)

### Patient Experience

![Patient Experience](screenshots/patient-experience.png)

---

## Project Files

The repository contains:

```text
dataset/
powerbi/
screenshots/
presentation/
README.md
```

The Power BI file contains the completed interactive dashboard and analytical model.

---

## Conclusion

The Healthcare Performance & Patient Analytics Dashboard transforms healthcare activity data into an interactive analytical tool covering patient demand, hospital operations, financial performance, and patient experience.

The analysis identifies important patterns in patient demographics, diagnoses, branch activity, departmental performance, state revenue, target achievement, waiting time, and satisfaction.

The dashboard demonstrates how Power BI can be used to move from raw healthcare data to structured analysis and management-focused insights.

---

## Author

**Adekola James**

IFEXA Power BI Final Project

**Tools:** Power BI | Power Query | DAX | Excel | GitHub
