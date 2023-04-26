---
title : "Clean up resource"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
1. Delete **fcj-costreport** bucket
   + Go to [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Click **Buckets**
   + Select **Bucket name**
   + Click **Empty**
   + Confirm
![001-empty-costreport](/images/4-clean/001-empty-costreport.png)
   + Go to [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Click **Buckets**
   + Select **Bucket name**
   + Click **Delete**
   + Confirm
![002-delete-costreport](/images/4-clean/002-delete-costreport.png)
2. Delete **fcj-cur-report** bucket
    + Repeat step 1
3. Delete glue crawler
   + Go to [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Click **Crawlers**
   + Select **Crawler**
   + Click **Delete crawler**
![003-delete-crawler](/images/4-clean/003-delete-crawler.png)
4. Delete glue table
   + Go to [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Click **Tables**
   + Select **Table**
   + Click **Delete**
![004-delete-glue-table](/images/4-clean/004-delete-glue-table.png)
![005-delete-ses](/images/4-clean/005-delete-ses.png)
![006-delete-glue-policy](/images/4-clean/006-delete-glue-policy.png)
![007-delete-glue-role](/images/4-clean/007-delete-glue-role.png)
![008-delete-lambda-policy](/images/4-clean/008-delete-lambda-policy.png)
![009-delete-lambda-role](/images/4-clean/009-delete-lambda-role.png)
![010-delete-lambda-function](/images/4-clean/010-delete-lambda-function.png)
![011-delete-cloudwatch-rule](/images/4-clean/011-delete-cloudwatch-rule.png)