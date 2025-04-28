******ETL Pipeline - S3, AWS Glue, IAM, Athena, Crawler, Database******
****Main Objective****
The goal of this project is to design a complete ETL (Extract, Transform, Load) pipeline using AWS services. Data present in the Staging layer will be moved to the Data Warehouse layer through AWS Glue. Once the Data Warehouse is populated, a new crawler will create a database and tables, and finally, we will query the data using AWS Athena.
The dataset used is the Spotify Database 2025.

**Step-by-Step Implementation**
**1. Created the S3 Bucket projects-spotify**

Inside the bucket, created two folders:

staging

datawarehouse

Uploaded three CSV files (album, artist, and track) into the staging folder.

**2. Used AWS Glue to Build the Visual ETL Pipeline**

Opened AWS Glue Studio.

Added three data sources:

album

artist

track

Specified the S3 paths for each data source (files located in the staging folder).

**3. Performed Data Transformation**

Inner Join between the album and artist datasets:

Join condition: album.artist_id = artist.id.

Right Join the result with the track dataset.

Drop Duplicate Fields:

After the joins, the id field appeared twice. Dropped the duplicate id field to clean the data.

**4. Specified the Destination**

Added a destination node.

Provided the S3 path for the datawarehouse folder in the projects-spotify bucket.

**5. Created an IAM Role with Required Permissions**

Permissions added:

AmazonS3FullAccess

CloudWatchLogsFullAccess

AWSGlueServiceRole

AWSGlueConsoleFullAccess

Assigned this IAM role to the Glue Job.

**6. Ran and Monitored the ETL Job**

Saved the pipeline and executed the job.

Upon successful execution:

Data was moved to the datawarehouse folder.

16 jobs were created automatically, each distributing data appropriately into subfolders.

**7. Created a Crawler in AWS Glue**

Opened AWS Glue > Crawlers.

Created a new crawler pointing to the datawarehouse S3 folder.

Set up a new database named spotify.

Selected this database in crawler options.

**8. Ran the Crawler**

Ran the crawler to crawl the datawarehouse data.

The crawler automatically created a new table based on the files.

**9. Set Up AWS Athena for Querying**

Opened AWS Athena.

Chose the spotify database.

Verified that the table (e.g., datawarehouse) with all the required columns was available.

**10. Created a New S3 Bucket for Athena Query Output**

Created a bucket named athena-output-spotify.

In Athena query editor, updated the query result location:

Go to Manage Settings > Set the S3 path to athena-output-spotify.

**11. Queried the Data Using Athena**
SELECT name FROM datawarehouse LIMIT 10;





The result was successfully displayed and stored in the athena-output-spotify bucket.

Summary
This project demonstrates a complete ETL pipeline setup using AWS services, from staging raw data in S3 to building a queryable data warehouse with Athena. It ensures efficient data movement, transformation, and accessibility for analytics.

