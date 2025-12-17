# Architecture & Implementation Plan

## Service mapping

| Layer          | Service (Cloud)      | Role in Solution                                                                                             | Related Module   |
| -------------- | -------------------- | ------------------------------------------------------------------------------------------------------------ | ---------------- |
| Storage        | Google Cloud Storage | Stores raw CSV and JSON files from CROs and EDC systems for auditing and traceability                        | Module 6         |
| Compute        | Cloud Run            | Runs the Flask application for data uploads, API access, and dashboard queries                               | Modules 3, 5, 10 |
| Serverless     | Cloud Functions      | Pulls EDC API data on a schedule and performs data validation                                    | Module 5         |
| Database / SQL | Cloud SQL            | Stores cleaned participant, site-level, and retention data for querying and reporting                        | Module 7         |
| Analytics / AI | Vertex AI Notebook   | Computes enrollment rates, screening outcomes, retention metrics, and generates forecasts using analytics/AI | Module 9         |
