HR Employee Attrition Analysis

End-to-End Data Analytics Project | Python + Power BI

📌 Project Overview

This project performs a complete end-to-end analysis of employee attrition using the IBM HR Analytics Dataset. The goal is to uncover the key factors that drive employees to leave an organization — and translate those findings into actionable HR recommendations.

The project is split into two phases:


Phase 1 — Python: Data cleaning, feature engineering, and exploratory data analysis (EDA)
Phase 2 — Power BI: Interactive 3-page dashboard with DAX measures for business stakeholders



Business Question: What factors most strongly predict employee attrition, and what can HR do about it?


🎯 Key Findings

FactorAttrition RateInsightOverTime: Yes30.5%3× higher than non-overtime (10.4%)OverTime: No10.4%Baseline — manageable levelSales Representative39.76%Highest attrition by job roleResearch Director2.50%Lowest attrition by job roleIncome Band: Low~29%Pay directly influences retentionTenure: 0–2 Years~34%New hires are the highest-risk groupMaritalStatus: Single25.5%2× higher than Married (12.5%)High Risk Employees154Low satisfaction + poor work-life balance


Income Gap: Employees who stayed earned ₹2,043/month more on average than those who left (₹6,830 vs ₹4,787)


🗂️ Project Structure

HR-Attrition-Analysis/
│
├── 📓 IBM_Attrition_Data_cleaning.ipynb   # Python notebook — cleaning + EDA
├── 📄 WA_Fn-UseC_-HR-Employee-Attrition.csv  # Raw dataset
├── 📄 HR_Attrition_Cleaned.csv            # Cleaned + engineered dataset (exported to Power BI)
├── 📊 HR_Attrition_Dashboard.pbix         # Power BI dashboard file
├── 📝 README.md                           # Project documentation
└── 📁 screenshots/
    ├── page1_overview.png
    ├── page2_risk_drivers.png
    └── page3_compensation_tenure.png


    🛠️ Tools & Technologies

ToolPurpose
Python 3Core programming languagepandasData loading, cleaning, transformation, exportnumpyNumeric operationsmatplotlibHistograms, bar chartsseabornBoxplots, correlation heatmapsGoogle ColabNotebook environmentPower BI DesktopInteractive dashboardDAXCalculated KPI measuresPower QueryData type verification before load


📋 Dataset


Source: IBM HR Analytics Employee Attrition & Performance — Kaggle
Size: 1,470 rows × 35 columns
Type: Fictional dataset created by IBM data scientists
No missing values, no duplicates


Ordinal column encoding (used in this project):

ColumnScaleEducation1=Below College → 5=DoctorJobSatisfaction1=Low → 4=Very HighEnvironmentSatisfaction1=Low → 4=Very HighWorkLifeBalance1=Bad → 4=BestPerformanceRating1=Low → 4=OutstandingJobInvolvement1=Low → 4=Very HighRelationshipSatisfaction1=Low → 4=Very High


🔄 Workflow

Raw CSV
   │
   ▼
Phase 1: Python
   ├── Data Inspection (shape, dtypes, nulls, duplicates)
   ├── Cleaning (drop constants, create binary flags)
   ├── Feature Engineering
   │     ├── Label mapping → _Label columns for 7 ordinal columns
   │     ├── Attrition_Flag (1/0), OverTime_Flag (1/0)
   │     ├── AgeGroup (18-25, 26-35, 36-45, 46-60)
   │     ├── IncomeBand (Low/Medium/High/Very High — quartile-based)
   │     ├── TenureGroup (New/Mid/Established/Veteran)
   │     └── DistanceBand (Near/Medium/Far)
   ├── EDA — Univariate (histograms, value counts, skew check)
   ├── EDA — Bivariate (attrition rate by each group via groupby)
   ├── Correlation Heatmap (numeric features vs Attrition_Flag)
   └── Export → HR_Attrition_Cleaned.csv
   │
   ▼
Phase 2: Power BI
   ├── Import cleaned CSV + verify data types in Power Query
   ├── Set Sort by Column for all _Label columns
   ├── Create 12 DAX measures
   └── Build 3-page interactive dashboard


   📊 Power BI Dashboard

Page 1 — HR Attrition Overview


Who is leaving?




KPI Cards: Total Employees, Total Attritions, Attrition Rate %, Avg Monthly Income
Bar Chart: Attrition Rate % by Department
Donut Chart: Employee distribution by Age Group
Slicers: Department, Gender, JobRole


Page 2 — Risk Drivers


Why are they leaving?




KPI Cards: Attrition Rate (OverTime) = 30.5%, Attrition Rate (No OverTime) = 10.4%, High Risk Employees = 154
Bar Charts: Attrition by OverTime, WorkLifeBalance, JobSatisfaction, EnvironmentSatisfaction, DistanceBand, TenureGroup
Matrix: JobRole × OverTime → Attrition Rate %


Page 3 — Compensation & Tenure


Does money and time matter?




KPI Cards: Avg Income (Stayed), Avg Income (Left), Income Gap (₹2.05K), Avg Tenure
Bar Charts: Attrition by IncomeBand, Avg Income by JobRole
Column Chart: Avg Income by Attrition (Stayed vs Left)
Scatter Plot: YearsAtCompany vs MonthlyIncome, colored by Attrition
Matrix: JobRole × IncomeBand → Attrition Rate %


⚙️ DAX Measures

Total Employees = COUNTROWS(Employees)

Total Attritions = CALCULATE(COUNTROWS(Employees), Employees[Attrition] = "Yes")

Attrition Rate % = DIVIDE([Total Attritions], [Total Employees], 0)

Avg Monthly Income = AVERAGE(Employees[MonthlyIncome])

Avg Income (Stayed) = CALCULATE([Avg Monthly Income], Employees[Attrition] = "No")

Avg Income (Left) = CALCULATE([Avg Monthly Income], Employees[Attrition] = "Yes")

Income Gap = [Avg Income (Stayed)] - [Avg Income (Left)]

Attrition Rate (OverTime) = CALCULATE([Attrition Rate %], Employees[OverTime] = "Yes")

Attrition Rate (No OverTime) = CALCULATE([Attrition Rate %], Employees[OverTime] = "No")

High Risk Employees =
CALCULATE(
    [Total Employees],
    Employees[JobSatisfaction] <= 2,
    Employees[WorkLifeBalance] <= 2
)


📈 Summary Insight


Overtime is the single strongest driver of employee attrition — employees working overtime leave at 31%, nearly 3× the rate of those who don't (10%). Compensation also plays a major role: employees who stayed earned an average of ₹6.83K versus ₹4.79K for those who left. Attrition risk is highest among new hires (0–2 years) and varies sharply by job role rather than department — Sales Representatives attrite at ~40% compared to just 2.5% for Research Directors. HR should prioritize reviewing overtime policies, reassessing pay in high-risk roles, and strengthening onboarding for new employees.

👤 Author

Anuj Sandip Jagtap
Data Analytics Intern | Analytics Career Connect
