---
title: "從 Azure 容器登錄中的 hello aaaDeploy tooAzure 容器執行個體 |Azure 文件"
description: "部署 tooAzure 從 hello Azure 容器登錄中的容器執行個體"
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
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="6c35e-103">部署 tooAzure 從 hello Azure 容器登錄中的容器執行個體</span><span class="sxs-lookup"><span data-stu-id="6c35e-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="6c35e-104">hello Azure 容器登錄中是以 Azure 為基礎的私人登錄中，為 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="6c35e-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="6c35e-105">本文件涵蓋如何 toodeploy 容器映像儲存在容器登錄中 Azure hello tooAzure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="6c35e-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="6c35e-106">使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="6c35e-106">Using hello Azure CLI</span></span>

<span data-ttu-id="6c35e-107">hello Azure CLI 包含可用來建立和管理 Azure 容器執行個體中的容器命令。</span><span class="sxs-lookup"><span data-stu-id="6c35e-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="6c35e-108">如果您指定的私人映像中 hello`create`命令時，您也可以指定 hello 映像登錄所需密碼 tooauthenticate 與 hello 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="6c35e-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="6c35e-109">hello`create`命令也支援指定 hello`registry-login-server`和`registry-username`。</span><span class="sxs-lookup"><span data-stu-id="6c35e-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="6c35e-110">不過，hello Azure 容器登錄中的 hello 登入伺服器會一律*registryname*。 azurecr.io 和 hello 預設使用者名稱是*registryname*，因此，如果這些值會推斷從 hello 映像名稱未明確提供。</span><span class="sxs-lookup"><span data-stu-id="6c35e-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="6c35e-111">使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6c35e-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="6c35e-112">您也可以包括 hello Azure Resource Manager 範本中指定的 Azure 容器登錄 hello 屬性`imageRegistryCredentials`hello 容器群組定義中的屬性：</span><span class="sxs-lookup"><span data-stu-id="6c35e-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="6c35e-113">tooavoid 儲存容器登錄密碼直接在 hello 範本中，我們建議您將其儲存為中的秘密[Azure 金鑰保存庫](../key-vault/key-vault-manage-with-cli2.md)使用 hello hello 範本中參考它[之間的原生整合hello Azure 資源管理員與金鑰保存庫](../azure-resource-manager/resource-manager-keyvault-parameter.md)。</span><span class="sxs-lookup"><span data-stu-id="6c35e-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="6c35e-114">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6c35e-114">Using hello Azure portal</span></span>

<span data-ttu-id="6c35e-115">如果您維護 hello Azure 容器登錄中的容器映像，您就可以在 Azure 容器執行個體使用 hello Azure 入口網站，輕鬆建立容器。</span><span class="sxs-lookup"><span data-stu-id="6c35e-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="6c35e-116">在 hello Azure 入口網站，瀏覽 tooyour 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="6c35e-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="6c35e-117">選擇存放庫。</span><span class="sxs-lookup"><span data-stu-id="6c35e-117">Choose Repositories.</span></span>

    ![hello Azure 入口網站中的 hello Azure 容器登錄中功能表][acr-menu]

3. <span data-ttu-id="6c35e-119">選擇您想從 toodeploy hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6c35e-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="6c35e-120">以滑鼠右鍵按一下 hello 標記您想 toodeploy hello 容器映像。</span><span class="sxs-lookup"><span data-stu-id="6c35e-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![可供使用 Azure Container Instances 來啟動容器的快顯功能表][acr-runinstance-contextmenu]

5. <span data-ttu-id="6c35e-122">輸入 hello 容器的名稱和 hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c35e-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="6c35e-123">如果您想要也可以變更 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6c35e-123">You can also change hello default values if you wish.</span></span>

    ![建立 Azure Container Instances 的功能表][acr-create-deeplink]

6. <span data-ttu-id="6c35e-125">Hello 部署完成之後，您可以巡覽 hello 通知窗格 toofind toohello 容器群組，其 IP 位址和其他屬性。</span><span class="sxs-lookup"><span data-stu-id="6c35e-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Azure Container Instances 容器群組的詳細資料檢視][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="6c35e-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c35e-127">Next steps</span></span>

<span data-ttu-id="6c35e-128">了解 toobuild 容器，將其推送 tooa 私用容器登錄中，並將其部署 tooAzure 容器的執行個體所[完成 hello 教學課程](container-instances-tutorial-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6c35e-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
