### Medallion Architecture Layer Comparison

| Category             | Bronze Layer                              | Silver Layer                                      | Gold Layer                                               |
|----------------------|--------------------------------------------|--------------------------------------------------|-----------------------------------------------------------|
| **Definition**       | Raw, unprocessed data as-is from sources  | Clean & standardized data                        | Business-ready data                                       |
| **Objective**        | Traceability & Debugging                  | Prepare data for analysis                        | Provide data for reporting & analytics                    |
| **Object Type**      | Tables                                     | Tables                                           | Views                                                     |
| **Load Method**      | Full Load (Truncate & Insert)             | Full Load (Truncate & Insert)                   | None                                                      |
| **Transformation**   | None (as-is)                               | - Cleaning<br>- Standardization<br>- Normalization<br>- Derived Columns<br>- Enrichment | - Integration<br>- Aggregation<br>- Business Logic & Rules |
| **Data Modeling**    | None (as-is)                               | None (as-is)                                    | - Star Schema<br>- Aggregated Objects<br>- Flat Tables     |
| **Audience**         | Data Engineers                             | Data Engineers<br>Data Analysts                  | Data Analysts<br>Business Users                            |

### ETL Workflow by Layer

| Step         | Bronze Layer                                       | Silver Layer                                    | Gold Layer                                      |
|--------------|----------------------------------------------------|------------------------------------------------|------------------------------------------------|
| **Analysis** | Interview source system experts                    | Explore & understand the data                  | Explore & understand business objects          |
| **Coding**   | Data Ingestion                                     | Data Cleansing                                 | Data Integration                               |
| **Validation**| Data Completeness & Schema Checks                | Data Correctness Checks                        | Data Integration Checks                        |
| **Docs & Version**| Document & version in Git                   | Document & version in Git                      | Document & version in Git                      |

### Source System Interview Checklist

| Area                          | Questions                                                                 |
|-------------------------------|---------------------------------------------------------------------------|
| **Business Context & Ownership** | - Who owns the data?<br>- What business process does it support?<br>- Any existing documentation?<br>- Is there a data model or catalog? |
| **Architecture & Technology**   | - How is data stored? (SQL, Oracle, AWS, etc.)<br>- What are the integration methods? (API, file extract, etc.) |
| **Extract & Load Strategy**     | - Incremental or full loads?<br>- What’s the data scope & history?<br>- Expected extract size?<br>- Any volume constraints?<br>- How to avoid performance issues?<br>- Required authentication (VPN, tokens, etc.) |
