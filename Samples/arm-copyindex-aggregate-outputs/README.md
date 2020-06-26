# ARM CopyIndex Aggregate Outputs

This template shows how to aggregate the outputs of linked templates inside a copy operation.

Useful for when you need to have downstream ARM dependencies on values generated in each iteration of the copy operation. For example, if you have to whitelist new created static Public IP addresses on Storage Accounts.

This template doesn't deploy any resources.

```bash
az group create -g arm-copyindex-aggregate-outputs -l eastus
az group deployment create -g arm-copyindex-aggregate-outputs --template-uri https://raw.githubusercontent.com/rjygraham/arm-templates/main/Samples/arm-copyindex-aggregate-outputs/azuredeploy.json
```
or...

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frjygraham%2Farm-templates%2Fmain%2FSamples%2Farm-copyindex-aggregate-outputs%2Fazuredeploy.json)