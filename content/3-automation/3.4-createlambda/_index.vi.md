---
title : "Tạo lambda function"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4. </b> "
---

+ Đi đến [Lambda Console](https://console.aws.amazon.com/lambda/home)
+ Nhấn **Functions**
+ Nhấn **Create function**
![001-create-lambda](/images/3.4-createlambda/001-create-lambda.png)
+ Nhập tên function: ```Auto_CUR_Delivery```
+ Chọn **Runtime**: Python 3.7
+ Nhấn **Change default execution role**
+ Chọn **Use an existing role**
+ Chọn **Role**: ```Lambda_Auto_CUR_Delivery_Role```
+ Nhấn **Create function**
![002-lambda-detail](/images/3.4-createlambda/002-lambda-detail.png)
+ Nhấn vào mục **Test**
+ Nhập **Event name**: ```AutoCURDeliveryTest```
+ Nhấn **Save**
![003-create-test](/images/3.4-createlambda/003-create-test.png)
+ Nhấn vào mục **Code** 
+ Nhấn **Upload from Amazon S3 location**
![004-upload-code](/images/3.4-createlambda/004-upload-code.png)
+ Dán **URL của file AutoCURDelivery.zip** trong phần trước
+ Nhấn **Save**
![005-upload-code2](/images/3.4-createlambda/005-upload-code2.png)
+ Nhấn **Edit** trong **Runtime settings**
![006-edit-runtime](/images/3.4-createlambda/006-edit-runtime.png)
+ Sửa **Handler** thành ```auto_cur_delivery.lambda_handler```
+ Nhấn **Save**
![007-edit-runtime-detail](/images/3.4-createlambda/007-edit-runtime-detail.png)
+ Nhấn vào mục **Configuration**
+ Nhấn **General configuration**
+ Nhấn **Edit**
![008-general-configuration](/images/3.4-createlambda/008-general-configuration.png)
+ Sửa **Memory** thành **256**
+ Sửa **Timeout** thành **5 min 0 sec**
+ Nhấn **Save**
![009-general-configuration-detail](/images/3.4-createlambda/009-general-configuration-detail.png)
+ Nhấn vào mục **Test**
+ Nhấn **Test**
+ Kiểm tra **Excution result: successed**
![010-test](/images/3.4-createlambda/010-test.png)
+ Kiểm tra **Email của bạn**
![011-email](/images/3.4-createlambda/011-email.png)