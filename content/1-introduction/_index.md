---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---
This hands-on lab will guide you through deploying an demo automatic CUR query & E-mail delivery solution using Athena, Lambda, SES and CloudWatch. The Lambda function is triggered by a CloudWatch event, it then runs saved queries in Athena against your CUR file. The queries are grouped into a single report file (xlsx format), and sends report via SES. This solution provides automated reporting to your organization, to both consumers of cloud and financial teams.

Provide automated financial reports across your organization