# GetYourDataOut - Export log analytics data to Azure blob storage.

A simple Jupyter notebook to export your log analytics tabels to a storage account.   
After configuring the values, the notebook will run kql query in the set time interval.   
Events are grouped into parquest files by a specified time interval.  
It will save the returned data to the storage account in time formated path(y=XXXX/m=XX/d=XX/h=XX).

## Requirements
- Azure Log Analytics Workspace - Where data will be exported from.
- Computing service             - To run a Jupyter python notebook (Databricks | Azure notebooks | Your own solution)
- Azure Data Lake               - To store the exported data.
- Azure app registration        - With Log Analytics reader permisions.
- Key-Vault                     - To store your secrets (do this insted of saving secrets in your code).

## Note
Before running the notebook, you will need to manully create the expected container under the DataLake. 
export-<tablename> in lowercase letters.

For example:
- AuditLogs -> export-auditlogs

## Usage
Set the configuration values and run the script :)  
For automaticlly exporting the data, set a Databricks job to run the notebook (or other scheduling service of your choice). 

## Configuration

Variable | Description
:--- | :---
storage_account | name of the Azure storage account.
tenant_id | id of your Azure tenant.
scope_name | name of your databricks secrets scope.
aad_appid | id of your azure ad app registration.
workspace_id | id of your log analytics workspace.
service_credential_key_name_storage_key | name of your storage key-vault secret.
service_credential_key_name_datalake | name of your datalake key-vault secret.
service_credential_key_name_service_principal | name of your service principal key-vault secret.
tables | comma separated list of tables to extract.
interval | time interval (in minutes) of events to bundle into one file.
days_ago | number of days ago to start collecting from.
