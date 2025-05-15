# airflow-dbt-cubejs-powerbi-postgres

This repository demonstrates a complete end-to-end analytical pipeline using Apache Airflow for orchestration, dbt for data transformation, Cube.js for semantic modeling, and Power BI for visualization, all leveraging a PostgreSQL database.

## Overview

This project provides a practical example of how to integrate these powerful tools to build a robust and scalable data analytics workflow. It includes:

* **Airflow DAGs:** Defining the workflow for orchestrating dbt runs, Cube.js data model deployments/refreshes, and potentially data loading tasks.
* **dbt Project:** Demonstrating data transformations within PostgreSQL using dbt models.
* **Cube.js Schema:** Defining a semantic layer on top of the transformed data for efficient querying and analysis.
* **Configuration Examples:** Providing guidance on connecting each component (Airflow, dbt, Cube.js) to the PostgreSQL database.
* **Power BI Guidance:** Offering insights on connecting Power BI to Cube.js for data visualization.

## Architecture

```mermaid
graph LR
    A[PostgreSQL Database] --> B(dbt);
    B --> C(Cube.js);
    C --> D(Power BI);
    E[Airflow] --> B;
    E --> C;
    subgraph Data Pipeline
        direction LR
        B -- Transforms Data --> C
    end
    subgraph Orchestration
        direction LR
        E -- Triggers & Monitors --> B
        E -- Triggers & Monitors --> C
    end