# 🇮🇳 Aadhaar Enrolment Analysis — UIDAI Data

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-005C84?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft&logoColor=white)
![Data Source](https://img.shields.io/badge/Source-UIDAI%20Open%20Data-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-success?style=for-the-badge)

> 🏛️ Government open data | 📍 State & district level analysis | 👥 Demographic & seasonal patterns across India

---

## 📊 End-to-End Analytics Pipeline

```
UIDAI CSV Data → Power Query (Cleaning & Standardization) → DAX (Measures) → Power BI (2-Page Dashboard) → Governance Insights
```

---

## 📌 Project Overview

India's Aadhaar programme generates enrolment data at a massive scale — across every state, district, age group, and season. But raw numbers alone don't tell administrators **where to send resources, which demographics are underserved, or when enrolment peaks create operational pressure.**

This project analyzes UIDAI's official Aadhaar enrolment dataset to surface **regional disparities, demographic participation gaps, district-level hotspots, and seasonal trends** — translating government data into actionable planning insights.

---

## 🎯 Problem Statement

Governance bodies face three core planning challenges with enrolment data:

1. **Which states and districts need more enrolment infrastructure?**
2. **Which age groups are underrepresented in which regions?**
3. **When do seasonal spikes occur — and how should resources be pre-positioned?**

This dashboard answers all three with interactive, drill-down visuals.

---

## 📷 Dashboard Preview

### 📌 Page 1 — Overview Analysis
[![Overview Dashboard](Screenshot%202026-01-17%20145055.png)](https://github.com/khush3521/-Aadhaar-Enrolment-Analysis/blob/main/Screenshot%202026-01-17%20145055.png)

### 📌 Page 2 — Behaviour & Pattern Analysis
[![Pattern Analysis](Screenshot%202026-01-17%20145106.png)](https://github.com/khush3521/-Aadhaar-Enrolment-Analysis/blob/main/Screenshot%202026-01-17%20145106.png)

---

## 📈 Key Insights & Governance Impact

| Finding | Planning Implication |
|---|---|
| **Enrolment varies significantly across states** | High-disparity states need targeted outreach programs |
| **Certain districts act as enrolment hotspots** | These locations require additional infrastructure & staffing |
| **Age-group participation differs by region** | Elderly and rural populations show lower enrolment rates — need mobile camps |
| **Clear seasonal spikes in enrolment activity** | Pre-position resources before peak months to avoid bottlenecks |
| **Urban districts dominate volume** | Rural districts need awareness campaigns to close the gap |

---

## 📊 Dashboard Structure

### 🔹 Page 1 — Overview Analysis
A national-level summary for administrators and policymakers:
- **Total Aadhaar Enrolments** — overall programme scale
- **State-wise Enrolment Distribution** — map and bar chart
- **Age-Group Distribution** — who is enrolling across India
- **Enrolment Trend Over Time** — month-by-month trajectory

### 🔹 Page 2 — Behaviour & Pattern Analysis
Deep-dive for district planners and field officers:
- **State-wise Enrolments by Age Group** — demographic breakdown per state
- **High-Activity Districts** — hotspot identification for resource planning
- **Seasonal Patterns** — monthly enrolment cycles and peak periods

---

## 🧠 DAX Measures

```DAX
-- Total Enrolments
Total Enrolments = SUM(aadhaar_data[EnrolmentCount])

-- State-wise Enrolment Share
State Enrolment % =
DIVIDE(
    CALCULATE([Total Enrolments], ALLEXCEPT(aadhaar_data, aadhaar_data[State])),
    CALCULATE([Total Enrolments], ALL(aadhaar_data))
)

-- Top Enrolling District
Top District =
CALCULATE(
    FIRSTNONBLANK(aadhaar_data[District], 1),
    TOPN(1, VALUES(aadhaar_data[District]), [Total Enrolments], DESC)
)

-- Enrolments by Age Group
Senior Enrolments =
CALCULATE([Total Enrolments], aadhaar_data[AgeGroup] = "60+")

Youth Enrolments =
CALCULATE([Total Enrolments], aadhaar_data[AgeGroup] = "0–18")

-- Monthly Enrolment (Seasonal Trend)
Monthly Enrolments =
CALCULATE([Total Enrolments], ALLEXCEPT(aadhaar_data, aadhaar_data[Month]))

-- MoM Growth
MoM Growth % =
VAR CurrentMonth = [Total Enrolments]
VAR PriorMonth = CALCULATE([Total Enrolments], DATEADD(aadhaar_data[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PriorMonth, PriorMonth)
```

---

## 🔄 Methodology

**1. Data Merging & Cleaning**
Combined multiple CSV files from UIDAI, removed nulls, standardized state/district name formats for consistent mapping.

**2. Feature Engineering (Power Query)**
- Extracted `Year` and `Month` from date fields for time-series analysis
- Standardized age-group labels across different file formats
- Created `Total Enrolment` as a calculated column (`Price × Quantity` equivalent for this domain)

**3. Data Modeling**
Built a star schema in Power BI — fact table (enrolments) linked to dimension tables (State, District, AgeGroup, Date).

**4. Dashboard Design**
Designed for two audiences: Page 1 for national policymakers (overview), Page 2 for district-level planners (operational detail).

---

## 🛠 Tools & Technologies

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Interactive dashboard & data modeling |
| DAX | Enrolment KPIs & analytical measures |
| Power Query | Data merging, cleaning & standardization |
| UIDAI Open Data | Official government CSV dataset |

---

## 📂 Dataset Attributes

| Column | Description |
|---|---|
| State | Indian state name |
| District | District within state |
| Pincode | Geographic pincode |
| Age Group | Demographic age bracket |
| Enrolment Count | Number of Aadhaar enrolments |
| Date / Month | Time of enrolment activity |

> **Data Source:** UIDAI Aadhaar Enrolment and Update Dataset (official government open data)

---

## 🏛️ Impact & Applicability

This analysis directly supports:
- **Resource allocation** — identify districts under infrastructure pressure
- **Outreach planning** — target underrepresented demographics with mobile camps
- **Seasonal preparedness** — pre-deploy staff and equipment before peak months
- **Policy reporting** — data-backed evidence for programme reviews

---

## 📂 Repository Structure

```
Aadhaar-Enrolment-Analysis/
│
├── data/
│   └── aadhaar_enrolment.csv
│
├── powerbi/
│   └── Aadhaar_Enrolment_Dashboard.pbix
│
├── Screenshot 2026-01-17 145055.png     ← Page 1 preview
├── Screenshot 2026-01-17 145106.png     ← Page 2 preview
└── README.md
```

> 💡 **Tip:** Rename screenshot files to `page1_overview.png` and `page2_patterns.png` for cleaner repo presentation.

---

## 🔮 Future Improvements

- Add **district-level map visualization** using shape maps
- Integrate **population census data** to calculate enrolment penetration rate (%)
- Build **predictive model** for forecasting seasonal enrolment spikes
- Add **gender-wise enrolment breakdown** if available in future UIDAI releases
- Publish to **Power BI Service** for live government dashboard sharing

---

## 👨‍💻 Author

**Khush Panchal** — Data Analyst
Specializing in business intelligence, public sector analytics & data storytelling

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/khush-panchal-96b557352)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-black?style=flat&logo=github)](https://github.com/khush3521)

---

⭐ If you found this project valuable, please consider starring this repository!
