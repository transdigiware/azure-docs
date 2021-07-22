---
title: Deploy SAP S/4HANA or BW/4HANA on an Azure VM | Microsoft Docs
description: Deploy SAP S/4HANA or BW/4HANA on an Azure VM
services: virtual-machines-linux
documentationcenter: ''
author: hobru
manager: timlt
editor: ''
tags: azure-resource-manager
keywords: ''

ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/26/2021
ms.author: hobruche

---
# SAP Cloud Appliance Library

The [SAP Cloud Appliance Library](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) enables you to quickly create a demo environment with a fully preconfigured SAP system. Within a few clicks, you can have your SAP system up and running. The following links highlight several solutions that you can quickly deploy on Azure. Just select  the "Create Instance" link. 

You will need to authenticate with your S-User or P-User. You can create a P-User free of charge via the [SAP Community](https://community.sap.com/).  Find more details outlined below.

| Solution | Link |
| -------------- | :--------- | 
| **SAP S/4HANA 2020 FPS01, Fully-Activated Appliance**  Apr 21, 2021 | [Create Instance](https://cal.sap.com/registration?sguid=a0b63a18-0fd3-4d88-bbb9-4f02c13dc343&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
|This appliance contains SAP S/4HANA 2020 (FPS01) with pre-activated SAP Best Practices for SAP S/4HANA core functions, and further scenarios for Service, Master Data Governance (MDG), Transportation Mgmt. (TM), Portfolio Mgmt. (PPM), Human Capital Management (HCM), Analytics, Migration Cockpit, and more. User access happens via SAP Fiori, SAP GUI, SAP HANA Studio, Windows remote desktop, or the backend operating system for full administrative access. |  [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/a0b63a18-0fd3-4d88-bbb9-4f02c13dc343) | 
| **SAP S/4HANA 2020 FPS02**  Jun 10, 2021 | [Create Instance](https://cal.sap.com/registration?sguid=c7cff775-cbf7-4cd1-a907-6eeca95a0946&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
| This solution comes as a standard S/4HANA system installation including a remote desktop for easy frontend access. It contains a pre-configured and activated SAP S/4HANA Fiori UI in client 100, with prerequisite components activated as per SAP note 3045635 Rapid Activation for SAP Fiori in SAP S/4HANA 2020 FPS02. See More Information Link. | [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/c7cff775-cbf7-4cd1-a907-6eeca95a0946) | 
| **SAP Business One 10.0 PL02, version for SAP HANA**   Aug 4, 2020 | [Create Instance](https://cal.sap.com/registration?sguid=371edc8c-56c6-4d21-acb4-2d734722c712&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
|Trusted by over 70,000 small and midsize businesses in 170+ countries, SAP Business One is a flexible, affordable, and scalable ERP solution with the power of SAP HANA. The solution is pre-configured using a 31-day trial license and has a demo database of your choice pre-installed. See the getting started guide to learn about the scope of the solution and how to easily add new demo databases.| [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/371edc8c-56c6-4d21-acb4-2d734722c712) | 
| **SAP Financial Services Data Platform 1.13**  Jun 6, 2021 | [Create Instance](https://cal.sap.com/registration?sguid=5e351903-8fbe-40ce-b7ae-8ec53cb1ddb8&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
|SAP Financial Services Data Management aims to support customers in the building of a data platform for the banking and insurance industries on SAP HANA. It helps the customer to reduce redundancies by managing enterprise data with a \"single source of truth\" approach through a harmonized integrated data model.|  [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/5e351903-8fbe-40ce-b7ae-8ec53cb1ddb8) | 
| **SAP S/4HANA 1909 FPS02, Fully-Activated Appliance**  Jul 1, 2020 | [Create Instance](https://cal.sap.com/registration?sguid=2c257186-95e8-4be7-b218-909ba4328add&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
|This appliance contains SAP BusinessObjects BI Platform 4.3 Support Package 1 Patch 4: (i) On the Linux instance, the BI Platform and Web Intelligence servers are running on the default installed Tomcat (ii) On the Windows instance, you can use the SAP BI SP1 Patch 4 version of the clients tools to connect to the server: Web Intelligence Rich Client, Information Design Tool, Universe Design Tool.|  [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/2c257186-95e8-4be7-b218-909ba4328add) | 
| **SAP BusinessObjects Business Intelligence platform 4.3 SP01**  May 25, 2021 | [Create Instance](https://cal.sap.com/registration?sguid=d493ec12-e9ec-4000-9164-30bacc56b412&provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) |
|This appliance contains SAP BusinessObjects BI Platform 4.3 Support Package 1 Patch 4: (i) On the Linux instance, the BI Platform and Web Intelligence servers are running on the default installed Tomcat (ii) On the Windows instance, you can use the SAP BI SP1 Patch 4 version of the clients tools to connect to the server: Web Intelligence Rich Client, Information Design Tool, Universe Design Tool.|  [Details](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8#/solutions/d493ec12-e9ec-4000-9164-30bacc56b412) | 



---







## Setup and get started with SAP Cloud Appliance Library

> [!NOTE]
> For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/catalog?provider=208b780d-282b-40ca-9590-5dd5ad1e52e8) website. SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
> As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL. We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.

## Create an account in the SAP CAL
1. To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP. Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure. In the account definition, you need to:

    a. Select the deployment model on Azure (Resource Manager or classic).

    b. Enter your Azure subscription. An SAP CAL account can be assigned to one subscription only. If you need more than one subscription, you need to create another SAP CAL account.

    c. Give the SAP CAL permission to deploy into your Azure subscription.

    > [!NOTE]
    > The next steps show how to create an SAP CAL account for Resource Manager deployments. If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account. The new SAP CAL account needs to deploy in the Resource Manager model.

2. Create a new SAP CAL account. The **Accounts** page shows three choices for Azure: 

    a. **Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.

    b. **Microsoft Azure** is the new Resource Manager deployment model.

    c. **Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.

    To deploy in the Resource Manager model, select **Microsoft Azure**.

    ![SAP CAL Account Details](./media/cal-s4h/s4h-pic-2a.png)

3. Enter the Azure **Subscription ID** that can be found on the Azure portal.

   ![SAP CAL Accounts](./media/cal-s4h/s4h-pic3c.png)

4. To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**. The following page appears in the browser tab:

   ![Internet Explorer cloud services sign-in](./media/cal-s4h/s4h-pic4c.png)

5. If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected. The following page appears in the browser tab:

   ![Internet Explorer cloud services confirmation](./media/cal-s4h/s4h-pic5a.png)

6. Click **Accept**. If the authorization is successful, the SAP CAL account definition displays again. After a short time, a message confirms that the authorization process was successful.

7. To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.

   ![Account to user association](./media/cal-s4h/s4h-pic8a.png)

8. To associate your account with the user that you use to sign in to the SAP CAL, click **Review**. 
 
9. To create the association between your user and the newly created SAP CAL account, click **Create**.

   ![User to SAP CAL account association](./media/cal-s4h/s4h-pic9b.png)

You successfully created an SAP CAL account that is able to:

- Use the Resource Manager deployment model.
- Deploy SAP systems into your Azure subscription.

Now you can start to deploy S/4HANA into your user subscription in Azure.

> [!NOTE]
> Before you continue, determine whether you have required Azure core quotas. Some solutions in SAP CAL uses M-Series VMs of Azure to deploy some of the SAP HANA-based solutions. Your Azure subscription might not have any M-Series core quotas. If so, you might need to contact Azure support to get a required quota.

> [!NOTE]
> When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region. To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP. You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.

## Deploy a solution

Let's deploy a solution from the **Solutions** page of the SAP CAL. The SAP CAL has two sequences to deploy:

- A basic sequence that uses one page to define the system to be deployed
- An advanced sequence that gives you certain choices on VM sizes 

We demonstrate the basic path to deployment here.

1. On the **Account Details** page, you need to:

    a. Select an SAP CAL account. (Use an account that is associated to deploy with the Resource Manager deployment model.)

    b. Enter an instance **Name**.

    c. Select an Azure **Region**. The SAP CAL suggests a region. If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.

    d. Enter a master **Password** for the solution of eight or nine characters. The password is used for the administrators of the different components.

   ![SAP CAL Basic Mode: Create Instance](./media/cal-s4h/s4h-pic10a.png)

2. Click **Create**, and in the message box that appears, click **OK**.

   ![SAP CAL Supported VM Sizes](./media/cal-s4h/s4h-pic10b.png)

3. In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL. To use password protection for the private key, click **Download**. 

   ![SAP CAL Private Key](./media/cal-s4h/s4h-pic10c.png)

4. Read the SAP CAL **Warning** message, and click **OK**.

   ![SAP CAL Warning](./media/cal-s4h/s4h-pic10d.png)

    Now the deployment takes place. After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.

5. To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal: 

   ![SAP CAL objects deployed in the new portal](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. On the SAP CAL portal, the status appears as **Active**. To connect to the solution, click **Connect**. Different options to connect to the different components are deployed within this solution.

   ![SAP CAL Instances](./media/cal-s4h/active_solution.png)

7. Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**. 

   ![Connect to the Instance](./media/cal-s4h/connect_to_solution.png)

    The documentation names the users for each of the connectivity methods. The passwords for those users are set to the master password you defined at the beginning of the deployment process. In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system. 

    For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:

   ![SM50 in the preinstalled SAP GUI](./media/cal-s4h/gui_sm50.png)

    Or if you use the DBACockpit, the instance might look like this:
 

   ![SM50 in the DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.

If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure. The support queue is BC-VCM-CAL.







