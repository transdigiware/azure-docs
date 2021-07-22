---
title: Configure Form Recognizer containers
titleSuffix: Azure Applied AI Services
description: Learn how to configure the Form Recognizer container to parse form and table data.
author: laujan
manager: nitinme
ms.service: applied-ai-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 07/01/2021
ms.author: lajanuar
---
# Configure Form Recognizer containers

> [!IMPORTANT]
>
> Form Recognizer containers are in gated preview. To use them, you must submit an [online request](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUNlpBU1lFSjJUMFhKNzVHUUVLN1NIOEZETiQlQCN0PWcu), and have it approved. See [**Request approval to run container**](form-recognizer-container-install-run.md#request-approval-to-run-the-container) below for more information.

With Azure Form Recognizer containers, you can build an application architecture that's optimized to take advantage of both robust cloud capabilities and edge locality. Containers provide a minimalist, virtually-isolated environment that can be easily deployed on-premise and in the cloud. In this article, you will learn to configure the Form Recognizer container run-time environment by using the `docker compose` command arguments. Form Recognizer features are supported by six Form Recognizer feature containers—**Layout**, **Business Card**,**ID Document**,  **Receipt**, **Invoice**, **Custom**. These containers have several required settings and a few optional settings. For a few examples, see the [Example docker-compose.yml file](#example-docker-composeyml-file) section.

## Configuration settings

Each container has the following configuration settings:

|Required|Setting|Purpose|
|--|--|--|
|Yes|[ApiKey](#apikey-and-billing-configuration-setting)|Tracks billing information.|
|Yes|[Billing](#apikey-and-billing-configuration-setting)|Specifies the endpoint URI of the service resource on Azure. For more information on obtaining _see_ [Billing]](form-recognizer-container-install-run.md#billing). For more information and a complete list of regional endpoints, _see_ [Custom subdomain names for Cognitive Services](../../cognitive-services-custom-subdomains.md).|
|Yes|[Eula](#eula-setting)| Indicates that you've accepted the license for the container.|
|No|[ApplicationInsights](#applicationinsights-setting)|Enables adding [Azure Application Insights](/azure/application-insights) telemetry support to your container.|
|No|[Fluentd](#fluentd-settings)|Writes log and, optionally, metric data to a Fluentd server.|
|No|HTTP Proxy|Configures an HTTP proxy for making outbound requests.|
|No|[Logging](#logging-settings)|Provides ASP.NET Core logging support for your container. |

> [!IMPORTANT]
> The [`ApiKey`](#apikey-and-billing-configuration-setting), [`Billing`](#apikey-and-billing-configuration-setting), and [`Eula`](#eula-setting) settings are used together. You must provide valid values for all three settings; otherwise, your containers won't start. For more information about using these configuration settings to instantiate a container, see [Billing](form-recognizer-container-install-run.md#billing).

## ApiKey and Billing configuration setting

The `ApiKey` setting specifies the Azure resource key that's used to track billing information for the container. The value for the ApiKey must be a valid key for the resource that's specified for `Billing` in the "Billing configuration setting" section.

The `Billing` setting specifies the endpoint URI of the resource on Azure that's used to meter billing information for the container. The value for this configuration setting must be a valid endpoint URI for a resource on Azure. The container reports usage about every 10 to 15 minutes.

 You can find these settings in the Azure portal on the **Keys and Endpoint** page.

   :::image type="content" source="../media/containers/keys-and-endpoint.png" alt-text="Screenshot: Azure portal keys and endpoint page.":::

## Eula setting

[!INCLUDE [Container shared configuration eula settings](../../../../includes/cognitive-services-containers-configuration-shared-settings-eula.md)]

## ApplicationInsights setting

[!INCLUDE [Container shared configuration ApplicationInsights settings](../../../../includes/cognitive-services-containers-configuration-shared-settings-application-insights.md)]

## Fluentd settings

[!INCLUDE [Container shared configuration fluentd settings](../../../../includes/cognitive-services-containers-configuration-shared-settings-fluentd.md)]

## HTTP proxy credentials settings

[!INCLUDE [Container shared configuration fluentd settings](../../../../includes/cognitive-services-containers-configuration-shared-settings-http-proxy.md)]

## Logging settings

[!INCLUDE [Container shared configuration logging settings](../../../../includes/cognitive-services-containers-configuration-shared-settings-logging.md)]

## Volume settings

Use [**volumes**](https://docs.docker.com/storage/volumes/) to read and write data to and from the container. Volumes are the preferred for persisting data generated and used by Docker containers. You can specify an input mount or an output mount by including the `volumes` option and specifying `type` (bind), `source` (path to the folder) and `target` (file path parameter).

The Form Recognizer container requires an input volume and an output volume. The input volume can be read-only (`ro`), and it's required for access to the data that's used for training and scoring. The output volume has to be writable, and you use it to store the models and temporary data.

The exact syntax of the host volume location varies depending on the host operating system. Additionally, the volume location of the [host computer](form-recognizer-container-install-run.md#host-computer-requirements) might not be accessible because of a conflict between the Docker service account permissions and the host mount location permissions.

## Example docker-compose.yml file

The **docker compose** method is comprised of three steps:

 1. Create a Dockerfile.
 1. Define the services in a **docker-compose.yml** so they can be run together in an isolated environment.
 1. Run `docker-compose up` to start and run your services.

### Single container example

In this example, enter {FORM_RECOGNIZER_ENDPOINT_URI} and {FORM_RECOGNIZER_API_KEY} values for your Layout container instance.

#### **Layout container**

```yml
version: "3.9"
services:
azure-cognitive-service-layout:
    container_name: azure-cognitive-service-layout
    image: mcr.microsoft.com/azure-cognitive-services/form-recognizer/layout
    environment:
      - EULA=accept
      - billing={FORM_RECOGNIZER_ENDPOINT_URI}
      - apikey={FORM_RECOGNIZER_API_KEY}

    ports:
      - "5000"
    networks:
      - ocrvnet
networks:
  ocrvnet:
    driver: bridge
```

### Multiple containers example

#### **Receipt and OCR Read containers**

In this example, enter {FORM_RECOGNIZER_ENDPOINT_URI} and {FORM_RECOGNIZER_API_KEY} values for your Receipt container and {COMPUTER_VISION_ENDPOINT_URI} and {COMPUTER_VISION_API_KEY} values for your Computer Vision Read container.

```yml
version: "3"
services:
  azure-cognitive-service-receipt:
    container_name: azure-cognitive-service-receipt
    image: cognitiveservicespreview.azurecr.io/microsoft/cognitive-services-form-recognizer-receipt:2.1
    environment:
      - EULA=accept 
      - billing={FORM_RECOGNIZER_ENDPOINT_URI}
      - apikey={FORM_RECOGNIZER_API_KEY}
      - AzureCognitiveServiceReadHost=http://azure-cognitive-service-read:5000
    ports:
      - "5000:5050"
    networks:
      - ocrvnet
  azure-cognitive-service-read:
    container_name: azure-cognitive-service-read
    image: mcr.microsoft.com/azure-cognitive-services/vision/read:3.2
    environment:
      - EULA=accept 
      - billing={COMPUTER_VISION_ENDPOINT_URI}
      - apikey={COMPUTER_VISION_API_KEY}
    networks:
      - ocrvnet

networks:
  ocrvnet:
    driver: bridge
```

## Next steps

> [!div class="nextstepaction"]
> [Learn more about running multiple containers and the docker compose command](form-recognizer-container-install-run.md)
