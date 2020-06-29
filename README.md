# ARM Templates

A collection of helpful Azure Resource Manager templates.

## ARM CopyIndex Aggregate Outputs
This template shows how to aggregate the outputs of linked templates inside a copy operation.

Useful for when you need to have downstream ARM dependencies on values generated in each iteration of the copy operation. For example, if you have to whitelist new created static Public IP addresses on Storage Accounts.

This template doesn't deploy any resources.

[arm-copyindex-aggregate-outputs](Samples/arm-copyindex-aggregate-outputs)

## Start/Deallocate VM

This template deploys a Logic App that executes a Resource Graph query to find all VMs tagged with a specific time to be started or deallocated. If VMs are found that match the current time, the Logic App proceeds in started or deallocating all matched VMs.

[logicapp-start-deallocate-vm](Samples/logicapp-start-deallocate-vm)

## Crontab Start/Deallocate VM

This is the successor of the Start/Deallocate VM template. This template deploys a solution that will identify VMs tagged with a crontab formatted tag value and will start/deallocate the VM if the crontab value matches the current execution time.

[logicapp-crontab-start-deallocate-vm](Samples/logicapp-crontab-start-deallocate-vm)