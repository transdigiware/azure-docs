---
title: Deploy Azure Arc data controller from Azure portal| Direct connect mode
description: Explains how to deploy the data controller in direct connect mode from Azure portal. 
author: dnethi
ms.author: dinethi
ms.reviewer: mikeray
services: azure-arc
ms.service: azure-arc
ms.subservice: azure-arc-data
ms.date: 07/13/2021
ms.topic: overview
---

#  Create Azure Arc data controller from Azure portal - Direct connectivity mode

[!INCLUDE [azure-arc-data-preview](../../../includes/azure-arc-data-preview.md)]

This article describes how to deploy the Azure Arc data controller in direct connect mode during the current preview of this feature. 

## Complete prerequisites

Before you begin, verify that you have completed the prerequisites in [Deploy data controller - direct connect mode - prerequisites](create-data-controller-direct-prerequisites.md).

## Deploy Azure Arc data controller

Azure Arc data controller create flow can be launched from the Azure portal in one of the following ways:

- From the search bar in Azure portal, search for "Azure Arc data controllers", and select "+ Create"
- From the Overview page of your Azure Arc-enabled Kubernetes cluster,
  - Select "Extensions (preview)" under Settings.
  - Select "Add" from the Extensions overview page and then select "Azure Arc data controller"
  - Select Create from the Azure Arc data controller marketplace gallery
  
Either of these actions should bring you to the Azure Arc data controller prerequisites page of the create flow.

- Ensure the Azure Arc-enabled Kubernetes cluster (Direct connectivity mode) option is selected. Select "Next : Data controller details"
- In the **Data controller details** page:
  - Select the Azure Subscription and Resource group where the Azure Arc data controller will be projected to.
  - Enter a **name** for the Data controller
  - Select a pre-created **Custom location** or select "Create new" to create a new custom location. If you choose to create a new custom location, enter a name for the new custom location, select the Azure Arc-enabled Kubernetes cluster from the dropdown, and then enter a namespace to be associated with the new custom location, and finally select Create in the Create new custom location window. Learn more about [custom locations](../kubernetes/conceptual-custom-locations.md)
  - **Kubernetes configuration** - Select a Kubernetes configuration template that best matches your Kubernetes distribution from the dropdown. If you choose to use your own settings or have a custom profile you want to use, select the Custom template option from the dropdown. In the blade that opens on the right side, enter the details for Docker credentials, repository information, Image tag, Image pull policy, infrastructure type, storage settings for data, logs and their sizes, Service type, and ports for controller and management proxy. Select Apply when all the required information is provided. You can also choose to upload your own template file by selecting the "Upload a template (JSON) from the top  of the blade. If you use custom settings and would like to download a copy of those settings, use the "Download this template (JSON)" to do so. Learn more about [custom configuration profiles](create-custom-configuration-template.md).
  - Select the appropriate **Service Type** for your environment
  - **Administrator account** - Enter the credentials for the Data controller login and password
  - **Service Principal** - Enter the Client Id, Tenant ID and the Client Secret information for the Service principal account to be used.
  - Select the "Next: Additional settings" button to proceed forward after all the required information is provided.
- In the **Additional Settings** page:
  - If you choose to upload your logs to Azure Log Analytics automatically, enter the Log Analytics workspace ID and the Log analytics shared access key
  - If you choose to NOT upload your logs to Azure Log Analytics automatically, uncheck the "Enable logs upload" checkbox.
  - Select :Next: Tags" to proceed.
- In the **Tags** page, enter the Names and Values for your tags and select "Next: Review + Create".
- In the **Review + Create** page, view the summary of your deployment. Ensure all the settings look correct and select "Create" to start the deployment of Azure Arc data controller.

## Monitor the creation from Azure portal

Selecting the "Create" button from the previous step should launch the Azure deployment overview page which shows the progress of the deployment of Azure Arc data controller.

## Monitor the creation from your Kubernetes cluster

The progress of Azure Arc data controller deployment can be monitored as follows:

- Check if the CRDs are created by running ```kubectl get crd ``` from your cluster  
- Check if the namespace is created by running ```kubectl get ns``` from your cluster
- Check if the custom location is created by running ```az customlocation list --resource-group <resourcegroup> -o table``` 
- Check the status of pod deployment by running ```kubectl get pods -ns <namespace>```

## Next steps

[Create an Azure Arc-enabled SQL managed instance](create-sql-managed-instance.md)

[Create an Azure Arc-enabled PostgreSQL Hyperscale server group](create-postgresql-hyperscale-server-group.md)
