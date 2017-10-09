---
title: "aaaCreate 的私用 Docker 登錄-而 Azure 入口網站 |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure 入口網站"
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
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="b2c3f-103">建立受管理的容器登錄中使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b2c3f-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="b2c3f-104">Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="b2c3f-105">本指南詳述建立受管理的 Azure 容器登錄中執行個體使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="b2c3f-106">受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="b2c3f-107">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2c3f-107">Log in tooAzure</span></span>

<span data-ttu-id="b2c3f-108">登入 toohello http://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b2c3f-109">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="b2c3f-109">Create a container registry</span></span>

1. <span data-ttu-id="b2c3f-110">按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="b2c3f-111">搜尋 hello marketplace 中的**Azure 容器登錄**並加以選取。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="b2c3f-112">按一下**建立**來開啟 hello ACR 建立刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![容器登錄庫設定](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="b2c3f-114">在 hello **Azure 容器登錄中**刀鋒視窗中，輸入下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="b2c3f-115">完成後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="b2c3f-116">a.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-116">a.</span></span> <span data-ttu-id="b2c3f-117">**登錄名稱**：指定登錄的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="b2c3f-118">在此範例中，是 hello 登錄名稱*myAzureContainerRegistry1*，但以取代您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="b2c3f-119">hello 名稱只能包含字母和數字。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="b2c3f-120">b.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-120">b.</span></span> <span data-ttu-id="b2c3f-121">**資源群組**： 選取現有[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="b2c3f-122">c.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-122">c.</span></span> <span data-ttu-id="b2c3f-123">**位置**： 選取 hello 服務所在的 Azure 資料中心位置[可用](https://azure.microsoft.com/regions/services/)，例如**美國中南部**。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="b2c3f-124">d.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-124">d.</span></span> <span data-ttu-id="b2c3f-125">**系統管理使用者**： 如果您想，讓系統管理員使用者 tooaccess hello 登錄。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="b2c3f-126">您可以變更此設定建立 hello 登錄之後。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="b2c3f-127">e.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-127">e.</span></span> <span data-ttu-id="b2c3f-128">**使用 managed 的登錄**： 選取 [是] toohave ACR 自動管理 hello 登錄存放裝置、 使用 webhook，以及使用 AAD 驗證。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="b2c3f-129">f.</span><span class="sxs-lookup"><span data-stu-id="b2c3f-129">f.</span></span> <span data-ttu-id="b2c3f-130">**定價層**：選取定價層，以在這裡查看 ACR 定價的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="b2c3f-131">登入 tooACR 執行個體</span><span class="sxs-lookup"><span data-stu-id="b2c3f-131">Log in tooACR instance</span></span>

<span data-ttu-id="b2c3f-132">然後再推送和提取容器映像，您必須登入 toohello ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="b2c3f-133">toodo 因此，使用 Azure CLI 2.0 hello。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="b2c3f-134">首先，如有需要登入 Azure 使用 hello [az 登入](/cli/azure/#login)命令。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="b2c3f-135">接下來，使用 hello [az acr 登入](/cli/azure/acr#login)命令 toolog toohello Azure 容器登錄中的。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="b2c3f-136">使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="b2c3f-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="b2c3f-137">列出容器映像</span><span class="sxs-lookup"><span data-stu-id="b2c3f-137">List container images</span></span>

<span data-ttu-id="b2c3f-138">使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c3f-139">目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="b2c3f-140">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="b2c3f-140">List repositories</span></span>

<span data-ttu-id="b2c3f-141">hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="b2c3f-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="b2c3f-142">列出標籤</span><span class="sxs-lookup"><span data-stu-id="b2c3f-142">List tags</span></span>

<span data-ttu-id="b2c3f-143">hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：</span><span class="sxs-lookup"><span data-stu-id="b2c3f-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="b2c3f-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2c3f-144">Next steps</span></span>

<span data-ttu-id="b2c3f-145">在這個快速入門中，您已建立的受管理的 Azure 容器登錄中執行個體使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b2c3f-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2c3f-146">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="b2c3f-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
