---
title : "Sử dụng dữ liệu CUR mẫu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1. </b> "
---

<!-- #### Sử dụng dữ liệu CUR mẫu -->
1. Tạo bucket cho báo cáo CUR
   + Đi đến [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
   + Nhấn **Buckets** sau đó Nhấn **Create Bucket**.
   ![create-bucket](/images/2.1-sample/001-create-bucket.png)
   + Điền **Bucket name** cho CUR Report: ```fcj-cur-report```
   ![fcj-cur-report-name](/images/2.1-sample/002-fcj-cur-report-name.png)
   + Nhấn **Create Bucket**
   ![fcj-cur-report-name](/images/2.1-sample/003-create-bucket.png)

2. Tạo cấu trúc thư mục
   + Tạo cấu trúc thư mục như sau **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018**
   + Sau đó tạo thêm ba thư mục trong thư mục **year=2018**: **(month=10, month=11, month=12)**
   ![folder-structure](/images/2.1-sample/004-folder-structure.png)
   

3. Tải xuống dữ liệu CUR mẫu (3 parquet files):
   + [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet)
   + [November 2018 Usage](/Nov2018-WorkshopCUR-00001.snappy.parquet)
   + [December 2018 Usage](/Dec2018-WorkshopCUR-00001.snappy.parquet)

4. Upload [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet) vào **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/**
   + Đi đến đường dẫn **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/**, Nhấn **Upload**
   ![folder-structure](/images/2.1-sample/005-click-upload-parquet.png)
   + Kiểm tra đường dẫn **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=10/Upload**, Upload [October 2018 Usage](/Oct2018-WorkshopCUR-00001.snappy.parquet) parquet file
   ![upload-parquet](/images/2.1-sample/006-upload-parquet.png)
   + Kiểm tra upload thành công
   ![success-upload-parquet](/images/2.1-sample/007-success-upload-parquet.png)
5. Tương tự, Upload [November 2018 Usage](/Nov2018-WorkshopCUR-00001.snappy.parquet) vào đường dẫn **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=11/**
6. Tương tự, Upload [December 2018 Usage](/Dec2018-WorkshopCUR-00001.snappy.parquet) vào đường dẫn **(bucket name)/cur/WorkshopCUR/WorkshopCUR/year=2018/month=12/**