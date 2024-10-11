## Preparation
- [x] Client account should have multiple projects, branches and dashboard min 40
SP.5
- [x] Client account with role that have module user configuration and not
- [x] Account should have multiple roles for showing sorting functionality, pagination
SP.8
- [ ] Account with access to managing
- [ ] Account with no access to managing
- [ ] Account with super admin role
## Accounts

| email                 |            | Note                   |
| --------------------- | ---------- | ---------------------- |
| maria@sampingan.co.id | Asdasd123. | Super Admin of QBX     |
| fyretyni@cyclelove.cc |            | Attendance only on QBX |

## Notes
1. Role list table
	1. role name still use snake case. miss map from FE
	2. listed modules should modules name not only group BE
	3. actor name should be bold text format on updated by and created by FE
	4. When search field triggered, pagination not reset to one FE
	5. Page indicator should not showing "Page **1 of 0**". Should show "Page 1 of 1" instead FE (same in admin portal)
2. Admin details page 
	1. ![[Screenshot 2024-07-01 at 13.46.47.png]] This checkbox on the section should be checked for client with recruitment only (FE)
	2. Endpoint edit admin raise not found (404) due to invalid query (active only) BE -> without managing access
	3. Endpoint edit admin raise 500 on client with managing access
	```shell
	curl 'https://hcm.dev.kerjaan.co.id/v1/sso/core/accounts/1110' \
  -X 'PUT' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en,en-US;q=0.9,id;q=0.8' \
  -H 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiIiLCJpZCI6IjE5NyIsIm1hbmFnaW5nSUQiOiIzMTAiLCJyZWNydWl0bWVudElEIjoiMCIsImVtYWlsIjoibWFyaWFAc2FtcGluZ2FuLmNvLmlkIiwicGhvbmVOdW1iZXIiOiI4NzgzNDM0MzQzNDMyIiwiY291bnRyeUNvZGUiOiIrNjIiLCJzdGF0dXMiOiJhY3RpdmUiLCJyb2xlcyI6WyJzYW1waW5nYW5fYnVzaW5lc3MiXSwidHlwZSI6InNzb19jbGllbnRfYWNjb3VudCIsInR5cGVzIjpbInNhbXBpbmdhbl9idXNpbmVzcyJdLCJleHAiOjE3MTk5MDMwOTYsImlzcyI6InNzby12MS4wLjAifQ.oGDLCnwM458rfaEZ_CqrEAQ1_MujAaEuStkouXcdxEs' \
  -H 'content-type: application/json' \
  -H 'dnt: 1' \
  -H 'origin: https://client-dev.staffincsuite.co' \
  -H 'priority: u=1, i' \
  -H 'referer: https://client-dev.staffincsuite.co/' \
  -H 'sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: cross-site' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36' \
  -H 'x-client-timezone: Asia/Jakarta' \
  --data-raw '{"managing_id":3339,"recruitment_id":0,"name":"Admin Baru Baru","email":"isa+aaa@staffinc.co","phone_number":"8100920481211","role_id":12208,"project_ids":[1742,1561],"branch_ids":[1769,1750,1749,1730,1729,1710,1708,1707,1706,1705,1704,1692,1649,1648,1647,1518,1517,1516,1480,1479,1478,1477,1476,1475,1474,1471,1470,1469,1468,1467,1466,1465,1330,1153,1121,1120,1119,1118,1114,1101,1098,1097,1096,1093,1092,1077,1076,1075,1074,1073,1067,1066,1047,1010,879,812,742,741,740,706,500,489,485,311,232,135,132,131,130,129,128,86,35],"analytic_dashboard_ids":[3141]}'
```
4. ![[Screenshot 2024-07-01 at 14.01.15.png]] Handle condition when
	1. `Selected all` checked and no search triggered
	2. `Selected all` checked and with search triggered
5. Implement force login when handling multiple logout from managing
6. Endpoint get /accounts raise 403 forbidden BE
```shell
curl 'https://hcm.dev.kerjaan.co.id/v1/sso/core/accounts?filter=&keyword=&limit=10&offset=0&sort=' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en,en-US;q=0.9,id;q=0.8' \
  -H 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiIiLCJpZCI6IjEwNDEiLCJtYW5hZ2luZ0lEIjoiMzI2MyIsInJlY3J1aXRtZW50SUQiOiI0OTMwMyIsImVtYWlsIjoibWFyaWErc3VwZXJzckBzdGFmZmluYy5jbyIsInBob25lTnVtYmVyIjoiODUyODUyODUxMTIzIiwiY291bnRyeUNvZGUiOiIrNjIiLCJzdGF0dXMiOiJhY3RpdmUiLCJyb2xlcyI6WyJzYW1waW5nYW5fYnVzaW5lc3MiXSwidHlwZSI6InNzb19jbGllbnRfYWNjb3VudCIsInR5cGVzIjpbInNhbXBpbmdhbl9idXNpbmVzcyJdLCJleHAiOjE3MTk5MDU3MzgsImlzcyI6InNzby12MS4wLjAifQ.r0xWOkH3ktHSqg-4HkUvOR9eZ7PoMSYi_P_bS835srg' \
  -H 'dnt: 1' \
  -H 'origin: https://client-dev.staffincsuite.co' \
  -H 'priority: u=1, i' \
  -H 'referer: https://client-dev.staffincsuite.co/' \
  -H 'sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: cross-site' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36' \
  -H 'x-client-timezone: Asia/Jakarta'
```
7. Create endpoint path for accessing master data like projects, payroll-group etc BE (TODO)
8. 