# Crontab Start/Deallocate VM

This template deploys two Logic Apps and a Storage Account to handle starting and deallocating VMs tagged with a crontab formatted tag value.

1. The discovery Logic App is triggered on a schedule and executes a Resource Graph query to find all VMs tagged with a crontab formatted tag value that matches the current day and time and places a message on a queue to either start or deallocate the VM based on which tag matched the query.

2. The processor Logic App pulls messages from the queue and either starts or deallocates the VM. 

## Setup

```bash
az group create -g VM-AUTOMATION -l eastus
az group deployment create -g VM-AUTOMATION --template-uri https://raw.githubusercontent.com/rjygraham/arm-templates/main/Samples/logicapp-crontab-start-deallocate-vm/azuredeploy.json
```
or...

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frjygraham%2Farm-templates%2Fmain%2FSamples%2Flogicapp-crontab-start-deallocate-vm%2Fazuredeploy.json)

Once the Logic Apps are deployed, grant the system assigned managed identities a role assignment over the scopes in which you'd like the logic apps to execute.

- The discovery Logic App requires `Microsoft.Compute/virtualMachines/read` so Reader might be a good built-in role to assign this Logic App.
- The processor Logic App requires `Microsoft.Compute/virtualMachines/start/action` and `Microsoft.Compute/virtualMachines/deallocate/action`. The least privilege built-in role that includes these permissions is Virtual Machine Contributor. So you can start there or create a custom role with these specific actions.


## Crontab tags

When deploying this template, you will be asked to provide the tag names that will be searched for starting/deallocating VMs. The tag value values should be in the [crontab](https://en.wikipedia.org/wiki/Cron) format:
```
 ┌───────────── minute (0 - 59)
 │ ┌───────────── hour (0 - 23)
 │ │ ┌───────────── day of the month (1 - 31)
 │ │ │ ┌───────────── month (1 - 12)
 │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
 │ │ │ │ │                                   7 is also Sunday on some systems)
 │ │ │ │ │
 │ │ │ │ │
 * * * * *
```

Currently, this solution requires the following values in the crontab expression:

- Minute and hour components of the contab must be numerical and not `*`.
- Day of the month and month components must be `*`. 
- Day of the week component must be a single number or comma separated list of numbers.

### Examples

Some examples of valid crontab pairs.

Start VMs every weekday at 7am ET and deallocate them every weekday at 7pm ET:

|Tag Key|Tag Value|
|-|-|
|StartCron|0 11 * * 1,2,3,4,5|
|DeallocateCron|0 21 * * 1,2,3,4,5|

Start VMs every Monday at 7am ET and deallocate them every Friday at 7pm ET:
|Tag Key|Tag Value|
|-|-|
|StartCron|0 11 * * 1|
|DeallocateCron|0 21 * * 5|

## Limitations

This solution currently has the limitation of returning 1000 records from the Resource Graph query. If you anticipate having more than 1000 results at a time, you can easily modify the processor Logic App to loop through the subscriptions and execute a Resource Graph query per subscription instead of sending a single query for all subscriptions.

## License


The MIT License (MIT)

Copyright © 2020 Ryan Graham

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.