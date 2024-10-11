
| Critical | Medium | Non Bug | AFI | Oncall |
| -------- | ------ | ------- | --- | ------ |
| 1        | 1      | 0       | 4   | Hasbi  |

- Absensi tereject menjadi absen
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725849091803129)
    - Issue
        - Attendance has been rejected but no Action Log is found
    - Root Cause
        - Endpoint Bulk Update Branch Shift : Unintended update on attendances.created_at into attendance with old ID
    - Long Term Solution (Prevention)
        - [https://github.com/sampingantech/kerjaansvc/pull/5345](https://github.com/sampingantech/kerjaansvc/pull/5345)
    - Short Term
        - Update attendance status into waiting for check in, thus employee able to do check in
    - Status Done
    - Severity **Medium**
    - Notes
        - Need to recheck the occurrence of the anomaly - post hotfix release
        - Need to make sure if employee able to check in normally even if the assigned branch is different from the attendance’s branch
        - Need to make sure if employee’s attendance can be included in payroll creation if they are able to checkin in different branch
- Absensi di all client berubah menjadi WCI Env: Seamless Client Portal - Staffinc Suite
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725869635197919)
    - Issue
        - Wrong query update attendance into waiting for check in
        ```sql
        update attendance_recap
        set
        status = ‘waiting_for_checkin’,
        latest_status =  ‘waiting_for_checkin’,
        agent_request_status = null,
        attendance_dispute_status = null
        from attendance_recap ar
        where ar.attendance_id in {3560719,3561540,3561543,3560722,3560724,3561546,3560726,3561549,3560727,3561556,3560731,3561553,3560733,3561552,3561559,3560735,3560736,3561555}
        ```
    - Solution
        - Update attendance recap status, latest_status, agent_request_status by inferring from attendance and agent request table
            - TODO : attach the resouce link
        - Update attendance recap by inferring from dispute request
            - New Schema (user_experience_logs.metadata column)
            - Old Schema (user_experience_logs.new_value column)
        - Update Attendance Recap by inferring from Edit single/bulk attendance recap status
            - (user_experience_logs.metadata column)
    - Status Done
    - Severity **Critical**
    - Follow Up
        - Restrict Prod Access, only allowed to SRE, Tech Lead, BE Lead
- Tidak mendapatkan OTP
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725952749900299)
    - Issue
        - 3rd Party Error
	- Short Term:
		- Use default OTP
    - Solution
        - Upgrade tier Meta
        - Follow Up to qiscuss as OTP Provider
        - Long Term :
            - AFI
    - Status : In Progress
    - Severity **AFI**
- Tidak mendapatkan Kode OTP
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1726034819599639)
    - Issue
        - error in service provider (data is unable to be tracked for this cases)
    - Solution
        - long term: [AFI][BE] Handling error log for error responses from OTP service Provider
        - Short term : Default OTP
    - Status : In Progress
    - Severity **AFI**
- Disbursement API Validation Error
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1726056319243729)
    - Issue
        - Email not validated when creating disbursement
    - Solution
        - AFI - Included in RTS : Add validation in email when create disbursement
    - Status : In progress
    - Severity **AFI**
- Beberapa disbursement id statusnya in progress padahal sudah beberapa hari
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1726124234168689)
    - Issue
        - Status in xendit and staffinc not match
        - No callback been received
    - Solution
        - AFI to create worker tasks to check into xendit via the disbursement details endpoint
    - Status : In progress
    - Severity **AFI**