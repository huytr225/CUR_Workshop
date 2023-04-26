---
title : "Create a lambda function"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4. </b> "
---

+ Go to [Lambda Console](https://console.aws.amazon.com/lambda/home)
+ Click **Functions**
+ Click **Create function**
![001-create-lambda](/images/3.4-createlambda/001-create-lambda.png)
+ Enter function name: ```Auto_CUR_Delivery```
+ Select **Runtime**: Python 3.7
+ Click **Change default execution role**
+ Select **Use an existing role**
+ Select **Role**: ```Lambda_Auto_CUR_Delivery_Role```
+ Click **Create function**
![002-lambda-detail](/images/3.4-createlambda/002-lambda-detail.png)
+ Click **Test** section
+ Enter **Event name**: ```AutoCURDeliveryTest```
+ Click **Save**
![003-create-test](/images/3.4-createlambda/003-create-test.png)
+ Click **Code** section
+ Click **Upload from Amazon S3 location**
![004-upload-code](/images/3.4-createlambda/004-upload-code.png)
+ Paste **URL of AutoCURDelivery.zip** in previous section.
+ Click **Save**
![005-upload-code2](/images/3.4-createlambda/005-upload-code2.png)
+ Click **Edit** in **Runtime settings**
![006-edit-runtime](/images/3.4-createlambda/006-edit-runtime.png)
+ Change **Handler** to: ```auto_cur_delivery.lambda_handler```
+ Click **Save**
![007-edit-runtime-detail](/images/3.4-createlambda/007-edit-runtime-detail.png)
+ Click **Configuration** section
+ Click **General configuration**
+ Click **Edit**
![008-general-configuration](/images/3.4-createlambda/008-general-configuration.png)
+ Edit **Memory** to: **256**
+ Edit **Timeout** to **5 min 0 sec**
+ Click **Save**
![009-general-configuration-detail](/images/3.4-createlambda/009-general-configuration-detail.png)
+ Click **Test** section
+ Click **Test**
+ Check **Ẽxcution result: successed**
![010-test](/images/3.4-createlambda/010-test.png)
+ Check **your email inbox**
![011-email](/images/3.4-createlambda/011-email.png)