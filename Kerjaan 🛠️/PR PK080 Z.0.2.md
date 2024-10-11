# How To Test

Tested on sample branch shift record with id 15943 on dev database
```sql
UPDATE
	postgres.public.branch_shifts
SET
	period = tstzrange(lower(period)::date + time '05:00:00', upper(period)::date + time '22:00:00', '[]')
WHERE
	id = 15943;
```
Test with case `["2024-03-24 00:00:00+00","2024-03-24 23:59:59.999999+00"]`
Before query run
```json
  {
    "id": 15943,
    "agent_id": 4413,
    "branch_id": 135,
    "period": ["2024-03-24 00:00:00+00","2024-03-24 23:59:59.999999+00"],
    "created_at": "2024-03-24 16:15:00.417606+00",
    "updated_at": "2024-03-24 16:16:56.306901+00",
    "shift_pattern_id": 149
  }
```
After query run
```json
  {
    "id": 15943,
    "agent_id": 4413,
    "branch_id": 135,
    "period": ["2024-03-23 22:00:00+00","2024-03-24 15:00:00+00"],
    "created_at": "2024-03-24 16:15:00.417606+00",
    "updated_at": "2024-03-24 16:16:56.306901+00",
    "shift_pattern_id": 149
  }
```