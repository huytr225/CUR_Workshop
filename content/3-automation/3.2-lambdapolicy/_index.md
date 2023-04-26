---
title : "Create Lambda policy"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---
1. Create policy 
   + Go to [Amazon IAM](https://console.aws.amazon.com/iamv2)
   + Click **Policies** then click **Create Policy**.
   ![create-policy](/images/3.2-lambdapolicy/001-create-policy.png)
   + Click **JSON** Tab
   + Copy JSON, modify the **your-cur-query-results-bucket** to your bucket
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
    + Check there is **no space** at the first line
    + Click **Next: Tags**
   ![002-policy](/images/3.2-lambdapolicy/002-policy.png)
   + Click **Next: Review**
   ![003-next](/images/3.2-lambdapolicy/003-next.png)
   + Enter **policy name**: ```Lambda_Auto_CUR_Delivery_Access```
   + Click **Create policy**
   ![004-review](/images/3.2-lambdapolicy/004-review.png)
2. Create Role
   + Go to [Amazon IAM](https://console.aws.amazon.com/iamv2)
   + Click **Roles** then click **Create role**.
   ![005-create-role](/images/3.2-lambdapolicy/005-create-role.png)
   + Select **Lambda**
   + Click **Next**
   ![006-trusted-entity](/images/3.2-lambdapolicy/006-trusted-entity.png)
   + Search for policy: ```Lambda_Auto_CUR_Delivery_Access```
   + Select policy
   + Click **Next**
   ![007-add-permissions](/images/3.2-lambdapolicy/007-add-permissions.png)
   + Enter role name: ```Lambda_Auto_CUR_Delivery_Role```
   ![008-role-name](/images/3.2-lambdapolicy/008-role-name.png)
   + Click **Create role**
   ![009-create-role](/images/3.2-lambdapolicy/009-create-role.png)
   