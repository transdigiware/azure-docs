---
title: Teams meeting interoperability
titleSuffix: An Azure Communication Services concept document
description: Join Teams meetings
author: chpalm
manager: chpalm
services: azure-communication-services

ms.author: chpalm
ms.date: 06/30/2021
ms.topic: overview
ms.service: azure-communication-services
---

# Teams interoperability

> [!IMPORTANT]
> BYOI interoperability is in public preview and broadly available on request. To enable/disable [Teams tenant interoperability](../concepts/teams-interop.md), complete [this form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR21ouQM6BHtHiripswZoZsdURDQ5SUNQTElKR0VZU0VUU1hMOTBBMVhESS4u).
>
> Microsoft 365 authenticated interoperability is in private preview, and restricted using service controls to Azure Communication Services early adopters. To join early access program, complete [this form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR8MfnD7fOYZEompFbYDoD4JUMkdYT0xKUUJLR001ODdQRk1ITTdOMlRZNSQlQCN0PWcu).
>
> Preview APIs and SDKs are provided without a service-level agreement, and are not recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Azure Communication Services can be used to build custom applications that interact with Microsoft Teams. End users of your Communication Services application can interact with Teams participants over voice, video, chat, and screen sharing.

Azure Communication Services supports two types of Teams interoperability depending on the identity of the end user:

- **Bring your own identity.** You control user authentication and users of your custom applications don't need to have Azure Active Directory identities or Teams licenses to join Teams meetings. Teams treats your application as anonymous external user.
- **Microsoft 365 Teams identity.** Your application acts on behalf of an end user's Microsoft 365 identity and their Teams configured resources. These authenticated applications can make calls and join meetings seamlessly on behalf of Microsoft 365 users.

Applications can implement both authentication schemes and leave the choice of authentication up to the end user.

## Bring your own identity
Bring your own identity (BYOI) is the common model for using Azure Communication Services and Teams interoperability. It supports any identity provider and authentication scheme. Your app can join Microsoft Teams meetings, and Teams will treat these users as anonymous external accounts. The name of Communication Services users displayed in Teams is configurable via the Communication Services Calling SDK.

This capability is ideal for business-to-consumer applications that bring together employees (familiar with Teams) and external users (using a custom application experience) into a meeting experience. Meeting details that need to be shared with external users of your application can be retrieved via the Graph API or from the calendar in Microsoft Teams.

External users will be able to use core audio, video, screen sharing, and chat functionality via Azure Communication Services SDKs. Features such as raised hand, together mode, and breakout rooms will only be available for Teams users. Communication Services users can send and receive messages only while present in the Teams meeting and if the meeting is not scheduled for a channel.

Your custom application should consider user authentication and other security measures to protect Teams meetings. Be mindful of the security implications of enabling anonymous users to join meetings, and use the [Teams security guide](/microsoftteams/teams-security-guide#addressing-threats-to-teams-meetings) to configure capabilities available to anonymous users.

Additional information on required dataflows for joining Teams meetings is available at the [client and server architecture page](client-and-server-architecture.md). The [Group Calling Hero Sample](../samples/calling-hero-sample.md) provides example code for joining a Teams meeting from a web application.

## Microsoft 365 Teams identity
The Azure Communication Services Calling SDK can be used with Microsoft 365 Teams identities to support Teams-like experiences for Teams interoperability. Microsoft 365 Teams identities are provided and authenticated by Azure Active Directory. Your app can make or accept calls with a regular Microsoft 365 identity. All attributes and details about the user are bound to the Azure Active Directory user.

This identity model is ideal for use cases where a custom user interface is needed, where the Teams client is not available for your platform, or where the Teams client does not support a sufficient level of customization. For example, an application can be used to answer phone calls on behalf of the end user's Teams provisioned PSTN number and have a user interface optimized for a receptionist or call center business process.  

Calling and screen sharing functionality is available via the Communication Services Calling SDK. Calling management is available via Graph API, configuration in the Teams client or Teams Admin Portal. Chat functionality is available via Graph API.

Teams users are authenticated via the MSAL library against Azure Active Directory in the client application. Authentication tokens are exchanged for Microsoft 365 Teams token via the Communication Services Identity SDK. You are encouraged to implement an exchange of tokens in your backend services as exchange requests are signed by credentials for Azure Communication Services. In your backend services, you can require any additional authentication.

To learn more about the functionality, join our TAP program for early access by completing [this form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR8MfnD7fOYZEompFbYDoD4JUMkdYT0xKUUJLR001ODdQRk1ITTdOMlRZNSQlQCN0PWcu).

## Comparison

|Criteria|Bring your own identity| Microsoft 365 Teams identity|
|---|---|---|
|Applicable| In business-to-consumer scenarios for consumer applications | In business-to-business or business-to-consumer scenarios on business applications |
|Identity provider|Any|Azure Active Directory|
|Authentication & authorization|Custom*| Azure Active Directory and custom*|
|Calling available via | Communication Services Calling SDKs | Communication Services Calling SDKs |
|Chat available via | Communication Services Chat SDKs | Graph API |
|PSTN support| outbound voice call, outbound direct routing, [details](./telephony-sms/telephony-concept.md) | inbound call assigned to Teams identity, outbound call using calling plan|

\* Server logic issuing access tokens can perform any custom authentication and authorization of the request.

## Privacy
Interoperability between Azure Communication Services and Microsoft Teams enables your applications and users to participate in Teams calls, meetings, and chat. It is your responsibility to ensure that the users of your application are notified when recording or transcription are enabled in a Teams call or meeting.

Microsoft will indicate to you via the Azure Communication Services API that recording or transcription has commenced and you must communicate this fact, in real time, to your users within your application’s user interface. You agree to indemnify Microsoft for all costs and damages incurred as a result of your failure to comply with this obligation.

## Pricing
All usage of Azure Communication Service APIs and SDKs increments [Azure Communication Service billing meters](https://azure.microsoft.com/pricing/details/communication-services/). Interactions with Microsoft Teams, such as joining a meeting or initiating a phone call using a Teams allocated number, will increment these meters but there is no additional fee for the Teams interoperability capability itself, and there is no pricing distinction between the BYOI and Microsoft 365 authentication options.

If your Azure application has an end user spend 10 minutes in a meeting with a user of Microsoft Teams, those two users combined consumed 20 calling minutes. The 10 minutes exercised through the custom application and using Azure APIs and SDKs will be billed to your resource. However the 10 minutes consumed by the end user in the native Teams application is covered by the applicable Teams license and is not metered by Azure.

## Teams in Government Clouds (GCC)
Azure Communication Services interoperability isn't compatible with Teams deployments using [Microsoft 365 government clouds (GCC)](/MicrosoftTeams/plan-for-government-gcc) at this time.

## Next steps

> [!div class="nextstepaction"]
> [Join a BYOI calling app to a Teams meeting](../quickstarts/voice-video-calling/get-started-teams-interop.md)
> [Authenticate Microsoft 365 users](../quickstarts/manage-teams-identity.md)
