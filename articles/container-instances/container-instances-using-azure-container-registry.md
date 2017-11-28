---
title: "從 Azure Container Registry 部署至 Azure Container Instances | Azure Docs"
description: "從 Azure Container Registry 部署至 Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="816d6-103">從 Azure Container Registry 部署至 Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="816d6-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="816d6-104">Azure Container Registry 是以 Azure 為基礎的私人登錄，用於裝載 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="816d6-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="816d6-105">本文說明如何將儲存於 Azure Container Registry 的容器映像部署至 Azure Container Instances。</span><span class="sxs-lookup"><span data-stu-id="816d6-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="816d6-106">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="816d6-106">Using the Azure CLI</span></span>

<span data-ttu-id="816d6-107">Azure CLI 包括可用於建立和管理 Azure Container Instances 中容器的命令。</span><span class="sxs-lookup"><span data-stu-id="816d6-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="816d6-108">如果您在 `create` 命令中指定私人映像，則也可以指定對容器登錄進行驗證所需的映像登錄密碼。</span><span class="sxs-lookup"><span data-stu-id="816d6-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="816d6-109">`create` 命令也支援指定 `registry-login-server` 和 `registry-username`。</span><span class="sxs-lookup"><span data-stu-id="816d6-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="816d6-110">不過，Azure Container Registry 的登入伺服器永遠會是 registryname.azurecr.io，而預設使用者名稱是 registryname，因此如果未明確提供，您仍可從映像名稱推斷這些值。</span><span class="sxs-lookup"><span data-stu-id="816d6-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="816d6-111">使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="816d6-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="816d6-112">您可以在容器群組定義中加入 `imageRegistryCredentials` 屬性，以在 Azure Resource Manager 範本中指定 Azure Container Registry 的屬性：</span><span class="sxs-lookup"><span data-stu-id="816d6-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="816d6-113">為了避免在範本中直接儲存容器登錄密碼，我們建議您將其儲存為 [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) 中的祕密，並在範本中使用 [Azure Resource Manager 和 Key Vault 之間的原生整合](../azure-resource-manager/resource-manager-keyvault-parameter.md)參考該祕密。</span><span class="sxs-lookup"><span data-stu-id="816d6-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="816d6-114">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="816d6-114">Using the Azure portal</span></span>

<span data-ttu-id="816d6-115">如果您在 Azure Container Registry 中保有容器映像，您就可以使用 Azure 入口網站在 Azure Container Instances 中輕鬆地建立容器。</span><span class="sxs-lookup"><span data-stu-id="816d6-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="816d6-116">在 Azure 入口網站中，瀏覽到您的容器登錄。</span><span class="sxs-lookup"><span data-stu-id="816d6-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="816d6-117">選擇存放庫。</span><span class="sxs-lookup"><span data-stu-id="816d6-117">Choose Repositories.</span></span>

    ![Azure 入口網站中的 Azure Container Registry 功能表][acr-menu]

3. <span data-ttu-id="816d6-119">選擇您想要從哪個存放庫進行部署。</span><span class="sxs-lookup"><span data-stu-id="816d6-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="816d6-120">以滑鼠右鍵按一下您想要部署的容器映像標記。</span><span class="sxs-lookup"><span data-stu-id="816d6-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![可供使用 Azure Container Instances 來啟動容器的快顯功能表][acr-runinstance-contextmenu]

5. <span data-ttu-id="816d6-122">分別為容器和資源群組輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="816d6-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="816d6-123">如有需要，您也可以變更預設值。</span><span class="sxs-lookup"><span data-stu-id="816d6-123">You can also change the default values if you wish.</span></span>

    ![建立 Azure Container Instances 的功能表][acr-create-deeplink]

6. <span data-ttu-id="816d6-125">部署完成之後，您可以從 [通知] 窗格瀏覽至容器群組，以尋找其 IP 位址和其他屬性。</span><span class="sxs-lookup"><span data-stu-id="816d6-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Azure Container Instances 容器群組的詳細資料檢視][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="816d6-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="816d6-127">Next steps</span></span>

<span data-ttu-id="816d6-128">透過[完成教學課程](container-instances-tutorial-prepare-app.md)，了解如何建置容器、將其推送至私人容器登錄和將其部署至 Azure Container Instances。</span><span class="sxs-lookup"><span data-stu-id="816d6-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
