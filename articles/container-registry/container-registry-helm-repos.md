---
title:  Store Helm charts
description: Learn how to store Helm charts for your Kubernetes applications using repositories in Azure Container Registry
ms.topic: article
ms.date: 07/19/2021
---

# Push and pull Helm charts to an Azure container registry

To quickly manage and deploy applications for Kubernetes, you can use the [open-source Helm package manager][helm]. With Helm, application packages are defined as [charts](https://helm.sh/docs/topics/charts/), which are collected and stored in a [Helm chart repository](https://helm.sh/docs/topics/chart_repository/).

This article shows you how to host Helm charts repositories in an Azure container registry, using Helm 3 commands and storing charts as [OCI artifacts](container-registry-image-formats.md#oci-artifacts). In many scenarios, you would build and upload your own charts for the applications you develop. For more information on how to build your own Helm charts, see the [Chart Template Developer's Guide][develop-helm-charts]. You can also store an existing Helm chart from another Helm repo.

## Helm 3 or Helm 2?

To store, manage, and install Helm charts, you use commands in the Helm CLI. Major Helm releases include Helm 3 and Helm 2. For details on the version differences, see the [version FAQ](https://helm.sh/docs/faq/). 

Helm 3 should be used to host Helm charts in Azure Container Registry. With Helm 3, you:

* Can store and manage Helm charts in repositories in an Azure container registry
* Store Helm charts in your registry as [OCI artifacts](container-registry-image-formats.md#oci-artifacts). Azure Container Registry provides GA support for OCI artifacts, including Helm charts.
* Authenticate with your registry using the `helm registry login` or `az acr login` command.
* Use `helm chart` commands to push, pull, and manage Helm charts in a registry
* Use `helm install` to install charts to a Kubernetes cluster from a local repository cache.

### Feature support

Azure Container Registry supports specific Helm chart management features depending on whether you are using Helm 3 (current) or Helm 2 (deprecated).

| Feature | Helm 2 | Helm 3 |
| ---- | ---- | ---- |
| Manage charts using `az acr helm` commands | :heavy_check_mark: | |
| Store charts as OCI artifacts | | :heavy_check_mark:  |
| Manage charts using `az acr repository` commands and the **Repositories** blade in Azure portal| | :heavy_check_mark:  |


> [!NOTE]
> As of Helm 3, [az acr helm][az-acr-helm] commands for use with the Helm 2 client are being deprecated. A minimum of 3 months' notice will be provided in advance of command removal.

### Chart version compatibility

The following Helm [chart versions](https://helm.sh/docs/topics/charts/#the-apiversion-field) can be stored in Azure Container Registry and are installable by the Helm 2 and Helm 3 clients. 

| Version | Helm 2 | Helm 3 |
| ---- | ---- | ---- |
| apiVersion v1 | :heavy_check_mark: | :heavy_check_mark: |
| apiVersion v2 | | :heavy_check_mark: |

### Migrate from Helm 2 to Helm 3

If you've previously stored and deployed charts using Helm 2 and Azure Container Registry, we recommend migrating to Helm 3. See:

* [Migrating Helm 2 to 3](https://helm.sh/docs/topics/v2_v3_migration/) in the Helm documentation.
* [Migrate your registry to store Helm OCI artifacts](#migrate-your-registry-to-store-helm-oci-artifacts), later in this article

## Prerequisites

The following resources are needed for the scenario in this article:

- **An Azure container registry** in your Azure subscription. If needed, create a registry using the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI](container-registry-get-started-azure-cli.md).
- **Helm client version 3.1.0 or later** - Run `helm version` to find your current version. For more information on how to install and upgrade Helm, see [Installing Helm][helm-install].
- **A Kubernetes cluster** where you will install a Helm chart. If needed, create an [Azure Kubernetes Service cluster][aks-quickstart]. 
- **Azure CLI version 2.0.71 or later** - Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].

## Enable OCI support

Use the `helm version` command to verify that you have installed Helm 3:

```console
helm version
```

Set the following environment variable to enable OCI support in the Helm 3 client. Currently, this support is experimental and subject to change. 

```console
export HELM_EXPERIMENTAL_OCI=1
```

## Create a sample chart

Create a test chart using the following commands:

```console
mkdir helmtest

cd helmtest
helm create hello-world
```

As a basic example, change directory to the `templates` folder and first delete the contents there:

```console
cd hello-world/templates
rm -rf *
```

In the `templates` folder, create a file called `configmap.yaml`, by running the following command:

```console
cat <<EOF > configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: hello-world-configmap
data:
  myvalue: "Hello World"
EOF
```

For more about creating and running this example, see [Getting Started](https://helm.sh/docs/chart_template_guide/getting_started/) in the Helm Docs.

## Save chart to local registry cache

Change directory to the `hello-world` subdirectory. Then, run `helm chart save` to save a copy of the chart locally and also create an alias with the fully qualified name of the registry (all lowercase) and the target repository and tag. 

In the following example, the registry name is *mycontainerregistry*, the target repo is *helm/hello-world*, and the target chart tag is *0.1.0*. To successfully pull dependencies, the target chart image name and tag must match the name and version in `Chart.yaml`.

```console
cd ..
helm chart save . hello-world:0.1.0
helm chart save . mycontainerregistry.azurecr.io/helm/hello-world:0.1.0
```

Run `helm chart list` to confirm you saved the charts in the local registry cache. Output is similar to:

```console
REF                                                      NAME            VERSION DIGEST  SIZE            CREATED
hello-world:0.1.0                                        hello-world      0.1.0   5899db0 3.2 KiB        2 minutes 
mycontainerregistry.azurecr.io/helm/hello-world:0.1.0    hello-world      0.1.0   5899db0 3.2 KiB        2 minutes
```

## Authenticate with the registry

Run  `helm registry login` to authenticate with the registry. You may pass [registry credentials](container-registry-authentication.md) appropriate for your scenario, such as service principal credentials, or a repository-scoped token.

For example, create an Azure Active Directory [service principal with pull and push permissions](container-registry-auth-service-principal.md#create-a-service-principal) (AcrPush role) to the registry. Then supply the service principal credentials to `helm registry login`. The following example supplies the password using an environment variable:

```console
echo $spPassword | helm registry login mycontainerregistry.azurecr.io \
  --username <service-principal-id> \
  --password-stdin
```

> [!TIP]
> You can also login to the registry with your [individual Azure AD identity](container-registry-authentication.md?tabs=azure-cli#individual-login-with-azure-ad) to push and pull Helm charts.

## Push chart to registry

Run the `helm chart push` command in the Helm 3 CLI to push the chart to the fully qualified target repository:

```console
helm chart push mycontainerregistry.azurecr.io/helm/hello-world:0.1.0
```

After a successful push, output is similar to:

```output
The push refers to repository [mycontainerregistry.azurecr.io/helm/hello-world]
ref:     mycontainerregistry.azurecr.io/helm/hello-world:0.1.0
digest:  5899db028dcf96aeaabdadfa5899db025899db025899db025899db025899db02
size:    3.2 KiB
name:    hello-world
version: 0.1.0
```

## List charts in the repository

As with images stored in an Azure container registry, you can use [az acr repository][az-acr-repository] commands to show the repositories hosting your charts, and chart tags and manifests. 

For example, run [az acr repository show][az-acr-repository-show] to see the properties of the repo you created in the previous step:

```azurecli
az acr repository show \
  --name mycontainerregistry \
  --repository helm/hello-world
```

Output is similar to:

```output
{
  "changeableAttributes": {
    "deleteEnabled": true,
    "listEnabled": true,
    "readEnabled": true,
    "writeEnabled": true
  },
  "createdTime": "2020-03-20T18:11:37.6701689Z",
  "imageName": "helm/hello-world",
  "lastUpdateTime": "2020-03-20T18:11:37.7637082Z",
  "manifestCount": 1,
  "registry": "mycontainerregistry.azurecr.io",
  "tagCount": 1
}
```

Run the [az acr repository show-manifests][az-acr-repository-show-manifests] command to see details of the chart stored in the repository. For example:

```azurecli
az acr repository show-manifests \
  --name mycontainerregistry \
  --repository helm/hello-world --detail
```

Output, abbreviated in this example, shows a `configMediaType` of `application/vnd.cncf.helm.config.v1+json`:

```output
[
  {
    [...]
    "configMediaType": "application/vnd.cncf.helm.config.v1+json",
    "createdTime": "2020-03-20T18:11:37.7167893Z",
    "digest": "sha256:0c03b71c225c3ddff53660258ea16ca7412b53b1f6811bf769d8c85a1f0663ee",
    "imageSize": 3301,
    "lastUpdateTime": "2020-03-20T18:11:37.7167893Z",
    "mediaType": "application/vnd.oci.image.manifest.v1+json",
    "tags": [
      "0.1.0"
    ]
```

## Pull chart to local cache

To install a Helm chart to Kubernetes, the chart must be in the local cache. In this example, first run `helm chart remove` to remove the existing local chart named `mycontainerregistry.azurecr.io/helm/hello-world:0.1.0`:

```console
helm chart remove mycontainerregistry.azurecr.io/helm/hello-world:0.1.0
```

Run `helm chart pull` to download the chart from the Azure container registry to your local cache:

```console
helm chart pull mycontainerregistry.azurecr.io/helm/hello-world:0.1.0
```

## Export Helm chart

To work further with the chart, export it to a local directory using `helm chart export`. For example, export the chart you pulled to the `install` directory:

```console
helm chart export mycontainerregistry.azurecr.io/helm/hello-world:0.1.0 \
  --destination ./install
```

To view information for the exported chart in the repo, run the `helm show chart` command in the directory where you exported the chart.

```console
cd install
helm show chart hello-world
```

Helm returns detailed information about the latest version of your chart, as shown in the following sample output:

```output
apiVersion: v2
appVersion: 1.16.0
description: A Helm chart for Kubernetes
name: hello-world
type: application
version: 0.1.0    
```

## Install Helm chart

Run `helm install` to install the Helm chart you pulled to the local cache and exported. Specify a release name such as *myhelmtest*, or pass the `--generate-name` parameter. For example:

```console
helm install myhelmtest ./hello-world
```

Output after successful chart installation is similar to:

```console
NAME: myhelmtest
LAST DEPLOYED: Fri Mar 20 14:14:42 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

To verify the installation, run the `helm get manifest` command. 

```console
helm get manifest myhelmtest
```

The command returns the YAML data in your `configmap.yaml` template file.

Run `helm uninstall` to uninstall the chart release on your cluster:

```console
helm uninstall myhelmtest
```

## Delete chart from the registry

To delete a chart from the container registry, use the [az acr repository delete][az-acr-repository-delete] command. Run the following command and confirm the operation when prompted:

```azurecli
az acr repository delete --name mycontainerregistry --image helm/hello-world:0.1.0
```

## Migrate your registry to store Helm OCI artifacts

If you previously set up your Azure container registry as a chart repository using Helm 2 and the `az acr helm` commands, we recommend that you [upgrade][helm-install] to the Helm 3 client. Then, follow these steps to store the charts as OCI artifacts in your registry. 

> [!IMPORTANT]
> * After you complete migration from a Helm 2-style (index.yaml-based) chart repository to OCI artifact repositories, use the Helm CLI and `az acr repository` commands to manage the charts. See previous sections in this article. 
> * The Helm OCI artifact repositories are not discoverable using Helm commands such as `helm search` and `helm repo list`. For more information about Helm commands used to store charts as OCI artifacts, see the [Helm documentation](https://helm.sh/docs/topics/registries/).

### Enable OCI support

Ensure that you are using the Helm 3 client:

```console
helm version
```

Enable OCI support in the Helm 3 client. Currently, this support is experimental and subject to change.

```console
export HELM_EXPERIMENTAL_OCI=1
```

### List current charts

List the charts currently stored in the registry, here named *myregistry*:

```console
helm search repo myregistry
```

Output shows the charts and chart versions:

```
NAME                            CHART VERSION   APP VERSION     DESCRIPTION                                       
myregistry/ingress-nginx        3.20.1          0.43.0          Ingress controller for Kubernetes...
myregistry/wordpress            9.0.3           5.3.2           Web publishing platform for building...
[...]
```

### Save charts as OCI artifacts

For each chart in the repo, pull the chart locally, and save it as an OCI artifact. Example:

```console 
helm pull myregisry/ingress-nginx --untar
cd ingress-nginx
helm chart save . myregistry.azurecr.io/ingress-nginx:3.20.1
```

### Push charts to registry

Login to the registry:

```azurecli
az acr login --name myregistry
```

Push each chart to the registry:

```console
helm chart push myregistry.azurecr.io/ingress-nginx:3.20.1
```

After pushing a chart, confirm it is stored in the registry:

```azurecli
az acr repository list --name myregistry
```

After pushing all of the charts, optionally remove the Helm 2-style chart repository from the registry. Doing so reduces storage in your registry:

```console
helm repo remove myregistry
```

## Next steps

* For more information on how to create and deploy Helm charts, see [Developing Helm charts][develop-helm-charts].
* Learn more about installing applications with Helm in [Azure Kubernetes Service (AKS)](../aks/kubernetes-helm.md).
* Helm charts can be used as part of the container build process. For more information, see [Use Azure Container Registry Tasks][acr-tasks].

<!-- LINKS - external -->
[helm]: https://helm.sh/
[helm-install]: https://helm.sh/docs/intro/install/
[develop-helm-charts]: https://helm.sh/docs/chart_template_guide/

<!-- LINKS - internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
[aks-quickstart]: ../aks/kubernetes-walkthrough.md
[acr-bestpractices]: container-registry-best-practices.md
[az-acr-login]: /cli/azure/acr#az_acr_login
[az-acr-helm]: /cli/azure/acr/helm
[az-acr-repository]: /cli/azure/acr/repository
[az-acr-repository-show]: /cli/azure/acr/repository#az_acr_repository_show
[az-acr-repository-delete]: /cli/azure/acr/repository#az_acr_repository_delete
[az-acr-repository-show-manifests]: /cli/azure/acr/repository#az_acr_repository_show_manifests
[acr-tasks]: container-registry-tasks-overview.md
