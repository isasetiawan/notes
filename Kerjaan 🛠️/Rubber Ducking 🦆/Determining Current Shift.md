Determining current shift involve two fetched shift that use `lower(period)` as reference:
1. `prev_shift` which fetched using query `where lower(period) <= now()`
2. `next_shift` which fetched using query `where lower(period) => now()`

Hence for `prev_shift` there are ranges and clauses to be considered to return previous shift:
1. $now() \in [s, e] \cup \sim finished(shift)$
2. $now() \in [e, e+9] \cup \sim checkout(shift)$
3. $\sim isNone(nextShift)$
Meanwhile for `next_shift` there will clauses only:
1. $now() \in [s-4, e] \sim finished(shift)$
2. $now() \in [e, e+9] \cup \sim checkout(shift)$

Where:
1. $s$ is `lower(period)`
2. $e$ is `upper(period)`
3. $now()$ is current date time
4. $checkin(shift)$ indicate the $shift$ already checkin at current time
5. $checkout(shift)$ indicate the $shift$ already checkout at current time
6. $finished(shift)$ indicate the $shift$ shift already checkin and checkout 

This PR modify `determine_current_shift_based_on_two_shifts` to follow above condition

## Truth table

After doing deeper vision quest, I found that the above condition can be simplified into truth table that crossing between period and state of shift as below:

| Period Range    | Allowed States                                            | Desc                      |
| --------------- | --------------------------------------------------------- | ------------------------- |
| $[s-4, s]$      | `check_in`, `check_out`,`finished`, and other leave state | early checkin period      |
| $[s,e]$         | `check_in`, `check_out`,`finished`,and other leave state  | within shift period       |
| $[e,e+9]$       | `check_out`,`finished`                                    | grace period              |
| $[e+9, \infty]$ | `finished`                                                | after end of grace period |
Where:
1. $s$ is scheduled shift start time
2. $e$ is scheduled shift end time

