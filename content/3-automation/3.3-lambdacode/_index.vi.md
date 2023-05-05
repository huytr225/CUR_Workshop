---
title : "Cấu hình các tham số và tải mã nguồn lên S3"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

#### Cấu hình các tham số
1. Download code: **[AutoCURDelivery](/AutoCURDelivery.zip)** về máy. File zip gồm có:
   + auto_cur_delivery.py - Lambda function code
   + config.yml - file cấu hình
   + package/ - Tất cả các dependencies, thư viện, bao gồm pandas, numpy, Xlrd, Openpyxl, Xlsxwriter, pyyaml
2. Unzip code [AutoCURDelivery](/AutoCURDelivery.zip), sau đó mở **config.yml** trong một trình soạn thảo văn bản như Notepad hoặc IDE
3. Cấu hình các tham số trong **config.yml**
   + **CUR_Output_Location**: S3 Bucket để lưu trữ file kết quả, VD. ```S3://fcj-costreport/out-put/```
   + **CUR_DB**: CUR database và tên bảng được sử dụng trong Athena (tạo ra bởi Crawler), VD. ```'"cost"."fcj_cur_report"'```
   + **CUR_Report_Name**: Tên file báo cáo được gửi cùng với SES dưới dạng tệp đính kèm, VD. ```cost_utilization_report.xlsx```
   + **Region**: Region mà dịch vụ SES được gọi, VD. ```us-east-1```
   + **Subject**: Chủ đề thư, VD. ```Cost and Utilization Report```
   + **Sender**: Địa chỉ e-mail người gửi, VD. ```john@example.com```
   + **Recipient**: Địa chỉ e-mail người nhận. Nếu có nhiều người nhận, hãy phân tách bằng dấu phẩy, VD. ```john@example.com,alice@example.com```
    ```
    # Cost Report output location
    CUR_Output_Location: S3://fcj-costreport/out-put/  

    # GLUE database name and table
    CUR_DB: '"cost"."fcj_cur_report"'

    #CUR file name with suffix '.xlsx', which is sent as attachment via SES
    CUR_Report_Name: cost_utilization_report.xlsx

    #SES configuration
    Region: us-east-1
    Subject: Cost and Utilization Report
    #i.e. 'john@example.com'
    Sender: 'huytrandinh225@gmail.com'
    #If there are mulitple recipients, seperate them by commas. i.e. 'john@example.com,alice@example.com'
    Recipient: 'huytrandinh225@gmail.com'
    ```
    ![001-config-yml](/images/3.3-lambdacode/001-config-yml.png)
4. Giữ nguyên cấu hình khác và lưu lại **config.yml**
5. Cấu hình các tham số sau trong file **auto_cur_delivery.py** (chỉ với dữ liệu mẫu):
   + Comment 2 dòng: **curYear = datetime.datetime.now().year**, **curMonth = datetime.datetime.now().month**
   + Thêm 2 dòng: **curYear = 2018**, **curMonth = 12**
    ![002-auto-cur](/images/3.3-lambdacode/002-auto-cur.png)
6. Giữ nguyên cấu hình khác và lưu lại **auto_cur_delivery.py**
7. Zip file **auto_cur_delivery.py**, **config.yml** và **package** thành **AutoCURDelivery.zip**
    ![003-zip-file](/images/3.3-lambdacode/003-zip-file.png)

#### Tải mã nguồn lên S3
1. Đi đến [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
2. Chọn Bucket để tải tệp lên
    ![004-select-bucket](/images/3.3-lambdacode/004-select-bucket.png)
3. Nhấn **Upload**
    ![005-upload-file](/images/3.3-lambdacode/005-upload-file.png)
4. Upload file **NEW AutoCURDelivery.zip**
5. Nhấn **Upload**
    ![006-upload-file-2](/images/3.3-lambdacode/006-upload-file-2.png)
6. Sau khi upload thành công, nhấn vào tên file **AutoCURDelivery.zip**
    ![007-upload-success](/images/3.3-lambdacode/007-upload-success.png)
7. **Copy URL** để upload Lamda code từ S3 (lưu lại)
    ![008-copy-url](/images/3.3-lambdacode/008-copy-url.png)

