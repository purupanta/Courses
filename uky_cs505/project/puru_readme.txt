# README for "SQLiteToMySQL.ipynb"
-----------------------------------

## Overview
This notebook, "SQLiteToMySQL", is designed to facilitate the conversion of SQLite
database files (.db) into MySQL-compatible SQL files (.sql). While SQLite is a popular
choice for local databases, MySQL is often preferred for larger-scale applications. This
tool enables users to seamlessly migrate data and schema structures from SQLite to MySQL.

## Input
The notebook requires a list of SQLite database files (.db) as input. For our purpose we
are includeing: TPCH-3K.db, TPCH-6K.db, TPCH-12K.db, TPCH-120K.db. SQLite databases are
characterized by their .db extension and are supported by SQLite and similar database
systems, but not directly supported by MySQL.

## Purpose
MySQL does not natively support .db files. Hence, this program converts SQLite .db files
into .sql files, which contain SQL commands representing the database schema and data.
These generated SQL files can then be easily imported into MySQL, allowing users to
replicate the database structure and import datasets seamlessly.

## How to Run
1. Install anaconda from https://www.anaconda.com/download/success
2. Open anaconda navigator and jupyter notebook.
3. Open SQLiteToMySQL.ipynb in jupyter notebook.
4. Adjust the directory configurations and the ".db" files location in the main block of the
   python file, '__main__'
5. Executing this python script creates converted .sql files for each of the .dbo file, which
   can then simply run in MySQL to create schema and insert datasets.

## Data Mapping
When converting datatypes from .db files to the corresponding MySQL datatypes the following 
mapping is used:
- 'TEXT': 'TEXT'
- 'INTEGER': 'INT'
- 'REAL': 'DOUBLE'
- 'BLOB': 'LONGBLOB'
- 'NULL': 'NULL'
- 'NUM' : 'DATE'

========================================================================================================================================================================

# README for "tpch_benchmark.ipynb"
-----------------------------------

#Input
The following MySQL databases: 'cs505_prj_tpch_3k', 'cs505_prj_tpch_12k', 'cs505_prj_tpch_60k', 'cs505_prj_tpch_120k'.
the TPC-H query1 through query 22 were stored in MySQL as procedure view in the previous step.

# Prerequsites
install library "mysql-connector-python" to establish MySQL conneciton through Python:
!pip install mysql-connector-python

# Purpose
The python script "tpch_benchmark.ipynb" is created to execute the 22 standard TPC-H queries stored in MySQL database as a stored-procedure-view
and measure the execution time and throughput for each of the queries ran over.

# How to execute the TPC-H benchmark queries:
the TPC-H query1 through query22 were stored in MySQL as procedure view. The python script "tpch_benchmark.ipynb" needs to be executed step-by-step in Anaconda python notebook
1. Install anaconda from https://www.anaconda.com/download/success
2. Open anaconda navigator and jupyter notebook.
3. Open tpch_benchmark.ipynb in jupyter notebook.
4. Adjust the database connectivity with "config" dictionary variable, having host, database username, port, password. In my case MySQL was set up in localhost.
   Once the conneciton is established, the query string builds up dynamically based on what TPC-H query we are executing.
5. The python timer measures the time and lets the query execute.
6. After the query executed, the timer measures the time in seconds again and calculates the time taken to execute the query as:
   Execution time = end_time - start_time
7. The "write_report" function writes the collected a report-tuple into csv file as output.
   the report_tuple is defined as dictionary and gets populated at each query completes execution:
   report_tuple = {
        'query_string': query_string,
        'start_time_s': '',
        'end_time_s': '',
        'execution_time_s': '',
        'throughput': ''
    }

========================================================================================================================================================================

CODE HELP REFERENCES:
-----------------------------------

1. https://github.com/Unity-Technologies/mysql-connector-python/blob/master/lib/mysql/connector/connection.py
2. https://gist.github.com/techouse/4deb94eee58a02d104c6?permalink_comment_id=4356734
3. https://github.com/majidalavizadeh/sqlite-to-mysql

