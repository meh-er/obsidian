
#SaN 

## Security Misconfiguration
The whole web app stack must be secured!
- Make sure **up to date** wrt security patches
	- OS, Web/App Server/ DBMS, app framework, libs...
- Disable **unnecessary features**
	- Default accounts, demo pages, debug interfaces
- Use **minimum privilege**
	- Separate concerns, ACLs per component/app
- Ensure **error handling does not expose info** 
	- Customers should not see actual stack errors ever
- Have a **repeatable security config process**
	- An app-specific checklist to work through
	- Uniform config for development, QA, deployment
- Have an **automated checking process**
	- Ensure configuration security