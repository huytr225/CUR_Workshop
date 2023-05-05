---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

Trong bài Lab này, bạn sẽ được hướng dẫn triển khai một giải pháp thử nghiệm **tự động truy vấn Báo cáo chi phí và mức sử dụng & gửi email** bằng Athena, Lambda, SES và CloudWatch.

Hàm Lambda được kích hoạt bởi CloudWatch Event, sau đó chạy các câu truy vấn đã lưu bởi Athena lên file CUR (Báo cáo chi phí và mức sử dụng) của bạn. Kết quả truy vấn được nhóm lại thành một file báo cáo duy nhất (định dạng xlsx) và gửi file báo cáo qua Email bằng SES. Giải pháp này cung cấp báo cáo tự động cho tổ chức của bạn, và cho người dùng đám mây.

![main-architecture](/images/main-architecture.png)


#### Báo cáo chi phí và mức sử dụng (CUR)
**Báo cáo chi phí và mức sử dụng** là **Cost and Usage Reports (CUR)** chứa dữ liệu chi phí và mức sử dụng chi tiết nhất.

**Báo cáo chi phí và mức sử dụng** theo dõi việc sử dụng AWS của bạn và cung cấp các khoản phí ước tính liên quan đến tài khoản của bạn. Mỗi báo cáo chứa các dòng, mỗi dòng có sản phẩm AWS, loại sử dụng và hoạt động mà bạn sử dụng trong tài khoản AWS của mình. Bạn có thể tùy chỉnh CUR để tổng hợp thông tin theo giờ, ngày hoặc tháng.


**AWS Cost and Usage Reports** có thể:
- Gửi các file báo cáo đến S3 bucket của bạn
- Cập nhật báo cáo lên đến ba lần một ngày
- Tạo, truy xuất và xóa báo cáo của bạn bằng CUR API của AWS 

**More infomation**:
- [AWS Cost and Usage Reports là gì?](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html)
- [Cách tạo Cost and Usage Reports (CUR)](https://docs.aws.amazon.com/cur/latest/userguide/cur-create.html)



#### Amazon Athena
**Amazon Athena** là một dịch vụ truy vấn tương tác được sử dụng để phân tích dữ liệu trong Amazon S3 với SQL tiêu chuẩn. Chúng ta chỉ cần trỏ đến dữ liệu của bạn trong Amazon S3, xác định schema và bắt đầu truy vấn bằng trình chỉnh sửa truy vấn tích hợp. Amazon Athena cho phép chúng ta khai thác tất cả dữ liệu của mình trong Amazon S3 mà không cần phải thiết lập các quy trình ETL phức tạp. Amazon Athena tính tiền dựa trên các truy vấn được chạy.

**Amazon Athena** sử dụng Presto với hỗ trợ SQL ANSI và hoạt động với nhiều định dạng dữ liệu tiêu chuẩn, bao gồm CSV, JSON, ORC, Avro và Parquet. Athena được khuyến nghị cho nhu cầu truy vấn nhanh, nhưng nó cũng có thể xử lý các phân tích phức tạp, bao gồm các phép Join với lượng dữ liệu lớn, các window functions và mảng.

**More infomation**: [Amazon Athena là gì?](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)

#### SES
**Amazon Simple Email Service (SES)** là một nền tảng email cung cấp một cách dễ dàng và tiết kiệm chi phí để bạn gửi và nhận email sử dụng địa chỉ email và tên miền của riêng bạn.

Xây dựng một giải pháp email quy mô lớn thường là một thách thức phức tạp và tốn kém cho một doanh nghiệp. Bạn phải đối mặt với các thách thức về cơ sở hạ tầng như quản lý máy chủ email, cấu hình mạng và địa chỉ IP. Ngoài ra, nhiều giải pháp email bên thứ ba yêu cầu hợp đồng và đàm phán giá cả, cũng như chi phí ban đầu đáng kể. Amazon SES loại bỏ những thách thức này và cho phép bạn tận dụng cơ sở hạ tầng email mà Amazon.com đã xây dựng để phục vụ khách hàng quy mô lớn của riêng mình.
