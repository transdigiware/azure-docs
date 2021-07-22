---
title: Important changes coming to Azure Security Center
description: Upcoming changes to Azure Security Center that you might need to be aware of and for which you might need to plan 
author: memildin
manager: rkarlin
ms.service: security-center
ms.topic: overview
ms.date: 07/22/2021
ms.author: memildin

---

# Important upcoming changes to Azure Security Center

> [!IMPORTANT]
> The information on this page relates to pre-release products or features, which may be substantially modified before they are commercially released, if ever. Microsoft makes no commitments or warranties, express or implied, with respect to the information provided here.

On this page, you'll learn about changes that are planned for Security Center. It describes planned modifications to the product that might impact things like your secure score or workflows.

If you're looking for the latest release notes, you'll find them in the [What's new in Azure Security Center](release-notes.md).


## Planned changes

| Planned change                                                                                                                                                                                          | Estimated date for change |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| [CSV exports to be limited to 20 MB](#csv-exports-to-be-limited-to-20-mb)                                                                                                                               | July 2021                 |
| [Legacy implementation of ISO 27001 is being replaced with new ISO 27001:2013](#legacy-implementation-of-iso-27001-is-being-replaced-with-new-iso-270012013)                                            | July 2021                 |
| [Deprecating recommendation 'Log Analytics agent health issues should be resolved on your machines'](#deprecating-recommendation-log-analytics-agent-health-issues-should-be-resolved-on-your-machines) | July 2021                 |
| [Logical reorganization of Azure Defender for Resource Manager alerts](#logical-reorganization-of-azure-defender-for-resource-manager-alerts)                                                           | August 2021               |
| [Enhancements to recommendation to classify sensitive data in SQL databases](#enhancements-to-recommendation-to-classify-sensitive-data-in-sql-databases)                                               | Q3 2021                   |
| [Enable Azure Defender security control to be included in secure score](#enable-azure-defender-security-control-to-be-included-in-secure-score)                                                         | Q3 2021                   |
|                                                                                                                                                                                                         |                           |


### CSV exports to be limited to 20 MB

**Estimated date for change:** July 2021

When exporting Security Center recommendations data, there's currently no limit on the amount of data that you can download.

:::image type="content" source="media/upcoming-changes/download-csv-report.png" alt-text="Security Center's 'download CSV report' button to export recommendation data.":::

With this change, we're instituting a limit of 20 MB.

If you need to export larger amounts of data, use the available filters before selecting, or select subsets of your subscriptions and download the data in batches.

:::image type="content" source="media/upcoming-changes/filter-subscriptions.png" alt-text="Filtering subscriptions in the Azure portal.":::

Learn more about [performing a CSV export of your security recommendations](continuous-export.md#manual-one-time-export-of-alerts-and-recommendations).

### Legacy implementation of ISO 27001 is being replaced with new ISO 27001:2013

**Estimated date for change:** July 2021

The legacy implementation of ISO 27001 will be removed from Security Center's regulatory compliance dashboard. If you're tracking your ISO 27001 compliance with Security Center, onboard the new ISO 27001:2013 standard for all relevant management groups or subscriptions, and the current legacy ISO 27001 will soon be removed from the dashboard.

:::image type="content" source="media/upcoming-changes/removing-iso-27001-legacy-implementation.png" alt-text="Security Center's regulatory compliance dashboard showing the message about the removal of the legacy implementation of ISO 27001." lightbox="media/upcoming-changes/removing-iso-27001-legacy-implementation.png":::

### Deprecating recommendation 'Log Analytics agent health issues should be resolved on your machines'

**Estimated date for change:** July 2021

We've found that recommendation **Log Analytics agent health issues should be resolved on your machines** impacts secure scores in ways that are inconsistent with Security Center's Cloud Security Posture Management (CSPM) focus. Typically, CSPM relates to identifying security misconfigurations. Agent health issues don't fit into this category of issues.

Also, the recommendation is an anomaly when compared with the other agents related to Security Center: this is the only agent with a recommendation related to health issues.

The recommendation will be deprecated.

As a result of this deprecation, we'll also be making minor changes to the recommendations for installing the Log Analytics agent (**Log Analytics agent should be installed on...**).

It's likely that this change will impact your secure scores. For most subscriptions, we expect the change to lead to an increased score, but it's possible the updates to the installation recommendation might result in decreased scores in some cases.

> [!TIP]
> The [asset inventory](asset-inventory.md) page will also be affected by this change as it also displays information about whether or not a machine is monitored, not monitored, or partially monitored (a state which refers to an agent with health issues). 


### Logical reorganization of Azure Defender for Resource Manager alerts

**Estimated date for change:** August 2021

The alerts listed below are currently provided as part of the [Azure Defender for Resource Manager](defender-for-resource-manager-introduction.md) plan.

As part of a logical reorganization of some of the Azure Defender plans, we're moving some alerts from **Azure Defender for Resource Manager** to **Azure Defender for servers**.

The alerts will be organized according to two main principles:

- Alerts that provide control-plane protection - across many Azure resource types - will be part of Azure Defender for Resource Manager
- Alerts that protect specific workloads will be moved to the corresponding Azure Defender plan that relates to that workload

These are the alerts that are currently part of Azure Defender for Resource Manager, and which, as a result of this change, will be moved to Azure Defender for servers:

- ARM_AmBroadFilesExclusion
- ARM_AmDisablementAndCodeExecution
- ARM_AmDisablement
- ARM_AmFileExclusionAndCodeExecution
- ARM_AmTempFileExclusionAndCodeExecution
- ARM_AmTempFileExclusion
- ARM_AmRealtimeProtectionDisabled
- ARM_AmTempRealtimeProtectionDisablement
- ARM_AmRealtimeProtectionDisablementAndCodeExec
- ARM_AmMalwareCampaignRelatedExclusion
- ARM_AmTemporarilyDisablement
- ARM_UnusualAmFileExclusion
- ARM_CustomScriptExtensionSuspiciousCmd
- ARM_CustomScriptExtensionSuspiciousEntryPoint
- ARM_CustomScriptExtensionSuspiciousPayload
- ARM_CustomScriptExtensionSuspiciousFailure
- ARM_CustomScriptExtensionUnusualDeletion
- ARM_CustomScriptExtensionUnusualExecution
- ARM_VMAccessUnusualConfigReset
- ARM_VMAccessUnusualPasswordReset
- ARM_VMAccessUnusualSSHReset

Learn more about the [Azure Defender for Resource Manager](defender-for-resource-manager-introduction.md) and [Azure Defender for servers](defender-for-servers-introduction.md).


### Enhancements to recommendation to classify sensitive data in SQL databases

**Estimated date for change:** Q3 2021

The recommendation **Sensitive data in your SQL databases should be classified** in the **Apply data classification** security control will be replaced with a new version that's better aligned with Microsoft's data classification strategy. As a result the recommendation's ID will also change (currently, it's b0df6f56-862d-4730-8597-38c0fd4ebd59).

### Enable Azure Defender security control to be included in secure score

**Estimated date for change:** Q3 2021

Security Center's hardening recommendations are grouped into security controls. Each control is a logical group of related security recommendations, and reflects a vulnerable attack surface. The contribution of each security control towards the overall secure score is shown clearly on the recommendations page as well as in the list of controls in [Security controls and their recommendations](secure-score-security-controls.md#security-controls-and-their-recommendations).

Since its introduction, the **Enable Azure Defender** control has had a maximum possible score of 0 points. **With this change, the control will contribute towards your secure score**.

When you enable Azure Defender you'll extend the capabilities of Security Center's free mode to your workloads running in private and other public clouds, providing unified security management and threat protection across your hybrid cloud workloads. Some of the major features of Azure Defender are: integrated Microsoft Defender for Endpoint licenses for your servers, vulnerability scanning for virtual machines and container registries, security alerts based on advanced behavioral analytics and machine learning, and container security features. For a full list, see [Azure Security Center free vs Azure Defender enabled](security-center-pricing.md).

With this change, there will be an impact on the secure score of any subscriptions that aren't protected by Azure Defender. We suggest you enable Azure Defender before this change occurs to ensure there is no impact on your scores. 

Learn more in [Quickstart: Enable Azure Defender](enable-azure-defender.md).


## Next steps

For all recent changes to the product, see [What's new in Azure Security Center?](release-notes.md).