| Medium | Non Bug | AFI | Oncall |
| ------ | ------- | --- | ------ |
| 6      | 2       | 1   | Isa    |

- Shift sudah benar, namun pada attendance recap masih terdapat double dot
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725259719545619)
    - Issue
        - Leftover issue from migration PK080
    - Solution
        - Solved by running gradually update query
    - Status Done
    - Severity **Medium**
- Kendala pada bulk edit additional data
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725261340329009)
    - Issue
        - Data point got deleted when not filled in csv row for bulk edit
    - Status: Considered as AFI due to tech limitation
    - Severity **Non Bug**
- Keterangan "WIB" di Shift menjadi "null"
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725266977908169)
    - Issue
        - Bulk create shift endpoint does not fill schedule_timezone
        - Days off shift time does not follow new spec (05-22)
    - Solution
        - Fix the code
        - Fix existing data by running gradual update query
    - Status Done
    - Severity **Medium**
- Double shift day off
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725270086055789)
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725274495506249)
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725357137883849)
    - Issue
        - Impact from migration issue PK080
        - The shift has been modified by user which mean unable to be fixed due to different user intent
    - Solution
        - Checking with user_experience_logs
    - Status Considered non bug
    - Severity **Non Bug**
- Attendance recap pada branch tertentu gabisa dibuka
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725278869427339)
    - Issue
        - Currently the code to handle attendance recap fetching is distinguish by branch with shift and branch without shift
        - Attendance recap sometimes shows records of agent from previous branch, the previous branch could be without shift
        - Since PK080 attendance recap with shift is date-grouped by schedule start time instead of attendance_date
    - Solution
        - Adding fallback when attendance recap records does not field period for date-grouping
    - Status Hot-fixed
    - Severity **Medium**
- User portal tidak bisa akses attendance detail
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725350135563329)
    - Issue
        - User cannot see attendance recap detail record
        - Due to user not assigned to previous branch of the attendance record
    - Solution
        - Assign the user to the branch
    - Status AFI
    - Severity **AFI**
- Tidak bisa membuat password
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725356837388799)
    - Issue
        - Seamless portal user cannot set password due to sampingan_id is null
        - Due to wrong comparison with == 0 and == null
    - Solution
        - Run update query to set password manually (short term)
        - [PR](https://github.com/sampingantech/hcmsvc/pull/250) hotfix ready by [Rifan Nur Muhammad](mailto:rifan@staffinc.co)
    - Status waiting for confirmation
    - Severity **Medium**
- Agent seharusnya mendapatkan shift day off, namun status pada attendance recap WCI
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725521564385729)
    - Issue
        - Shift assigned as days off but the attendance recap dot shown waiting for checking
        - Wrong attendance id on changing shift
    - Status
	    - Done
        - Short term available
    - Severity **Medium**
- Tidak bisa melakukan check in
    - [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1725530983616239)
    - Issue
        - Happened in staffing supervise
        - Attendance record got soft deleted
        - Attendance record got created on the days before current day, meanwhile the branch is without shift
        - Related to wrong attendance id update on update shift
    - Status
        - Not yet picked up
        - Short term available
	- Severity **Medium**