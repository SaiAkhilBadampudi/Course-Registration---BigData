# 📚 Curricular Data Analytics for the iSchool

## Project Overview

This project is a final exam for IST 469/769, designed to test distributed data processing and analytics skills. The goal is to analyze course registration and curricular data from the iSchool's student enrollment system. The project focuses on deriving meaningful insights and relationships within the data, particularly for the **Applied Data Science (ADS)** and **Information Systems (IS)** programs.

The project requires a multi-faceted approach, utilizing various distributed technologies to prepare, store, and analyze data for different purposes, including both structured and graph-based analysis.

## ⚙️ Technical Environment

The entire project is run within a `docker-compose` environment, which provisions a suite of connected services for a comprehensive data pipeline:

* **`mongodb`**: A database storing course, program, and student reference data.
* **`minio`**: An S3-compatible object store containing student enrollment data (`sections.csv`, `enrollments.csv`).
* **`cassandra`**: A distributed NoSQL database for storing wide, denormalized data.
* **`elasticsearch`**: A search and analytics engine for full-text search and dashboarding.
* **`neo4j`**: A graph database for analyzing relationships between courses and programs.
* **`kibana`**: A data visualization and dashboarding tool that connects to Elasticsearch.
* **`jupyter`**: A Jupyter Lab instance for running PySpark code.

## 📈 Data Pipeline & Analytics

The project follows a multi-stage data pipeline to achieve its analytical goals:

### Data Ingestion and Preparation
* Data from `mongodb` and `minio` is ingested into a Spark environment.
* Raw data is transformed and denormalized into "wide tables" suitable for loading into `cassandra` and `elasticsearch`.
* Data is loaded into `cassandra` with a well-designed key schema to support fast lookups.
* Data is loaded into `elasticsearch` and configured for visualization in Kibana.
* Program and course data is loaded into `neo4j` to create a graph-based representation of the curriculum.

### Data Analysis and Visualization
* **Graph-based Analysis**: Cypher queries in `neo4j` are used to find relationships, such as courses required by both the IS and ADS programs.
* **Dashboarding**: Kibana is used to build two interactive dashboards:
    * **Student Dashboard**: Visualizes a student's program, GPA, and courses taken from the Elasticsearch `enrollments` index.
    * **Course Dashboard**: Displays course-related visualizations (e.g., enrollment-to-capacity ratios, course counts) from the Elasticsearch `sections` index, filtered by academic year.
* **Reporting**: Spark SQL and the DataFrame API are used to generate various data reports and summaries.

## 🎯 Key Achievements

* Demonstrated proficiency in connecting and integrating multiple distributed data systems.
* Performed complex data preparation and denormalization using PySpark.
* Implemented appropriate data models for different database types (Cassandra, Elasticsearch, Neo4j) to optimize for specific use cases.
* Used graph database queries (Cypher) to uncover hidden relationships in curricular data.
* Built interactive dashboards using Kibana to provide user-friendly insights for data analysts at the iSchool.

## 📦 Getting Started

To run this project, clone the repository and use `docker-compose` to start the environment:

```bash
# Clone the repository
git clone [https://github.com/mafudge/ist769sp24final.git](https://github.com/mafudge/ist769sp24final.git)
cd ist769sp24final

# Build and start the environment
docker-compose build
docker-compose up -d
