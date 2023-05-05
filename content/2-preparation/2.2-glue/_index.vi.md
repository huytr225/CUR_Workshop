---
title : "Sử dụng AWS Glue để cho phép truy cập file CUR qua Amazon Athena"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.2. </b> "
---

Kế hoạch của chúng ta là sử dụng AWS Glue và lập lịch một Crawler. Sau đó Crawler sẽ quét các file CUR, tạo ra cơ sở dữ liệu và tạo bảng cho các file đã quét qua.

Để truy cập và phân tích các file CUR bằng SQL, chúng ta sẽ sử dụng Athena. Athena là một giải pháp không cần máy chủ cho phép thực hiện truy vấn SQL trên các khối lượng dữ liệu lớn. Athena chỉ tính phí cho dữ liệu đã được duyệt qua, và không có chi phí định kỳ nếu dữ liệu không được truy vấn.



1. Thiết lập một Crawler
   + Đi đến [AWS Glue Console](https://console.aws.amazon.com/glue)
   + Nhấn **Crawlers** sau đó Nhấn **Create crawler**.
   ![create-crawler](/images/2.2-glue/001-create-crawler.png)
   + Điền **Crawler name**: ```COST_CUR_Crawler```
   + Nhấn **Next**
   ![crawler-properties](/images/2.2-glue/002-crawler-properties.png)
   + Nhấn **Add a data source**
   ![add-datasource](/images/2.2-glue/003-add-datasource.png)
   + Nhấn **Browse S3**, sau đó Chọn **fcj-cur-report** Bucket
   + Nhấn **Exclude files matching pattern**
   ![add-datasource-detail](/images/2.2-glue/004-add-datasource-detail.png)
   + Kiểm tra đường dẫn S3 là chính xác
   + Thêm **Exclude Pattern**: ```**.json```,  ```**.yml```,  ```**.sql```,  ```**.csv```,  ```**.gz```,  ```**.zip```, ```**/cost_and_usage_data_status/*```, ```aws-programmatic-access-test-object```
   + Nhấn **Add an S3 data source**
   ![add-datasource-detail-2](/images/2.2-glue/005-add-datasource-detail-2.png)
   + Nhấn **Next**
   ![add-datasource-next](/images/2.2-glue/006-add-datasource-next.png)
   + Nhấn **Create new IAM role**: ```Cost_Crawler```
   + Nhấn **Update chosen IAM role**
   + Nhấn **Next**
   ![security-settings](/images/2.2-glue/007-security-settings.png)
   + Nhấn **Add database**
   ![add-database](/images/2.2-glue/008-add-database.png)
   + Điền tên Glue Database: ```cost```
   + Nhấn **Create database**
   ![create-database](/images/2.2-glue/009-create-database.png)
   + Nhấn **Refresh Target database**
   + Chọn **cost** database
   + Chọn **Create a single schema for each S3 path**
   + Chọn **Add new columns only**
   + Chọn **Ignore the change and don't update the table in the data catalog**
   ![set-output-and-scheduling](/images/2.2-glue/010-set-output-and-scheduling.png)
   + Chọn Frequency **Daily**
   + Start hour: **20**
   + Minute of the hour: **00**
   + Nhấn **Next**
   ![set-output-and-scheduling2](/images/2.2-glue/011-set-output-and-scheduling2.png)
   + Kiểm tra và Nhấn **Create crawler**
   ![review](/images/2.2-glue/012-review.png)
2. Chạy clawer
   + Kiểm tra tên Crawler: **Cost_CUR_Crawler**
   ![click-crawler](/images/2.2-glue/013-click-crawler.png)
   + Nhấn **Run crawler**
   + Đợi Status chuyển sang **Completed**
   ![run-crawler](/images/2.2-glue/014-run-crawler.png)
3. Kiểm tra dữ liệu trong Glue database
   + Nhấn **Tables** trong Data Catalog
   + Nhấn tên của bảng: **fcj-cur-report**
   ![cost-table](/images/2.2-glue/015-cost-table.png)
   + Nhấn **Advanced properties**
   + Kiểm tra số record **recordCount** ~ 334911 records 
   ![check-record-count](/images/2.2-glue/016-check-record-count.png)
4. Sử dụng **Amazon Athena** để truy vấn file CUR
   + Nhấn vào ô **3 chấm** và Chọn **Load partitions** 
   ![load-partitions](/images/2.2-glue/017-load-partitions.png)
   + Chúng ta sẽ truy vấn thử dữ liệu của file CUR. Nhấn vào ô **3 chấm** và Chọn **Preview table**
   ![preview-table](/images/2.2-glue/018-preview-table.png)
   