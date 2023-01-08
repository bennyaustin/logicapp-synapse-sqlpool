# logicapp-synapse-sqlpool
Logic App to Pause, Resume, Dial-Up and Dial-Down Synapse Dedicated SQL Pool

## Pre-Requisites
 - Grant the Managed Identity of this Logic App the Contibutor role to the Synapse Dedicated SQL Pool that you wish to manage
 - Grant the Managed Identity of this Logic App the db_owner role to the Synapse Dedicated SQL Pool that you wish to manage
```sql
CREATE USER [logic-app-name] FROM EXTERNAL PROVIDER
GO

EXEC sp_addrolemember 'db_owner', [logic-app-name]
GO
```
## Deploy project to Azure using Powershell Az module
From PowerShell console execute the following commands
- cd 'bin folder'
- Connect-AzAccount -Tenant XX-YY-ZZ -Subscription XX-YY-ZZ
- .\Deploy-AzureResourceGroup.ps1 -ArtifactStagingDirectory . -TemplateFile LogicApp.json -TemplateParametersFile LogicApp.parameters.json
