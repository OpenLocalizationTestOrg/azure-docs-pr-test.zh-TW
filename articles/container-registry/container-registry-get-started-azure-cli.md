---
title: "建立私人 Docker 容器登錄 - Azure CLI | Microsoft Docs"
description: "使用 Azure CLI 2.0 開始建立及管理私人 Docker 容器登錄"
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
ms.openlocfilehash: 2875f4089231ed12a0312b2c2e077938440365c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a><span data-ttu-id="7b94d-103">使用 Azure CLI 2.0 建立私人 Docker 容器登錄</span><span class="sxs-lookup"><span data-stu-id="7b94d-103">Create a private Docker container registry using the Azure CLI 2.0</span></span>
<span data-ttu-id="7b94d-104">在 Linux、Mac 或 Windows 電腦上，使用 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 中的命令建立容器登錄及管理其設定。</span><span class="sxs-lookup"><span data-stu-id="7b94d-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="7b94d-105">您也可以使用 [Azure 入口網站](container-registry-get-started-portal.md)或以程式設計方式用容器登錄 [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376) 來建立及管理容器登錄。</span><span class="sxs-lookup"><span data-stu-id="7b94d-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="7b94d-106">如需相關背景和概念，請參閱[概觀](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="7b94d-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="7b94d-107">如需容器登錄庫 CLI 命令 (`az acr` 命令) 的說明，請傳遞 `-h` 參數至任何命令。</span><span class="sxs-lookup"><span data-stu-id="7b94d-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7b94d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b94d-108">Prerequisites</span></span>
* <span data-ttu-id="7b94d-109">**Azure CLI 2.0**若要安裝並開始使用 CLI 2.0，請參閱[安裝指示](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="7b94d-110">執行 `az login`登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b94d-110">Log in to your Azure subscription by running `az login`.</span></span> <span data-ttu-id="7b94d-111">如需詳細資訊，請參閱[開始使用 CLI 2.0](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="7b94d-112">**資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b94d-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="7b94d-113">請確定資源群組是位於[可使用](https://azure.microsoft.com/regions/services/)容器登錄庫服務的位置。</span><span class="sxs-lookup"><span data-stu-id="7b94d-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="7b94d-114">若要使用 CLI 2.0 建立資源群組，請參閱 [CLI 2.0 參考](/cli/azure/group)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="7b94d-115">**儲存體帳戶** (選用)：建立標準 Azure [儲存體帳戶](../storage/common/storage-introduction.md)以支援相同位置中的容器登錄。</span><span class="sxs-lookup"><span data-stu-id="7b94d-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="7b94d-116">如果您以 `az acr create` 建立登錄庫時沒有指定儲存體帳戶，此命令會為您建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b94d-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span></span> <span data-ttu-id="7b94d-117">若要使用 CLI 2.0 建立儲存體帳戶，請參閱 [CLI 2.0 參考](/cli/azure/storage/account)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="7b94d-118">目前不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b94d-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="7b94d-119">**服務主體** (選用)：當您使用 CLI 建立登錄，依預設不會做存取設定。</span><span class="sxs-lookup"><span data-stu-id="7b94d-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span></span> <span data-ttu-id="7b94d-120">您可以將現有的 Azure Active Directory 服務主體指派至登錄庫 (或建立並指派新的)，或是啟用登錄庫的管理員使用者帳戶，根據您的需求而定。</span><span class="sxs-lookup"><span data-stu-id="7b94d-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span></span> <span data-ttu-id="7b94d-121">請參閱本文稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="7b94d-121">See the sections later in this article.</span></span> <span data-ttu-id="7b94d-122">如需登錄庫存取權的詳細資訊，請參閱[驗證容器登錄庫](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="7b94d-123">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="7b94d-123">Create a container registry</span></span>
<span data-ttu-id="7b94d-124">執行 `az acr create` 命令建立容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="7b94d-124">Run the `az acr create` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="7b94d-125">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7b94d-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="7b94d-126">範例中的登錄庫名稱是 `myRegistry1`，請換成您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="7b94d-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="7b94d-127">下列命令使用最少的參數的 `myResourceGroup` 資源群組中建立容器登錄 `myRegistry1`，並使用基本 sku：</span><span class="sxs-lookup"><span data-stu-id="7b94d-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup`, and using the *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="7b94d-128">`--storage-account-name` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="7b94d-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="7b94d-129">如果未指定，則會在指定的資源群組中使用由登錄名稱和時間戳記所組成的名稱建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b94d-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

<span data-ttu-id="7b94d-130">建立登錄時，輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="7b94d-130">When the registry is created, the output is similar to the following:</span></span>

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


<span data-ttu-id="7b94d-131">請特別注意︰</span><span class="sxs-lookup"><span data-stu-id="7b94d-131">Take special note:</span></span>

* <span data-ttu-id="7b94d-132">`id` - 登錄庫在訂用帳戶中的識別碼，如果您要指派服務主體，則需要此識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b94d-132">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span></span>
* <span data-ttu-id="7b94d-133">`loginServer` - 您指定用來[登入登錄庫](container-registry-authentication.md)的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="7b94d-133">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span></span> <span data-ttu-id="7b94d-134">在此範例中，此名稱為 `myregistry1.exp.azurecr.io` (全部小寫)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-134">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="7b94d-135">指派服務主體</span><span class="sxs-lookup"><span data-stu-id="7b94d-135">Assign a service principal</span></span>
<span data-ttu-id="7b94d-136">使用 CLI 2.0 的命令將 Azure Active Directory 服務主體指派到登錄。</span><span class="sxs-lookup"><span data-stu-id="7b94d-136">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span></span> <span data-ttu-id="7b94d-137">這些範例中的服務主體是指派至擁有者角色，但如果您想要，可以指派至[其他角色](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="7b94d-137">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a><span data-ttu-id="7b94d-138">建立服務主體並指派對登錄庫的存取權</span><span class="sxs-lookup"><span data-stu-id="7b94d-138">Create a service principal and assign access to the registry</span></span>
<span data-ttu-id="7b94d-139">在下列命令中，將「對登錄庫的擁有者角色存取權」指派給新服務主體；此處登錄庫的識別碼是以 `--scopes` 參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="7b94d-139">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span></span> <span data-ttu-id="7b94d-140">以 `--password` 參數指定強式密碼。</span><span class="sxs-lookup"><span data-stu-id="7b94d-140">Specify a strong password with the `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="7b94d-141">指派現有的服務主體</span><span class="sxs-lookup"><span data-stu-id="7b94d-141">Assign an existing service principal</span></span>
<span data-ttu-id="7b94d-142">如果您已經有服務主體，想將對登錄庫的擁有者角色存取權指派給它，請執行類似下列範例的命令。</span><span class="sxs-lookup"><span data-stu-id="7b94d-142">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span></span> <span data-ttu-id="7b94d-143">您使用 `--assignee` 參數傳遞服務主體應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="7b94d-143">You pass the service principal app ID using the `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="7b94d-144">管理管理員認證</span><span class="sxs-lookup"><span data-stu-id="7b94d-144">Manage admin credentials</span></span>
<span data-ttu-id="7b94d-145">系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b94d-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="7b94d-146">下列範例示範用 `az acr` CLI 命令來管理容器登錄庫的管理員認證。</span><span class="sxs-lookup"><span data-stu-id="7b94d-146">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="7b94d-147">取得管理員使用者認證</span><span class="sxs-lookup"><span data-stu-id="7b94d-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="7b94d-148">啟用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="7b94d-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="7b94d-149">停用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="7b94d-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="7b94d-150">列出映像和標籤</span><span class="sxs-lookup"><span data-stu-id="7b94d-150">List images and tags</span></span>
<span data-ttu-id="7b94d-151">使用 `az acr` CLI 命令來查詢儲存機制中的映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="7b94d-151">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7b94d-152">目前，容器登錄庫不支援用 `docker search` 命令查詢映像和標籤。</span><span class="sxs-lookup"><span data-stu-id="7b94d-152">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="7b94d-153">列出儲存機制</span><span class="sxs-lookup"><span data-stu-id="7b94d-153">List repositories</span></span>
<span data-ttu-id="7b94d-154">下列範例會以 JSON (JavaScript 物件標記法) 格式列出登錄庫中的儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="7b94d-154">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="7b94d-155">列出標籤</span><span class="sxs-lookup"><span data-stu-id="7b94d-155">List tags</span></span>
<span data-ttu-id="7b94d-156">下列範例會以 JSON 格式列出 **samples/nginx** 儲存機制上的標籤：</span><span class="sxs-lookup"><span data-stu-id="7b94d-156">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="7b94d-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b94d-157">Next steps</span></span>
* [<span data-ttu-id="7b94d-158">使用 Docker CLI 推送您的第一個映像</span><span class="sxs-lookup"><span data-stu-id="7b94d-158">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
