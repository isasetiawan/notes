#issues #kerjaan

Related to issue where days off schedule shifted one day before
Impact: Any leave request on D-1 is bounded the days off that already shifted back to proper date

Objective: 
Find impacted leave request that have one day period but includes the days off shift schedule on the outside leave period.

Challenges:
validating on how leave request is bounded by leave period using query period.

[code](https://github.com/sampingantech/kerjaansvc/blob/a1daa8d77d1e8e67a151db8ce6f1a216128005f4/app/handlers/agents/agent_leaves.py#L147-L148)
```python
    timezone = IndonesiaTimeEnum.WEST_TIME

    period = (
        datetime.combine(leave_request.period[0], time(0, 0)),
        datetime.combine(leave_request.period[1], time(23, 59)),
    )
    datetime_period = (
        pytz.timezone(timezone).localize(period[0]),
        pytz.timezone(timezone).localize(period[1]),
    )

    attendances = await agent_leaves_use_case.get_by_branch_agent_period(
        branch.id, current_user.id, datetime_period
    )
```
[code](https://github.com/sampingantech/kerjaansvc/blob/96711157d81c3757318a31d4ffa919269f29ecb8/app/domains/attendances/repositories/attendances.py#L292-L293)
```python
        if isinstance(period, tuple):
            query.append_whereclause(self.model.c.created_at.between(*period))
```

BUT. the bound is based on `attendances.created_at` . meanwhile the impacted data point form migration issue is `attendance_recap.period` and `branch_shifts.period`.
But. the reported issue may be appears on approving leave request.

Actual case
agent request period is 
* `["2024-08-30 17:00:00+00","2024-08-31 16:59:59+00"]`
bounded attendance is records with `created_at` 
* `2024-08-31 22:00:00.000000 +00:00` -> follow 05-22 probably due to attendance edit status
* `2024-08-31 03:00:30.000000 +00:00`


~~fact: created_at may be got synced -> **possible cause in approving leave request process** [code](https://github.com/sampingantech/kerjaansvc/blob/b98569715d006bbba4bdeed3ccc9aa8569b2e1fc/app/handlers/clients/agent_requests.py#L138)~~

## Actual Timeline
* 2024-08-24 07:20:39.379177 +00:00
	* agent request created
* 2024-08-26 09:08:44.776636+00
	* attendance with id 11776292 binded
* 2024-08-26 09:11:36.094296 +00:00
	* agent request approved
* 2024-08-26 09:08:44.776636 +00:00
	* shift id 3515945 created
* 2024-08-29 02:49:43.318457 +00:00
	* shift id 3520304 created
