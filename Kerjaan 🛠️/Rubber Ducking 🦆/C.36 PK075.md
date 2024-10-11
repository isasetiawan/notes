The Story
> CP Users can disburse the Payroll Report with Finalized Status from the Payroll Report Beta System by selecting the report from the option provided in the Disbursement Creation Page

List of ACs
* AC: Able to include the generated payroll report from the Payroll Report BETA system with status finalized to the disbursement creation process
	* Could be fulfilled by modify endpoint payroll report list by adding flag query param with this [task](https://www.notion.so/staffinc/Software-Design-Document-PK075-RTS-Payroll-03570d562b7c414c9342d6699fb92d50?pvs=4#ed436ca6f519498387b0ab01523ae839) 
* ACs: 
	* Able to see all the finalized employee payroll reports under the selected Payroll Report shown on the Select Agent section in the Disbursement creation process with the correct data from the generated Payroll Report beta
	* Able to select the finalized employee payroll report with filled payment information in the table list to proceed to the disbursement creation process
		* Require to check new payroll report creation on how new payroll will be related to old payroll report details
		* If the creation process also creating old payroll report details records, then this AC covered to become check current implementation only
* Able to generate the disbursement batch for the payroll report from the Payroll Report BETA system with the selected employee payroll report under it with a max 1000 transactions per batch
	* Unknown

Action:
- [ ] Check on how old payroll report details related on new payroll creation
- [ ] Simulate creation using manual query insert
- [ ] Testing the code from loca
- [ ] Create PR
- [ ] Create video proof