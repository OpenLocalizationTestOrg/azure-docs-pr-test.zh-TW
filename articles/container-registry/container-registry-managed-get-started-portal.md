---
title: "建立私人 Docker 登錄 - Azure 入口網站 | Microsoft Docs"
description: "使用 Azure 入口網站開始建立及管理私人 Docker 容器登錄"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="2125b-103">使用 Azure 入口網站建立受管理的容器登錄</span><span class="sxs-lookup"><span data-stu-id="2125b-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="2125b-104">Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。</span><span class="sxs-lookup"><span data-stu-id="2125b-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="2125b-105">本指南詳述如何使用 Azure 入口網站建立受管理的 Azure Container Registry 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2125b-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="2125b-106">受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。</span><span class="sxs-lookup"><span data-stu-id="2125b-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="2125b-107">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="2125b-107">Log in to Azure</span></span>

<span data-ttu-id="2125b-108">登入 Azure 入口網站，網址是 http://portal.azure.com/。</span><span class="sxs-lookup"><span data-stu-id="2125b-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="2125b-109">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="2125b-109">Create a container registry</span></span>

1. <span data-ttu-id="2125b-110">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2125b-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="2125b-111">在 Marketplace 中搜尋 **Azure 容器登錄**，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="2125b-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="2125b-112">按一下 [建立]，這樣會開啟 ACR 建立刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2125b-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![容器登錄庫設定](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="2125b-114">在 [Azure 容器登錄] 刀鋒視窗中，輸入下列資訊。</span><span class="sxs-lookup"><span data-stu-id="2125b-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="2125b-115">完成後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2125b-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="2125b-116">a.</span><span class="sxs-lookup"><span data-stu-id="2125b-116">a.</span></span> <span data-ttu-id="2125b-117">**登錄名稱**：指定登錄的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="2125b-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="2125b-118">在此範例中，登錄庫名稱是 *myAzureContainerRegistry1*，但請替換成您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="2125b-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="2125b-119">此名稱只能包含字母和數字。</span><span class="sxs-lookup"><span data-stu-id="2125b-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="2125b-120">b.</span><span class="sxs-lookup"><span data-stu-id="2125b-120">b.</span></span> <span data-ttu-id="2125b-121">**資源群組**：選取現有的[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)，或輸入新群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="2125b-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="2125b-122">c.</span><span class="sxs-lookup"><span data-stu-id="2125b-122">c.</span></span> <span data-ttu-id="2125b-123">**位置**：選取[可使用](https://azure.microsoft.com/regions/services/)此服務的 Azure 資料中心位置，例如 [美國中南部]。</span><span class="sxs-lookup"><span data-stu-id="2125b-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="2125b-124">d.</span><span class="sxs-lookup"><span data-stu-id="2125b-124">d.</span></span> <span data-ttu-id="2125b-125">**管理員使用者**：如果您想，可啟用管理員使用者存取登錄。</span><span class="sxs-lookup"><span data-stu-id="2125b-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="2125b-126">您可以在建立登錄庫後變更此設定。</span><span class="sxs-lookup"><span data-stu-id="2125b-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="2125b-127">e.</span><span class="sxs-lookup"><span data-stu-id="2125b-127">e.</span></span> <span data-ttu-id="2125b-128">**使用受管理登錄**：選取 [是]，讓 ACR 自動管理登錄儲存體、使用 Webhook，以及使用 AAD 驗證。</span><span class="sxs-lookup"><span data-stu-id="2125b-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="2125b-129">f.</span><span class="sxs-lookup"><span data-stu-id="2125b-129">f.</span></span> <span data-ttu-id="2125b-130">**定價層**：選取定價層，以在這裡查看 ACR 定價的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2125b-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="2125b-131">登入 ACR 執行個體</span><span class="sxs-lookup"><span data-stu-id="2125b-131">Log in to ACR instance</span></span>

<span data-ttu-id="2125b-132">發送和提取容器映像之前，您必須登入 ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2125b-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="2125b-133">若要這麼做，請使用 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="2125b-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="2125b-134">首先，如有需要，請使用 [az login](/cli/azure/#login) 命令登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="2125b-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="2125b-135">接下來，使用 [az acr login](/cli/azure/acr#login) 命令登入 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="2125b-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="2125b-136">使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="2125b-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="2125b-137">列出容器映像</span><span class="sxs-lookup"><span data-stu-id="2125b-137">List container images</span></span>

<span data-ttu-id="2125b-138">使用 `az acr` CLI 命令來查詢儲存機制中的映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="2125b-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2125b-139">目前，容器登錄庫不支援用 `docker search` 命令查詢映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="2125b-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="2125b-140">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="2125b-140">List repositories</span></span>

<span data-ttu-id="2125b-141">下列範例會以 JSON (JavaScript 物件標記法) 格式列出登錄庫中的儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="2125b-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="2125b-142">列出標籤</span><span class="sxs-lookup"><span data-stu-id="2125b-142">List tags</span></span>

<span data-ttu-id="2125b-143">下列範例會以 JSON 格式列出 **samples/nginx** 儲存機制上的標籤：</span><span class="sxs-lookup"><span data-stu-id="2125b-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="2125b-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2125b-144">Next steps</span></span>

<span data-ttu-id="2125b-145">在本快速入門中，您已使用 Azure 入口網站建立受管理的 Azure Container Registry 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2125b-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2125b-146">使用 Docker CLI 推送您的第一個映像</span><span class="sxs-lookup"><span data-stu-id="2125b-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)