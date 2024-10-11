Context:
> Planned solution to generating payslip PDF file is to use generated Jinja template then convert it into PDF using existing library called wkhtmltopdf. The template is created by FE and passed to BE repo in order to be use

Problems:
> There is unsupported flex box css by wkhtmltopdf causing the generated psd is messy since the engine used by wkhtmltopdf is QTWebKit which considered [obsolete](https://wkhtmltopdf.org/status.html)

Decision Tree:
* Rewrite html template to support the old engine
	* cons:
		* Doubting to keep obsolete library
		* Limiting template expression by obsolete lib
	* pros:
		* Template could be generated directly
* Exploring other library
	* weasyprint
		* cons
			* has same issue with wkhtmltopdf
			* unsupported css flexbox
	* xhtmltopdf
		* cons
			* there is no way to debug the issue
	* headless browsers
		* cons
			* hypothetically high usage of CPU/Memory usage
			* contains unknown risk
		* pros
			* Generated PDF is expected
			* No style sheet constraint
			* FE able to express the template using latest CSS style