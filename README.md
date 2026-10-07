# Timesheets Data Warehouse

An Oracle-based data warehousing project for integrating and analyzing employee timesheet, absence, and work schedule data. The project implements an ETL workflow, organizes the data into a dimensional model, and provides SQL reports for daily and monthly activity analysis.

## Project Overview

Organizations often store employee schedules, timesheets, and absences in separate operational datasets. This project brings those records together in a data warehouse so that employee activity can be analyzed over time.

The solution separates data processing into three layers:

- **Source** — original operational data.
- **Staging** — an intermediate area where data is prepared for loading.
- **Target** — the data warehouse, organized for reporting and analysis.

After the data is loaded, SQL queries can summarize activity by date and other descriptive attributes.

## Project Objectives

The project demonstrates how to:

- Design an ETL process using Oracle SQL.
- Separate source, staging, and target data.
- Build a dimensional model using a star schema.
- Store activity records in a central fact table.
- Connect fact data to descriptive dimensions using primary and foreign keys.
- Record load information for auditing.
- Create SQL reports using joins, grouping, and analytic functions.
- Improve query access with indexes, views, and a materialized view.
- Work with a semi-structured data column using JSON or XML.

## ETL Process

The ETL workflow consists of three stages.

### 1. Extract

Data is collected from the operational source tables, including timesheet, absence, and employee schedule information.

### 2. Transform

The extracted data is prepared in the staging layer. This step supports data organization and validation before the records are loaded into the warehouse.

### 3. Load

Prepared records are inserted into the target dimensions and the `FACT_ACTIVITY` table. Load information is recorded in `AUDIT_LOAD` to support traceability.

```text
Source Data
    ↓
Staging Layer
    ↓
Dimensions and FACT_ACTIVITY
    ↓
Daily and Monthly Reports
```

## Data Warehouse Model

The warehouse uses a **star schema**. The central fact table stores activity records, while dimension tables provide descriptive information for analysis.

### Fact table

- **`FACT_ACTIVITY`** — stores employee activity records and references the relevant dimension records through foreign keys.

### Dimension tables

Dimension tables store descriptive context for the activity records, such as information related to dates, employees, or activity types.

### Audit table

- **`AUDIT_LOAD`** — stores information about ETL loads and helps track when data was processed.

The primary keys uniquely identify records in each table. Foreign keys connect the fact table to its dimensions and help maintain referential integrity.

## Project Data

The project was tested with the following record counts:

| Dataset or table | Record count |
|---|---:|
| Timesheets | 3,050 |
| Absences | 63 |
| Source employee schedule | 80 |
| Staging employee schedule | 4,800 |
| Total fact records | 3,113 |

These counts can be used when running validation queries to compare the source, staging, and target layers.

## SQL Features

The project demonstrates several Oracle SQL and database concepts:

- **Constraints** to define data integrity rules.
- **Primary keys** to uniquely identify table records.
- **Foreign keys** to connect the fact table and dimensions.
- **Indexes** on selected columns to support query performance.
- A **semi-structured column** for JSON or XML data.
- A **view** for presenting reusable query results.
- A **materialized view** for storing precomputed results.
- `GROUP BY` for summarizing activity.
- `LEFT JOIN` for retaining records from the main table when related data is missing.
- An analytic function for calculations across related rows.
- `AUDIT_LOAD` for recording ETL load information.

## Reports

The reporting queries support analysis of employee activity across different time periods.

### Daily report

Groups activity by date and displays daily totals. This report can help identify how activity is distributed across working days.

### Monthly report

Groups activity by year and month. This report provides a higher-level view of activity over time.

### Activity analysis

Uses joins between the fact table and dimension tables to display activity together with descriptive information. Aggregations can then be applied to compare activity across dates or categories.

## Validation

Validation queries are used to check the data at different stages of the ETL process. They can help confirm that:

- Source records were copied into staging as expected.
- Records were loaded into the target tables.
- Fact records reference valid dimension records.
- The total number of loaded activity records matches the expected result.

## Technologies

- **Database:** Oracle Database
- **Language:** SQL
- **Data warehousing approach:** ETL
- **Dimensional model:** Star schema

## Running the Project

1. Open Oracle SQL Developer or another Oracle SQL client.
2. Connect to an Oracle database using a user with permission to create tables, views, indexes, and other database objects.
3. Run the SQL scripts from the repository in dependency order:
   - Create the source and staging objects.
   - Create the target dimensions, fact table, and audit table.
   - Load and transform the data.
   - Create indexes, views, and the materialized view.
   - Run the reporting and validation queries.
4. Review the query results and compare the record counts across the source, staging, and target layers.

> Run the scripts in the order provided by the project. Some scripts depend on tables or other objects created earlier.

## Project Structure

The repository contains the SQL scripts used to create and populate the database, together with the queries used for reporting and validation.

```text
ETL-Project/
├── SQL scripts for source and staging data
├── SQL scripts for dimensions and fact tables
├── ETL and data loading scripts
├── Reporting queries
└── Validation queries
```

## Project Purpose

This project was developed as a practical exercise in database design and data warehousing. It combines relational database concepts with an ETL workflow and a dimensional model to make timesheet and absence data easier to analyze.

## Author

**Cristina Fatan**
