---
title: "aaaCreate 私用 Docker 容器登錄中的 Azure CLI |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="34187-103">建立受管理的容器登錄中使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="34187-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="34187-104">Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。</span><span class="sxs-lookup"><span data-stu-id="34187-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="34187-105">本指南詳述建立受管理的 Azure 容器登錄中執行個體使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="34187-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="34187-106">受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。</span><span class="sxs-lookup"><span data-stu-id="34187-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="34187-107">如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="34187-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="34187-108">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="34187-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="34187-109">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="34187-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="34187-110">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="34187-110">Create a resource group</span></span>

<span data-ttu-id="34187-111">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="34187-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="34187-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="34187-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="34187-113">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westcentralus*位置。</span><span class="sxs-lookup"><span data-stu-id="34187-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="34187-114">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="34187-114">Create a container registry</span></span>

<span data-ttu-id="34187-115">建立使用 hello ACR 執行個體[az acr 建立](/cli/azure/acr#create)命令。</span><span class="sxs-lookup"><span data-stu-id="34187-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="34187-116">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="34187-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="34187-117">hello 範例中的 hello 登錄名稱是*myContainerRegistry1*，以取代您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="34187-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="34187-118">建立 hello 登錄時，hello 輸出會是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="34187-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="34187-119">登入 tooACR 執行個體</span><span class="sxs-lookup"><span data-stu-id="34187-119">Log in tooACR instance</span></span>

<span data-ttu-id="34187-120">然後再推送和提取容器映像，您必須登入 toohello ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="34187-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="34187-121">因此，使用 toodo 的 hello [az acr 登入](/cli/azure/acr#login)命令。</span><span class="sxs-lookup"><span data-stu-id="34187-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="34187-122">hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。</span><span class="sxs-lookup"><span data-stu-id="34187-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="34187-123">使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="34187-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="34187-124">列出容器映像</span><span class="sxs-lookup"><span data-stu-id="34187-124">List container images</span></span>

<span data-ttu-id="34187-125">使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。</span><span class="sxs-lookup"><span data-stu-id="34187-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="34187-126">目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。</span><span class="sxs-lookup"><span data-stu-id="34187-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="34187-127">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="34187-127">List repositories</span></span>

<span data-ttu-id="34187-128">hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="34187-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="34187-129">列出標籤</span><span class="sxs-lookup"><span data-stu-id="34187-129">List tags</span></span>

<span data-ttu-id="34187-130">hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：</span><span class="sxs-lookup"><span data-stu-id="34187-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="34187-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34187-131">Next steps</span></span>

<span data-ttu-id="34187-132">在這個快速入門中，您已建立受管理的 Azure 容器登錄中執行個體，使用 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="34187-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="34187-133">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="34187-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
