---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="4ad9d-103">建立私用 Docker 容器登錄中使用 hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ad9d-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="4ad9d-104">使用中的命令[Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate 容器登錄中，從您的 Windows 電腦管理其設定。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="4ad9d-105">您也可以建立及管理使用 hello 容器登錄[Azure 入口網站](container-registry-get-started-portal.md)，hello [Azure CLI](container-registry-get-started-azure-cli.md)，或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="4ad9d-106">背景和概念，請參閱[hello 概觀](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4ad9d-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="4ad9d-107">如需支援的 Cmdlet 完整清單，請參閱 [Azure 容器登錄管理 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4ad9d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="4ad9d-108">Prerequisites</span></span>
* <span data-ttu-id="4ad9d-109">**Azure PowerShell**: tooinstall 和開始使用 Azure PowerShell，請參閱 hello[安裝指示](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="4ad9d-110">執行登入 Azure 訂用帳戶 tooyour `Login-AzureRMAccount`。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="4ad9d-111">如需詳細資訊，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="4ad9d-112">**資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="4ad9d-113">請確定 hello 資源群組是在 hello 容器登錄服務所在的位置[可用](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="4ad9d-114">toocreate 資源群組，使用 Azure PowerShell，請參閱[hello PowerShell 參考](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="4ad9d-115">**儲存體帳戶**（選擇性）： 建立標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)tooback hello 容器登錄中 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="4ad9d-116">如果您未指定儲存體帳戶時建立登錄中的以`New-AzureRMContainerRegistry`，hello 命令為您建立一個。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="4ad9d-117">toocreate 儲存體帳戶使用 PowerShell，請參閱[hello PowerShell 參考](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="4ad9d-118">目前不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="4ad9d-119">**服務主體** (選用)：當您使用 PowerShell 建立登錄時，依預設不會針對存取進行設定。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="4ad9d-120">根據您的需求，您可以指派現有的 Azure Active Directory 服務主體 tooa 登錄或建立並指派新的。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="4ad9d-121">或者，您可以啟用 hello 登錄系統管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="4ad9d-122">請參閱本文稍後的 hello 章節。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-122">See hello sections later in this article.</span></span> <span data-ttu-id="4ad9d-123">如需登錄存取權的詳細資訊，請參閱[與 hello 容器登錄中的 Authenticate](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="4ad9d-124">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="4ad9d-124">Create a container registry</span></span>
<span data-ttu-id="4ad9d-125">執行 hello`New-AzureRMContainerRegistry`命令 toocreate 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="4ad9d-126">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="4ad9d-127">hello 範例中的 hello 登錄名稱`MyRegistry`，但以取代您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="4ad9d-128">下列命令會使用 hello 最少參數 toocreate 容器登錄中的 hello `MyRegistry` hello 資源群組中`MyResourceGroup`hello 美國中南部位置中：</span><span class="sxs-lookup"><span data-stu-id="4ad9d-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="4ad9d-129">`-StorageAccountName` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="4ad9d-130">如果未指定，儲存體帳戶建立 hello 登錄名稱所組成的名稱，並 hello 的時間戳記指定資源群組。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="4ad9d-131">指派服務主體</span><span class="sxs-lookup"><span data-stu-id="4ad9d-131">Assign a service principal</span></span>
<span data-ttu-id="4ad9d-132">使用 Azure Active Directory 的 PowerShell 命令 tooassign[服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)tooa 登錄。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="4ad9d-133">hello 這些範例中的服務主體指派 hello 擁有者角色，但您可以指派[其他角色](../active-directory/role-based-access-control-configure.md)如果您想要。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="4ad9d-134">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="4ad9d-134">Create a service principal</span></span>
<span data-ttu-id="4ad9d-135">在 hello 下列命令，會建立新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="4ad9d-136">指定強式密碼以 hello`-Password`參數。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="4ad9d-137">指派新的或現有的服務主體</span><span class="sxs-lookup"><span data-stu-id="4ad9d-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="4ad9d-138">您可以指派新的或現有的服務主體 tooa 登錄。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="4ad9d-139">tooassign 它擁有者角色存取 toohello 登錄中，執行下列範例命令類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="4ad9d-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="4ad9d-140">登入 toohello 登錄中以 hello 服務主體</span><span class="sxs-lookup"><span data-stu-id="4ad9d-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="4ad9d-141">之後指派 hello 服務主體 toohello 登錄，您可以使用登入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4ad9d-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="4ad9d-142">管理管理員認證</span><span class="sxs-lookup"><span data-stu-id="4ad9d-142">Manage admin credentials</span></span>
<span data-ttu-id="4ad9d-143">系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="4ad9d-144">hello 下列範例顯示 PowerShell 命令的容器登錄 toomanage hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4ad9d-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="4ad9d-145">取得管理員使用者認證</span><span class="sxs-lookup"><span data-stu-id="4ad9d-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="4ad9d-146">啟用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="4ad9d-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="4ad9d-147">停用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="4ad9d-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="4ad9d-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ad9d-148">Next steps</span></span>
* [<span data-ttu-id="4ad9d-149">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="4ad9d-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
