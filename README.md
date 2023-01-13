# logicapp-synapse-sqlpool
Logic App to Pause, Resume, Dial-Up and Dial-Down Synapse Dedicated SQL Pool

## Pre-Requisites
 - Grant the Managed Identity of this Logic App the Contibutor role to the Synapse Dedicated SQL Pool that you want to manage
 - Grant the Managed Identity of this Logic App the db_owner role to the Synapse Dedicated SQL Pool that you want to manage
```sql
CREATE USER [logic-app-name] FROM EXTERNAL PROVIDER
GO

EXEC sp_addrolemember 'db_owner', [logic-app-name]
GO
```
## Deploy project to Azure using Powershell Az module
From PowerShell console execute the following commands
```console
cd 'bin folder'
Connect-AzAccount -Tenant XX-YY-ZZ -Subscription XX-YY-ZZ
.\Deploy-AzureResourceGroup.ps1 -ArtifactStagingDirectory . -TemplateFile LogicApp.json -TemplateParametersFile LogicApp.parameters.json
```

## HTTP Trigger POST Payload Schema

```json
{
  "type": "object",
  "properties": {
    "action": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "subscriptionId": {
      "type": "string"
    },
    "resourceGroupName": {
      "type": "string"
    },
    "workspaceName": {
      "type": "string"
    },
    "sqlPoolName": {
      "type": "string"
    },
    "apiVersion": {
      "type": "string"
    }
  }
}
```

For example the body payload will look like this:
```json
{
    "action": "pause", #valid values - pause, resume, scale
    "sku": "DW100c",
    "subscriptionId": "XXX-YYY-ZZZ",
    "resourceGroupName": "rg-dataplatform",
    "workspaceName": "ba-synapseanalytics01",
    "sqlPoolName": "dw01",
    "apiVersion": "2021-03-01"
 }
```
