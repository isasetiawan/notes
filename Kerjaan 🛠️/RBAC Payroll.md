#kerjaan #PR

Testing account with payroll group and payroll module

```shell
curl --location --request GET 'localhost:8000/v1/client/payroll/payroll-components?limit=2' \ --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTM4LCJjbGllbnRfaWQiOjM2MiwiZW1haWwiOiJhc2RAbWFpbG8uY29tIiwibmFtZSI6IkFzZCIsImV4cCI6MTc1NzQyMTk0MH0.b316dEhxfz31z2Mbs1Ci_AoXEkU5Sswwonb18YlkYhU' \ --header 'User-Agent: Apidog/1.0.0 (https://apidog.com)'
```
respponse
```
{

"data": [

{

"id": "0191c260-82cc-775c-924a-938d9ea55bda",

"client_id": 362,

"component_type": "benefit",

"is_shown_on_payslip": false,

"is_taxable": false,

"name": "3LAB Hydra Day SPF 20 Broad Spectrum Water-Based Sunscreen",

"formula": "= BASE",

"name_on_payslip": "3LAB Hydra Day SPF 20 Broad Spectrum Water-Based Sunscreen",

"created_at": "2024-09-06T01:44:42.665636Z",

"created_by": "System Generated (Sample)",

"created_at_timezone": "Asia/Jakarta",

"updated_at": "2024-09-09T01:44:42.665636Z",

"updated_by": "fufufafa@fu.fa",

"updated_at_timezone": "Asia/Jakarta"

},

{

"id": "0191c260-82cc-7c0a-b8ca-37df45b3a65c",

"client_id": 362,

"component_type": "deduction",

"is_shown_on_payslip": false,

"is_taxable": false,

"name": "Amazonian Colored Clay Foundation Broad Spectrum SPF 15 Sunscreen",

"formula": "= BASE",

"name_on_payslip": "Amazonian Colored Clay Foundation Broad Spectrum SPF 15 Sunscreen",

"created_at": "2024-09-06T01:44:42.665636Z",

"created_by": "System Generated (Sample)",

"created_at_timezone": "Asia/Jakarta",

"updated_at": "2024-09-06T01:44:42.665636Z",

"updated_by": "System Generated (Sample)",

"updated_at_timezone": "Asia/Jakarta"

}

],

"meta": {

"limit": 2,

"offset": 0,

"total_data": 29

}

}
```