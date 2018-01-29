---
title: "Azure Kubernetes 叢集的服務主體"
description: "在 AKS 中建立和管理 Kubernetes 叢集的 Azure Active Directory 服務主體"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: get-started-article
ms.date: 11/30/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9814dca53f1a410f4d1e95cc18b98373f27f9802
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="service-principals-with-azure-container-service-aks"></a>服務主體與 Azure Container Service (AKS)

AKS 叢集需要 [Azure Active Directory 服務主體][aad-service-principal]，才能與 Azure API 進行互動。 需要服務主體，才能以動態方式管理資源，例如[使用者定義的路由][user-defined-routes]及[第 4 層 Azure Load Balancer][azure-load-balancer-overview]。

本文說明為 AKS 中 Kubernetes 叢集設定服務主體的各種選項。

## <a name="before-you-begin"></a>開始之前


若要建立 Azure AD 服務主體，您必須有足夠權限向 Azure AD 租用戶註冊應用程式，並將應用程式指派給您訂用帳戶中的角色。 如果您沒有必要的權限，您可能需要要求您的 Azure AD 或訂用帳戶管理員指派必要權限，或預先建立 Kubernetes 叢集的服務主體。

您也必須安裝和設定 Azure CLI 版本 2.0.21 或更新版本。 執行 `az --version` 以尋找版本。 如果您需要安裝或升級，請參閱[安裝 Azure CLI][install-azure-cli]。

## <a name="create-sp-with-aks-cluster"></a>建立 SP 與 AKS 叢集

當使用 `az aks create` 命令部署 AKS 叢集時，您可以選擇自動產生服務主體。

在下列範例中，會建立 AKS 叢集，因為未指定現有服務主體，所以會為叢集建立服務主體。 為了完成這項作業，您的帳戶必須具有建立服務主體的適當權限。

```azurecli
az aks create --name myK8SCluster --resource-group myResourceGroup --generate-ssh-keys
```

## <a name="use-an-existing-sp"></a>使用現有的 SP

可以使用現有的 Azure AD 服務主體，或預先建立以與 AKS 叢集搭配使用。 從您需要提供服務主體資訊之 Azure 入口網站部署叢集時，很有幫助。 在使用現有的服務主體時，必須將用戶端密碼設定為密碼。

## <a name="pre-create-a-new-sp"></a>預先建立新 SP

若要使用 Azure CLI 建立服務主體，請使用 [az ad sp create-for-rbac][az-ad-sp-create] 命令。

```azurecli
az ad sp create-for-rbac --skip-assignment
```

輸出大致如下。 記下 `appId` 和 `password`。 建立 AKS 叢集時，會使用這些值。

```json
{
  "appId": "7248f250-0000-0000-0000-dbdeb8400d85",
  "displayName": "azure-cli-2017-10-15-02-20-15",
  "name": "http://azure-cli-2017-10-15-02-20-15",
  "password": "77851d2c-0000-0000-0000-cb3ebc97975a",
  "tenant": "72f988bf-0000-0000-0000-2d7cd011db47"
}
```

## <a name="use-an-existing-sp"></a>使用現有的 SP

當使用預先建立的服務主體時，提供 `appId` 和 `password` 作為 `az aks create` 命令的引數值。

```azurecli-interactive
az aks create --resource-group myResourceGroup --name myK8SCluster --service-principal <appId> --client-secret <password>
```

如果您要使用 Azure 入口網站來部署 AKS 叢集，請在 AKS 叢集設定表單的 [服務主體用戶端識別碼] 欄位中輸入 `appId` 值，並在 [服務主體用戶端密碼] 欄位中輸入 `password` 值。

![瀏覽至 Azure 投票的影像](media/container-service-kubernetes-service-principal/sp-portal.png)

## <a name="additional-considerations"></a>其他考量

當使用 AKS 和 Azure AD 服務主體時，請記住下列項目。

* Kubernetes 的服務主體是叢集組態的一部分。 不過，請勿使用身分識別來部署叢集。
* 每個服務主體都會與 Azure AD 應用程式相關聯。 Kubernetes 叢集的服務主體可與任何有效的 Azure AD 應用程式名稱相關聯 (例如：`https://www.contoso.org/example`)。 應用程式的 URL 不一定是實際端點。
* 指定服務主體的 [用戶端識別碼] 時，您可以使用 `appId` 的值 (如本文所示) 或對應的服務主體`name` (例如，`https://www.contoso.org/example`)。
* 在 Kubernetes 叢集中的主要和節點 VM 上，服務主體認證會儲存在 `/etc/kubernetes/azure.json` 檔案中。
* 當您使用 `az aks create` 命令自動產生服務主體時，服務主體認證會寫入用來執行命令之電腦上的 `~/.azure/acsServicePrincipal.json` 檔案。
* 當您使用 `az aks create` 命令自動產生服務主體時，服務主體也可以向在訂用帳戶中建立的 [Azure Container Registry][acr-intro] 進行驗證。
* 刪除 `az aks create` 所建立的 AKS 叢集時，將不會刪除自動建立的服務主體。 您可以使用 `az ad sp delete --id $clientID` 將它刪除。

## <a name="next-steps"></a>後續步驟

如需有關 Azure Active Directory 服務主體的詳細資訊，請參閱 Azure AD 應用程式文件。

> [!div class="nextstepaction"]
> [應用程式和服務主體物件][service-principal]

<!-- LINKS - internal -->
[aad-service-principal]: ../active-directory/develop/active-directory-application-objects.md
[acr-intro]: ../container-registry/container-registry-intro.md
[az-ad-sp-create]: /cli/azure/ad/sp#az_ad_sp_create_for_rbac
[azure-load-balancer-overview]: ../load-balancer/load-balancer-overview.md
[install-azure-cli]: /cli/azure/install-azure-cli
[service-principal]: ../active-directory/develop/active-directory-application-objects.md
[user-defined-routes]: ../load-balancer/load-balancer-overview.md