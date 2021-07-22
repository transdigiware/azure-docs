---
title: Deploy and configure Azure VMware Solution
description: Learn how to use the information gathered in the planning stage to deploy and configure the Azure VMware Solution private cloud.
ms.topic: tutorial
ms.custom: contperf-fy22q1, devx-track-azurecli
ms.date: 07/09/2021

---

# Deploy and configure Azure VMware Solution

In this article, you'll use the information from the [planning section](production-ready-deployment-steps.md) to deploy and configure Azure VMware Solution. 

The diagram shows the deployment workflow of Azure VMware Solution. 

:::image type="content" source="media/deploy-azure-vmware-solution-workflow.png" alt-text="Diagram of the Azure VMware Solution deployment workflow." lightbox="media/deploy-azure-vmware-solution-workflow.png" border="false":::

## Step 1. Register the **Microsoft.AVS** resource provider

[!INCLUDE [register-resource-provider-steps](includes/register-resource-provider-steps.md)]

## Step 2. Create an Azure VMware Solution private cloud

[!INCLUDE [create-private-cloud-azure-portal-steps](includes/create-private-cloud-azure-portal-steps.md)]

>[!NOTE]
>For an end-to-end overview of this step, view the [Azure VMware Solution: Deployment](https://www.youtube.com/embed/gng7JjxgayI) video.


## Step 3. Connect to Azure Virtual Network with ExpressRoute

In the planning phase, you defined whether to use an *existing* or *new* ExpressRoute virtual network gateway.  

:::image type="content" source="media/connect-expressroute-vnet-workflow.png" alt-text="Diagram showing the workflow for connecting Azure Virtual Network to ExpressRoute in Azure VMware Solution." border="false":::

>[!IMPORTANT]
>[!INCLUDE [disk-pool-planning-note](includes/disk-pool-planning-note.md)] 

### Use a new ExpressRoute virtual network gateway

>[!IMPORTANT]
>You must have a virtual network with a GatewaySubnet that **does not** already have a virtual network gateway.

| If | Then  |
| --- | --- |
| You don't already have a virtual network...     |  Create the following:<ol><li><a href="tutorial-configure-networking.md#create-a-virtual-network">Virtual network</a></li><li><a href="../expressroute/expressroute-howto-add-gateway-portal-resource-manager.md#create-the-gateway-subnet">GatewaySubnet</a></li><li><a href="tutorial-configure-networking.md#create-a-virtual-network-gateway">Virtual network gateway</a></li><li><a href="tutorial-configure-networking.md#connect-expressroute-to-the-virtual-network-gateway">Connect ExpressRoute to the gateway</a></li></ol>        |
| You already have a virtual network **without** a GatewaySubnet...   | Create the following: <ol><li><a href="../expressroute/expressroute-howto-add-gateway-portal-resource-manager.md#create-the-gateway-subnet">GatewaySubnet</a></li><li><a href="tutorial-configure-networking.md#create-a-virtual-network-gateway">Virtual network gateway</a></li><li><a href="tutorial-configure-networking.md#connect-expressroute-to-the-virtual-network-gateway">Connect ExpressRoute to the gateway</a></li></ol>          |
| You already have a virtual network **with** a GatewaySubnet... | Create the following: <ol><li><a href="tutorial-configure-networking.md#create-a-virtual-network-gateway">Virtual network gateway</a></li><li><a href="tutorial-configure-networking.md#connect-expressroute-to-the-virtual-network-gateway">Connect ExpressRoute to the gateway</a></li></ol>    |


### Use an existing virtual network gateway

[!INCLUDE [connect-expressroute-to-vnet](includes/connect-expressroute-vnet.md)]


## Step 4. Validate the connection

You should have connectivity between the Azure Virtual Network where the ExpressRoute terminates and the Azure VMware Solution private cloud. 

1. Use a [virtual machine](../virtual-machines/windows/quick-create-portal.md#create-virtual-machine) within the Azure Virtual Network where the Azure VMware Solution ExpressRoute terminates (see [Step 3. Connect to Azure Virtual Network with ExpressRoute](#step-3-connect-to-azure-virtual-network-with-expressroute)).  

   1. Log into the Azure [portal](https://portal.azure.com).

   1. Navigate to a VM that is in the running state, and under **Settings**, select **Networking** and select the network interface resource.

      :::image type="content" source="../virtual-network/media/diagnose-network-routing-problem/view-nics.png" alt-text="Screenshot showing virtual network interface settings.":::

   1. On the left, select **Effective routes**. You'll see a list of address prefixes that are contained within the `/22` CIDR block you entered during the deployment phase.

1. If you want to log into both vCenter and NSX-T Manager, open a web browser and log into the same virtual machine used for network route validation.  

   You can identify the vCenter and NSX-T Manager console's IP addresses and credentials in the Azure portal.  Select your private cloud and then **Manage** > **Identity**.

   :::image type="content" source="media/tutorial-access-private-cloud/ss4-display-identity.png" alt-text="Screenshot showing the private cloud vCenter and NSX Manager URLs and credentials." border="true":::


## Next steps

In the next section, you'll connect Azure VMware Solution to your on-premises network through ExpressRoute.

> [!div class="nextstepaction"]
> [Connect to your on-premises environment](tutorial-expressroute-global-reach-private-cloud.md)
