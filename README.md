# LAD 3.x EventHub Sink

A sample Azure Resource Manager (ARM) template demonstrating using an Azure Storage Account and EventHub Sink with Linux Azure Diagnostics (LAD) VM Extension 3.x.

This template is based on the [Very simple deployment of a Linux Ubuntu VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux) sample template.

This template deploys a **Linux VM Ubuntu** using the latest patched version. This will deploy a Standard_B2s size VM and a 18.04-LTS Version as defaultValue in the resource group location and will return the admin user name, Virtual Network Name, Network Security Group Name and FQDN.

*Important*: The template file (azuredeploy.json) includes JSON comments to help explain various features. JSON comments are compatible with the Azure Cross Platform CLI, but may not be parsable by other tools (including the Azure Portal) unless the JSON comments are manually removed.

## Prerequisites

If you are new to Azure virtual machines, see:

- [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).
- [Azure Linux Virtual Machines documentation](https://docs.microsoft.com/azure/virtual-machines/linux/)
- [Azure Windows Virtual Machines documentation](https://docs.microsoft.com/azure/virtual-machines/windows/)
- [Template reference](https://docs.microsoft.com/azure/templates/microsoft.compute/allversions)
- [Quickstart templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Compute&pageNumber=1&sort=Popular)

If you are new to template deployment, see:

- [Azure Resource Manager documentation](https://docs.microsoft.com/azure/azure-resource-manager/)
- [Quickstart: Create an Ubuntu Linux virtual machine using an ARM template](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-template)

## Overview

In addition to deploying a Linux VM, this template also demonstrates deploying the following resources in the same template and configuring them to work together:

* [Azure Storage Account (Table, Blob, Queue)](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)
* [Azure Event Hub](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features)
* Dynamically generating SAS tokens for Azure Storage and Azure Event Hub
* Installing and configuring the Linux Azure Diagnostics VM Extension using the dynamically generated SAS tokens
* Configuring LAD to write to Azure Storage and Azure Event Hub
* Collecting custom log file data
* Collecting performance counters
* Collecting syslog data

## Usage

To deploy the template via the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/), customize azuredeploy.parameters.json, then execute the following replacing `<RESOURCE_GROUP>`, `<DEPLOYMENT_NAME>` and `<LOCATION>` with the appropriate values:

``` bash
az group create --name <RESOURCE_GROUP> --location <LOCATION>

az deployment group create \
  --name <DEPLOYMENT_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --template-file azuredeploy.json \
  --parameters @azuredeploy.parameters.json
```