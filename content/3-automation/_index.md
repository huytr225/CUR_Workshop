---
title : "Automated Athena CUR Query and E-mail Delivery"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---
This section will guide you through deploying an demo automatic CUR query & E-mail delivery solution using Athena, Lambda, SES and CloudWatch.


![main-architecture](/images/main-architecture.png)

#### Content
1. [Create S3 bucket for Lambda code and Results](/3-automation/3.1-s3/)
2. [Create Lambda policy](/3-automation/3.2-lambdapolicy/)
3. [Configure parameters of function code and upload code to S3](/3-automation/3.3-lambdacode/)
4. [Create a lambda function](/3-automation/3.4-createlambda)
5. [Explain Lambda code](/3-automation/3.5-lambdaexplain)
6. [Create scheduled CloudWatch event](/3-automation/3.6-cloudwatch)