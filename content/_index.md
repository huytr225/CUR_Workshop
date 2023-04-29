---
title : "Automated Athena CUR Query and E-mail Delivery"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
This hands-on lab will guide you through deploying an demo automatic CUR query & E-mail delivery solution using Athena, Lambda, SES and CloudWatch.

The Lambda function is triggered by a CloudWatch event, it then runs saved queries in Athena against your CUR file. The queries are grouped into a single report file (xlsx format), and sends report via SES. This solution provides automated reporting to your organization, to both consumers of cloud and financial teams.

![main-architecture](/images/main-architecture.png)


#### Cost and Usage Report (CUR)
**The AWS Cost and Usage Reports (AWS CUR)** contains the most comprehensive set of cost and usage data available.

**AWS Cost and Usage Reports** tracks your AWS usage and provides estimated charges associated with your account. Each report contains line items for each unique combination of AWS products, usage type, and operation that you use in your AWS account. You can customize the AWS Cost and Usage Reports to aggregate the information either by the hour, day, or month.

**AWS Cost and Usage Reports** can do the following:
- Deliver report files to your Amazon S3 bucket
- Update the report up to three times a day
- Create, retrieve, and delete your reports using the AWS CUR API Reference

**More infomation**:
- [What are AWS Cost and Usage Reports?](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html)
- [Creating Cost and Usage Reports](https://docs.aws.amazon.com/cur/latest/userguide/cur-create.html)



#### Amazon Athena
**Amazon Athena** an interactive query service used to analyze data in Amazon S3 with standard SQL. We simply point to your data in Amazon S3, define the schema and start querying with the built-in query editor. Amazon Athena allows us to mine all of our data in Amazon S3 without having to set up complex ETL processes. Amazon Athena charges based on queries run.

**Amazon Athena** uses Presto with ANSI SQL support and works with many standard data formats, including  CSV, JSON, ORC, Avro , and  Parquet. Athena is recommended for fast querying needs, but it can also handle complex analysis, including large joins, window functions, and arrays.

**More infomation**: [What is Amazon Athena?](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)

#### SES
**Amazon Simple Email Service (SES)** is an email platform that provides an easy, cost-effective way for you to send and receive email using your own email addresses and domains.

Building a large-scale email solution is often a complex and costly challenge for a business. You must deal with infrastructure challenges such as email server management, network configuration, and IP address reputation. Additionally, many third-party email solutions require contract and price negotiations, as well as significant up-front costs. Amazon SES eliminates these challenges and enables you to benefit from the years of experience and sophisticated email infrastructure Amazon.com has built to serve its own large-scale customer base.
