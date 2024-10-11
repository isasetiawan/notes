# Incident Timeline

| Time                          | Related Actors                  | Event                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 2024-08-27 11:04:05+07:00     | PIC Release PK080               | Running DML script to update days off shift schedule to default time (05:00:00+07 - 22:00:00+07)                                                                                                                                                                                                                                                                                           |
| 2024-08-28 01:04:05+07:00     | Business Ops                    | New [bug report](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1724779138716439) submitted reporting that all day off shift shifted to one day earlier                                                                                                                                                                                                                               |
| 2024-08-28 11:04:05+07:00     | PIC Release PK080               | Attempting to restore backed-up data query that having form update clause                                                                                                                                                                                                                                                                                                                  |
| 2024-08-28 09:34:18+07:00     | PIC Release PK080               | Attempt to restore data failed due inability IDE to handle large data. Attempt to use `pgcli`                                                                                                                                                                                                                                                                                              |
| 2024-08-28 09:34:18+07:00<br> | PIC Release PK080               | Actor unaware that backed-up update queries consist of 210568 rows and will take long-time execution due to backup query consist of                                                                                                                                                                                                                                                        |
| 2024-08-28 10:23:40+07:00<br> | Backend Team and Tech Lead      | Discussing on how backed-up date could be restored using shifting factor period by recognizing how shift schedule shifted from origin data. Based on discussion the schedule data could be categorized into two type i.e: with prefix 17:00 and prefix 00:00. The restore data strategy will use math operation to subtract and addition for impacted records to reduce update query load. |
| 2024-08-28 11:29:29+07:00<br> | PIC Release PK080               | Importing backup data to Google Sheet in order to distinguish update query based on categorized                                                                                                                                                                                                                                                                                            |
| 2024-08-28 16:27:43+07:00<br> | PIC Release PK080               | Actor realize that the data could not be categorized into two type of prefix                                                                                                                                                                                                                                                                                                               |
| 2024-08-29 06:40:00+07:00<br> | PIC Release PK080 and Tech Lead | Tech Lead suggest to build update query on small portion of data first by dividing data population into smaller period of schedule, and observable impact on defined branch and client. Build the update query and restore query                                                                                                                                                           |
| 2024-08-29 08:39:00+07:00     | PIC Release PK080 and Tech Lead | Running the built query on table `branch_shifts` with  period within range 2024-08-25 and 2024-08-31 and client **Bobobox** (212)                                                                                                                                                                                                                                                          |
| 2024-08-29 11:04:00+07:00     | PIC Release PK080 and Tech Lead | Issues found that there is inconsistent result between shifts and attendance recap records. Turns out the query was updating non days off shift instead of the days off.                                                                                                                                                                                                                   |
| 2024-08-29 11:30:00+07:00     | PIC Release PK080 and Tech Lead | Restoring data using restore query, Fixing update query                                                                                                                                                                                                                                                                                                                               |
| 2024-08-29 12:01:00+07:00 | PIC Release PK080 and Tech Lead | Running fixed update query on on branch first to be validated by ops teams on bug report thread |
| 2024-08-29 12:11:00+07:00 | Business Ops | Ops team validate that the query has correct impact on the records |
| 2024-08-29 12:49:00+07:00 | PIC Release PK080 and Tech Lead | Running fixed update query on all branches for schedule period within range 25 Aug 2024 and 2 Sept 2024 |
| 2024-08-29 14:39:00+07:00 | Tech Lead | Actor Found that there is 24K records found and will heavy to run all at once. And will be run the query by chunk of month instead from 2024 Feb to 2024 Aug |
| 2024-08-29 15:26:00+07:00 | Tech Lead | Actor found there is another data characteristics i.e stacked days-off shift in one date and day off that overlap with cross date. Actor build new query to handle data with stacked days off query |
| 2024-08-29 21:35:00+07:00 | Tech Lead | Actor execute built query on specific branch (7698) on week 35 |
| 2024-08-30 07:17:00+07:00 | Release PIC PK080 | Build query for handling cross date data characteristic |

# Impacts

1. All day off shift schedule shifted to one day earlier
2. Potential employee cannot check-in due to incorrect shift schedule

## Impact 1

By running DML script to update days off shift schedule to default time (05:00:00+07 - 22:00:00+07), all day off shift schedule shifted to one day earlier. This impact shown at **Shift** and **Attendance Recap** modules.

# Impact 2

Potential employee cannot check-in due to incorrect shift schedule. Since the day off shift schedule shifted to one day earlier, where there is might be working schedule on the day that should be day off.

# Root Cause

1. Incorrect query executed by the PIC Release PK080
2. Inability to restore backed-up data due to large data population

## Root Cause 1 Detail
The root cause of this incident is due to the incorrect data update query that was executed by the PIC Release PK080. The query was intended to update time part of the schedule to 05-22 WIB, Turns out it shift the schedule into 1 day earlier.

There is a bug on update clause
```pgsql
(lower(period)::date + time '05:00:00')::timestamp without time zone at time zone 'Asia/Jakarta',
```

If the we decompose as below:
```pgsql
SELECT ('2024-08-27 17:00:00+07'::date) "0",
 ('2024-08-27 17:00:00+07'::date + time '05:00:00') "1",
 ('2024-08-27 17:00:00+07'::date + time '05:00:00')::timestamp "2",
 ('2024-08-27 17:00:00+07'::date + time '05:00:00')::timestamp without time zone "3",
 ('2024-08-27 17:00:00+07'::date + time '05:00:00')::timestamp without time zone at time zone 'Asia/Jakarta' "4";

```
We can see how the date transform and got shifted by one day earlier.

