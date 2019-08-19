
# Data Modeling with Postgres Relational Database
In this project, I applied the concepts of data modelling with relational database Postgres and built an ETL pipeline using Python. I completed this project by defining fact and dimension tables for a star schema to handle specific analytical need and wrote an ETL pipeline that transfers data from JSON files in two local directories into tables in Postgres using Python and SQL.
## Requirement
A music app startup Sparkify needs to analyze the data it has been collecting on songs and user activity around listening those songs in their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to.
1.	The data related to user activity on the app resides in a directory of JSON log files.
2.	The metadata on the songs like title, artist name and length of the song resides in JSON files stored in separate directory.
## Data
Data set is a set of files in JSON format and contains two parts:
-	./data/song_data: static data about artists and songs
-	./data/log_data: event data of service usage e.g. who listened what song, when, where, and with which client

Below, some figures about the data set (results after running the etl.py):
-	./data/song_data: 71 files
-	./data/log_data: 30 files
-	songplays: 6820
-	(unique) user: 97
-	songs: 71
-	artists: 69

# Solution

## Prerequisites
Python3 is recommended as the environment. The most convenient way to install python is to use Anaconda (https://www.anaconda.com/distribution/) either via GUI or command line. Also, the following libraries are needed for the python environment to make Jupyter Notebook and Postgresql to work:
-	postgresql (+ dependencies) to enable sripts and Jupyter to connect to Postgresql DB.
-	jupyter (+ dependencies) to enable Jupyter Notebook.
-	ipython-sql (https://anaconda.org/conda-forge/ipython-sql) to make Jupyter Notebook and SQL queries to Postgresql work together. NOTE: you may need to install this library from command line.

# How to run
From the terminal with current directory set to project directory, run following command to complete initial setup by creates database and tables with appropriate schema in Postgres.
python create_tables.py  

Output: Script writes "Tables dropped successfully" and "Tables created successfully" if all tables were dropped and created without errors.

Run following command to execute python script that extract data related to songs and user activity logs from JSON files in data directory, does transformations and loads it into Postgres database for further analysis.
python etl.py  

Output: Script crawls through all the data directories, tells how many files it has to process, and writes to console the progress of the script as it processes them through. After successfully processing through a directory, script summarised the results:
-	"All xx files processed OK in aaa/abc123" (e.g. data/song_data) and
-	"All xx files processed OK in aaa/def456" (e.g. data/log_data).


# Database Schema
Following is ER Diagram that shows the star schema used to organize the data in different tables.

# Code organisation
The ETL code is modularised into separate files.
-	sql_queries.py contains SQL query statements for creating new tables with appropriate schema, inserting data into tables.
-	create_tables.py contains code for initial setup by creating database in Postgres and creating tables if not already present.
-	etl.py contains code for extracting data of songs and user activity from JSON files, doing necessary transformations on data and loading them into Postgres.
-	etl.ipynb is a Jupyter notebook that is helpful for developing, debugging and showcasing the unit code used for processing small amount of data related to songs and user activity.
-	test.ipynb is a Jupyter notebook which comes handy to check the initial few rows of each of the database tables, which are supposed to be loaded as part of this ETL task.
-	data is a directory of files containing metadata related to songs and logs of user activity in JSON format.


