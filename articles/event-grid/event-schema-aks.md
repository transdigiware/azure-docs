---
title: Azure Kubernetes Service as Event Grid source (Preview)
description: This article describes how to use Azure Kubernetes Service as an Event Grid event source. It provides the schema and links to tutorial and how-to articles. 
author: zr-msft
ms.topic: conceptual
ms.date: 07/12/2021
ms.author: zarhoads
---

# Azure Kubernetes Service (AKS) as an Event Grid source (Preview)

This article provides the properties and schema for AKS events. For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md). It also gives you a list of quick starts and tutorials to use AKS as an event source.

[!INCLUDE [preview features callout](../aks/includes/preview/preview-callout.md)]

## Available event types

AKS emits the following event types

|    Event Type                                             |    Description                                                       |
|-----------------------------------------------------------|----------------------------------------------------------------------|
| Microsoft.ContainerService.NewKubernetesVersionAvailable  | Triggered when the list of available Kubernetes versions is updated. |

## Properties common to all events

# [Event Grid event schema](#tab/event-grid-event-schema)
When an event is triggered, the Event Grid service sends data about that event to subscribing endpoint.
This section contains an example of what that data would look like for each event. Each event has the following top-level data:

|     Property          |     Type     |     Description                                                                                                                                |
|-----------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------|
|    `topic`              |    string    |    Full resource path to the event   source. This field isn't writeable. Event Grid provides this value.                                      |
|    `subject`            |    string    |    Publisher-defined path to the   event subject.                                                                                              |
|    `eventType`          |    string    |    One of the registered event   types for this event source.                                                                                  |
|    `eventTime`          |    string    |    The time the event is generated   based on the provider's UTC time.                                                                         |
|    `id`                 |    string    |    Unique identifier for the event.                                                                                                            |
|    `data`               |    object    |    Blob storage event data.                                                                                                                    |
|    `dataVersion`        |    string    |    The schema version of the data   object. The publisher defines the schema version.                                                          |
|    `metadataVersion`    |    string    |    The schema version of the event   metadata. Event Grid defines the schema of the top-level properties. Event   Grid provides this value.    |

# [Cloud event schema](#tab/cloud-event-schema)

When an event is triggered, the Event Grid service sends data about that event to subscribing endpoint.
This section contains an example of what that data would look like for each event. Each event has the following top-level data:

|     Property          |     Type     |     Description                                                                                                                                |
|-----------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------|
|    `source`              |    string    |    Full resource path to the event   source. This field isn't writeable. Event Grid provides this value.                                      |
|    `subject`            |    string    |    Publisher-defined path to the   event subject.                                                                                              |
|    `type`          |    string    |    One of the registered event   types for this event source.                                                                                  |
|    `time`          |    string    |    The time the event is generated   based on the provider's UTC time.                                                                         |
|    `id`                 |    string    |    Unique identifier for the event.                                                                                                            |
|    `data`               |    object    |    Blob storage event data.                                                                                                                    |
| `specversion` | string | CloudEvents schema specification version. |

---

## Example events

### NewKubernetesVersionAvailable

# [Event Grid event schema](#tab/event-grid-event-schema)

```json
{
    "topic": "/subscriptions/<id>/resourceGroups<rg>/providers/Microsoft.ContainerService/managedClusters/<cluster>",
    "subject": "<cluster>",
    "eventType": "Microsoft.ContainerService.NewKubernetesVersionAvailable",
    "id": "1234567890abcdef1234567890abcdef12345678",
    "data": {
      "latestSupportedKubernetesVersion": "1.20.7",
      "latestStableKubernetesVersion": "1.19.11",
      "lowestMinorKubernetesVersion": "1.18.19",
      "latestPreviewKubernetesVersion": "1.21.1"
    },
    "dataVersion": "1",
    "metadataVersion": "1",
    "eventTime": "2021-07-01T04:52:57.0000000Z",
    "EventProcessedUtcTime": "2021-07-02T04:40:04.1049205Z",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": "2021-07-01T04:52:58.8650000Z"
}
```
# [Cloud event schema](#tab/cloud-event-schema)

```json

{
    "source": "/subscriptions/<id>/resourceGroups<rg>/providers/Microsoft.ContainerService/managedClusters/<cluster>",
    "subject": "<cluster>",
    "type": "Microsoft.ContainerService.NewKubernetesVersionAvailable",
    "id": "1234567890abcdef1234567890abcdef12345678",
    "data": {
      "latestSupportedKubernetesVersion": "1.20.7",
      "latestStableKubernetesVersion": "1.19.11",
      "lowestMinorKubernetesVersion": "1.18.19",
      "latestPreviewKubernetesVersion": "1.21.1"
    },
    "specversion": "1.0",
    "time": "2021-07-01T04:52:57.0000000Z",
    "EventProcessedUtcTime": "2021-07-02T04:40:04.1049205Z",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": "2021-07-01T04:52:58.8650000Z"
}
```

---

The data object contains the following properties:

|    Property                        | Type   | Description                                                  |
|------------------------------------|--------|--------------------------------------------------------------|
| `latestSupportedKubernetesVersion` | string | The latest supported version of Kubernetes available.        |
| `latestStableKubernetesVersion`    | string | The latest stable supported version of Kubernetes available. |
| `lowestMinorKubernetesVersion`     | string | The lowest supported version of Kubernetes available.        |
| `latestPreviewKubernetesVersion`   | string | The latest preview version of Kubernetes available.          |

## Next steps

* For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)
* For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md)