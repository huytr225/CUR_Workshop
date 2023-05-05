---
title : "Tự động truy vấn CUR bằng Athena và gửi Email bằng SES"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---
Phần này sẽ hướng dẫn bạn triển khai giải pháp tự động truy vấn CUR & gửi e-mail bằng cách sử dụng Athena, Lambda, SES và CloudWatch.


![main-architecture](/images/main-architecture.png)

#### Content
1. [Tạo bucket S3 cho mã nguồn Lambda và file kết quả](/3-automation/3.1-s3/)
2. [Tạo Lambda policy](/3-automation/3.2-lambdapolicy/)
3. [Cấu hình các tham số và tải mã nguồn lên S3](/3-automation/3.3-lambdacode/)
4. [Tạo lambda function](/3-automation/3.4-createlambda)
5. [Giải thích mã nguồn Lambda](/3-automation/3.5-lambdaexplain)
6. [Lập lịch sự kiện CloudWatch](/3-automation/3.6-cloudwatch)