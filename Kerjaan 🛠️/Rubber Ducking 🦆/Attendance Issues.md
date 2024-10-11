Based on [this](https://github.com/sampingantech/kerjaansvc/blob/90c994dbc03cd7aebca4459e69892ba3c31f68f7/app/domains/attendances/entities/attendance_recap.py#L630-L646) pre-fixed code, attendance record counted as *Menunggu Konfirmasi*  based on this clause that could be written by this boolean algebra:

$$F=(A+B+C)D$$
Where:
* $A$ : attendance status is **Waiting for checking**
```python
recap.status in [
	AttendanceRecapStatusEnum.waiting_for_checkin
]
```
* $B$: attendance status is **Waiting for checkout**
```python
recap.status in [
	AttendanceRecapStatusEnum.waiting_for_checkout
]
```
* $C$: attendance status is **Pending**
```python
recap.status in [
	AttendanceRecapStatusEnum.waiting_for_confirmation,
    AttendanceRecapStatusEnum.waiting_approval,
]
```
* $D$: agent request status is pending or half day leave
```python
(
	recap.agent_request_status.is_pending()
	or recap.agent_request_status.is_half_day_leave
)
```

Meanwhile, based on this PK054 [reference] attendance record counted as *Menunggu Konfirmasi* should be:
$$F = ((A+B+C)D)+C $$
And can be derived as below: 
$$F = (AD+BD+CD)+C $$
$$F = AD+BD+CD+C $$
$$F = AD+BD+(D+1)C $$
$$F = AD+BD+C $$
$$F = (A+B)D+C $$
Hence, based on that equation, the python code should be:
```python
if (
    (
        recap.status
        and recap.status
        in [
            AttendanceRecapStatusEnum.waiting_for_checkin,
            AttendanceRecapStatusEnum.waiting_for_checkout,
        ]
    )
    and (
        recap.agent_request_status
        and (
            recap.agent_request_status.is_pending()
            or recap.agent_request_status.is_half_day_leave
        )
    )
    or (
        recap.status
        and recap.status
        in [
            AttendanceRecapStatusEnum.waiting_for_confirmation,
            AttendanceRecapStatusEnum.waiting_approval,
        ]
    )
):
    summary.total_waiting_for_confirmation += 1
```
