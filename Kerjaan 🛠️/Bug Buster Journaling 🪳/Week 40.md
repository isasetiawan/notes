
| Critical | Medium | Non Bug | AFI | Oncall |
| -------- | ------ | ------- | --- | ------ |
| 0        | 4      | 2       | 4   | Rifan  |
* OTP Issue  
  * Thread  
    * https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727746484880429  
  * Root Cause  
    * Current tier for OTP Blast is 1000  
  * Current Status  
    * Short Term Available  
      * OTP Via SMS  
      * If OTP Via SMS not working, set default OTP  
* Can’t download payslip because the success disbursement was overridden by the previous disbursement which has failed status  
  * Thread  
    * https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727796449575249  
  * Issue  
    * User create disbursement for payroll report A, then reject this first disbursement  
    * Callback from this first disbursement was failed until twice attempt  
    * User create another disbursement for payroll report A, then approve this disbursement  
    * Callback from this second disbursement was success  
    * Callback from the first disbursement was success and overriding the callback from the second disbursement  
  * Current Status  
    * Done, update is\_paid into True for the corresponding disbursement details  
  * Long Term  
    * How to prevent override callback :   
      * AFI If is_paid true, can’t be overridden  
* Can’t create password when create admin in Seamless Admin Portal  
  * Thread   
    * [https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727852841241659](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727852841241659)  
  * Issue   
    * Related sentry error : [https://sentry.sampingan.co/sampingan/accountsvc/issues/29440/?query=is%3Aunresolved](https://sentry.sampingan.co/sampingan/accountsvc/issues/29440/?query=is%3Aunresolved)  
    * Clients don’t have Recruitment Portal ID (old data). The current client creation should always generate Recruitment Portal ID  
  * Current Status  
    * By updating the client’s data, the endpoint InternalUpdateClient will automatically generate Recruitment Portal ID  
    * Engineers provide a list of clients who don’t have a Recruitment Portal ID, so that Business Ops can modify it to prevent the same issue from happening in the future.
* Status disbursement in queue dan tidak ada datanya dalam Seamless
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1728128591439219
	* Root Cause:
		* one worker inactive 
		* client_export_payslip_to_email