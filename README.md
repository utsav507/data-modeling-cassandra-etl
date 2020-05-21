# Sparkify Cassandra ETL

This project consists on putting into practice the following concepts:
- Data modeling with Cassandra
- ETL pipeline using Python

## Context

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

They'd like a data engineer to create an Apache Cassandra database which can create queries on song play data to answer the questions, and wish to bring you on the project. Your role is to create a database for this analysis. You'll be able to test your database by running queries given to you by the analytics team from Sparkify to create the results.

In this project, I will model the data by creating tables in Apache Cassandra to run queries.

### Data
- **event datasets**: all csv files are in subdirectory under */event_data/. 

Example file path:

event_data/2018-11-08-events.csv
event_data/2018-11-09-events.csv


## Keyspaces
There are 3 keyspaces created in this project (session_songs, user_history, user_songs).

On why to use a relational database for this case:
- The data types are structured (we know before-hand the sctructure of the jsons we need to analyze, and where and how to extract and transform each field)
- The amount of data we need to analyze is not big enough to require big data related solutions.
- Ability to use SQL that is more than enough for this kind of analysis
- Data needed to answer business questions can be modeled using simple ERD models
- We need to use JOINS for this scenario

#### Keyspaces
**session_songs** - give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
- sessionid     int
- iteminsession int
- artist        text
- song_length   float
- song_title    text
- primary key (sessionid, iteminsession)

**user_history** - give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
- song_title text,
- userid     int,
- firstname  text,
- lastname   text,
- primary key (song_title, userid)

**user_songs** - give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
- userid     int,
- sessionid  int,
- artist     text,
- firstname  text,
- lastname   text,
- song_title text,
- primary key (userid, sessionid)



## Project structure

Files used on the project:
1. **event_data** folder at home of the project, where all needed csv files reside.
2. **event_datafile_new** contains results of new compiled events from etl pipeline.
3. **etl-pipeline-cassandra.ipynb** creates etl pipeline in apache cassandra.
4. **README.md** current file, provides discussion on my project.

### Break down of steps followed

##### Project Steps

1. Modeling your NoSQL database or Apache Cassandra database
2. Design tables to answer the queries outlined in the project template
3. Write Apache Cassandra CREATE KEYSPACE and SET KEYSPACE statements
4. Develop your CREATE statement for each of the tables to address each question
5. Load the data with INSERT statement for each of the tables
6. Include IF NOT EXISTS clauses in your CREATE statements to create tables only if the tables do not already exist. We recommend you also include DROP TABLE statement for each table, 7. this way you can run drop and create tables whenever you want to reset your database and test your ETL pipeline
8. Test by running the proper select statements with the correct WHERE clause

#### Build ETL Pipeline
1. Implement the logic in section Part I of the notebook to iterate through each event file in event_data to process and create a new CSV file in Python
2. Make necessary edits to Part II of the notebook to include Apache Cassandra CREATE and INSERT statements to load processed records into relevant tables in your data model
3. Test by running SELECT statements after running the queries on your database

## ETL pipeline

Prerequisites: 
1. Start Cassandra service if installed locally on Mac by going to Terminal
2. Run following cmd on terminal: brew services start cassandra

## Authors

* **Utsav Shah** - [Github](https://github.com/utsav507)