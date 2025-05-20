# Job Requisition Aging & SLA Compliance Dashboard (Google Looker Studio)

## 📊 Overview
This dashboard provides insights into how long job requisitions remain open and tracks compliance with Service Level Agreements (SLAs). It's designed to help recruitment teams improve process efficiency and accountability.

## 🎯 Objectives
- Monitor average time-to-fill and SLA adherence
- Identify bottlenecks in requisition closure
- Flag overdue or long-aged open requisitions
- Support recruitment operations with actionable analytics

## 🧰 Tools Used
- **Google Looker Studio** for visualization
- **CSV (mock data)** simulating requisitions, their durations, and statuses

## 📁 Dataset Fields
- `Requisition_ID`
- `Job_Title`
- `Department`
- `Recruiter`
- `Recruiter_Display`
- `Open_Date`
- `Close_Date`
- `Status` (Open, Filled, Cancelled)
- `Days_Open`
- `Days_Open_Bucket`
- `SLA_Target_Days` (default: 30 days)
- `SLA_Met` (Yes/No)
- `SLA_Status_Clean`

## ➕ Metrics & Calculated Fields Used in Looker Studio

### 🎨 Aging Color Bucket (Used for color-coding charts)
```sql
CASE
  WHEN Days_Open <= 56 THEN "01 - Light Orange"
  WHEN Days_Open <= 61 THEN "02 - Soft Orange"
  WHEN Days_Open <= 66 THEN "03 - Medium Orange"
  WHEN Days_Open <= 76 THEN "04 - Orange"
  ELSE "05 - Dark Orange"
END
```

### ✅ SLA Status Clean (Used to filter or group SLA performance)
```sql
CASE
  WHEN SLA_Met = "Yes" THEN "Yes"
  WHEN SLA_Met = "No" THEN "No"
  ELSE "Exclude"
END
```

## 📈 Key Visuals
- **Average Days Open by Department**
offers insights into how long requisitions remain open within each department, helping spot potential process delays.
- **SLA Compliance Rate Gauge**
displays the percentage of requisitions closed within SLA by each recruiter to highlight adherence and areas for improvement.
- **Open Requisitions Table with Aging Bucket**
presents the current breakdown of requisition statuses (Open, Filled, Cancelled), giving a snapshot of hiring pipeline activity.
- **Top 10 Longest Open Requisitions**
highlights the requisitions that have been open the longest (filtered to only those still open), helping prioritize follow-ups on overdue roles.

## 📂 File
- `job_requisition_sla_dashboard.csv` – sample dataset with 100 requisition records

## 🧪 Use Cases
- HR ops managers can monitor overdue requisitions
- Recruiters can prioritize based on time open
- SLA compliance reporting for executive teams

### 🔟 Top 10 Longest Open Requisitions (with Status Filter)

This table visual highlights the top 10 requisitions that have been open the longest. To ensure relevance, a filter is applied to only include requisitions with a status of `"Open"`.

#### Filter Applied:
- **Field:** `Status`
- **Condition:** `Status = "Open"`
- **Sort By:** `Days_Open` (Descending)
- **Limit Rows:** 10

This allows recruitment teams to quickly identify which active roles have remained unfilled for the longest period and may require escalation or follow-up.
