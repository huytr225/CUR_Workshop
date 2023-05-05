---
title : "Giải thích mã nguồn Lambda"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 3.5. </b> "
---

#### Giải thích file config.yml
Thiết lập tất cả cấu hình cần thiết cho mã nguồn Lambda
```
#Output cho báo cáo (S3)
CUR_Output_Location: S3://fcj-costreport/out-put/

# Tên CUR database và bảng Glue Crawler tạo ra
CUR_DB: '"cost"."fcj_cur_report"'

# Tên báo cáo gửi qua email
CUR_Report_Name: cost_utilization_report.xlsx

# cấu hình SES
Region: us-east-1
Subject: Cost and Utilization Report
#i.e. 'john@example.com'
Sender: 'huytrandinh225@gmail.com'
# Nếu có nhiều người thì phân cách bằng dấu phẩy. VD. 'john@example.com,alice@example.com'
Recipient: 'huytrandinh225@gmail.com'
#Mail body
Body_Text: "Hi,


Please find your Cost Utilization Report attached:

Cost_By_Service - Cost in the recent three month split by service (e.g. current month is Jul, the recent three months are Jul, Jun and May, same as below)

Data_Cost_By_Service - Data cost in the recent three month split by service 

MoM_Inter_AZ_DT(with graph) - Month over month inter-AZ data transfer usage and change in the recent three months

MTD_S3_By_Bucket - MTD S3 cost and usage type split by bucket name 

MTD_ELB_By_Name - MTD ELB cost split by ELB name and region

MTD_CF_By_Distribution - MTD Cloudfront cost and usage split by distribution id 



AWS Enterprise Support Team

"
```

#### Giải thích mã nguồn Lambda 
Lưu các câu truy vấn vào biến qStrList

```
# Code bên dưới tải chuỗi truy vấn (Query_String_List trong config.yml) vào biến qStrList

# Định nghĩa qStrList, và đưa tất cả các câu truy vấn vào qStrList (Tên truy vấn, câu truy vấn), đồng thời thay thế năm/tháng trong câu truy vấn
qStr = cfg['Query_String_List'] # Các câu truy vấn trong file config.yml
# print(qStr[0].values()[0])
qStrList = [] 


# Multiple charactors replacement in a string
# Hàm thay thế chuỗi, dùng dể thay thế các key -> value trong qStrSub đối với từng câu truy vấn trong biến qStr
#  VD: FROM CUR_DB -> FROM "cost"."fcj_cur_report"
def multReplace(string, substitutions): 
    substrings = sorted(substitutions, key=len, reverse=True)
    regex = re.compile('|'.join(map(re.escape, substrings)))
    return regex.sub(lambda match: substitutions[match.group(0)], string)


qStrSub = {
    'CUR_DB': curDB,
    'CUR_YEAR': str(curYear),
    'CUR_MONTH': str(curMonth),
    # 'CUR_WEEK': str(curWk),
    'CUR_OR_LAST_YEAR': str(curOrLastYr),
    'LAST_YEAR': str(lastYear),
    'LAST_MONTH': str(lastMon),
    # 'LAST_WEEK': str(lastWk),
    'PRE_LAST_MONTH': str(preLastMon)
    # 'PRE_LAST_WEEK': str(preLastWk)
}
for i in range(len(qStr)):
    # print(list(qStr[i].values())[0])
    qString = multReplace(list(qStr[i].values())[0], qStrSub)
    qStrList.append({'name': list(qStr[i].keys())[0], 'queryString': qString})
```
Luồng chạy của mã:
1. CloudWatch Event kích hoạt Lambda function
   - Hàm sẽ chạy từ Handler chúng ta định nghĩa:
   - auto_cur_delivery (tên file)
   - lambda_handler (tên hàm)
   - Trong mục **3.4 Tạo lambda function** chúng ta sửa **Handler** thành ```auto_cur_delivery.lambda_handler```
   - -> Hàm sẽ chạy từ **auto_cur_delivery.lambda_handler**
2. queryCUR: Truy vấn file CUR bằng Athena
3. 'OutputLocation': Nơi lưu trữ kêt quả truy vấn
4. cpResultsTolocal: Lấy kêt quả truy vấn (CSV)
    - csvToXlsx: Chuyển csv thành xlsx
    - processExcel: Kết hợp tất cả các file xlsx thành một file báo cáo xlsx duy nhất
5. sendReport: Gửi báo cáo CUR qua SES
6. client.send_raw_email: Gửi báo cáo CUR qua SES đến người nhận
![main-architecture](/images/main-architecture.png)
```
# =========== Function Execution ==================
def lambda_handler(event, context):                   # 1. CloudWatch Event kích hoạt Lambda function
    queryCUR(qStrList, curOutLoc)                     # 2. Query CUR using Athena
    waitQueryExecution(queryExpiration, qStrList)
    cpResultsTolocal(curBucket, curKeyPath, qStrList) # 4. cpResultsTolocal: Lấy kêt quả truy vấn (CSV)
    csvToXlsx(qStrList)                               #     - csvToXlsx: Chuyển csv thành xlsx
    processExcel(curReportName, qStrList)             #     - processExcel: Kết hợp tất cả các file xlsx thành một file báo cáo xlsx duy nhất
    response = sendReport(region, subject, sender, recipient, curReportName, bodyText) # 5. sendReport: Gửi báo cáo CUR qua SES
    return response
```

```
def queryCUR(queryList, targetLocation):
    client = boto3.client('athena')
    print("Starting query CUR ... ")
    for i in range(len(queryList)):
        resp = client.start_query_execution(
            QueryString=queryList[i]['queryString'],
            ResultConfiguration={
                'OutputLocation': targetLocation      # 3. 'OutputLocation': Nơi lưu trữ kêt quả truy vấn
            })
        queryList[i]['queryId'] = resp['QueryExecutionId']
        print("Query " + queryList[i]['name'] + ' cost, queryId is ' + queryList[i]['queryId'])
```
```
# Send CUR report via SES to Recipients

response = client.send_raw_email(                     # 6. client.send_raw_email: Gửi báo cáo CUR qua SES đến người nhận
            Source=sesSender,
            Destinations=sesReceiver.split(','),
            RawMessage={
                'Data': msg.as_string()
            }
        )
```