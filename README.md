# OPERATIONAL RESOURCE INTELLIGENCE DASHBOARD & CONSUMPTION ANALYTICS
🏢 **1. Executive Summary & Context**

In a multi-branch corporate environment, managing operational expenditures (OPEX) often suffers from Data Silos - where information on electricity, fuel, and supplies is scattered across different local reports.

This project involved the digital transformation of the resource monitoring process. I built a centralized Operational Intelligence System that consolidates data from multiple sources into a single "Source of Truth." This system allows the leadership team to shift from reactive tracking (finding out what was spent last month) to proactive cost optimization (identifying trends in real-time).

**🛠 2. Technical Core & Architecture**
**A. Data Modeling (The Foundation)**

To ensure high performance with large datasets, I implemented a Star Schema architecture:

Fact Tables: Centralized fct_Consumption and fct_Budget tables containing transactional logs.

Dimension Tables: Optimized lookup tables for dim_Branch, dim_Category, dim_Users, and a dedicated dim_Calendar.

Relationships: Many relationships established to ensure clean filtering without circular dependency risks.

**B. Analytical Logic (Advanced DAX)**

The core of the intelligence lies in the DAX measures developed to handle Time-Intelligence and Variance Analysis:

YoY Comparisons: Calculated Year-over-Year consumption growth to normalize seasonal peaks.

Dynamic Efficiency Metrics: Measures that calculate the Average Consumption per Month/Branch, allowing for fair comparisons regardless of branch size.

Conditional Formatting Logic: DAX-driven rules to flag "Anomalies" or "Budget Overruns" using visual cues.

Budget Compliance % = 
VAR Actual = [Total Actual Spend]
VAR Budget = [Total Budget Allocation]
RETURN 
IF(
    ISBLANK(Budget), 
    BLANK(), 
    DIVIDE(Actual - Budget, Budget, 0)
)

🖥 **3. Multi-Layered Dashboard Navigation**

The dashboard is designed as a 4-tier analytical journey, catering to different stakeholder needs:

- Level 1: Executive Overview: A Pulse view for C-level executives focusing on total OPEX vs. Budget and high-level YTD performance.

- Level 2: Resource Deep-Dive (Paper & Gasoline): Focused on logistics and consumable waste. Helps the Supply Chain team optimize inventory.

- Level 3: Energy Intelligence (Electricity): A specialized view for the Facilities department to monitor the company’s energy footprint.

- Level 4: Branch Performance Audit: A granular view that allows managers to drill down into specific locations to identify high-waste behaviors or operational inefficiencies.

💡 **4. Business Insights & Strategic Recommendations**

Through data exploration, three critical insights were identified that directly influenced management decisions:

- Head office Concentration (70.14%): Analysis revealed that the Head Office consumes over 70% of total system-wide resources.

- Action: Recommended a specialized audit of HO facilities and implemented a smart-lighting policy.

- Early Q1 Spikes: Identified a recurring surge in resource usage every January/February.

- Action: Restructured the quarterly budget to front-load resources for the beginning of the year, preventing mid-quarter shortages.

- Efficiency Benchmarking: Discovered that while Branch D3 has a lower total spend, its Average Consumption per User was 20% higher than the company average.

- Action: Flagged for a "Best Practice" training session to align D3 with higher-performing branches like TB.

📈 **5. Measurable Impact (ROI)**

- 90% Automation: Eliminated 16+ hours of manual Excel data consolidation per month.

- Transparency: Reduced "Shadow Spending" by providing branch managers with self-service visibility into their remaining budget.

- Data Accuracy: Improved reporting integrity by 100% through the automation of the ETL pipeline, eliminating human-entry errors.

📂 **6. How to Use this Repository**

View Screenshots: Navigate to the /images folder to see the UI/UX design of each tier.

Explore the Model: Open the .pbix file to examine the Star Schema and DAX measures.

Data Dictionary: Refer to Documentation.xlsx for field definitions and data sources.

Link to access this demo: 
1. https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%201.png
2. https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%202.png
3. https://github.com/lethhgnhung-cloud/consumption-monitoring-dashboard/blob/main/Snapshot%203.png
