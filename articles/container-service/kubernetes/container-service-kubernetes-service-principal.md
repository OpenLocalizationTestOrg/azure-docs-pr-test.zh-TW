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
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="96195-103">在 Container Service 中設定 Kubernetes 叢集的 Azure AD 服務主體</span><span class="sxs-lookup"><span data-stu-id="96195-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="96195-104">在 Azure 容器服務中，需要 Kubernetes 叢集[Azure Active Directory 服務主體](../../active-directory/develop/active-directory-application-objects.md)toointeract Azure 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="96195-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="96195-105">hello 服務主體需要 toodynamically 管理資源例如[使用者定義的路由](../../virtual-network/virtual-networks-udr-overview.md)和 hello[層 4 Azure 負載平衡器](../../load-balancer/load-balancer-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="96195-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="96195-106">本文將說明不同的選項 tooset 服務主體 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="96195-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="96195-107">例如，如果您安裝並設定 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)，您可以執行 hello [ `az acs create` ](/cli/azure/acs#create)命令 toocreate hello Kubernetes 叢集和 hello 服務主體在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="96195-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="96195-108">Hello 服務主體的需求</span><span class="sxs-lookup"><span data-stu-id="96195-108">Requirements for hello service principal</span></span>

<span data-ttu-id="96195-109">您可以使用現有 Azure AD 服務主體符合 hello 下列需求，或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="96195-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="96195-110">**範圍**: hello hello 訂用帳戶中的資源群組 toodeploy hello Kubernetes 叢集，或 (較不 restrictively) hello 訂用帳戶使用 toodeploy hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="96195-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="96195-111">**角色**：**參與者**</span><span class="sxs-lookup"><span data-stu-id="96195-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="96195-112">**用戶端密碼**：必須是密碼。</span><span class="sxs-lookup"><span data-stu-id="96195-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="96195-113">目前，您無法使用針對憑證驗證設定的服務主體。</span><span class="sxs-lookup"><span data-stu-id="96195-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="96195-114">toocreate 服務主體，您必須具有權限 tooregister 應用程式與您的 Azure AD 租用戶，tooassign hello 應用程式 tooa 角色您訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="96195-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="96195-115">如果您擁有 hello 所需的權限，toosee [hello 入口網站中檢查](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="96195-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="96195-116">選項 1：在 Azure AD 中建立服務主體</span><span class="sxs-lookup"><span data-stu-id="96195-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="96195-117">如果您想 toocreate Azure AD 服務主體，在部署 Kubernetes 叢集之前，Azure 會提供數種方法。</span><span class="sxs-lookup"><span data-stu-id="96195-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="96195-118">hello，下列命令範例顯示如何 toodo 這與 hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="96195-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="96195-119">您也可以建立服務主體使用[Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md)，hello[入口網站](../../azure-resource-manager/resource-group-create-service-principal-portal.md)，或其他方法。</span><span class="sxs-lookup"><span data-stu-id="96195-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="96195-120">輸出是類似 toohello 下列 （如下所示 redacted）：</span><span class="sxs-lookup"><span data-stu-id="96195-120">Output is similar toohello following (shown here redacted):</span></span>

![建立服務主體](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="96195-122">反白顯示為 hello**用戶端識別碼**(`appId`) 和 hello**用戶端密碼**(`password`)，您使用服務主體參數做為叢集部署。</span><span class="sxs-lookup"><span data-stu-id="96195-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="96195-123">建立 hello Kubernetes 叢集時，指定服務主體</span><span class="sxs-lookup"><span data-stu-id="96195-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="96195-124">提供 hello**用戶端識別碼**(也稱為 hello `appId`，應用程式識別碼) 和**用戶端密碼**(`password`) 的現有服務主體做為參數，當您建立 helloKubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="96195-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="96195-125">請確定 hello 服務主體符合 hello 的需求，在開始這篇文章的 hello。</span><span class="sxs-lookup"><span data-stu-id="96195-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="96195-126">部署使用 hello hello Kubernetes 叢集時，您可以指定這些參數[Azure 命令列介面 (CLI) 2.0](container-service-kubernetes-walkthrough.md)， [Azure 入口網站](../dcos-swarm/container-service-deployment.md)，或其他方法。</span><span class="sxs-lookup"><span data-stu-id="96195-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="96195-127">當指定 hello**用戶端識別碼**，是確定 toouse hello `appId`，不 hello `ObjectId`，hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="96195-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="96195-128">hello 下列範例顯示其中一種方式 toopass hello 參數以 hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="96195-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="96195-129">這個範例會使用 hello [Kubernetes 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)。</span><span class="sxs-lookup"><span data-stu-id="96195-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="96195-130">[下載](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json)hello 範本參數檔案`azuredeploy.parameters.json`從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="96195-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="96195-131">toospecify hello 服務主體，輸入的值`servicePrincipalClientId`和`servicePrincipalClientSecret`hello 檔案中。</span><span class="sxs-lookup"><span data-stu-id="96195-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="96195-132">(您也需要 tooprovide 自己值`dnsNamePrefix`和`sshRSAPublicKey`。</span><span class="sxs-lookup"><span data-stu-id="96195-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="96195-133">hello 後者是 hello SSH 公開金鑰的金鑰 tooaccess hello 叢集）。儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="96195-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![傳遞服務主體參數](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="96195-135">下列命令，並透過執行的 hello `--parameters` tooset hello 路徑 toohello azuredeploy.parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="96195-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="96195-136">此命令會將部署在您建立稱為資源群組中的 hello 叢集`myResourceGroup`hello 美國西部區域中。</span><span class="sxs-lookup"><span data-stu-id="96195-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="96195-137">選項 2： 建立 hello 的叢集時，產生服務主體`az acs create`</span><span class="sxs-lookup"><span data-stu-id="96195-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="96195-138">如果您要執行 hello [ `az acs create` ](/cli/azure/acs#create)命令 toocreate hello Kubernetes 叢集，您必須 hello 選項 toogenerate 服務主體自動。</span><span class="sxs-lookup"><span data-stu-id="96195-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="96195-139">至於其他 Kubernetes 叢集建立選項，您可以在執行 `az acs create` 時指定現有服務主體的參數。</span><span class="sxs-lookup"><span data-stu-id="96195-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="96195-140">不過，當您省略這些參數，hello Azure CLI 會建立一個用於自動與容器服務。</span><span class="sxs-lookup"><span data-stu-id="96195-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="96195-141">這會明確地在 hello 部署期間會發生。</span><span class="sxs-lookup"><span data-stu-id="96195-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="96195-142">hello 下列命令會建立 Kubernetes 叢集並產生 SSH 金鑰和服務主體認證：</span><span class="sxs-lookup"><span data-stu-id="96195-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="96195-143">如果您的帳戶不包含 hello Azure AD 和訂用帳戶的權限 toocreate 服務主體，hello 命令會產生類似的錯誤太`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="96195-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="96195-144">其他考量</span><span class="sxs-lookup"><span data-stu-id="96195-144">Additional considerations</span></span>

* <span data-ttu-id="96195-145">如果您沒有權限 toocreate 服務主體您訂用帳戶中，您可能需要 tooask 您的 Azure AD 或訂用帳戶管理員 tooassign hello 必要的權限，或請要求他們以 Azure 容器服務的服務主體 toouse。</span><span class="sxs-lookup"><span data-stu-id="96195-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="96195-146">hello 服務主體的 Kubernetes 是 hello 叢集組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="96195-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="96195-147">不過，請勿使用 hello 識別 toodeploy hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="96195-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="96195-148">每個服務主體都會與 Azure AD 應用程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="96195-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="96195-149">hello Kubernetes 叢集的服務主體可以是相關聯的任何有效的 Azure AD 應用程式名稱 (例如： `https://www.contoso.org/example`)。</span><span class="sxs-lookup"><span data-stu-id="96195-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="96195-150">hello hello 應用程式的 URL 沒有 toobe 實際的端點。</span><span class="sxs-lookup"><span data-stu-id="96195-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="96195-151">當指定 hello 服務主體**用戶端識別碼**，您可以使用的 hello hello 值`appId`（如本文中所示） 或 hello 相對應的服務主體`name`(例如，`https://www.contoso.org/example`)。</span><span class="sxs-lookup"><span data-stu-id="96195-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="96195-152">在 hello master 和 hello Kubernetes 叢集中的 Vm 代理程式，hello 服務主體認證會儲存在 hello 檔案 /etc/kubernetes/azure.json。</span><span class="sxs-lookup"><span data-stu-id="96195-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="96195-153">當您使用 hello`az acs create`自動命令 toogenerate hello 服務主體，hello 服務主體認證會寫入 toohello 檔案 ~/.azure/acsServicePrincipal.json hello 機器上的使用 toorun hello 命令。</span><span class="sxs-lookup"><span data-stu-id="96195-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="96195-154">當您使用 hello`az acs create`自動命令 toogenerate hello 服務主體，也可以驗證 hello 服務主體[Azure 容器登錄](../../container-registry/container-registry-intro.md)中建立 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="96195-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="96195-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96195-155">Next steps</span></span>

* <span data-ttu-id="96195-156">[開始使用容器服務叢集中的 Kubernetes](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="96195-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="96195-157">tootroubleshoot hello 服務主體的 Kubernetes，請參閱 hello [ACS Engine 文件集](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="96195-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


