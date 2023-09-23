# data-roles-analysis-23-24
A data analysis project on the most valued analysis tools and qualifications to land data analysis job roles for 2023–2024 in the United Kingdom. It is intended for those in need of self-development and a job in the field of data analytics, such as myself. The project utilizes the Ask, Prepare, Process, Analyze, Share, and Act frameworks using Excel, SQL, and Tableau. The primary Excel dataset consists of live 2023–2024 data analysis job roles with statistics about the companies, their offerings, skill requirements, and qualifications needed for the roles. The data cleaning and analysis steps were done using SQL. The visualizations were created using Tableau.

The steps and outline are inspired by the Google Data Analytics Capstone Project published by <ins>[Medium]( https://medium.com/analytics-vidhya/this-case-study-is-for-google-data-analytics-gda-capstone-project-course-54047cccf7cb)</ins>

## 1 Ask
During this phase, we establish the problem, outline the goals of our case study, and demonstrate the anticipated results.
### 1.1 Background
Research has been conducted on skills needed for data analysis roles in particular, and the Google Data Analytics Course has prioritized certain tools for the field. Results articulate that SQL, R, Python, Tableau, PowerBI, and Excel are the most valued tools in the data industry.

I believe analyzing job requirements and ranking skills and tools by value can be a great starting point for those in need of self-development in the field of data analytics, especially fresh graduates like myself.
### 1.2 Case Study Task
Conduct a data analysis on 2023–2024 job listings in the data analytics domain to identify and rank the most essential analysis tools and skills sought by employers. Summarize patterns and correlations to guide individuals in self-development for successful career opportunities in data analytics.
### 1.3 Objectives
- What are some available 2023–2024 data analytics roles in the UK?
- What tools are most valued by employers?
- What are the most common qualification requirements?
### 1.4 Deliverables
- A clear summary of the business task
- A description of all data sources used
- Documentation of any cleaning or manipulation of data
- A summary of analysis conducted using SQL queries
- Supporting visualizations and key findings created using Tableau
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
- 61 roles were collected between September 13 and September 16, 2023.
- Attributes include company, number of employees, type of role, salary, qualifications and skill requirements.
- Not all attributes will be analyzed, but were included since they are a great source of reference for job surfing. 
### 2.2 Limitations
- Data includes several null values that are uncontrollable due to all job listing having inconsistencies.
- The number of roles collected are less than a 100 since roles are limited at the time.
- Roles are bound to expire at unexpected times since most deadlines are "rolling".
- Some other useful analysis tools will not be collected nor covered in the analysis.
### 2.3 Is data ROCCC?
ROCCC stands for Reliable, Original, Comprehensive, Current and Cited. It is used as a measurement for good data.
- Reliable: Medium/Low - 61 roles can be considered an adequate population.
- Original: High - Primary data collected manually from several job portals.
- Comprehensive: High - Data is very useful towards case study question
- Current: High - Data is for 2023/2024
- Cited: Medium - Data is primary; however, research was conducted over several portals that were not mentioned in the data set since the roles are presented in several websites.

The dataset is of adequate quality overall. Good conclusions can be drawn based on the information collected.

### 2.4 Dataset Used
```bash
data_roles_project.csv
```
Note: Tableau was spelled incorrectly. (Tableu-*Tableau)
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
### 3.1 Formatting Data Before Importing
Most columns such as salary, tools and more were formatted in Excel to the correct data types to be acknowledged by SQL.
### 3.2 Importing the Dataset
The Excel file was saved as a CSV file to be imported into SQL.

Creating dataset within a project (infinite-deck-395615), dataset ID:
```bash
infinite-deck-395615.data_roles_23_24
```

Creating table included within the project and datset, table ID:
```bash
infinite-deck-395615.data_roles_23_24
```
### 3.3 Previewing Table
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

### 3.4 Cleaning the Data
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
### 3.5 Null Values
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/43cc3ac2-b9e5-4b17-a1db-b3def9480df0)

The dataset includes null values that cannot be deleted. These null values are just some inconsistencies in job descriptions that can be ignored. However, the jobs that do include data in such attributes can provide useful information for analyzing the details of data analyst roles.

## 4 Analysis
Performing analysis to obtain:
- Number of times each skill was mentioned for a role
- Percentage of roles that require university degrees
- Percentage of roles that require a STEM degree if a degree is required

### 4.1 Skill Counter
```bash
--creating a table for counting the number of times each skill or tool appeared in role requirements

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

A table was created for future visualizations. Cases were used to identify which of the following tools appear to be 'true' or '1' from the dataset. meaning they appeared in a job description.

The final table:

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/76aa738c-14b0-4f89-9f0e-ddcfac774ac7)

The analysis tells us from our limited sources that SQL appeared to be the most demanded data analytics tool. The rankings of all the tools out of 61 roles were:
- SQL-43
- Excel-38
- Python-35
- PowerBI-26
- R-18
- Tableu-15

A larger population of data will make this discovery more reliable. However, it can still be a reference for starters in need of learning skills to enter the field.

### 4.2 Degree Percentage
Analyzing the percentage of jobs that require a minimum bachelor's degree and if the degree is STEM

```bash
CREATE TABLE infinite-deck-395615.data_roles_23_24.degree_percentage AS
SELECT
--percentage of jobs that need Bachelors, rounded to nearest integer
ROUND(SUM(CASE WHEN MinimumQualification="Bachelors" THEN 1 ELSE 0 END)/COUNT(Company)*100, 0)AS degree_percentage,
No degree percentage rounded to nearest integer
ROUND(SUM(CASE WHEN MinimumQualification="Bachelors" THEN 0 ELSE 1 END)/COUNT(Company)*100, 0)AS no_degree_percentage,
--percentage of STEM degrees for jobs that need Bachelors, rounded to nearest integer
ROUND(SUM(CASE WHEN Degree="STEM" THEN 1 ELSE 0 END)/SUM(CASE WHEN MinimumQualification="Bachelors" THEN 1 ELSE 0 END)*100,0) AS STEM_percentage

