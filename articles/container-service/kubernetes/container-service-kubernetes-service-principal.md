---
title: "Azure Kubernetes 叢集 aaaService 主體 |Microsoft 文件"
description: "在 Azure Container Service 中建立和管理 Kubernetes 叢集的 Azure Active Directory 服務主體"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>在 Container Service 中設定 Kubernetes 叢集的 Azure AD 服務主體


在 Azure 容器服務中，需要 Kubernetes 叢集[Azure Active Directory 服務主體](../../active-directory/develop/active-directory-application-objects.md)toointeract Azure 應用程式開發介面。 hello 服務主體需要 toodynamically 管理資源例如[使用者定義的路由](../../virtual-network/virtual-networks-udr-overview.md)和 hello[層 4 Azure 負載平衡器](../../load-balancer/load-balancer-overview.md)。 


本文將說明不同的選項 tooset 服務主體 Kubernetes 叢集。 例如，如果您安裝並設定 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)，您可以執行 hello [ `az acs create` ](/cli/azure/acs#create)命令 toocreate hello Kubernetes 叢集和 hello 服務主體在 hello 相同的時間。


## <a name="requirements-for-hello-service-principal"></a>Hello 服務主體的需求

您可以使用現有 Azure AD 服務主體符合 hello 下列需求，或另外新建一個。

* **範圍**: hello hello 訂用帳戶中的資源群組 toodeploy hello Kubernetes 叢集，或 (較不 restrictively) hello 訂用帳戶使用 toodeploy hello 叢集。

* **角色**：**參與者**

* **用戶端密碼**：必須是密碼。 目前，您無法使用針對憑證驗證設定的服務主體。

> [!IMPORTANT] 
> toocreate 服務主體，您必須具有權限 tooregister 應用程式與您的 Azure AD 租用戶，tooassign hello 應用程式 tooa 角色您訂用帳戶中。 如果您擁有 hello 所需的權限，toosee [hello 入口網站中檢查](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)。 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>選項 1：在 Azure AD 中建立服務主體

如果您想 toocreate Azure AD 服務主體，在部署 Kubernetes 叢集之前，Azure 會提供數種方法。 

hello，下列命令範例顯示如何 toodo 這與 hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)。 您也可以建立服務主體使用[Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md)，hello[入口網站](../../azure-resource-manager/resource-group-create-service-principal-portal.md)，或其他方法。

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

輸出是類似 toohello 下列 （如下所示 redacted）：

![建立服務主體](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

反白顯示為 hello**用戶端識別碼**(`appId`) 和 hello**用戶端密碼**(`password`)，您使用服務主體參數做為叢集部署。


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>建立 hello Kubernetes 叢集時，指定服務主體

提供 hello**用戶端識別碼**(也稱為 hello `appId`，應用程式識別碼) 和**用戶端密碼**(`password`) 的現有服務主體做為參數，當您建立 helloKubernetes 叢集。 請確定 hello 服務主體符合 hello 的需求，在開始這篇文章的 hello。

部署使用 hello hello Kubernetes 叢集時，您可以指定這些參數[Azure 命令列介面 (CLI) 2.0](container-service-kubernetes-walkthrough.md)， [Azure 入口網站](../dcos-swarm/container-service-deployment.md)，或其他方法。

>[!TIP] 
>當指定 hello**用戶端識別碼**，是確定 toouse hello `appId`，不 hello `ObjectId`，hello 服務主體。
>

hello 下列範例顯示其中一種方式 toopass hello 參數以 hello Azure CLI 2.0。 這個範例會使用 hello [Kubernetes 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)。

1. [下載](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json)hello 範本參數檔案`azuredeploy.parameters.json`從 GitHub。

2. toospecify hello 服務主體，輸入的值`servicePrincipalClientId`和`servicePrincipalClientSecret`hello 檔案中。 (您也需要 tooprovide 自己值`dnsNamePrefix`和`sshRSAPublicKey`。 hello 後者是 hello SSH 公開金鑰的金鑰 tooaccess hello 叢集）。儲存 hello 檔案。

    ![傳遞服務主體參數](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. 下列命令，並透過執行的 hello `--parameters` tooset hello 路徑 toohello azuredeploy.parameters.json 檔案。 此命令會將部署在您建立稱為資源群組中的 hello 叢集`myResourceGroup`hello 美國西部區域中。

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>選項 2： 建立 hello 的叢集時，產生服務主體`az acs create`

如果您要執行 hello [ `az acs create` ](/cli/azure/acs#create)命令 toocreate hello Kubernetes 叢集，您必須 hello 選項 toogenerate 服務主體自動。

至於其他 Kubernetes 叢集建立選項，您可以在執行 `az acs create` 時指定現有服務主體的參數。 不過，當您省略這些參數，hello Azure CLI 會建立一個用於自動與容器服務。 這會明確地在 hello 部署期間會發生。 

hello 下列命令會建立 Kubernetes 叢集並產生 SSH 金鑰和服務主體認證：

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> 如果您的帳戶不包含 hello Azure AD 和訂用帳戶的權限 toocreate 服務主體，hello 命令會產生類似的錯誤太`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>其他考量

* 如果您沒有權限 toocreate 服務主體您訂用帳戶中，您可能需要 tooask 您的 Azure AD 或訂用帳戶管理員 tooassign hello 必要的權限，或請要求他們以 Azure 容器服務的服務主體 toouse。 

* hello 服務主體的 Kubernetes 是 hello 叢集組態的一部分。 不過，請勿使用 hello 識別 toodeploy hello 叢集。

* 每個服務主體都會與 Azure AD 應用程式相關聯。 hello Kubernetes 叢集的服務主體可以是相關聯的任何有效的 Azure AD 應用程式名稱 (例如： `https://www.contoso.org/example`)。 hello hello 應用程式的 URL 沒有 toobe 實際的端點。

* 當指定 hello 服務主體**用戶端識別碼**，您可以使用的 hello hello 值`appId`（如本文中所示） 或 hello 相對應的服務主體`name`(例如，`https://www.contoso.org/example`)。

* 在 hello master 和 hello Kubernetes 叢集中的 Vm 代理程式，hello 服務主體認證會儲存在 hello 檔案 /etc/kubernetes/azure.json。

* 當您使用 hello`az acs create`自動命令 toogenerate hello 服務主體，hello 服務主體認證會寫入 toohello 檔案 ~/.azure/acsServicePrincipal.json hello 機器上的使用 toorun hello 命令。 

* 當您使用 hello`az acs create`自動命令 toogenerate hello 服務主體，也可以驗證 hello 服務主體[Azure 容器登錄](../../container-registry/container-registry-intro.md)中建立 hello 相同訂用帳戶。




## <a name="next-steps"></a>後續步驟

* [開始使用容器服務叢集中的 Kubernetes](container-service-kubernetes-walkthrough.md)。

* tootroubleshoot hello 服務主體的 Kubernetes，請參閱 hello [ACS Engine 文件集](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting)。


