---
title: Registry service tiers and features
description: Learn about the features and limits (quotas) in the Basic, Standard, and Premium service tiers (SKUs) of Azure Container Registry.
ms.topic: article
ms.date: 06/24/2021
---

# Azure Container Registry service tiers

Azure Container Registry is available in multiple service tiers (also known as SKUs). These tiers provide predictable pricing and several options for aligning to the capacity and usage patterns of your private Docker registry in Azure.

| Tier | Description |
| --- | ----------- |
| **Basic** | A cost-optimized entry point for developers learning about Azure Container Registry. Basic registries have the same programmatic capabilities as Standard and Premium (such as Azure Active Directory [authentication integration](container-registry-authentication.md#individual-login-with-azure-ad), [image deletion][container-registry-delete], and [webhooks][container-registry-webhook]). However, the included storage and image throughput are most appropriate for lower usage scenarios. |
| **Standard** | Standard registries offer the same capabilities as Basic, with increased included storage and image throughput. Standard registries should satisfy the needs of most production scenarios. |
| **Premium** | Premium registries provide the highest amount of included storage and concurrent operations, enabling high-volume scenarios. In addition to higher image throughput, Premium adds features such as [geo-replication][container-registry-geo-replication] for managing a single registry across multiple regions, [content trust](container-registry-content-trust.md) for image tag signing, [private link with private endpoints](container-registry-private-link.md) to restrict access to the registry. |

The Basic, Standard, and Premium tiers all provide the same programmatic capabilities. They also all benefit from [image storage][container-registry-storage] managed entirely by Azure. Choosing a higher-level tier provides more performance and scale. With multiple service tiers, you can get started with Basic, then convert to Standard and Premium as your registry usage increases.

## Service tier features and limits

The following table details the features and registry limits of the Basic, Standard, and Premium service tiers.

[!INCLUDE [container-instances-limits](../../includes/container-registry-limits.md)]

## Registry throughput and throttling

### Throughput 

When generating a high rate of registry operations, use the service tier's limits for read and write operations and bandwidth as a guide for expected maximum throughput. These limits affect data-plane operations including listing, deleting, pushing, and pulling images and other artifacts.

To estimate the throughput of image pulls and pushes specifically, consider the registry limits and these factors: 

* Number and size of image layers
* Reuse of layers or base images across images
* additional API calls that might be required for each pull or push

For details, see documentation for the [Docker HTTP API V2](https://docs.docker.com/registry/spec/api/).

When evaluating or troubleshooting registry throughput, also consider the configuration of your client environment:

* your Docker daemon configuration for concurrent operations
* your network connection to the registry's data endpoint (or endpoints, if your registry is [geo-replicated](container-registry-geo-replication.md)).

If you experience issues with throughput to your registry, see [Troubleshoot registry performance](container-registry-troubleshoot-performance.md). 

#### Example

Pushing a single 133 MB `nginx:latest` image to an Azure container registry requires multiple read and write operations for the image's five layers: 

* Read operations to read the image manifest, if it exists in the registry
* Write operations to write the configuration blob of the image
* Write operations to write the image manifest

### Throttling

You may experience throttling of pull or push operations when the registry determines the rate of requests exceeds the limits allowed for the registry's service tier. You may see an HTTP 429 error similar to `Too many requests`.

Throttling could occur temporarily when you generate a burst of image pull or push operations in a very short period, even when the average rate of read and write operations is within registry limits. You may need to implement retry logic with some backoff in your code or reduce the maximum rate of requests to the registry.

## Changing tiers

You can change a registry's service tier with the Azure CLI or in the Azure portal. You can move freely between tiers as long as the tier you're switching to has the required maximum storage capacity. 

There is no registry downtime or impact on registry operations when you move between service tiers.

### Azure CLI

To move between service tiers in the Azure CLI, use the [az acr update][az-acr-update] command. For example, to switch to Premium:

```azurecli
az acr update --name myregistry --sku Premium
```

### Azure portal

In the container registry **Overview** in the Azure portal, select **Update**, then select a new **SKU** from the SKU drop-down.

![Update container registry SKU in Azure portal][update-registry-sku]

## Pricing

For pricing information on each of the Azure Container Registry service tiers, see [Container Registry pricing][container-registry-pricing].

For details about pricing for data transfers, see [Bandwidth Pricing Details](https://azure.microsoft.com/pricing/details/bandwidth/). 

## Next steps

**Azure Container Registry Roadmap**

Visit the [ACR Roadmap][acr-roadmap] on GitHub to find information about upcoming features in the service.

**Azure Container Registry UserVoice**

Submit and vote on new feature suggestions in [ACR UserVoice][container-registry-uservoice].

<!-- IMAGES -->
[update-registry-sku]: ./media/container-registry-skus/update-registry-sku.png

<!-- LINKS - External -->
[acr-roadmap]: https://aka.ms/acr/roadmap
[container-registry-pricing]: https://azure.microsoft.com/pricing/details/container-registry/
[container-registry-uservoice]: https://feedback.azure.com/forums/903958-azure-container-registry

<!-- LINKS - Internal -->
[az-acr-update]: /cli/azure/acr#az_acr_update
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-storage]: container-registry-storage.md
[container-registry-delete]: container-registry-delete.md
[container-registry-webhook]: container-registry-webhook.md
