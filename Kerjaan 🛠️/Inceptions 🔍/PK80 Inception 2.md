## Sub Group 1 Shift Pattern Creation
1. UI simplification
2. Day-off shift type time changed from whole day (00:00 - 23:59) into (05:22) in order to handle different timezone in Indonesia
3. New field timezone in creation shift pattern
4. Default shift will be considered as timezone WIB
5. New filter in shift type in the page (replace dropdown filter)
	1. shift type
	2. start time
	3. end time
	4. timezone
6. No change in shift type search
## Sub Group 3 Detail and Modification
1. Shift pattern modification on start time, end time and timezone will be affected into future assigned shift
2. Shift type deletion
	1. Entry point from detail 
	2. Default shift can be deleted
	3. Will be affected to future assigned shift in future, will be assigned to default
	4. Past shift should be remaining the same
3. Shift pattern deletion
	1. Will be affected to future assigned shift in future, will be assigned to default
	2. Past shift should be remaining the same
## Group 2
1. Migration
	1. Future default shift became (05:00 - 22:00)

## Group 3 Shift Pattern assignment & Modification
1. worker assignment will consist of timezone
2. shift drop down list for assignment will contain timezone information
### Single Shift Assignment
1. Temporary allocation will be still the same
2. Validation
	1. same branch assignment
	2. remove overlap check shift
	3. Maximum shift in one day is 3
3. Activity log
### Multiple Assignment
1. New timezone information
2. Multiple date selection contain year information
3. Bulk assignment result will list down all failed assignment
4. CSV template reference will contains list of shift alongside with related timezone
5. Activity log

## Group 4 Handling Branch Without shift
1. Day off time will be change to (05 -22)
2. Default timezone will be WIB
## Group 7 Attendance Recap
1. Add timezone information in attendance detail
2.  Add timezone information in raw data download

## Group 5 Schedule Availability
### Current Shift Availability
S: start time of the shift, E: end time of the shift
1. Checkin period is S-4 hour until E
2. Checkin reminder push notification still the same
3. Checkout only for branch required to checkout
4. Checkout period is E unt E+9 (grace period)
5. Consideration for refactoring endpoint get current branch due its complexity
### Next shift availability 
1. E-24 hour and current shift is completed
Add ability to simulate current time
### 

# Notes

Agent Leave Request Creation
* Timezone of requested period is forced to WIB
- Current condition on leave request creation
	* Fetch default shift type on current client
	- Update-insert attendance and shift on enumerated requested leave period
		- Get attendance and shift on enumerated date period ([code](https://github.com/sampingantech/kerjaansvc/blob/b510166af86f2124ebd6086b13e58fdce5c33762/app/domains/attendances/usecases/agent_leaves.py#L435)) **if exist**
		- Create default shift with fetched shift type and create attendance enumerated date period ([code](https://github.com/sampingantech/kerjaansvc/blob/b510166af86f2124ebd6086b13e58fdce5c33762/app/domains/attendances/usecases/agent_leaves.py#L473-L498)) **if not exist**
	- Pair created and fetched attendance record on leave request (`attendance_detail`)
- Handle for without shift branch
	- Update-insert attendance based on enumerated requested period
		- Get attendance on enumerated date period **if exist**
		- Create attendance enumerated date period **if not exist**
	- Pair created and fetched attendance record on leave request (`attendance_detail`)