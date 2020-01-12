Project 3: Song Play Analysis With S3 and Redshift

Objectives:

1) Load the data from S3 bucket by using AWS redshift
The Redshift service is where data will be ingested and transformed,
in fact though COPY command we will access to the JSON files inside
the buckets and copy their content on our staging tables
2) Perform ETL process
In this project most of ETL is done with SQL (Python used just as bridge), transformation and data normalization is done by Query, check out the sql_queries python module

Methodology:
1) Connect to AWS and acquire the ARN & Host name by running IaC.ipynb
2) Run create_tables.py
3) Run etl.py

The design of the schema is shown in (Project 3 schema.png), where it shows a fact table connected to 4 dimension tables as a star
schema with 2 staging tables. 

The songplays table is the core of this schema, is it our fact table and
it contains foreign keys to four tables;

start_time REFERENCES time(start_time)
user_id REFERENCES time(start_time)
song_id REFERENCES songs(song_id)
artist_id REFERENCES artists(artist_id)
There are also two staging tables; One for song dataset and one for
and one for event dataset


Project files:

create_tables.py - This script will drop old tables (if exist) ad re-create new tables
etl.py - This script executes the queries that extract JSON data from the S3 bucket and ingest them to Redshift
sql_queries.py - This file contains variables with SQL statement in String formats, partitioned by CREATE, DROP, COPY and INSERT statements
dhw.cfg - Configuration file used that contains info about Redshift, IAM and S3
