* **Overtime sudah di approved namun masih muncul di page pending approval request**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727068092951439
	* Issue
		* Same issue with [this](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1722324050129839)
		* Chronology
			* Agent create overtime request on same date
			* CP user approve the request
			* Agent create overtime request on same date again
		* Expected
			* pending request should be hide from pending approval page
		* Current Status
			* No decision taken from first issue
			* Short term available
*  **Issue OTP Staffinc Jobs**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727079003577519
	* Issue
		* Related to previous OTP issue
	* Current Status
		* Short-term available
		* By inserting mongo db document on `otps` collections
* **client confirmation token expiration time cuma 5 menit**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727119318477999
	* Issue
		* Miss-configured email token expiry period from from 300s to 259200
	* Current Status
		* Fixed by creating pr to repo `infra-kerjaan`
* **Status attendance salah**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727152766032229
	* Issue
		* Chronology
			* 2024-08-11 10:03:20.504243 +00:00
				* Create Leave request
				* For 31 Aug and 1 Sept
			* 2024-08-12 02:01:15.246951 +00:00
				* Leave Request Approved
				* 1st layer
			* 2024-08-12 02:56:30.022623 +00:00
				* Leave Request Approved
				* 2nd Layer
			* 2024-09-17 04:44:51.332605 +00:00
				* Dispute Created
				* For attendance 1 Sept change status to approved
			* 2024-09-17 09:17:42.433909 +00:00
				* Dispute Approved
			* 2024-09-17 09:17:42.523032 +00:00
				* Agent Request Become rejected
				* Attendance at 31 Aug status getting WCI
		* Missing link
			* The dispute request created is changes from `waiting from checking` to `present`
			* Meanwhile, current status at at the time dispute created is `rejected`
		* Possibilities
			* Relate to issue attendance status not change by approved leave request
			* Cron job that used to generate daily attandance
	* Current Status
		* Short-term available
		* Unable to reproduce 
* **Status disbursement masih in progress sampai skrg, padahal sudah diproses disbursement sejak jam 9 pagi.**
	* Thread 
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727253951336949
	* Issue
		* Disbursement stuck at pending status due to there is one transaction with OCBC bank still pending from xendit
		* Require to generate payslip regardless of disbursement status
		* Script to generate pay-slip from local
	* Current Status
		* AFI related
		* Short term available
	* **Todo**
		* Announce to considered bug if still pending in range 24 hour after request
		* If payslip required to be generated, request for short-term request instead
		* Share the script
* **Tidak bisa mendaftarkan new partner**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727345453979779
	* Issue
		* [sentry](https://sentry.staffinc.co/organizations/staffinc/issues/7421/?project=2&query=is:unresolved&stream_index=1)
		* Not null violation on `report_assignment_id`
		* The id should be fetched or created based on the code
		* Try with case report assignment is soft deleted
	* Current Status
		* Intermittent
		* Not happened again

* **Ketika mendaftarkan new partner, setelah diapprove. status inactive, assigned agent nya blank, latlong nya tidak tereflect di databasenya**
	* Thread
		* https://staffinc-co.slack.com/archives/C015UUA1K8F/p1727346093096939
	* Issue
		* Created partner from agent became inactive
		* Lat long not stored from partner creation from agent
			* Due to incorrect API contract
		* Created partner not auto assigned to agent considered as AFI
	* Current Status
		* Hot-fixed
# Action Items
- [ ] Check on SLO due to SSE endpoints
# Performance
* Performance ([here](https://app.datadoghq.com/dashboard/kcv-mwi-fwb/kerjaan-service-monitoring?fromUser=false&fullscreen_end_ts=1726794753395&fullscreen_paused=false&fullscreen_refresh_mode=sliding&fullscreen_section=overview&fullscreen_start_ts=1726189953395&fullscreen_widget=7475676929454144&refresh_mode=sliding&from_ts=1726189914863&to_ts=1726794714863&live=true))
	- 272ms -> 272ms
* SLO Metric ([here](https://app.datadoghq.com/dashboard/pa7-5ag-3g5/kerjaan-be-dashboard?fromUser=true&refresh_mode=paused&from_ts=1725940320000&to_ts=1726545420000&live=false))
	* Kerjaansvc  99.32% -> 98.35%
	* Filesvc 98.85% -> 98.98%
	* SLO Metric HCMSVC ([here](https://app.datadoghq.com/dashboard/7ey-w3w-ric/hcmsvc-monitoring?fromUser=false&refresh_mode=sliding&from_ts=1725940714319&to_ts=1726545514319&live=true))
	* Hcmsvc 98.5% -> 98.155%
