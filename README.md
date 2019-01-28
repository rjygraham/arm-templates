# ARM Templates

A collection of helpful Azure Resource Manager templates.

## ARM CopyIndex Aggregate Outputs
This template shows how to aggregate the outputs of linked templates inside a copy operation.

Useful for when you need to have downstream ARM dependencies on values generated in each iteration of the copy operation. For example, if you have to whitelist new created static Public IP addresses on Storage Accounts.

This template doesn't deploy any resources.

```bash
az group create -g arm-copyindex-aggregate-outputs -l eastus
az group deployment create -g arm-copyindex-aggregate-outputs --template-uri https://raw.githubusercontent.com/rjygraham/arm-templates/master/src/arm-copyindex-aggregate-outputs/azuredeploy.json
```
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frjygraham%2Farm-templates%2Fmaster%2Fsrc%2Farm-copyindex-aggregate-outputs%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>