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

## Security, Identity, and Governance Basics

Credentials for accessing cloud services would be managed using environmental variables to ensure that no sensitive data is hard-coded in the databases or flask application. Role-based access control would be given to users with specific permissions. For instance, study coordinators would only be able to upload files, while analysts can query the dashboards, and administrators can manage the infrastructure. To ensure that patient information is protected, all personal health information will be de-identified. This would be done by using only assigned participant IDs that contain no personal information. 

## Cost and Operational Considerations

The components that might cost the most are Cloud Run compute for the Flask app and Vertex AI notebooks. This is because running these applications and predictive models consumes compute and memory the most frequently, especially if there are many incoming requests. However, to minimize costs, serverless functions that are used for the scheduled EDC API pulls will only be executed when triggered. Additionally, data storage costs will be low because JSON and CSV files are usually small, and the older files can be moved to cheaper archival storage when needed. To keep this project in a friendly student budget, analytics frequency should be limited and only recent datasets will be stored in the cloud. 
