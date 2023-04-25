---
title : "Explain lambda function"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 3.5. </b> "
---

#### Explain config.yml
```
CUR_Output_Location: S3://fcj-costreport/out-put/

#CUR database name and table
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
#Mail body
Body_Text: "Hi,


Please find your Cost Utilization Report attached:

Cost_By_Service - Cost in the recent three month split by service (e.g. current month is Jul, the recent three months are Jul, Jun and May, same as below)

Data_Cost_By_Service - Data cost in the recent three month split by service 

MoM_Inter_AZ_DT(with graph) - Month over month inter-AZ data transfer usage and change in the recent three months

MTD_S3_By_Bucket - MTD S3 cost and usage type split by bucket name 

MTD_ELB_By_Name - MTD ELB cost split by ELB name and region

MTD_CF_By_Distribution - MTD Cloudfront cost and usage split by distribution id 



AWS Enterprise Support Team

"
```