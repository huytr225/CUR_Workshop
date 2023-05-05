---
title : "Explain Lambda code"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 3.5. </b> "
---

#### Explain config.yml
Setup all the config nessesary for Lambda code
```
#S3 Location for output
CUR_Output_Location: S3://fcj-costreport/out-put/

#CUR database name and table in Glue
CUR_DB: '"cost"."fcj_cur_report"'

#CUR file name with suffix '.xlsx', which is sent as attachment via SES
CUR_Report_Name: cost_utilization_report.xlsx

#SES configuration
Region: us-east-1
Subject: Cost and Utilization Report
#i.e. 'john@example.com'
Sender: 'huytrandinh225@gmail.com'
#If there are mulitple recipients, seperate them by commas. i.e. 'john@example.com,alice@example.com'
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

#### Eplain Lambda code
Load query string into qStrList 

```
# The code below load query string (Query_String_List in config.yml) into qStrList variable 

# Define a dic list qStrList, and load all query strings into qStrList with the pair key (Name, queryString), also replace year/month in the strings
qStr = cfg['Query_String_List']
# print(qStr[0].values()[0])
qStrList = []


# Multiple charactors replacement in a string
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



Flow of code:
1. CloudWatch Event activate Lambda function
   - The function run from Handler we define:
   - auto_cur_delivery (file name)
   - lambda_handler(function name)
   - In **3.4 Create a lambda function** we Change Handler to: ```auto_cur_delivery.lambda_handler```
   - -> function run from **auto_cur_delivery.lambda_handler**
2. queryCUR: Query CUR using Athena 
3. 'OutputLocation': output location of query result
4. cpResultsTolocal: Get query result (CSV)
    - csvToXlsx: Change csv to xlsx
    - processExcel: Combine all xlsx files in to a single xlsx report file
5. sendReport: Send CUR report via SES
6. client.send_raw_email: Send CUR report via SES to Recipients
![main-architecture](/images/main-architecture.png)
```
# =========== Function Execution ==================
def lambda_handler(event, context):
    queryCUR(qStrList, curOutLoc) # 2. queryCUR: Query CUR using Athena 
    waitQueryExecution(queryExpiration, qStrList)
    cpResultsTolocal(curBucket, curKeyPath, qStrList) # 4. cpResultsTolocal: Get query result (CSV)
    csvToXlsx(qStrList)                               #     - csvToXlsx: Change csv to xlsx
    processExcel(curReportName, qStrList)             #     - processExcel: Combine all xlsx files in to a single xlsx report file
    response = sendReport(region, subject, sender, recipient, curReportName, bodyText) # 5. sendReport: Send CUR report via SES
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
                'OutputLocation': targetLocation # 3. 'OutputLocation': output location of query result
            })
        queryList[i]['queryId'] = resp['QueryExecutionId']
        print("Query " + queryList[i]['name'] + ' cost, queryId is ' + queryList[i]['queryId'])
```
```
# Send CUR report via SES to Recipients

response = client.send_raw_email( # 6. client.send_raw_email: Send CUR report via SES to Recipients
            Source=sesSender,
            Destinations=sesReceiver.split(','),
            RawMessage={
                'Data': msg.as_string()
            }
        )
```