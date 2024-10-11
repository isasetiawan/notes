## PRD Section
### Group 1
* SA.1 Client List table 
	* Typical table
* SA.2 Client status inactivation
	- Fill inactivation reason
	- When client inactivated, JWT session directly impacted
	- When client activated, inactive reason removed
	- Data Logging
		- Shown on 
			- client created at & by
		- Client data Last updated at & by
		- Only logged in BE:
		    * Client active status updated at & by
		    * Client inactive status updated at & by
			* What data was changed in Client
### Group 2
* SA.3 Client Creation
	- New data point for client creation
	- Collapsible section
	- Mandatory fields indicator
* SA.4 About Client Section
	- Organizer Renaming
	- Remove waterfall relation between Organizer and Business Type
* SA.5 Subscription & Token Config section as-is
	- Recruitment related
	- Module dropdown
		- Relate to list of menu in client portal
		- Can be different from subscription
* SA.6 Super Admin Section
	- Information related to super admin client account
	- Management Analytic Access
		- The mandatory is depends on subscription plan
* SA.7 More Client Info Section
	- Mostly no changes
	- City Field: 
		Use data related to cities table
* SA.8 Person in Charge Section
	- Different from information in super admin section
	- Phone number starts with `+62`
* SA.9 Legal Information Section
	- Consist of Tax and Client Legal Name
	- Remove Legal Docs data point
### Group 17
* C.7 Default shift pattern creation on client creation
* C.8 Default leave policy creation on client creation
* C.9 Default digital form creation on client creation
### Group 3
* SP.1 Users are able to self-serve their client registration as-is
### Group 4
* SA.11-14 Client Details Menu
	* Entry point from `Edit` button on table row
	* Consist of 3 seperated tab
		- Client Details
		- Subscription
		- Settings
	* Settings Tab Currently on for Portal Access Control for setting up admins and roles
### Group 5
* SA.15 Edit Mode of Client Details Tab
	* Expandable section from **More Client** Info to **Legal Information**
	* Handling unsaved changes
	* Handling in saving data fields changes
* SA.16 Client Status Section
* SA.17 About Client Section
### Group 6 Subscription Tab
* SA.21 Edit mode of Subscription Plan section
	* Mostly unchanged because related to recruitment platform
* SA.22 Edit Mode of Token Section
	* Handling of edit token information
	* Consist of 
		* Talent search Token
		* Job Post Token
	* Each token could be toped up or deducted using modal
* SA.23 Subscription History
	* List of history of subscription plan
	* History can be changed
* SA.24
* SA.25 Edit mode on Module Eligibility Data Point
	* The change of this data point should be directly impact to client portal user
### Group 7
* SA.26 Viewing Role list in Client details settings
	* Pagination
	* Sorting 
	* Search by role name or id
* SA.27
	* view list of module per row
* SA.28 Download template for bulk role creation
	* Reference 1
		* Module Group
		* Module Name
		* Module Access ID
	* Creation Template
		* Role Name*
		* Module Access Id* (from Reference 1)
* SA.29 Create new roles via bulk upload
	* Maximum rows is 50000
	* Enable partial success
	* Remove trailing whitespace validation 
* SA.30 Download template for bulk role update
	* Same as creation template
	* Reference
		* consist of list of module access id
* SA.31 Edit new roles via bulk upload
	* Same as creation 
### Group 8
* SA.32 Viewing list of admin in clients settings
	* Paginated
	* Sort by id
	* Search by id, name and email
* SA.33 View admin detail
	* using pop up
* SA.34 Active/Inactive Toggle
	* show dialog confirmation when changing status
	* inactivating admin affect JWT session directly
* SA.35 Download template for bulk create admin
	* When super admin created auto-assign to all branches, projects etc in the client
* SA.36 Uploading template for bulk create admin
	* Enable partial success
	* Return result of uploading process
### Group 14
* C.4 Client portal users that are not super admins are auto-assigned to a branch they created
### Group 9
* SP.2 Receiving email verification for new created client account
	* From seamless client portal and client portal
* SP.3 Users are able to change their password from seamless portal login page as-is
* SP.4 Users are able to login only from Seamless Portal to access either Recruitment or Managing portal as-is
* C.1 Remove change password functionality in Managing Client Portal
### Group 10
* D.1 Migrate existing clients to new structure after release
* D.2 Migrate existing roles to new structure after release
* D.3 Migrate existing admins to new structure after release
### Group 13
* SP.6 List of admin mirrored from admin table from Seamless client portal
	* Handle Nano ID
	* 
* SP.7 Ability to add admin
	* Handle branch and project assignment for super admin, automatically assigned to add branch and project, add label to place holder
* SP.8 Ability to edit admin
	* Entry point from see details
* SP.9 Ability to toggle admin status active or inactive
	* same impact as seamless portal admin
	* for super admin, status cannot be changed
	* activating validation
		* need to do email verification
### Group 15
* C.5 Add data restriction by current client agent and branch assignment
* C.6 