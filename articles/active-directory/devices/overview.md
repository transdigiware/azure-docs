---
title: What is device identity in Azure Active Directory?
description: Device identities and their use cases

services: active-directory
ms.service: active-directory
ms.subservice: devices
ms.topic: overview
ms.date: 06/09/2021

ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sandeo, ravenn, spunukol, jogro, jploegert

ms.collection: M365-identity-device-management
---
# What is a device identity?

A [device identity](/graph/api/resources/device?view=graph-rest-1.0) is an object in Azure Active Directory (Azure AD). This device object is similar to users, groups, or applications. A device identity gives administrators information they can use when making access or configuration decisions.

![Devices displayed in Azure AD Devices blade](./media/overview/azure-active-directory-devices-all-devices.png)

There are three ways to get a device identity:

- Azure AD registration
- Azure AD join
- Hybrid Azure AD join

Device identities are a prerequisite for scenarios like [device-based Conditional Access policies](../conditional-access/require-managed-devices.md) and [Mobile Device Management with Microsoft Endpoint Manager](/mem/endpoint-manager-overview).

## Modern device scenario

The modern device scenario focuses on two of these methods: 

- [Azure AD registration](concept-azure-ad-register.md) 
   - Bring your own device (BYOD)
   - Mobile device (cell phone and tablet)
- [Azure AD join](concept-azure-ad-register.md)
   - Windows 10 devices owned by your organization
   - [Windows Server 2019 and newer servers in your organization running as VMs in Azure](howto-vm-sign-in-azure-ad-windows.md)

[Hybrid Azure AD join](concept-azure-ad-join-hybrid.md) is seen as an interim step on the road to Azure AD join. Hybrid Azure AD join provides organizations support for downlevel Windows versions back to Windows 7 and Server 2008. All three scenarios can coexist in a single organization.

## Resource access

Registering and joining devices to Azure AD gives users Seamless Sign-on (SSO) to cloud-based resources.

Devices that are Azure AD joined benefit from [SSO to your organization's on-premises resources](azuread-join-sso.md).

## Provisioning

Getting devices in to Azure AD can be done in a self-service manner or a controlled process managed by administrators.

## License requirements

[!INCLUDE [Active Directory P1 license](../../../includes/active-directory-p1-license.md)]

## Next steps

- Learn more about [Azure AD registered devices](concept-azure-ad-register.md)
- Learn more about [Azure AD joined devices](concept-azure-ad-join.md)
- Learn more about [hybrid Azure AD joined devices](concept-azure-ad-join-hybrid.md)
- To get an overview of how to manage device identities in the Azure portal, see [Managing device identities using the Azure portal](device-management-azure-portal.md).
- To learn more about device-based Conditional Access, see [Configure Azure Active Directory device-based Conditional Access policies](../conditional-access/require-managed-devices.md).
