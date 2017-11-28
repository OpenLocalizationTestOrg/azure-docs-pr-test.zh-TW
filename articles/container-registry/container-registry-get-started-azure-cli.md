---
title: "aaaCreate 私用 Docker 容器登錄中的 Azure CLI |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="6b72c-103">建立私用 Docker 容器登錄中使用 Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="6b72c-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="6b72c-104">在 hello 中使用命令[Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate 容器登錄和管理其設定從 Linux、 Mac 或 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="6b72c-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="6b72c-105">您也可以建立及管理使用 hello 容器登錄[Azure 入口網站](container-registry-get-started-portal.md)或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="6b72c-106">背景和概念，請參閱[hello 概觀](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6b72c-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="6b72c-107">如需容器登錄 CLI 命令的說明 (`az acr`命令)，傳遞 hello`-h`參數 tooany 命令。</span><span class="sxs-lookup"><span data-stu-id="6b72c-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6b72c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6b72c-108">Prerequisites</span></span>
* <span data-ttu-id="6b72c-109">**Azure CLI 2.0**: tooinstall 和開始使用 hello CLI 2.0，請參閱 hello[安裝指示](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="6b72c-110">執行登入 Azure 訂用帳戶 tooyour `az login`。</span><span class="sxs-lookup"><span data-stu-id="6b72c-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="6b72c-111">如需詳細資訊，請參閱[hello CLI 2.0 使用者入門](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="6b72c-112">**資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6b72c-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="6b72c-113">請確定 hello 資源群組是在 hello 容器登錄服務所在的位置[可用](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="6b72c-114">使用資源群組的 toocreate hello CLI 2.0，請參閱[hello CLI 2.0 參考](/cli/azure/group)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="6b72c-115">**儲存體帳戶**（選擇性）： 建立標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)tooback hello 容器登錄中 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="6b72c-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="6b72c-116">如果您未指定儲存體帳戶時建立登錄中的以`az acr create`，hello 命令為您建立一個。</span><span class="sxs-lookup"><span data-stu-id="6b72c-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="6b72c-117">儲存體帳戶使用 toocreate hello CLI 2.0，請參閱[hello CLI 2.0 參考](/cli/azure/storage/account)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="6b72c-118">目前不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="6b72c-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="6b72c-119">**服務主體**（選擇性）： 當您建立登錄以 hello CLI 時，依預設它會無法存取權限設定。</span><span class="sxs-lookup"><span data-stu-id="6b72c-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="6b72c-120">根據您的需求，您可以指定現有的 Azure Active Directory 服務主體 tooa 登錄 （或建立並指派新的），或啟用 hello 登錄系統管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b72c-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="6b72c-121">請參閱本文稍後的 hello 章節。</span><span class="sxs-lookup"><span data-stu-id="6b72c-121">See hello sections later in this article.</span></span> <span data-ttu-id="6b72c-122">如需登錄存取權的詳細資訊，請參閱[與 hello 容器登錄中的 Authenticate](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="6b72c-123">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="6b72c-123">Create a container registry</span></span>
<span data-ttu-id="6b72c-124">執行 hello`az acr create`命令 toocreate 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="6b72c-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="6b72c-125">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6b72c-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="6b72c-126">hello 範例中的 hello 登錄名稱`myRegistry1`，但以取代您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="6b72c-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="6b72c-127">下列命令會使用 hello 最少參數 toocreate 容器登錄中的 hello `myRegistry1` hello 資源群組中`myResourceGroup`，並使用 hello*基本*sku:</span><span class="sxs-lookup"><span data-stu-id="6b72c-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="6b72c-128">`--storage-account-name` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="6b72c-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="6b72c-129">如果未指定，儲存體帳戶建立 hello 登錄名稱所組成的名稱，並 hello 的時間戳記指定資源群組。</span><span class="sxs-lookup"><span data-stu-id="6b72c-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="6b72c-130">建立 hello 登錄時，hello 輸出會是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="6b72c-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="6b72c-131">請特別注意︰</span><span class="sxs-lookup"><span data-stu-id="6b72c-131">Take special note:</span></span>

* <span data-ttu-id="6b72c-132">`id`Hello 登錄您的訂閱，如果您想要 tooassign 服務主體，則需要在識別項。</span><span class="sxs-lookup"><span data-stu-id="6b72c-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="6b72c-133">`loginServer`-您指定過 hello 完整限定的名稱[登入 toohello 登錄](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6b72c-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="6b72c-134">在此範例中，hello 名稱是`myregistry1.exp.azurecr.io`（全部小寫）。</span><span class="sxs-lookup"><span data-stu-id="6b72c-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="6b72c-135">指派服務主體</span><span class="sxs-lookup"><span data-stu-id="6b72c-135">Assign a service principal</span></span>
<span data-ttu-id="6b72c-136">使用 CLI 2.0 命令 tooassign Azure Active Directory 服務主體 tooa 登錄。</span><span class="sxs-lookup"><span data-stu-id="6b72c-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="6b72c-137">hello 這些範例中的服務主體指派 hello 擁有者角色，但您可以指派[其他角色](../active-directory/role-based-access-control-configure.md)如果您想要。</span><span class="sxs-lookup"><span data-stu-id="6b72c-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="6b72c-138">建立服務主體，並指派存取 toohello 登錄</span><span class="sxs-lookup"><span data-stu-id="6b72c-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="6b72c-139">Hello 下列命令，在新的服務主體指派擁有者角色存取 toohello 登錄識別碼傳遞以 hello`--scopes`參數。</span><span class="sxs-lookup"><span data-stu-id="6b72c-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="6b72c-140">指定強式密碼以 hello`--password`參數。</span><span class="sxs-lookup"><span data-stu-id="6b72c-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="6b72c-141">指派現有的服務主體</span><span class="sxs-lookup"><span data-stu-id="6b72c-141">Assign an existing service principal</span></span>
<span data-ttu-id="6b72c-142">如果您已經有服務主體，而且想 tooassign 它擁有者角色存取 toohello 登錄中，執行下列範例命令類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="6b72c-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="6b72c-143">您將使用 hello hello 服務主體的應用程式識別碼傳遞`--assignee`參數：</span><span class="sxs-lookup"><span data-stu-id="6b72c-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="6b72c-144">管理管理員認證</span><span class="sxs-lookup"><span data-stu-id="6b72c-144">Manage admin credentials</span></span>
<span data-ttu-id="6b72c-145">系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b72c-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="6b72c-146">下列範例會顯示的 hello `az acr` CLI 命令的容器登錄 toomanage hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6b72c-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="6b72c-147">取得管理員使用者認證</span><span class="sxs-lookup"><span data-stu-id="6b72c-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="6b72c-148">啟用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="6b72c-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="6b72c-149">停用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="6b72c-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="6b72c-150">列出映像和標籤</span><span class="sxs-lookup"><span data-stu-id="6b72c-150">List images and tags</span></span>
<span data-ttu-id="6b72c-151">使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。</span><span class="sxs-lookup"><span data-stu-id="6b72c-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="6b72c-152">目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。</span><span class="sxs-lookup"><span data-stu-id="6b72c-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="6b72c-153">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="6b72c-153">List repositories</span></span>
<span data-ttu-id="6b72c-154">hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="6b72c-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="6b72c-155">列出標籤</span><span class="sxs-lookup"><span data-stu-id="6b72c-155">List tags</span></span>
<span data-ttu-id="6b72c-156">hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：</span><span class="sxs-lookup"><span data-stu-id="6b72c-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="6b72c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b72c-157">Next steps</span></span>
* [<span data-ttu-id="6b72c-158">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="6b72c-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
