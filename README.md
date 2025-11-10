# Enterprise-Bordereau-Management
📘 **Overview**

A comprehensive data analytics and reporting solution designed to monitor operational transactions within a cloud-based data ecosystem.
This project demonstrates end-to-end expertise — from data modeling and warehouse design to building dynamic, parameter-driven reports that track submission schedules and missing transaction identifiers.
The system leverages **Azure Synapse Analytics**, **Power BI**, **SQL**, and **DAX**, emphasizing automation, exception tracking, and business-driven reporting for enhanced operational transparency.

Reports support:
- Interactive parameter-based filtering 
- Conditional formatting for quick exception identification  
- Multi-format export options (Excel, PDF)

⚙️ **System Architecture**
1. **Data Source Layer** 
Type: NoSQL (Azure Cosmos DB)
Purpose: Stores contract- and transaction-level data used for downstream analytics and monitoring in CosmosDB containers.
2. **Data Warehouse Layer**
Platform: Cloud Data Warehouse (Azure Synapse Analytics)
Core Views:
_vw_submission_schedule_ – Tracks expected vs. actual submission timelines
_vw_transaction_monitor_ – Monitors data processing status and updates for OSND
These curated views act as the foundation for analytical transformations and reporting.

3. **Semantic Model**
Built using Power BI Desktop, the semantic model aggregates, cleans, and structures data from the warehouse for report consumption. _Key Features_:
   - Dynamic database parameter to switch between environments (DEV/UAT/PROD).
   - DAX-based calculated columns for performance and timeliness tracking.
   - Calculated Field	Description
      - _DaysDifference_: Calculates the number of days between expected and actual receipt dates.
      - _PendingDays_:	Shows remaining or overdue days for unreceived submissions.
      - _DerivedStatus_:	Classifies records as Pending, Overdue, or Received.
      - _StatusColor_:	Applies conditional color formatting based on timeliness and category.

4. **Deployment**
  
    Environments:
    - _DEV_ – Development and unit testing
    - _UAT_ – User Acceptance Testing
    - _PROD_ – Live production data

📈 **Reports Developed**
1. Submission Monitor Report

Tracks the receipt status and timeliness of scheduled data submissions for each contract or project.

Key Functionalities:

Displays expected vs. actual receipt timelines.

Uses color-coded visual cues:
🟢 On Schedule — More than 7 days away from expected date.
🟠 Due Soon — Within the next 7 days.
🔴 Overdue — Expected date passed, not received.
🟢 Received On Time — Received before or on expected date.
🔴 Received Late — Received after expected date.

Displayed Fields:
record_id, status, document_type, submission_date, reporting_period, expected_date, received_by, received_on, business_unit, contract_name, DerivedStatus

Available Filters:

Document Type

Reporting Period

Status

Business Unit

Contract ID

This report provides a consolidated view of submission timeliness, improving accountability and reducing manual monitoring efforts.

2. Identifier Tracking Report

Monitors and identifies missing or delayed unique identifiers for processed transactions.

About the Identifier:
Each transaction record carries a unique identifier (e.g., a combination of reference number and date) generated upon successful processing.
Missing identifiers may indicate unprocessed or unsubmitted transactions — crucial for ensuring data completeness.

Key Functionalities:

Detects missing identifiers across active records.

Enables targeted filtering for root-cause analysis.

Ensures reconciliation between processed and unprocessed transactions.

Displayed Fields:
record_id, contract_id, entity_name, is_active, effective_start, effective_end, reporting_year, commission_rate, brokerage_rate, contract_category, product_segment, business_class, unique_identifier, currency, risk_type, partner, market_region, contract_name, business_unit

Available Filters:

Partner / Carrier

Reporting Year

Unique Identifier

Contract ID

This report allows teams to detect missing reference IDs early, improving data reliability and process traceability.

🧮 Tech Stack
Component	Technology
Data Source	NoSQL (Azure Cosmos DB / MongoDB)
Data Warehouse	Azure Synapse Analytics / Snowflake
Transformation Layer	SQL Views, DAX Expressions
Reporting	Power BI Desktop (Semantic Model), Power BI Report Builder (Paginated Reports)
Languages	SQL, DAX
🔄 CI/CD Deployment

A CI/CD pipeline was implemented for seamless deployment across environments:

Development: Feature design, data validation, and local report testing.

UAT: User acceptance and functionality verification.

Production: Live environment deployment after automated validation.

Pipeline Features:

Version-controlled Power BI and SQL artifacts.

Automated build and deployment via YAML pipelines.

Environment variables for dynamic database and connection string mapping.

This ensured consistent releases, faster testing cycles, and minimal downtime during updates.

🚀 Outcomes & Impact

✅ Automated submission and identifier tracking
🕒 Reduced manual tracking time via centralized reports
🎯 Quick anomaly detection through visual indicators
⚙️ Multi-environment dynamic configuration
💡 Improved auditability, compliance, and operational oversight



