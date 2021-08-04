# Project Data Warehouse

## Project Overview
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

In this project, we will create an ETL pipeline to build a data warehouses hosted on Amazon AWS Redshift.


## Datasets

Datasets used in this project are provided in two public S3 buckets. One bucket contains info about songs and artists, the second bucket has info concerning actions done by users (which song are listening, etc.. ). The objects contained in both buckets are JSON files.

The Redshift service is where data will be ingested and transformed, in fact though COPY command we will access to the JSON files inside the buckets and copy their content on our staging tables.

## Schema for Song Play Analysis

#### Fact Table
songplays - records in event data associated with song plays. Columns for the table:

    songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### Dimension Tables 
##### users

    user_id, first_name, last_name, gender, level
##### songs

    song_id, title, artist_id, year, duration

##### artists

    artist_id, name, location, lattitude, longitude

##### time

    start_time, hour, day, week, month, year, weekday



#### Setup Configurations 
Setup the dwh.cfg file (File excluded by .gitignore). File format for **dwh.cfg**

```
[CLUSTER]
HOST=''
DB_NAME=''
DB_USER=''
DB_PASSWORD=''
DB_PORT=5439

[IAM_ROLE]
ARN=<IAM Role arn>

[S3]
LOG_DATA='s3://udacity-dend/log_data'
LOG_JSONPATH='s3://udacity-dend/log_json_path.json'
SONG_DATA='s3://udacity-dend/song_data'

```

### Create tables

    $ python create_tables.py

### Load Data

    $ python etl.py


Starter Template by [Udacity](https://www.udacity.com/course/data-engineer-nanodegree--nd027)

Reference: [AWS Redshift Doc](https://aws.amazon.com/redshift/getting-started/?p=rs&bttn=hero&exp=b)