# Use Case Description
The Clinical Trial Screening, Enrollment, and Retention Tracker is a cloud-based platform that would give clinical trial sponsors further insight into their trial performance by centralizing participant-level screening data, site-level enrollment metrics, and retention data across multiple sites and trials.

## Problem Statement

Many clinical research studies, especially those that are run by Contract Research Organizations (CROs), are required to meet enrollment timelines, as well as recruit a certain number of participants. However, there are challenges such as delayed data reporting, participant screening challenges, and underperforming sites. Some clinical sites submit data in spreadsheets and manual data entry can cause delays and errors. Additionally, many participants fail eligibility criteria or may withdraw from the study. Some sites also enroll fewer participants and may experience higher drop out rates, but without a centralized cloud platform, sponsors lack these real-time insights. As a result, trials get delayed which causes an increase in costs and creates longer drug development timelines. 

## Data Sources
- **Site Level Enrollment Data**:
  - Since many sites rely on manual workflows, this data is shared by organizations as spreadsheets. It would show how well each trial and site is performing relative to the target. These spreadsheets can come in the form of CSV files.
- **Participant-Level Screening Data**:
  - This data comes from Electronic Data Capture systems such as REDCap or Oracle Clinical. This information is recorded by study coordinators during a participant's visit and can show eligibility assessments. The data can be accessed in JSON format from APIs.
- **Visit Completion Data**:
  - This information comes from EDC systems in JSON format from APIs. This data can show missed visits, early withdrawals, and dropouts due to any adverse events. This can help detect trends of disengagement before a participant fully withdraws from the study.
- **Historical Enrollment Data**:
  - This data comes from past clinical trials which can be stored in a SQL database. This data can predict trends such as expected trial completion date and enrollment forecasting.


## Basic Workflow
1. CROs and EDC systems submit screening, enrollment, and retention data through file uploads or scheduled API pulls
2. All CSV and JSON files are stored in cloud object storage for auditing purposes
3. Automated processing cleans the data and standardizes it
4. The cleaned data is saved in a centralized database where it can be queried
5. The system analyzes enrollment progress, screening outcomes, and retention rates to identify risks
6. A web reports and visualizes key metrics and trends for trials and study sites
7. The system flags specific trials or sites that are underperforming due to low enrollment or high withdrawal rates
8. When new data is uploaded, the dashboards are updated automatically


