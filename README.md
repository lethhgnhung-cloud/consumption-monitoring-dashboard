# 📊 Operational Resource Intelligence Dashboard

> **A centralized Power BI solution for multi-branch OPEX monitoring — consolidating electricity, fuel, and supply data into a single source of truth.**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Advanced-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Problem Statement](#-problem-statement)
- [Solution Architecture](#-solution-architecture)
- [Dashboard Design](#-dashboard-design)
- [Key DAX Measures](#-key-dax-measures)
- [Business Insights](#-business-insights)
- [Measurable Impact](#-measurable-impact)
- [Screenshots](#-screenshots)
- [Repository Structure](#-repository-structure)
- [How to Use](#-how-to-use)

---

## 🎯 Project Overview

This project delivers an end-to-end **Operational Intelligence System** built in Power BI for a multi-branch corporate environment. It replaces fragmented, manual Excel-based reporting with an automated, interactive dashboard that enables leadership to shift from **reactive tracking** to **proactive cost optimization**.

| Attribute | Details |
|-----------|---------|
| **Tool** | Microsoft Power BI Desktop |
| **Data Model** | Star Schema |
| **Analytics Layer** | Advanced DAX (Time Intelligence + Variance Analysis) |
| **Scope** | Electricity · Fuel (Gasoline) · Office Supplies |
| **Stakeholders** | C-Suite · Finance · Facilities · Supply Chain · Branch Managers |

---

## 🔍 Problem Statement

In a multi-branch corporate environment, operational expenditure (OPEX) tracking suffered from three critical pain points:

- **Data Silos** — Electricity, fuel, and supply data lived in separate local reports with no unified view.
- **Manual Consolidation** — Finance teams spent 16+ hours per month aggregating Excel files, introducing human-entry errors.
- **Reactive Decision-Making** — Management only discovered budget overruns after the fact, with no early-warning system.

---

## 🏗️ Solution Architecture

### Data Modeling — Star Schema

To ensure high performance with large datasets, the solution implements a **Star Schema** with clear separation between facts and dimensions.

```
                    ┌─────────────┐
                    │ dim_Calendar│
                    └──────┬──────┘
                           │
┌──────────────┐    ┌──────▼──────┐    ┌──────────────┐
│  dim_Branch  ├────► fct_Consump │◄───┤ dim_Category │
└──────────────┘    └──────┬──────┘    └──────────────┘
                           │
┌──────────────┐    ┌──────▼──────┐
│  dim_Users   ├────► fct_Budget  │
└──────────────┘    └─────────────┘
```

| Table | Type | Description |
|-------|------|-------------|
| `fct_Consumption` | Fact | Transactional resource consumption logs |
| `fct_Budget` | Fact | Allocated budget per branch / category / period |
| `dim_Branch` | Dimension | Branch metadata and hierarchy |
| `dim_Category` | Dimension | Resource type classification |
| `dim_Users` | Dimension | Employee/user lookup |
| `dim_Calendar` | Dimension | Date table for time-intelligence functions |

> All relationships are designed to prevent circular dependency risks, ensuring clean cross-filtering across all visuals.

---

## 🖥️ Dashboard Design

The report is structured as a **4-tier analytical journey**, each tier designed for a specific stakeholder group.

### Level 1 — Executive Overview
> **Audience:** C-Suite / Leadership Team

A high-level pulse view showing total OPEX vs. Budget, YTD performance KPIs, and top-level variance indicators — designed for a 30-second read.

### Level 2 — Resource Deep-Dive (Paper & Gasoline)
> **Audience:** Supply Chain / Procurement Team

Focused analysis on logistics and consumable waste. Helps identify over-ordering patterns and optimize inventory replenishment cycles.

### Level 3 — Energy Intelligence (Electricity)
> **Audience:** Facilities & Infrastructure Department

Specialized view to monitor the company's energy footprint, track peak usage periods, and support sustainability reporting.

### Level 4 — Branch Performance Audit
> **Audience:** Regional & Branch Managers

Granular drill-down by branch location to identify high-waste behaviors, compare efficiency benchmarks, and surface operational inefficiencies.

---

## 🧮 Key DAX Measures

### Budget Compliance %
Calculates the variance between actual spend and allocated budget, returning `BLANK` when no budget exists to prevent misleading visuals.

```dax
Budget Compliance % =
VAR Actual = [Total Actual Spend]
VAR Budget = [Total Budget Allocation]
RETURN
    IF(
        ISBLANK(Budget),
        BLANK(),
        DIVIDE(Actual - Budget, Budget, 0)
    )
```

### Year-over-Year (YoY) Growth
```dax
YoY Consumption Growth % =
VAR CurrentYear = [Total Consumption]
VAR PriorYear   = CALCULATE([Total Consumption], SAMEPERIODLASTYEAR(dim_Calendar[Date]))
RETURN
    IF(
        ISBLANK(PriorYear),
        BLANK(),
        DIVIDE(CurrentYear - PriorYear, PriorYear, 0)
    )
```

### Average Consumption per User
```dax
Avg Consumption per User =
DIVIDE(
    [Total Consumption],
    DISTINCTCOUNT(dim_Users[UserID]),
    0
)
```

> Additional DAX logic includes **conditional formatting rules** to automatically flag anomalies and budget overruns using color-coded visual cues.

---

## 💡 Business Insights

Three critical insights were surfaced from data exploration that directly influenced management decisions.

### 1. Head Office Resource Concentration — 70.14%
Analysis revealed that the Head Office consumes **over 70% of total system-wide resources** despite not proportionally hosting more staff.

**Action Taken:** Initiated a specialized HO facilities audit and implemented a smart-lighting policy to reduce passive consumption.

---

### 2. Recurring Q1 Spending Spikes
A consistent surge in resource usage was identified every **January/February** across multiple years, exceeding quarterly budgets mid-cycle.

**Action Taken:** Restructured the quarterly budget model to **front-load resources for Q1**, preventing mid-quarter shortages and emergency procurement.

---

### 3. Efficiency Anomaly at Branch D3
Branch D3 showed a **lower total spend** but its **Average Consumption per User was 20% higher** than the company average — a hidden inefficiency masked by smaller headcount.

**Action Taken:** Flagged D3 for a "Best Practice" benchmarking session, using high-performing branches (e.g., Branch TB) as reference models.

---

## 📈 Measurable Impact

| Metric | Result |
|--------|--------|
| **Automation Rate** | 90% — eliminated 16+ hours of manual Excel consolidation per month |
| **Reporting Accuracy** | 100% improvement through automated ETL pipeline, removing human-entry errors |
| **Budget Transparency** | Reduced "shadow spending" by giving branch managers self-service visibility into live budget status |
| **Decision Speed** | Shifted from monthly reactive reviews to real-time proactive monitoring |

---

## 📸 Screenshots

| Dashboard Tier | Preview |
|----------------|---------|
| Executive Overview | [View Snapshot 1](https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%201.png) |
| Resource Deep-Dive | [View Snapshot 2](https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%202.png) |
| Energy Intelligence | [View Snapshot 3](https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%203.png) |
| Branch Performance Audit | [View Snapshot 4](https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%204.png) |

---

## 📂 Repository Structure

```
consumption-monitoring-dashboard/
│
├── 📁 images/                    # UI/UX screenshots for all 4 dashboard tiers
│   ├── Snapshot 1.png            # Executive Overview
│   ├── Snapshot 2.png            # Resource Deep-Dive
│   ├── Snapshot 3.png            # Energy Intelligence
│   └── Snapshot 4.png            # Branch Performance Audit
│
├── 📊 Dashboard.pbix             # Main Power BI file (Star Schema + DAX measures)
├── 📋 Documentation.xlsx         # Data dictionary, field definitions, and source mapping
└── 📄 README.md                  # This file
```

---

## 🚀 How to Use

**Prerequisites:** Microsoft Power BI Desktop (latest version recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard.git
   ```

2. **Open the report**
   - Launch Power BI Desktop
   - Open `Dashboard.pbix`

3. **Explore the data model**
   - Navigate to **Model View** to inspect the Star Schema and table relationships
   - Review all DAX measures in the **Data Pane**

4. **Reference the documentation**
   - Open `Documentation.xlsx` for full field definitions, data source descriptions, and transformation logic

5. **Browse screenshots**
   - Navigate to the `/images` folder for a quick visual walkthrough of each dashboard tier

---

*If you find this project useful, feel free to ⭐ star the repository.*
