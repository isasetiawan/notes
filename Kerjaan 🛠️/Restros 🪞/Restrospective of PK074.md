# Topic 1: A significant number of production bugs were reported one week after the release of PK074

## Expectation
**No major bug after released**
## Actual
2 Major bug reported in #supportcenter related to 
1. Guard issue & super admin permission 
2. Employee can’t do onboard (401)
## Retrospective From BE
1. Existing implementation not properly covered
	1. RBAC guard
	2. Create a new RBAC with changes scope for RBAC. e.g: move recruitment as modules
	3. Hidden condition from existing services, e.g accountsvc, ssosvc
	4. Mongodb usage
	5. Unideal existing implementation of distributed system
2. Improper scoping strategy at first, resulting in release scope too large (large risk also) which result in too many scopes to check to handle in a single release
	1. Should split into several sub scopes, release by each scopes, e.g.:
	2. Feature flagging for disabling role and account modification, followed by release 
	3. Fixing RBAC issue by creating in house RBAC, followed by release
	4. Improvement on management of client and client account in seamless admin, followed by release
	5. Modification on client account modification to seamless portal, followed by release
## Retrospective From FE
1. Scope too large which impacts to the several codebases (SP, SAP), lack of knowledge of current implementation codebase (missing the context of current impl)
2. Missing second sprint context resulting missing too much information to release preparation
3. Lack of visit implementation codebase thoroughly since the spec is too large and contains several repositories are involve (some libraries are quite different) resulting in different code approach
### Questions
1. Should we have some kind of short meeting before release to fill up each other knowledge so the PIC have all the information
## Action Items, PIC and Timeline

