---
title : "Lập lịch sự kiện CloudWatch"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 3.6. </b> "
---
+ Đi đến [Cloudwatch Console](https://console.aws.amazon.com/cloudwatch/home)
+ Click **Rules**
+ Click **Create rule**
![001-create-rule](/images/3.6-cloudwatch/001-create-rule.png)
+ Select **Schedule**
+ Fixed rate of **5 minutes**
+ Select **Target**: **Lambda function**
+ Select **Function**: **Auto_CUR_Delivery**
+ Click **Configure details**
![002-create-rule-detail](/images/3.6-cloudwatch/002-create-rule-detail.png)
+ Enter **Rule name**: ```5_min_auto_cur_delivery```
+ Click **Create rule**
![003-rule-detail](/images/3.6-cloudwatch/003-rule-detail.png)
+ Wait 5 minutes then check your email
![004-check-email](/images/3.6-cloudwatch/004-check-email.png)
+ **Disable** when not use
![005-disable-rule](/images/3.6-cloudwatch/005-disable-rule.png)