FROM `infinite-deck-395615.data_roles_23_24.data_roles_uk`
```

The same method of locating which data falls true applies for this analysis.  A table was created for future reference.

Final table:

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/cfba7613-85a7-40a0-a718-7db9df2ceb44)

The table explains that more than half of the roles require a minimum qualification of a bachelor's degree, and 64 percent of those roles require a STEM degree.

## 5 Share
In this step, visualizations are created and published using Tableau Public.

### 5.1 Skill Chart
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/9ce10d56-578e-4fc2-adf8-d9db442b787d)

The above image is a bar chart arranged in descending order to indicate which skills are the most demanded. The simplicity and comprehensiveness are the reasons this type of chart was chosen. This chart visualizes the previous findings of the rankings of tools in a more visually appealing and understandable way. As mentioned previously,
- SQL is evidently the most popular tool for data analytics. This could be due to its reputation for high speed and efficiency with huge amounts of data compared to other query languages. SQL is also simple, with a user-friendly and easily understandable syntax.
- Excel came in second as the most popular spreadsheet tool. Most Microsoft appliances tend to be popularized in the work industry due to their reputation for success.
- Python came in third place over R as the most demanded programming language. Python has a very simple syntax, which makes it an easy language to learn.
- Finally, PowerBI came in fourth place, making it the more popular BI tool over Tableau. This leads back to the point about Microsoft, a very reliable source for applications.

<ins>[Link to chart](https://public.tableau.com/views/DataRolesStats/Sheet1?:language=en-US&:display_count=n&:origin=viz_share_link)</ins>

### 5.2 Degree Chart
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/f7bf1346-6dac-4258-91f3-600ec895c0dc)
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/3b007984-5518-4926-8efc-49bfd34aacc1)

A pie chart was generated for this condition, as it is the best for percentage comparisons. The data was converted into a percentage after importing the dataset to Tableau Public since it's default data type is a float. As explained before, a bit more than half of the jobs require a bachelor's degree. 
- 53% of roles require a minimum of a bachelor's degree
- 47% do not require a degree

<ins>[Link to chart](https://public.tableau.com/views/DegreeChart/Sheet1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)</ins>

### 5.3 STEM Chart
Most of the jobs that require bachelor's degrees specifically ask for a STEM specification.

![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/ac4df88e-247a-4eac-adc6-0fcb5bad9f6c)
![image](https://github.com/joeykhouryy/data-roles-analysis-23-24/assets/144739073/54b6f8e3-3fba-4656-a62e-bac304f988a7)

- 64% of roles that require a degree ask for STEM specifically. STEM degrees provide a very relevant skillset to the field of data. Mathematics, statistics, and programming are examples of courses such degrees provide. This may give employees a head start when attempting to learn the data analytics tools the company may provide.
36% accept anything else

<ins>[Link to chart](https://public.tableau.com/views/STEMChart/Sheet1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)</ins>

## 6 Act
This section involves recommendations based on the analysis.
### 6.1 Which tool should upcoming data analysts prioritize?
One of the main points of this project was to determine which data analytics tool is most demanded by employers. The analysis shows that SQL is a widely recognized tool by several companies and should almost be treated like an obligatory skill to learn when entering the field of data. However, most of the other tools did receive a lot of numbers as well. Meaning, prioritization is key in such a situation. This can be used as a reference for which tools to learn first, depending on how important they are to employers. The main question is why certain tools are required more than others. Every tool has its advantages and disadvantages for companies. Factors like the type of data being processed and the size. The five known characteristics of big data, known as the 5 V's (velocity, volume, value, variety, and veracity), can be a method of determining the size of the data to know which tool to use. Some companies require spreadsheet skills at most for data analyst roles involving smaller datasets. Whereas, other roles may require the use of structured query languages that efficiently deal with larger amounts of data, such as SQL. The role itself can also be a factor in determining which tool to learn. If the job seeker is more into the artistic and creative side of data, then data visualization tools can be a proirity, as some firms have roles specifically for visualizations. If the job seeker is more into programming, then according to the bar chart in Section 5.1, Python is a popular and reliable choice to go for. The analysis in Section 5.1 also states that Microsoft applications tend to be in higher demand than others due to their reputation for reliability and success. Therefore, the job seeker can look into learning all the useful Microsoft tools for data analytics as a start.
### 6.2 Does a bachelor's degree increase the chances of securing a data role?
According to Section 5.2, the chart indicates that a bit more than half the roles require a degree. Meaning that a degree is more of a recommendation than a requirement. The field of data analytics can be a competitive space. The higher the qualification, the higher the chance of being recognized by employers. This can be a great addition to a portfolio, aside from the data tools mentioned previously. Section 5.3 also states that jobs that ask for degrees usually ask for a STEM specification (63% of the jobs that require degrees).