```json
[
  {
    "0": "2024-08-27",
    "1": "2024-08-27 05:00:00.000000",
    "2": "2024-08-27 05:00:00.000000",
    "3": "2024-08-27 05:00:00.000000",
    "4": "2024-08-26 22:00:00.000000 +00:00"
  }
]
```

## Root Cause 2 Detail

The prepared backup data query consist of 210568 rows and will take long-time execution due to backup query consist of. The actor unaware that backed-up update queries consist of 210568 rows and will take long-time execution. And the update clause consist of unecessary column update that could be skipped.

Here is a sample of the backed-up data query:
```pgsql
UPDATE public.attendance_recap SET branch_id = 1543, agent_id = 69189, branch_shift_id = 917163, attendance_date = '2023-05-02 00:00:00.000000 +00:00', period = '["2023-05-02 00:00:00+00","2023-05-02 23:59:59.999999+00"]', status = 'day_off', checkin_at = null, checkout_at = null, overtime_minutes = null, created_at = '2023-04-30 11:33:22.581009 +00:00', updated_at = null, attendance_id = 3889656, approval_type = null, latest_status = 'day_off', agent_request_status = null, attendance_dispute_status = null, early_checkout_time_diff_minutes = 0 WHERE id = 12233439;
UPDATE public.attendance_recap SET branch_id = 539, agent_id = 55240, branch_shift_id = 918763, attendance_date = '2023-05-01 00:00:00.000000 +00:00', period = '["2023-05-01 00:00:00+00","2023-05-01 23:59:59.999999+00"]', status = 'approved', checkin_at = null, checkout_at = null, overtime_minutes = null, created_at = '2023-04-30 12:24:28.776412 +00:00', updated_at = '2023-05-22 06:48:41.396532 +00:00', attendance_id = 3891256, approval_type = null, latest_status = 'approved', agent_request_status = null, attendance_dispute_status = null, early_checkout_time_diff_minutes = 0 WHERE id = 12235199;
UPDATE public.attendance_recap SET branch_id = 539, agent_id = 55240, branch_shift_id = 932346, attendance_date = '2023-05-02 00:00:00.000000 +00:00', period = '["2023-05-02 00:00:00+00","2023-05-02 23:59:59.999999+00"]', status = 'approved', checkin_at = null, checkout_at = null, overtime_minutes = null, created_at = '2023-05-01 09:08:10.243858 +00:00', updated_at = '2023-05-22 06:48:56.786084 +00:00', attendance_id = 3909000, approval_type = null, latest_status = 'approved', agent_request_status = null, attendance_dispute_status = null, early_checkout_time_diff_minutes = 0 WHERE id = 12259584;
```


# Solutions

Since the data design spec for shift and attendance are not centralized, there is some data point that not affected by DML migration script. The data point attached in table `attendance_recap` column `attendance_date`. Hence this query is built to fix shifted days off schedule:

```sql
begin;  
with updated_branch_shifts as (  
    update branch_shifts bs set  
        period = tstzrange(  
                ((attendance_date at time zone bs.schedule_timezone)::date +  
                 (lower(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                bs.schedule_timezone,  
                ((attendance_date at time zone bs.schedule_timezone)::date +  
                 (upper(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                bs.schedule_timezone,  
                '[]'  
                 )  
        from attendance_recap ar where  
            ar.branch_shift_id = bs.id  
                and bs.id in (select bs.id  
                              FROM branch_shifts bs  
                                       JOIN shift_patterns sp ON sp.id = shift_pattern_id  
                                       JOIN shift_types st ON sp.shift_type_id = st.id  
                                       JOIN attendance_recap ar ON ar.branch_shift_id = bs.id  
                              WHERE bs.deleted_at is null  
                                and st.is_time_off is TRUE  
                                and ar.attendance_date at time zone bs.schedule_timezone between '2022-01-01' and '2023-01-01'  
                                and (lower(bs.period) != (((attendance_date at time zone bs.schedule_timezone)::date +  
                                                           (lower(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                                                          bs.schedule_timezone)  
                                  or upper(bs.period) != (((attendance_date at time zone bs.schedule_timezone)::date +  
                                                           (upper(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                                                          bs.schedule_timezone))  
                                and ((attendance_date at time zone bs.schedule_timezone)::date +  
                                     (lower(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                                    bs.schedule_timezone <= ((attendance_date at time zone bs.schedule_timezone)::date +  
                                                             (upper(bs.period) at time zone bs.schedule_timezone)::time)::timestamp at time zone  
                                                            bs.schedule_timezone)  
        returning bs.id, bs.period)  
UPDATE attendance_recap  
SET period = ubs.period  
FROM updated_branch_shifts ubs  
WHERE attendance_recap.branch_shift_id = ubs.id;  
commit;
```

Some parameters on this clause may ajdusted to control data portion 

```sql
and ar.attendance_date at time zone bs.schedule_timezone between '2022-01-01' and '2023-01-01'
```
# Further Actions

1. [Formalize](https://staffinc-co.slack.com/archives/C024JHHERND/p1724818590308779) the process of DML script execution to avoid incorrect data update.
2. Will monitor the issue for the next 2 weeks to ensure the data consistency and no further issue found.
3. For next development:
	1. Planning for data migration should always consider size of impact 
	2. Migration should consider space and time complexity for planning, whether it is for migration UP or rollback DOWN
	3. Migration should planned for minimal risk of unexpected behavior by defining impacted data population.
	4. For DML migration testing, there is should be a test session between backend and QA team to ensure the data consistency.
	5. Migration testing plan should be written in migration task during writing soulution phase
	6. Writing SOP release that consist of time range (better within working hour)


