---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
1. Xóa **fcj-costreport** bucket
   + Đi đến [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Nhấn **Buckets**
   + Chọn **Bucket name**
   + Nhấn **Empty**
   + Xác nhận
![001-empty-costreport](/images/4-clean/001-empty-costreport.png)
   + Đi đến [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Nhấn **Buckets**
   + Chọn **Bucket name**
   + Nhấn **Delete**
   + Xác nhận
![002-delete-costreport](/images/4-clean/002-delete-costreport.png)
2. Xóa **fcj-cur-report** bucket
    + Lặp lại bước 1 
3. Xóa glue crawler
   + Đi đến [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Nhấn **Crawlers**
   + Chọn **Crawler**
   + Nhấn **Xóa crawler**
![003-delete-crawler](/images/4-clean/003-delete-crawler.png)
4. Xóa glue table
   + Đi đến [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Nhấn **Tables**
   + Chọn **Table**
   + Nhấn **Delete**
![004-delete-glue-table](/images/4-clean/004-delete-glue-table.png)
5. Xóa SES identity
   + Đi đến [AWS SES](https://console.aws.amazon.com/ses/home)
   + Nhấn **Verified identities**
   + Chọn  **Identity**
   + Nhấn **Delete**
![005-delete-ses](/images/4-clean/005-delete-ses.png)
6. Xóa glue policy
   + Đi đến [Amazon IAM](https://console.aws.amazon.com/iamv2)
   + Nhấn **Policies**
   + Search ```AWSGlueServiceRole-Cost_Crawler```
   + Chọn **Policy name**
   + Nhấn **Delete**
![006-delete-glue-policy](/images/4-clean/006-delete-glue-policy.png)
7. Xóa glue role
   + Nhấn **Roles**
   + Search ```AWSGlueServiceRole-Cost_Crawler```
   + Chọn **Role name**
   + Nhấn **Delete**
![007-delete-glue-role](/images/4-clean/007-delete-glue-role.png)
8. Xóa Lambda Policy
   + Nhấn **Policies**
   + Search ```Lambda_Auto_CUR_Delivery_Access```
   + Chọn **Policy name**
   + Nhấn **Delete**
![008-delete-lambda-policy](/images/4-clean/008-delete-lambda-policy.png)
9. Xóa Lambda Role
   + Nhấn **Roles**
   + Search ```Lambda_Auto_CUR_Delivery_Role```
   + Chọn **Role name**
   + Nhấn **Delete**
![009-delete-lambda-role](/images/4-clean/009-delete-lambda-role.png)
10. Xóa Lambda function
    + Đi đến [Lambda Console](https://console.aws.amazon.com/lambda/home)
    + Nhấn **Functions**
    + Chọn **Auto_CUR_Delivery** function
    + Nhấn **Delete**
![010-delete-lambda-function](/images/4-clean/010-delete-lambda-function.png)
11. Xóa cloudwatch rule
    + Đi đến [Cloudwatch Console](https://console.aws.amazon.com/cloudwatch/home)
    + Nhấn **Rules**
    + Chọn **5_min_auto_cur_delivery**
    + Nhấn **Delete**
![011-delete-cloudwatch-rule](/images/4-clean/011-delete-cloudwatch-rule.png)