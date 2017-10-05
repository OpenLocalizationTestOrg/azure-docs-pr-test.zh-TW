---
title: "建立私人 Docker 容器登錄 - Azure CLI | Microsoft Docs"
description: "使用 Azure CLI 2.0 開始建立及管理私人 Docker 容器登錄"
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
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="51b9a-103">使用 Azure CLI 建立受管理的容器登錄</span><span class="sxs-lookup"><span data-stu-id="51b9a-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="51b9a-104">Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。</span><span class="sxs-lookup"><span data-stu-id="51b9a-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="51b9a-105">本指南詳述如何使用 Azure CLI 建立受管理的 Azure Container Registry 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51b9a-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="51b9a-106">受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。</span><span class="sxs-lookup"><span data-stu-id="51b9a-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="51b9a-107">如果您選擇在本機安裝和使用 CLI，本快速入門會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="51b9a-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="51b9a-108">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="51b9a-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="51b9a-109">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="51b9a-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="51b9a-110">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="51b9a-110">Create a resource group</span></span>

<span data-ttu-id="51b9a-111">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b9a-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="51b9a-112">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="51b9a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="51b9a-113">下列範例會在 *westcentralus* 位置建立名為 *myResourceGroup* 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b9a-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="51b9a-114">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="51b9a-114">Create a container registry</span></span>

<span data-ttu-id="51b9a-115">使用 [az acr create](/cli/azure/acr#create) 命令，以建立 ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51b9a-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="51b9a-116">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="51b9a-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="51b9a-117">範例中的登錄名稱是 *myContainerRegistry1*，請替換成您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="51b9a-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="51b9a-118">建立登錄時，輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="51b9a-118">When the registry is created, the output is similar to the following:</span></span>

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

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="51b9a-119">登入 ACR 執行個體</span><span class="sxs-lookup"><span data-stu-id="51b9a-119">Log in to ACR instance</span></span>

<span data-ttu-id="51b9a-120">發送和提取容器映像之前，您必須登入 ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51b9a-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="51b9a-121">若要這樣做，請使用 [az acr login](/cli/azure/acr#login) 命令。</span><span class="sxs-lookup"><span data-stu-id="51b9a-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="51b9a-122">此命令在完成之後會傳回「登入成功」訊息。</span><span class="sxs-lookup"><span data-stu-id="51b9a-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="51b9a-123">使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="51b9a-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="51b9a-124">列出容器映像</span><span class="sxs-lookup"><span data-stu-id="51b9a-124">List container images</span></span>

<span data-ttu-id="51b9a-125">使用 `az acr` CLI 命令來查詢儲存機制中的映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="51b9a-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="51b9a-126">目前，容器登錄庫不支援用 `docker search` 命令查詢映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="51b9a-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="51b9a-127">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="51b9a-127">List repositories</span></span>

<span data-ttu-id="51b9a-128">下列範例會以 JSON (JavaScript 物件標記法) 格式列出登錄庫中的儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="51b9a-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="51b9a-129">列出標籤</span><span class="sxs-lookup"><span data-stu-id="51b9a-129">List tags</span></span>

<span data-ttu-id="51b9a-130">下列範例會以 JSON 格式列出 **samples/nginx** 儲存機制上的標籤：</span><span class="sxs-lookup"><span data-stu-id="51b9a-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="51b9a-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51b9a-131">Next steps</span></span>

<span data-ttu-id="51b9a-132">在本快速入門中，您已使用 Azure CLI 建立受管理的 Azure Container Registry 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51b9a-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51b9a-133">使用 Docker CLI 推送您的第一個映像</span><span class="sxs-lookup"><span data-stu-id="51b9a-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
