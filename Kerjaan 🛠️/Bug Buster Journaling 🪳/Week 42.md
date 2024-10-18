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
	* Status
* **Tidak bisa submit form "Tidak dapat terhubung ke server SE500"**
	* Thread
	* Issue
	* Solution
	* Status