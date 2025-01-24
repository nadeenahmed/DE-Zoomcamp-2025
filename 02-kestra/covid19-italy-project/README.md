# COVID-19 Italy Data Ingestion with Kestra
This project is part of the Data Engineering Zoomcamp by DataTalksClub. It focuses on workflow orchestration using Kestra, an open-source tool for building, scheduling, and monitoring workflows. The goal of this project is to ingest COVID-19 data for Italy into a PostgreSQL database using Kestra.

# Table of Contents
1. [Project Overview](#overview)
2. [Dataset](#dataset)
3. [Workflow Steps](#steps)
4. [Tools and Technologies](#tools)

---

## 📋 Project Overview <a name="overview"></a>

To apply the concepts learned during the Zoomcamp, I worked with COVID-19 data for Italy, a publicly available dataset that provides detailed information about cases, recoveries, and hospitalizations at both the province and region levels. 


The data was extracted from a [GitHub repository](https://github.com/RamiKrispin/covid19Italy/tree/master/csv) and ingested into a PostgreSQL database using Kestra workflows defined in YAML.


## 📂 Dataset <a name="dataset"></a>
The dataset used in this project is COVID-19 data for Italy, which includes:

- `italy_province`: daily summary of the outbreak on the region level
- `italy_province`: daily summary of the outbreak on the province level
  
The italy_region dataset provides an overall summary of the cases in Italy’s regions. The dataset contains the following fields:

- `date` - timestamp, a Date object
- `region_code` - the region code
- `region_name` - the region name
- `lat` - region latitude coordinate
- `long` - region longitude coordinate
- `hospitalized_with_symptoms` - daily number of patients hospitalized with symptoms
- `intensive_care` - daily number of patients on intensive care
- `total_hospitalized` - daily total number of patients hospitalized (hospitalized_with_symptoms + intensive_care)
- `home_confinement` - daily number of people under home confinement
- `cumulative_positive_cases` - a daily snapshot of the number of positive cases
- `daily_positive_cases` - daily new positive cases
- `daily_cases` - daily new positive, recovered, and death cases
- `recovered` - total number of recovered cases (cumulative)
- `death` - total number of death cases (cumulative)
- `cumulative_cases` - total number of positive cases, recovered, and death (cumulative)
- `total_tests` - total number of tests performed (cumulative)
- `region_spatial` - the spatial region names as in the output of the ne_states function from the rnaturalearth package

The italy_province dataset provides an overall summary of the cases in Italy’s regions. The dataset contains the following fields:

- `date` - timestamp, a Date object
- `region_code` - the region code
- `region_name` - the region name
- `province_code` - the province code
- `province_name` - the province name
- `province_abb` - the province abbreviation
- `lat` - province latitude coordinate
- `long` - province longitude coordinate
- `total_cases` - total number of positive cases (cumulative)
- `new_tests` - daily number of positive cases
- `province_spatial` - the spatial province names as in the output of the ne_states function from the rnaturalearth package

## 🚀 Workflow Steps <a name="steps"></a>
The workflow consists of the following steps:

1. Extract Data: Download the CSV files (italy_province.csv and italy_region.csv) from the GitHub repository.

2. Transform Data: Clean and preprocess the data (e.g., replace "NA" values with "0").

3. Load Data: Ingest the cleaned data into PostgreSQL tables (italy_province and italy_region).

4. Merge Data: Use SQL queries to merge data from staging tables into the main tables.

## 🛠️ Tools and Technologies <a name="tools"></a>

- `Kestra`: Workflow orchestration and scheduling.

- `PostgreSQL`: Database for storing the COVID-19 data.

- `YAML`: Used to define Kestra workflows.

- `Shell Scripting`: For data extraction and transformation.

- `Docker`: Used to containerize and set up Kestra and PostgreSQL for seamless deployment.

Feel free to explore the project and reach out if you have any questions or feedback! 😊
