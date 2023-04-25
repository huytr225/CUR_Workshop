---
title : "Automated Athena CUR Query and E-mail Delivery"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Automated Athena CUR Query and E-mail Delivery

### Overall
This hands-on lab will guide you through deploying an automatic CUR query & E-mail delivery solution using Athena, Lambda, SES and CloudWatch. The Lambda function is triggered by a CloudWatch event, it then runs saved queries in Athena against your CUR file. The queries are grouped into a single report file (xlsx format), and sends report via SES. This solution provides automated reporting to your organization, to both consumers of cloud and financial teams.

![ConnectPrivate](/images/architecture.png) 

### Content
 1. [Introduction ](1-introduce/)
 2. [Preparation](2-prerequiste/)
 <!-- 3. [Connect to EC2 instance](3-accessibilitytoinstances/)
 4. [Manage session logs](4-s3log/)
 5. [Port Forwarding](5-Portfwd/)
 6. [Clean up resources](6-cleanup/) -->
