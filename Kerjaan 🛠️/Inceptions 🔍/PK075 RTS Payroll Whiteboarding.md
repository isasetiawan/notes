# Group 1 Feature Flag

## Feature Flag
 Feature flag is use to enabling and disabling some payroll sub-modules
 1. Feature flag for Payroll Component and Payroll Report BETA
 2. Feature flag for Direct Payroll Report under payroll report creation
 Each feature flag belongs to specific client.
 Created data from those modules still remain regardless of the feature flag status.

# Group 2 Role and sub module assignment
How feature flag is related with assigned sub-module in RBAC

| Assigned Sub Module           | Feature Flag | Shown Menu                                                                         |
| ----------------------------- | ------------ | ---------------------------------------------------------------------------------- |
| payroll group                 | active       | payroll component **Beta**, payroll report **Beta**, payroll group                 |
| payroll report                | active       | payroll component **Beta**, payroll report **Beta**, payroll report                |
| payroll group, payroll report | active       | payroll component **Beta**, payroll report **Beta**, payroll group, payroll report |
| nothing                       | active       | nothing                                                                            |
| payroll report                | inactive     | payroll report                                                                     |
| payroll group                 | inactive     | payroll group                                                                      |
| nothing                       | inactive     | nothing                                                                            |
| payroll group, payroll report | inactive     | payroll group, payroll report                                                      |
# Group 4 Payroll Component

## Data Abstraction
### Payroll Component

| Field           | Type     | Notes                                   |
| --------------- | -------- | --------------------------------------- |
| ID              | sequence | Searchable                              |
| Component Name  | String   | Searchable                              |
| Component Type  | Enum     | Allowance/Deduction/Benefit. Filterable |
| Taxable         | Boolean  |                                         |
| Show on payslip | Boolean  |                                         |
| Payslip Name    | String   |                                         |
Component Type:
- Allowance: Additional payment to employee
- Deduction: Reduction of employee salary
- Benefit: Not deducting take home pay, and not adding take home pay but something that is beneficial to employee
Name on Payslip: Name that will be shown on payslip
Formula: Formula to calculate the component. currently only support `BASE` , Where `BASE` is defined on employee profile.

# Group 5 Payroll Component x Employee DB relevancy
...
# Group 6 Payroll Report List
## Data Points
1. Status: Different from current implementation. Will use Draft and Finalized ony
2. Entitled Month: Month of the payroll report. will replace current payroll report cycle. only consist of month and year only.
# Group 7 Payroll Report Creation
There is 7 steps to create payroll report represented as wizard form.
General Wizard Behavior:
1. Leaving the form from step greater than 1 will save the data as draft
2. Leaving the form from step 1 will not save the data
3. Jumping through step is not allowed
4. Going back to previous state will reset data on current step
5. Race condition is possible by multiple client account.
6. If other client account at same draft already in further step, current client account will redirected to list page when clicking next.
## Payroll Configuration
1. Name
2. Entitled Month: For information purpose only
3. Toggle Use Attendance Data: If enabled, will use attendance data to calculate payroll component. For current release will default to off
4. Disbursement By: Option to by who the payroll will be disbursed. Current release will support Staffinc only
5. Payroll Component: List of payroll component that will be used in this payroll report. Created from Payroll Component module.
6. If there any component deleted, will shown an error when clicking next
## Select Employee
### List of Available Employee
1. Will shown all employee regardless of status
2. Will shown on left side of the screen
3. Retrieve Data button will retrieve employee data from backend and remove employee that already selected
### List of Selected Employee
1. Will shown all selected employee
### Selecting Employee
1. By selection
2. By select all
3. By import CSV file that consist of employee ID
## Employee Data
### Employee Data Table
1. If any selected employee has no email, will shown warning due to impact on payslip delivery.
2. Show existence of NIK, and NPWP due to impact on tax calculation
3. Search by employee name
4. Filter by email existence
## Attendance Data
Will not implemented on current release
## Payroll Component
### Cross table between employee list and selected payroll component
1. Will shown all selected employee and selected payroll component
2. This table represent relevancy matrix between employee and payroll component
3. Able to bulk edit the value using CSV file
## Tax Calculation
Will not implemented on current release
## Results

