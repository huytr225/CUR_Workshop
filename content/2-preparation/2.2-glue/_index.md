---
title : "Use AWS Glue to enable access to CUR files via Amazon Athena"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.2. </b> "
---
Our plan is to utilize AWS Glue and setup a scheduled Crawler. The Crawler will examine the CUR files, generate a database, and create tables for the files that have been received. Any new editions of a CUR, or new monthly deliveries, will be automatically added.

To access and analyze our CUR files using SQL, we'll use Athena. Athena is a serverless alternative that allows for SQL queries to be executed on substantial data volumes. Athena is solely billed for data that has been examined, and there are no recurring expenses if the data is not being queried, which is different from a traditional database solution.

1. Setup a Crawler
   + Go to [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Click **Crawlers** then click **Create crawler**.
   ![create-crawler](/images/2.2-glue/001-create-crawler.png)
   + Enter **Crawler name**: ```COST_CUR_Crawler```
   + Click **Next**
   ![crawler-properties](/images/2.2-glue/002-crawler-properties.png)
   + Click **Add a data source**
   ![add-datasource](/images/2.2-glue/003-add-datasource.png)
   + Click **Browse S3**, then Select **fcj-cur-report** Bucket
   + Click **Exclude files matching pattern**
   ![add-datasource-detail](/images/2.2-glue/004-add-datasource-detail.png)
   + Check S3 path is correct
   + Add Exclude Pattern: ```**.json```,  ```**.yml```,  ```**.sql```,  ```**.csv```,  ```**.gz```,  ```**.zip```, ```**/cost_and_usage_data_status/*```, ```aws-programmatic-access-test-object```
   + Click **Add an S3 data source**
   ![add-datasource-detail-2](/images/2.2-glue/005-add-datasource-detail-2.png)
   + Click **Next**
   ![add-datasource-next](/images/2.2-glue/006-add-datasource-next.png)
   + Click **Create new IAM role**: ```Cost_Crawler```
   + Click **Update chosen IAM role**
   + Click **Next**
   ![security-settings](/images/2.2-glue/007-security-settings.png)
   + Click **Add database**
   ![add-database](/images/2.2-glue/008-add-database.png)
   + Enter Glue Database name: ```cost```
   + Click **Create database**
   ![create-database](/images/2.2-glue/009-create-database.png)
   + Refresh Target database
   + Select **cost** database
   + Select **Create a single schema for each S3 path**
   + Select **Add new columns only**
   + Select **Ignore the change and don't update the table in the data catalog**
   ![set-output-and-scheduling](/images/2.2-glue/010-set-output-and-scheduling.png)
   + Select Frequency **Daily**
   + Start hour: **20**
   + Minute of the hour: **00**
   + Click **Next**
   ![set-output-and-scheduling2](/images/2.2-glue/011-set-output-and-scheduling2.png)
   + Review and Click **Create crawler**
   ![review](/images/2.2-glue/012-review.png)
2. Run clawer
   + Click Name of the Crawler: **Cost_CUR_Crawler**
   ![click-crawler](/images/2.2-glue/013-click-crawler.png)
   + Click **Run crawler**
   + Wait for the status to change to **Completed**
   ![run-crawler](/images/2.2-glue/014-run-crawler.png)
3. Check data in the Glue database
   + Click **Tables** in the Data Catalog
   + Click Name of the Table: **fcj-cur-report**
   ![cost-table](/images/2.2-glue/015-cost-table.png)
   + Click **Advanced properties**
   + Check **recordCount** ~ 334911 records 
   ![check-record-count](/images/2.2-glue/016-check-record-count.png)
4. Using **Amazon Athena** to query our CUR files
   + Click on the **3 dot menu** and select **Load partitions** 
   ![load-partitions](/images/2.2-glue/017-load-partitions.png)
   + We will now preview the data. Click on the **3 dot menu** and select **Preview table**
   ![preview-table](/images/2.2-glue/018-preview-table.png)
   