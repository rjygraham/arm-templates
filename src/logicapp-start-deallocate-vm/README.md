# Start/Deallocate VM

This template deploys a Logic App that executes a Resource Graph query to find all VMs tagged with a specific time to be started or deallocated. If VMs are found that match the current time, the Logic App proceeds in started or deallocating all matched VMs.

## Setup

```bash
az group create -g VM-AUTOMATION -l eastus
az group deployment create -g VM-AUTOMATION --template-uri https://raw.githubusercontent.com/rjygraham/arm-templates/main/src/logicapp-start-deallocate-vm/azuredeploy.json
```
or...

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frjygraham%2Farm-templates%2Fmain%2Fsrc%2Flogicapp-start-deallocate-vm%2Fazuredeploy.json) 

Once the Logic App is deployed, grant the system assigned managed identity at least Virtual Machine Contributor over the scope in which you'd like the Logic App to manage VMs.

You also need to edit the Logic App and provide the credentials to the ARM and AzureVM connectors.