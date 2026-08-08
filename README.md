# Medicare Opioid Treatment Programs: Accessibility & Need Analysis

## Overview
The opioid crisis is one of the most severe public health challenges in the United States. While Medicare covers certified Opioid Treatment Programs (OTPs), access to these facilities is incredibly uneven. 

This project uses Power BI to analyze 12 years of CMS provider data. It is designed to serve multiple stakeholders: helping policymakers evaluate the impact of Medicare reimbursement expansions, allowing health insurance payers to identify critical funding gaps, and providing a localized referral engine for care coordinators. To provide a complete analytical picture, the dashboard's geographic data is evaluated against external 2024 CDC overdose mortality rates to highlight severe misalignments in care.

## Tech Stack & Data Engineering
* **Tools:** Power BI Desktop, DAX, Power Query
* **Data Source:** CMS.gov Provider Characteristics Registry (1,332 validated providers, 2014–2026).
* **Modeling:** Star Schema architecture with a custom, disconnected Date Dimension table to accurately track historical growth.
* **Cleaning:** Used Power Query to clean corrupted, concatenated string anomalies in the dataset, extracting valid 10-digit National Provider Identifiers (NPIs) for accurate distinct counting.
* **Custom DAX:** Embedded a dynamic U.S. Census population table directly into the data model using a `SWITCH` statement. This allows the dashboard to instantly calculate and display per-capita metrics based on user selection.

## Key Insights

### 1. The Misalignment Index (State-by-State Risk Ranking)
By dividing a state's Overdose Mortality Rate by its Clinic Density, we generate an **Overdose-to-Treatment Ratio**. A higher ratio indicates a severe lack of treatment infrastructure relative to the loss of life. 

The full analysis proves that supply does not match the actual need. High-population states like Florida and rural states like Mississippi have massive gaps in care, while states like Rhode Island and Maryland have much healthier treatment baselines relative to their crisis levels. 

Below is the complete dataset ranking from worst access (highest ratio) to best access (lowest ratio):

| Rank | State | Overdose Deaths (per 100k) | Clinic Density (per 100k) | Overdose-to-Treatment Ratio |
| :---: | :---: | :---: | :---: | :---: |
| 1 | MS | 25.6 | 0.10 | **250.9** |
| 2 | LA | 42.7 | 0.24 | **177.5** |
| 3 | MA | 33.7 | 0.20 | **168.5** |
| 4 | MO | 32.1 | 0.21 | **153.0** |
| 5 | AR | 14.7 | 0.10 | **150.3** |
| 6 | TN | 45.6 | 0.31 | **147.7** |
| 7 | DC | 59.5 | 0.44 | **134.7** |
| 8 | FL | 37.5 | 0.31 | **122.9** |
| 9 | OK | 21.0 | 0.17 | **121.6** |
| 10 | IN | 36.6 | 0.34 | **109.2** |
| 11 | NV | 27.6 | 0.28 | **98.0** |
| 12 | ID | 19.0 | 0.20 | **93.3** |
| 13 | MN | 23.3 | 0.26 | **89.1** |
| 14 | PA | 42.4 | 0.48 | **88.6** |
| 15 | WI | 27.7 | 0.32 | **86.2** |
| 16 | NM | 40.2 | 0.47 | **85.0** |
| 17 | TX | 16.6 | 0.20 | **84.4** |
| 18 | HI | 17.5 | 0.21 | **83.7** |
| 19 | KS | 17.0 | 0.20 | **83.3** |
| 20 | OH | 41.3 | 0.53 | **78.5** |
| 21 | KY | 46.8 | 0.60 | **78.5** |
| 22 | NY | 28.7 | 0.37 | **78.0** |
| 23 | NJ | 32.4 | 0.42 | **77.2** |
| 24 | MI | 30.5 | 0.40 | **76.5** |
| 25 | IA | 14.3 | 0.19 | **76.4** |
| 26 | WV | 38.6 | 0.51 | **75.9** |
| 27 | WA | 28.1 | 0.38 | **73.2** |
| 28 | AL | 25.5 | 0.35 | **72.4** |
| 29 | CT | 39.1 | 0.55 | **70.7** |
| 30 | SC | 35.8 | 0.52 | **68.7** |
| 31 | VA | 30.4 | 0.47 | **64.6** |
| 32 | OR | 25.8 | 0.40 | **64.2** |
| 33 | ME | 47.1 | 0.79 | **59.8** |
| 34 | IL | 28.1 | 0.49 | **56.9** |
| 35 | NH | 32.0 | 0.57 | **56.1** |
| 36 | DE | 48.0 | 0.87 | **55.0** |
| 37 | MT | 18.9 | 0.35 | **53.5** |
| 38 | UT | 20.3 | 0.38 | **53.4** |
| 39 | GA | 22.3 | 0.44 | **51.2** |
| 40 | NC | 36.3 | 0.71 | **51.1** |
| 41 | CO | 31.4 | 0.63 | **49.9** |
| 42 | SD | 5.4 | 0.11 | **49.6** |
| 43 | AZ | 26.9 | 0.62 | **43.5** |
| 44 | AK | 37.0 | 0.95 | **38.8** |
| 45 | CA | 13.5 | 0.35 | **38.1** |
| 46 | VT | 42.3 | 1.24 | **34.2** |
| 47 | MD | 42.4 | 1.26 | **33.6** |
| 48 | ND | 16.5 | 0.51 | **32.3** |
| 49 | RI | 39.3 | 1.37 | **28.7** |
| 50 | NE | 3.3 | 0.15 | **21.8** |


### 2. Local Care Coordination
Beyond macro-level analysis, this dashboard is designed for daily operational use. A hospital discharge planner can filter the dashboard to their state, view the active clinics, and instantly pull the phone number and address of the facility closest to a patient. This localized routing is critical for preventing 30-day hospital readmissions.

### 3. Policy Impact Over Time
The longitudinal line chart shows a sharp upward trend in clinic registrations following major federal Medicare reimbursement expansions. This proves that financial incentives successfully drive provider participation, even if the geographic distribution remains flawed.

## How to Use
1. Clone this repository and open `Opioid_Treatment_Program_Providers_Analysis.pbix` in Power BI Desktop.
2. Use the **State Slicer** at the top to filter the map and KPI cards to a specific region.
3. Scroll through the **Risk Ranking Matrix** to view the worst-to-best states by treatment availability.
4. Check the top right matrix to see specific facility contact information based on your map selection.

*Sources: Centers for Medicare & Medicaid Services (CMS) Provider Characteristics Registry (2026); Centers for Disease Control and Prevention (CDC) / KFF State Overdose Mortality Rates (2024).*
