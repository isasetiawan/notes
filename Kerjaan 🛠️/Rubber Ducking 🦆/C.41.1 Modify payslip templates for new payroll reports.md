## Constrains
* Only for beta payroll instead
* Fetch data from new payroll report database instead
## Changes
* Template
	* Header
	* General Information
		* agent name
		* entitled month
		* client name
		* position from
		* disbursed by
		* disbursed  at
	* Allowance Component
	* Deduction Component
	* Benefit Component
	* Take Home Pay
	* Footer
* Basic information
* Password Format `YYYYNNNN`
	* `YYYY` year of entitled month
	* `NNNN` agent pone number
## Steps
* build repo to get employee payroll report
* build repo to get employee payroll report component
* gather fetched data into new model
* parse into new template
* test the result