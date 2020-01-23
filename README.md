# ETL-Project
Team Project: Extract – Transform – Load (ETL) Report

Team members: Dakota Mason, Regina Neitzey, Arjun Nanje Gowda, and Pete Broll

22 Jan 2020

**Overview:**

Team conducted an Extract – Transform – Load effort using United States Wildfire data and Global Temperature data as an example of data processing to support multivariate analysis. Due to the limited amount of time available for this project, the team focused on wildfire and monthly average temperature data for the US State of California (CA) as a proof of concept. The methods used could be applied to more detailed location and expanded weather data.

**Datasets and sources:**

The datasets and sources were both from Kaggle:

1. 1.88 Million US Wildfires: 24 years of geo-referenced wildfire records by Rachael Tatman. This is sqlite database. URL: [https://www.kaggle.com/rtatman/188-million-us-wildfires](https://www.kaggle.com/rtatman/188-million-us-wildfires)
2. California Temperature – based on R script extracting data from Climate Change: Earth Surface Temperature Data. This code extracts monthly average temperature from a global temperature csv data file. URL: [https://www.kaggle.com/theroffness/california-temperature/data](https://www.kaggle.com/theroffness/california-temperature/data)

**Data Wrangling:**

All code for processing of the data was written in a Jupyter Notebook. Data wrangling steps for the US Wildfire data involved:

1. Opened a connection to the sqlite database.
2. Created a new empty list to hold data.
3. Used a sql statement to pull all Wildfire data for California – append the data to the list.
4. Used Pandas to convert the list to a dataframe
5. Reviewed the data available and decided which columns to retain.
6. Used Pandas to generate a new dataframe with on the reduced number of data columns.
7. Modified the date information to create a &quot;year-month&quot; variable (YYYYMM) to the dataframe to ease link to monthly average temperature data.

Data wrangling for the monthly average temperature data involved:

1. Used Pandas to read the csv file into a dataframe.
2. Filtered the data to California only.
3. Filtered the data to eliminate weather data prior to 1992 (the start of the Wildfire data).
4. Modified the date information to create a &quot;year-month&quot; variable (YYYYMM) to the dataframe to ease link to Wildfire data.

**Schemata:**

The team decided to use a relational database, PostgreSQL, to load the Wildfire dataframe and Average Temperature dataframe following the general outline below as:

1. The database was created in PostgreSQL (external to the Jupyter Notebook).
2. The database was connected within the jupyter notebook.
3. Added a replace statement to remove tables – allows old tables to be removed if the code is rerun.
4. Two tables for the database (one for the Wildfire dataframe and one for the Average Monthly Temperature dataframe) were created from within the notebook.
5. Employed ALTERTABLE to change the dataframe dates (string) to type datetime.
6. Wrote a join statement within jupyter notebook to join tables on column variable &#39;dt&#39;. This a one-to-many join (Average Monthly Temperature [one] – to – Wildfires [many]).