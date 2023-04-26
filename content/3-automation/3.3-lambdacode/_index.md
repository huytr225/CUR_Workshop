---
title : "Configure parameters of function code and upload code to S3"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

#### Configure parameters of function code
1. Download function code: **[AutoCURDelivery](/AutoCURDelivery.zip)** to your local disk. This zip file includes:
   + auto_cur_delivery.py - Lambda function code
   + config.yml - Configuration file
   + package/ - All dependencies, libraries, including pandas, numpy, Xlrd, Openpyxl, Xlsxwriter, pyyaml
2. Unzip function code [AutoCURDelivery](/AutoCURDelivery.zip), and open **config.yml** into a text editor
3. Configure the following parameters in **config.yml**
   + **CUR_Output_Location**: Your S3 bucket created previously, i.e. ```S3://fcj-costreport/out-put/```
   + **CUR_DB**: CUR database and table name defined in Athena, i.e. ```'"cost"."fcj_cur_report"'```
   + **CUR_Report_Name**: Report filename that is sent with SES as an attachment, i.e. ```cost_utilization_report.xlsx```
   + **Region**: The region where SES service is called, i.e. ```us-east-1```
   + **Subject**: SES mail subject, i.e. ```Cost and Utilization Report```
   + **Sender**: Your sender e-mail address, i.e. ```john@example.com```
   + **Recipient**: Your recipient e-mail addresses. If there are multiple recipients, separate them by comma, i.e. ```john@example.com,alice@example.com```
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
4. Keep other configuration unchanged and save **config.yml**
5. Configure the following parameters in **auto_cur_delivery.py** (for testing sample data):
   + Comment 2 lines: **curYear = datetime.datetime.now().year**, **curMonth = datetime.datetime.now().month**
   + Add 2 lines: **curYear = 2018**, **curMonth = 12**
    ![002-auto-cur](/images/3.3-lambdacode/002-auto-cur.png)
6. Keep other configuration unchanged and save **auto_cur_delivery.py**
7. Zip **auto_cur_delivery.py**, **config.yml** and **package** into **AutoCURDelivery.zip**
    ![003-zip-file](/images/3.3-lambdacode/003-zip-file.png)

#### Upload code to S3
1. Go to [Amazon S3 Buckets](https://console.aws.amazon.com/s3/buckets)
2. Select Bucket to upload file
    ![004-select-bucket](/images/3.3-lambdacode/004-select-bucket.png)
3. Click **Upload**
    ![005-upload-file](/images/3.3-lambdacode/005-upload-file.png)
4. Upload your **NEW AutoCURDelivery.zip** file
5. Click **Upload**
    ![006-upload-file-2](/images/3.3-lambdacode/006-upload-file-2.png)
6. After upload successfull, Click file name **AutoCURDelivery.zip**
    ![007-upload-success](/images/3.3-lambdacode/007-upload-success.png)
7. **Copy URL** for upload lambda code
    ![008-copy-url](/images/3.3-lambdacode/008-copy-url.png)

