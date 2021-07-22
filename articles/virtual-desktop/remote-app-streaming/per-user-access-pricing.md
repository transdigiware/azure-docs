---
title: Azure Virtual Desktop enroll per-user access pricing - Azure
description: How to enroll in per-user access pricing for Azure Virtual Desktop.
services: virtual-desktop
author: Heidilohr

ms.service: virtual-desktop
ms.topic: how-to
ms.date: 07/14/2021
ms.author: helohr
manager: femila
---

# Enroll your subscription in per-user access pricing

Before external users can connect to your deployment, you need to enroll your subscription in per-user access pricing. Per-user access pricing lets users outside of your organization access apps and desktops in your subscription. Your enrolled subscription will be charged each month based on the number of distinct users that connect to Azure Virtual Desktop resources.

## How to enroll

To enroll your Azure subscription into per-user access pricing:

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/).

2. Enter **Azure Virtual Desktop** into the search bar, then find and select **Azure Virtual Desktop** under Services.

3. In the **Azure Virtual Desktop** overview page, select **Per-user access pricing**.

4. In the list of subscriptions, select the subscription where you'll deploy Azure Virtual Desktop resources.

5. Select **Enroll**.

6. Review the Product Terms, then select **Enroll** to begin enrollment. It may take up to an hour for the enrollment process to finish.

7. After enrollment is done, check the value in the **Per-user access pricing** column of the subscriptions list to make sure it's changed from “Enrolling” to “Enrolled.”

## Next steps

To learn more about per-user access pricing, see [Understanding licensing and per-user access pricing](licensing.md). If you want to learn how to estimate per-user app streaming costs for your deployment, see [Estimate per-user app streaming costs for Azure Virtual Desktop](streaming-costs.md). For estimating total deployment costs, see [Understanding total Azure Virtual Desktop deployment costs](total-costs.md). 
