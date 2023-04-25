---
title : "Use Sample CUR Data"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1. </b> "
---

<!-- #### Use Sample CUR Data -->
1. Create bucket for CUR Report
   + Go to [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Click **Buckets** then click **Create Bucket**.
   ![create-bucket](/images/2.1-sample/001-create-bucket.png)
   + Enter **Bucket name** for CUR Report: ```fcj-cur-report```
   ![fcj-cur-report-name](/images/2.1-sample/002-fcj-cur-report-name.png)
   + Click **Create Bucket**
   ![fcj-cur-report-name](/images/2.1-sample/003-create-bucket.png)

2. Create folder structure
   + Create a folder structure which resembles **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018**
   + Then create three further folders within the **year=2018** folder **(month=10, month=11, month=12)**
   ![folder-structure](/images/2.1-sample/004-folder-structure.png)
   

3. Download Sample CUR data (3 three parquet files):
   + [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet)
   + [November 2018 Usage](/Nov2018-WorkshopCUR-00001.snappy.parquet)
   + [December 2018 Usage](/Dec2018-WorkshopCUR-00001.snappy.parquet)

4. Upload [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet) to **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/**
   + Go to **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/**, click **Upload**
   ![folder-structure](/images/2.1-sample/005-click-upload-parquet.png)
   + Check **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/Upload**, Upload [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet) parquet file
   ![upload-parquet](/images/2.1-sample/006-upload-parquet.png)
   + Upload success
   ![success-upload-parquet](/images/2.1-sample/007-success-upload-parquet.png)
5. Upload [November 2018 Usage](/Nov2018-WorkshopCUR-00001.snappy.parquet) to **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=11/**
6. Upload [December 2018 Usage](/Dec2018-WorkshopCUR-00001.snappy.parquet) to **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=12/**