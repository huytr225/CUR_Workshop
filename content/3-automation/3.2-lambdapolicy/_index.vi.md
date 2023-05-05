---
title : "Tạo Lambda policy"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---
1. Tạo policy 
   + Đi đến [Amazon IAM](https://console.aws.amazon.com/iamv2)
   + Nhấn **Policies** sau đó Nhấn **Create Policy**.
   ![create-policy](/images/3.2-lambdapolicy/001-create-policy.png)
   + Nhấn **JSON** Tab
   + Copy JSON bên dưới, sửa **your-cur-query-results-bucket** thành tên bucket của bạn
    ```
    {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Sid": "VisualEditor0",
             "Effect": "Allow",
             "Action": [
                 "s3:PutObject"
             ],
             "Resource": [
                 "arn:aws:s3:::your-cur-query-results-bucket*" 
             ]
         },
         {
             "Sid": "VisualEditor1",
             "Effect": "Allow",
             "Action": [
                 "athena:List*",
                 "athena:*QueryExecution",
                 "athena:Get*",
                 "athena:BatchGet*",
                 "glue:Get*",
                 "glue:BatchGet*",
                 "s3:Get*",
                 "s3:List*",
                 "SES:SendRawEmail",
                 "SES:SendEmail",
                 "logs:CreateLogStream",
                 "logs:CreateLogGroup",
                 "logs:PutLogEvents"
             ],
             "Resource": "*"
         }
     ]
    } 
    ```
    + Kiểm tra **không có dấu cách** ở dòng đầu tiên
    + Nhấn **Next: Tags**
   ![002-policy](/images/3.2-lambdapolicy/002-policy.png)
   + Nhấn **Next: Review**
   ![003-next](/images/3.2-lambdapolicy/003-next.png)
   + Điền **policy name**: ```Lambda_Auto_CUR_Delivery_Access```
   + Nhấn **Create policy**
   ![004-review](/images/3.2-lambdapolicy/004-review.png)
2. Tạo Role
   + Đi đến [Amazon IAM](https://console.aws.amazon.com/iamv2)
   + Nhấn **Roles** sau đó Nhấn **Create role**.
   ![005-create-role](/images/3.2-lambdapolicy/005-create-role.png)
   + Chọn **Lambda**
   + Nhấn **Next**
   ![006-trusted-entity](/images/3.2-lambdapolicy/006-trusted-entity.png)
   + Search for policy: ```Lambda_Auto_CUR_Delivery_Access```
   + Chọn policy
   + Nhấn **Next**
   ![007-add-permissions](/images/3.2-lambdapolicy/007-add-permissions.png)
   + Điền **role name**: ```Lambda_Auto_CUR_Delivery_Role```
   ![008-role-name](/images/3.2-lambdapolicy/008-role-name.png)
   + Nhấn **Create role**
   ![009-create-role](/images/3.2-lambdapolicy/009-create-role.png)
   