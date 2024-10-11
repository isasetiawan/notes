## Background

The issue happened when agent create leave request out side western Indonesia timezone. 
By default, when there is no attendance or shift in the period of agent request, the system will generate related attendance based on period day by day.

For example when requested leave period is `2024-07-02T00:00:00+08:00`  to `2024-07-03T23:59:59+08:00`  from middle Indonesia Time, the system will create attendance record with date `2024-07-02` and `2024-07-03`

The attendance creation process require not only date part but also time. Hence, the bug create attendance record with following date:
* `2024-07-01T16:00:00+00:00`
* `2024-07-03T15:59:59+00:00`
When the dates converted into WIB (our main timezone for attendances in system)
* `2024-07-01T23:00:00+00:00`
* `2024-07-03T22:59:59+00:00`
Since the attendance recap group the records based on date part only, the record appears shifted one day earlier than requested period.

Hence. The code patch will convert the requested period into main timezone instead as below:
* `2024-07-02T17:00:00+00:00`
* `2024-07-03T16:59:59+00:00`

## How to test

### With Shift
Create leave request 
```shell
curl --location --request POST 'http://localhost:8000/v1/agent/agent-leaves?timezone=Asia/Makassar' \ --header 'User-Agent: Stg.Staffinc Work/2.17.0 (com.kerjaan.app.dev; build:1; iOS 16.3.1) Alamofire/5.4.3' \ --header 'Accept-Language: en-ID;q=1.0, id-ID;q=0.9' \ --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NjQxNCwicGhvbmVfbnVtYmVyIjoiMDg1NzQ1MzA2NTg2IiwiY291bnRyeV9jb2RlIjoiKzYyIiwic3RhdHVzIjoiYWN0aXZlIiwicm9sZXMiOiJhZ2VudCIsImV4cCI6MTcxODc5NjMzMCwiaXNzIjoiYXV0aC12MC43LjAifQ.WEC0PUxKKySuXY4Ft1eFYgHJ0G69l2mckd958mgUSHA' \ --header 'Content-Type: application/json' \ --data-raw '{ "reason": "banaba", "leave_policy_id": 84, "action_timestamp": "2024-06-13T07:42:39+08:00", "period": [ "2024-07-02T00:00:00+08:00", "2024-07-03T23:59:59+08:00" ], "leave_time_type": "full_day", "supporting_doc_link": [ "https:\/\/kerjaan2-stg.s3-ap-southeast-1.amazonaws.com\/files\/162e207b-b127-402e-96e9-10b4a4970177.jpg" ] }'
```
Ensure create leave on attendance recap appear as the period
![[Screenshot 2024-06-13 at 07.25.26.png]]
### Without Shift
```shell
curl --location --request POST 'http://localhost:8000/v1/agent/agent-leaves?timezone=Asia/Makassar' \ --header 'User-Agent: Stg.Staffinc Work/2.17.0 (com.kerjaan.app.dev; build:1; iOS 16.3.1) Alamofire/5.4.3' \ --header 'Accept-Language: en-ID;q=1.0, id-ID;q=0.9' \ --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTcwNjcsInBob25lX251bWJlciI6IjA4MTcyMzQxMjkzMjIiLCJjb3VudHJ5X2NvZGUiOiIrNjIiLCJzdGF0dXMiOiJhY3RpdmUiLCJyb2xlcyI6ImFnZW50IiwiZXhwIjoxNzE5NDk3OTY0fQ.CkOB1IMr1x2EZMeDnHjrIgk454H1FcnCaOgK0-itUPM' \ --header 'Content-Type: application/json' \ --data-raw '{ "reason": "banaba", "leave_policy_id": 84, "action_timestamp": "2024-06-13T08:06:39+08:00", "period": [ "2024-06-17T00:00:00+08:00", "2024-06-18T23:59:59+08:00" ], "leave_time_type": "full_day", "supporting_doc_link": [ "https:\/\/kerjaan2-stg.s3-ap-southeast-1.amazonaws.com\/files\/162e207b-b127-402e-96e9-10b4a4970177.jpg" ] }'
```
![[Screenshot 2024-06-13 at 07.27.22.png]]