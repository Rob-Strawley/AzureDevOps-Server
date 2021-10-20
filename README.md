# AzureDevOps Server 2020
Information related to Azure DevOps Server

## Upgrade from TFS to DevOps Server on new hardware and new domain ##
Summary from the Microsoft Documentation- https://docs.microsoft.com/en-us/azure/devops/server/admin/move-across-domains?view=tfs-2018

### Prepare TFS ###
* Empty TFS Cache by copying and moving to another Folder, save for archiving. If cache is not empty, you may experience errors when importing TFS Databases into DevOps Server
* Conduct Full Backup of TFS Databases for archiving purposes, these will not be used for the actual import into Devops
* Stop TFS Server via command line: "TFSServicecontrol Quiesce"
* Detach Collections from TFS Console only, do NOT detach using SQL Server Management Studio
* Manually backup each TFS Database/Collection using SQL Server using SQL Server Management Studio

### SQL Server for DevOps Server ###
* SQL- Build SQL Server for DevOps Server (must be equal to or higher SQL version than TFS SQL Server)
* SQL- Add Admin and Service accounts to Server Roles (serveradmin and sysadmin)
* SQL- Add same accounts to server Logins
* SQL- Ensure SQL Server Agent is running

### DevOps Server ###
* Build DevOps Server per docs. For airgapped environments download Zulu8 Java and install. 
* Enter Java install as a System Environment variable path: JAVA_HOME C:\Program Files\Zulu\zulu8\, otherwise server may not recognize install

### Import TFS Collections ###
* Manually restore each TFS Collection in SQL Server for DevOps Server (may have to add option to REPLACE)
* Configure DevOps Server to use Existing database from the TFS restored databases
* Attach imported TFS Collections to DevOps Server instance
* Change users domain via command line: "TFSConfig identities /change /fromdomain:old.domain /todomain:new.domain
* Test URL
* Configure Backups
* Join DevOps Server to new domain
* Restart Server



## Import Work Items using csv ##
* Install TFS Standalone Office Integration installer (for using Excel)
* Create a Query based on Work Item Type (Any, Feature, etc.)
* Select "Open in Excel"
* Prepend Work Item ID numbers to the Title Column
* Delete all values under ID Column, DevOps will not recognize imported ID numbers, hence the prior prepend instruction
* Modify Columns to reflect the supported Column Order: ID,Work Item Type, Title, Assigned To, State, Area Path, Tags
* Must enter data in Work Item Type cells
* Save as csv
* Import into Azure DevOps Boards
* Import Item Limitations- https://docs.microsoft.com/en-us/azure/devops/organizations/settings/work/object-limits?view=azure-devops-2020

## Import Test Plans using csv ##
* Test Plans can only be imported individually by Test Suite, not as bulk. View Individual Test Suites in Grid View
* Select all fields
* Copy and Paste into an Excel Spreadsheet
* Prepend Work Item ID numbers to the Title Column
* Delete all values under ID Column, DevOps will not recognize imported ID numbers, hence the prior prepend instruction
* Must enter data in Work Item Type cells
* Must add a Revision number
* Modify Columns to reflect the supported Column Order: ID,Work Item Type, Title, Test Step, Step Action, Step Expected, Revision, Area Path, Assigned to, State
* Save as csv
* Import into Azure DevOps Test Plan




