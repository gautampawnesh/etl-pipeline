## Dataset Overview

Sparkify is a music streaming startup with an objective to provide a personalized and engaging music streaming experience to users, leveraging data analytics to enhance content recommendations, user segmentation, and overall customer satisfaction. 

The dataset includes user demographics, events info, songs details in the form of JSON. This is splited into events and songs data.

The goal of the company is to use these user behavioural data and songs data for the analytical purpose. The analytical business goal can be recommendations engines, user segmentation and improving user experience with the music.

## Database Schema 
Inorder to convert the OLTP data to OLAP, star schema strategy is used in this solution. The dataset is divided into fact tables like songplay, user, artist, song etc. Then the dataset from the s3 is copied to staging tables on redshift. Then the fact tables are loaded with necessary data from staging tables using INSERT operations. 

In order to further improve the query performance, the distribution strategies are used like 'All' for 'artist' and 'user' tables and key-based distribution strategies for 'time' and 'song' tables. 

## ETL Pipeline

1. Extraction: The data extraction phase occurs in the `load_staging_tables` function.
Which reads SQL queries from the `copy_table_queries` list, which contain COPY commands to extract data from files stored in Amazon S3 buckets into staging tables in Amazon Redshift.

2. Transformation: The tranformations are included in the INSERT command.

3. Loading: Data loading occurs in the `insert_tables` function.

## Example Queries

1. Aggregation based queries such as:
SELECT COUNT(DISTINCT user_id) AS total_users
FROM users; --> 96

2. Top Users based on number of songs listened:
SELECT u.first_name || ' ' || u.last_name AS user_name,
       COUNT(*) AS songs_played
FROM songplays sp
JOIN users u ON sp.user_id = u.user_id
GROUP BY user_name
ORDER BY songs_played DESC
LIMIT 10;

Output:
Chloe Cuevas	42
Kate Harrell	32

