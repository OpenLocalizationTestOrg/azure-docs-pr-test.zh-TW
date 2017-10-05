---
title: "Azure 容器登錄存放庫 | Microsoft Docs"
description: "如何使用 Docker 映像的 Azure 容器登錄存放庫"
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
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="f201f-103">使用 Azure PowerShell 建立私人 Docker 容器登錄</span><span class="sxs-lookup"><span data-stu-id="f201f-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="f201f-104">在 Windows 電腦上，使用 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) 中的命令建立容器登錄並管理其設定。</span><span class="sxs-lookup"><span data-stu-id="f201f-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="f201f-105">您也可以使用 [Azure 入口網站](container-registry-get-started-portal.md)、[Azure CLI](container-registry-get-started-azure-cli.md)，或以程式設計方式用容器登錄 [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376) 來建立並管理容器登錄。</span><span class="sxs-lookup"><span data-stu-id="f201f-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="f201f-106">如需相關背景和概念，請參閱[概觀](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="f201f-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="f201f-107">如需支援的 Cmdlet 完整清單，請參閱 [Azure 容器登錄管理 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)。</span><span class="sxs-lookup"><span data-stu-id="f201f-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f201f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f201f-108">Prerequisites</span></span>
* <span data-ttu-id="f201f-109">**Azure PowerShell**：若要安裝並開始使用 Azure PowerShell，請參閱[安裝指示](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="f201f-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="f201f-110">執行 `Login-AzureRMAccount`登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f201f-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="f201f-111">如需詳細資訊，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)。</span><span class="sxs-lookup"><span data-stu-id="f201f-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="f201f-112">**資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f201f-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="f201f-113">請確定資源群組是位於[可使用](https://azure.microsoft.com/regions/services/)容器登錄庫服務的位置。</span><span class="sxs-lookup"><span data-stu-id="f201f-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="f201f-114">如需使用 Azure PowerShell 來建立資源群組，請參閱 [PowerShell 參考](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)。</span><span class="sxs-lookup"><span data-stu-id="f201f-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="f201f-115">**儲存體帳戶** (選用)：建立標準 Azure [儲存體帳戶](../storage/common/storage-introduction.md)以支援相同位置中的容器登錄。</span><span class="sxs-lookup"><span data-stu-id="f201f-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="f201f-116">如果您以 `New-AzureRMContainerRegistry` 建立登錄庫時沒有指定儲存體帳戶，此命令會為您建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f201f-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="f201f-117">如需使用 PowerShell 來建立儲存體帳戶，請參閱 [PowerShell 參考](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)。</span><span class="sxs-lookup"><span data-stu-id="f201f-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="f201f-118">目前不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="f201f-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="f201f-119">**服務主體** (選用)：當您使用 PowerShell 建立登錄時，依預設不會針對存取進行設定。</span><span class="sxs-lookup"><span data-stu-id="f201f-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="f201f-120">您可以將現有的 Azure Active Directory 服務主體指派至登錄庫，或建立並指派一個新的，視您的需求而定。</span><span class="sxs-lookup"><span data-stu-id="f201f-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="f201f-121">或者，您也可以啟用登錄的管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f201f-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="f201f-122">請參閱本文稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="f201f-122">See the sections later in this article.</span></span> <span data-ttu-id="f201f-123">如需登錄庫存取權的詳細資訊，請參閱[驗證容器登錄庫](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="f201f-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="f201f-124">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="f201f-124">Create a container registry</span></span>
<span data-ttu-id="f201f-125">執行 `New-AzureRMContainerRegistry` 命令建立容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="f201f-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="f201f-126">當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="f201f-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="f201f-127">範例中的登錄庫名稱是 `MyRegistry`，請換成您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="f201f-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="f201f-128">下列命令使用最少的參數在「美國中南部」位置的 `MyResourceGroup` 資源群組中建立容器登錄庫 `MyRegistry`︰</span><span class="sxs-lookup"><span data-stu-id="f201f-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="f201f-129">`-StorageAccountName` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="f201f-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="f201f-130">如果未指定，則會在指定的資源群組中使用由登錄名稱和時間戳記所組成的名稱建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f201f-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="f201f-131">指派服務主體</span><span class="sxs-lookup"><span data-stu-id="f201f-131">Assign a service principal</span></span>
<span data-ttu-id="f201f-132">使用 PowerShell 的命令，將 Azure Active Directory [服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)指派到登錄庫。</span><span class="sxs-lookup"><span data-stu-id="f201f-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="f201f-133">這些範例中的服務主體是指派至擁有者角色，但如果您想要，可以指派至[其他角色](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f201f-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="f201f-134">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="f201f-134">Create a service principal</span></span>
<span data-ttu-id="f201f-135">在下列命令中，會建立新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="f201f-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="f201f-136">以 `-Password` 參數指定強式密碼。</span><span class="sxs-lookup"><span data-stu-id="f201f-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="f201f-137">指派新的或現有的服務主體</span><span class="sxs-lookup"><span data-stu-id="f201f-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="f201f-138">您可以將新的或現有的服務主體指派到登錄庫。</span><span class="sxs-lookup"><span data-stu-id="f201f-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="f201f-139">若要將擁有者角色存取權指派到登錄庫，請執行類似下列範例的命令：</span><span class="sxs-lookup"><span data-stu-id="f201f-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="f201f-140">使用服務主體登入登錄庫</span><span class="sxs-lookup"><span data-stu-id="f201f-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="f201f-141">將服務主體指派到登錄庫之後，您就可以使用下列命令來登入：</span><span class="sxs-lookup"><span data-stu-id="f201f-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="f201f-142">管理管理員認證</span><span class="sxs-lookup"><span data-stu-id="f201f-142">Manage admin credentials</span></span>
<span data-ttu-id="f201f-143">系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="f201f-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="f201f-144">下列範例示範用 PowerShell 命令來管理容器登錄庫的管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f201f-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="f201f-145">取得管理員使用者認證</span><span class="sxs-lookup"><span data-stu-id="f201f-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="f201f-146">啟用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="f201f-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="f201f-147">停用現有登錄庫的管理員使用者</span><span class="sxs-lookup"><span data-stu-id="f201f-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="f201f-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f201f-148">Next steps</span></span>
* [<span data-ttu-id="f201f-149">使用 Docker CLI 推送您的第一個映像</span><span class="sxs-lookup"><span data-stu-id="f201f-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
