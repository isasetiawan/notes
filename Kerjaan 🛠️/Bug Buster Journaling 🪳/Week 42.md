# Issues

* **Tidak bisa submit form**
	* Thread
		* [Link](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1728880126658379)
	* Issue
		* Continued from previous issue where skipped unique question is still validated
		* Skipped answer is excluded from validation [link](https://github.com/sampingantech/kerjaansvc/blob/31b8a1b0c3f3dda651020345992c9cc300b0aa65/app/library/jsonschema/main.py#L831-L846)
		* But the question schema not excluded before validation
	* Solution
		* Exclude skipped answers from question schema
		* [pull request](https://github.com/sampingantech/kerjaansvc/pull/5399)
	* Status
		* Deployed
* **attendance recap hilang dari tgl 7-17 september, namun di aplikasi staffinc work terdapat riwayatnya**
	* Thread
		* [Link](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1728902785409919)
	* Issue
		* Employee branch are changed over time
		* The employee has been unassigned from the branch
	* Solution
		* Consider not null previous branch
		* Line of [code](https://github.com/sampingantech/kerjaansvc/blob/d2c2ff64ee2a6944970ce7bec02a50c435f6ff49/app/models/branch_agents.py#L79-L84)
	* Status
		* Still testing on export attendance data
* **Tidak bisa submit form "Tidak dapat terhubung ke server SE500"**
	* Links
		* [Thread](https://staffinc-co.slack.com/archives/C015UUA1K8F/p1728965476906379)
		* [Sentry](https://sentry.staffinc.co/organizations/staffinc/issues/7749/?project=2&query=is:unresolved&stream_index=0)
	* Issue
		* Error happened due to when there is an error located in the root of question schema  [code](https://github.com/sampingantech/kerjaansvc/blob/2fb06fe6e1f83135d196ecae4c2a047901263d75/app/library/jsonschema/main.py#L594-L614) 
		* The error is not expected because the section is missing
		* The validation of missing section is required to ensure the chosen path of the section [code](https://github.com/sampingantech/kerjaansvc/blob/2fb06fe6e1f83135d196ecae4c2a047901263d75/app/library/jsonschema/main.py#L558-L562)
		* The missing section is caused by the removal of skipped answer from previous fix
	* Solution
		* Include skipped section as empty dictionary
		* Handle root validation of the schema 
	* Status
		* Deployed