This Logic App is used to Pause, Resume, Dial-Up and Dial-Down an instance of Azure Synapse Dedicated SQL Pool. 

## Usage
The logic app is invoked by calling the REST API endpoint. It supports the following parameters. The parameters are passed in the request body.

|Parameters|Values|
|:---------|:-----|
|action|pause, resume, dialup, dialdown|
|sku||
|subscriptionId|Azure Subscription ID|
|workspaceName|Synapse Analytics Workspace Name|
|sqlPoolName|Name of Dedicated SQL Pool|
|apiVersion| Version of Synapse Analytics REST API, Default value of 2021-03-01|

### Sample Request Body
```json
{
"action": "dialdown",
"sku": "DW500c",
"subscriptionId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"resourceGroupName": "MySynapseResourceGroup",
"workspaceName": "MySynapseWorkspace",
"sqlPoolName": "MySQLPool",
"apiVersion": "2021-03-01"
}

```

## Pre-Requisites
 - Grant the Managed Identity of this Logic App the Contibutor role to the Synapse Dedicated SQL Pool that you wish to manage
 - Grant the Managed Identity of this Logic App the db_owner role to the Synapse Dedicated SQL Pool that you wish to manage
```sql
CREATE USER [logic-app-name] FROM EXTERNAL PROVIDER
GO

EXEC sp_addrolemember 'db_owner', [logic-app-name]
GO
```
