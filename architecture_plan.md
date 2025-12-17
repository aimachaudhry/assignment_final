# Architecture & Implementation Plan

## Service Mapping

| Layer          | Service (Cloud)      | Role in Solution                                                                                             | Related Module   |
| -------------- | -------------------- | ------------------------------------------------------------------------------------------------------------ | ---------------- |
| Storage        | Google Cloud Storage | Stores raw CSV and JSON files from CROs and EDC systems for auditing and traceability                        | Module 6         |
| Compute        | Cloud Run            | Runs the Flask application for data uploads, API access, and dashboard queries                               | Modules 3, 5, 10 |
| Serverless     | Cloud Functions      | Pulls EDC API data on a schedule and performs data validation                                    | Module 5         |
| Database / SQL | Cloud SQL            | Stores cleaned participant, site-level, and retention data for querying and reporting                        | Module 7         |
| Analytics / AI | Vertex AI Notebook   | Computes enrollment rates, screening outcomes, retention metrics, and generates forecasts using analytics/AI | Module 9         |


## Data Flow Narrative
1. CROs submit CSV and JSON files through the Flask app, while EDC data is retrieved automatically using Cloud Functions
2. All files are stored in Google Cloud Storage with timestamps
3. Cloud Functions standardize incoming data, flagging any missing fields
4. Cloud Run cleans and transforms the data for database storage
5. Data is loaded into Cloud SQL tables for participant and site enrollment, as well as retention metrics
6. Vertex AI notebook computes enrollment trends and site risk scores
7. The Flask app queries the database to display dashboards
8. Scheduled APIs allows for continuous updates, keeping the dashboards current 
