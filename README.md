# data-roles-analysis-23-24
A data analysis project on the most valued analysis tools and skills to land data analysis job roles for 2023/2024 in the United Kingdom. It is intended for those in need of self-development and a job in the field of data analytics, such as myself. The project utilizes the Ask, Prepare, Process, Analyze, Share and Act framework using Excel, SQL and Tableu. The primary Excel dataset consists of live 2023/2024 data analysis job roles with stats about the companies, their offerings, skill requirements and qualifications needed for the roles. The data cleaning and analysis steps were done using SQL. The visualizations were created using Tableu.

Steps and outline are inspired by the Google Data Analytics Capstone Project published by medium.com.

## 1 Ask
During this phase, we establish the problem, outline the goals of our case study, and demonstrate the anticipated results.
### 1.1 Background
Research has been conducted on skills needed for data analysis roles in particular and the Google Data Analytics Course has prioritized certain tools for the field. Results articulate that SQL, R, Python, Tableu, PowerBI, and Excel are the most valued tools in the data industry.

I believe analyzing job requirements and ranking skills/tools by value can be a great starting point for those in need of self-development in the field of data analytics, especially fresh graduates like myself.
### 1.2 Case Study Task
Conduct a data analysis on 2023/2024 job listings in the data analytics domain to identify and rank the most essential analysis tools and skills sought by employers. Summarize patterns and correlations to guide individuals in self-development for successful career opportunities in data analytics.
### 1.3 Objectives
- What are some available 2023/2024 data anlaysis roles in the UK?
- What tools are most valued by employers?
- What are the most common qualification requirements?
### 1.4 Deliverables
- A clear summary of the business task
- A description of all data sources used
- Documentation of any cleaning or manipulation of data
- A summary of analysis conducted using SQL queries
- Supporting visualizations and key findings created using Tableu
- High-level content recommendations based on the analysis
### 1.5 Audience
- People interested in the field of data analytics.
- People learning data analytics.
- Individuals searching for a job in the field.
- Employers looking to open a role in data analytics.

## 2 Prepare
### 2.1 Data Source
- Primary data collected from several trusted job portals.
- Stored in Microsoft Excel.
- 61 roles collected between 13 September 2023 to 16 September 2023.
- Attributes include company, number of employees, type of role, salary, qualifications and skill requirements.
- Not all attributes will be analyzed, but were included since they are a great source of reference for job surfing. 
### 2.2 Limitations
- Data includes several null values that are uncontrollable due to all job listing having inconsistencies.
- The number of roles collected are less than a 100 since roles are limited at the time.
- Roles are bound to expire at unexpected times since most deadlines are "rolling".
- Some other useful analysis tools will not be collected nor covered in the analysis.
### 2.3 Is data ROCCC?
ROCCC stands for Reliable, Original, Comprehensive, Current and Cited. It is used as a measurement for good data.
- Reliable: Medium - 61 roles can be considered an adequate population.
- Original: High - Primary data collected manually from several job portals.
- Comprehensive: High - Data is very useful towards case study question
- Current: High - Data is for 2023/2024
- Cited: Medium - Data is primary, however research was conducted over several portals that were not mentioned in the data set since the roles are presented in several websites.

The dataset is of adequate quality overall. Good conclusions can be made based the information collected.

### 2.4 Dataset Used
```bash
data_roles_project.csv
```
<ins>[Link to dataset](https://github.com/joeykhouryy/data-roles-analysis-23-24/blob/main/data_roles_project.csv)</ins>
### 2.5 Tool
Excel was used for data collection and cleaning / SQL (Google Big Query) for cleaning and analysis.

## 3 Process
This step revolves around validating, handling, sorting and cleaning the data.
- Format to correct data types.
- Importing the data to SQL.
- Observe data as a whole.
- Investigate for errors and useless information.
- Acknowledge null values
## 3.1 Formatting Data Before Importing
Most columns such as salary, tools and more were formatted in Excel to the correct data types to be acknowledged by SQL.
## 3.2 Importing the Dataset
The Excel file was saved as a CSV file to be imported into SQL.

Creating dataset within a project (infinite-deck-395615), dataset ID:
```bash
infinite-deck-395615.data_roles_23_24
```

Creating table included within the project and datset, table ID:
```bash
infinite-deck-395615.data_roles_23_24
```
# 3.3 Previewing Table
Previewing data
```bash
--preview data

SELECT * 
FROM infinite-deck-395615.data_roles_23_24.Data_roles_project_first
```

First few columns of preview

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/85c615ba-49c4-4c93-89bc-479d4bd53065)


Preview indicates that blank columns were generated automatically

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/0a89dce8-b476-4cee-9b31-451e12cf5803)

## 3.4 Cleaning the Data
Deleting automatically generated empty columns
```bash
--cleaning the data
--deleting blank columns 

ALTER TABLE data_roles_23_24.data_roles_uk
DROP COLUMN string_field_14,
DROP COLUMN string_field_15,
DROP COLUMN string_field_16
```

Renaming invalid column names
```bash
--renaming columns

ALTER TABLE infinite-deck-395615.data_roles_23_24.data_roles_uk RENAME COLUMN BachelorsDegree TO Degree;
ALTER TABLE infinite-deck-395615.data_roles_23_24.data_roles_uk RENAME COLUMN BachelorsGrade TO Grade;
```
## 3.5 Null Values
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/43cc3ac2-b9e5-4b17-a1db-b3def9480df0)

The dataset includes null values that cannot be deleted. These null values are just some inconsistencies in job descriptions that can be ignored. However, the jobs that do include data in such attributes, can provide useful information into analyzing the details of data analyst roles.

## 4 Analysis
Performing analysis to obtain:
- Number of times each skill was mentioned for a role
- Percentage of roles that require university degrees
- Percentage of roles that require a STEM degree if a degree is required

## 4.1 Skill Counter
```bash
--creating a table for counting the number of times each skill/tool appeared in role requirements

CREATE TABLE infinite-deck-395615.data_roles_23_24.skill_count AS
SELECT 
 
SUM(CASE WHEN SQL THEN 1 ELSE 0 END) AS sql_count,
SUM(CASE WHEN R THEN 1 ELSE 0 END) AS r_count,
SUM(CASE WHEN Python THEN 1 ELSE 0 END) AS python_count,
SUM(CASE WHEN Tableu THEN 1 ELSE 0 END) AS tableu_count,
SUM(CASE WHEN PowerBI THEN 1 ELSE 0 END) AS powerbi_count,
SUM(CASE WHEN Excel THEN 1 ELSE 0 END) AS excel_count,

FROM `infinite-deck-395615.data_roles_23_24.data_roles_uk`
```

A table was created for future visualizations. Cases were used to identify which of the following tools appear to be 'true' or '1' from the dataset. Meaning, they appeared in a job description.

The final table:

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/76aa738c-14b0-4f89-9f0e-ddcfac774ac7)

The analysis tells us from our limited sources, that SQL appeared to be the most demanded data analytics tool. The rankings of all the tools out of 61 roles were:
- SQL-43
- Excel-38
- Python-35
- PowerBI-26
- R-18
- Tableu-15

A bigger population of data will make this discovery more reliable. However, it can still be a reference for starters in need of learning skills to enter the field.



