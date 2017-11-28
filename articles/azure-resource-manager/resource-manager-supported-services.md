---
title: "aaaAzure 資源提供者和資源類型 |Microsoft 文件"
description: "描述 hello 資源提供者支援資源管理員、 結構描述和可用的 API 版本，以及可以裝載 hello 資源 hello 區域。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="d43cb-103">資源提供者和類型</span><span class="sxs-lookup"><span data-stu-id="d43cb-103">Resource providers and types</span></span>

<span data-ttu-id="d43cb-104">在部署資源時，您經常需要 tooretrieve hello 資源提供者和類型資訊。</span><span class="sxs-lookup"><span data-stu-id="d43cb-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="d43cb-105">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="d43cb-105">In this article, you learn to:</span></span>

* <span data-ttu-id="d43cb-106">在 Azure 中檢視所有資源提供者</span><span class="sxs-lookup"><span data-stu-id="d43cb-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="d43cb-107">檢查資源提供者的註冊狀態</span><span class="sxs-lookup"><span data-stu-id="d43cb-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="d43cb-108">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="d43cb-108">Register a resource provider</span></span>
* <span data-ttu-id="d43cb-109">檢視資源提供者的資源類型</span><span class="sxs-lookup"><span data-stu-id="d43cb-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="d43cb-110">檢視資源類型的有效位置</span><span class="sxs-lookup"><span data-stu-id="d43cb-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="d43cb-111">檢視資源類型的有效 API 版本</span><span class="sxs-lookup"><span data-stu-id="d43cb-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="d43cb-112">您可以執行下列步驟透過 hello 入口網站、 PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="d43cb-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="d43cb-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d43cb-113">PowerShell</span></span>

<span data-ttu-id="d43cb-114">toosee 所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶，都使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="d43cb-115">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="d43cb-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="d43cb-116">註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="d43cb-117">註冊的 hello 範圍一律是 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43cb-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="d43cb-118">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d43cb-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="d43cb-119">不過，您可能需要 toomanually 註冊一些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="d43cb-120">tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="d43cb-121">這項作業包含在 hello 參與者和擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d43cb-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="d43cb-122">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="d43cb-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="d43cb-123">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="d43cb-124">為特定資源提供者，使用 toosee 資訊：</span><span class="sxs-lookup"><span data-stu-id="d43cb-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="d43cb-125">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="d43cb-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="d43cb-126">toosee hello 資源類型為資源提供者，使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="d43cb-127">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="d43cb-128">hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="d43cb-129">資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。</span><span class="sxs-lookup"><span data-stu-id="d43cb-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="d43cb-130">tooget hello 可用的 API 版本的資源類型，使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="d43cb-131">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="d43cb-132">資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。</span><span class="sxs-lookup"><span data-stu-id="d43cb-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="d43cb-133">此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="d43cb-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="d43cb-134">資源類型的 tooget hello 支援位置使用。</span><span class="sxs-lookup"><span data-stu-id="d43cb-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="d43cb-135">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="d43cb-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d43cb-136">Azure CLI</span></span>
<span data-ttu-id="d43cb-137">toosee 所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶，都使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="d43cb-138">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="d43cb-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="d43cb-139">註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="d43cb-140">註冊的 hello 範圍一律是 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43cb-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="d43cb-141">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d43cb-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="d43cb-142">不過，您可能需要 toomanually 註冊一些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="d43cb-143">tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="d43cb-144">這項作業包含在 hello 參與者和擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d43cb-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="d43cb-145">它會傳回一則訊息說明註冊持續進行中。</span><span class="sxs-lookup"><span data-stu-id="d43cb-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="d43cb-146">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="d43cb-147">為特定資源提供者，使用 toosee 資訊：</span><span class="sxs-lookup"><span data-stu-id="d43cb-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="d43cb-148">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="d43cb-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="d43cb-149">toosee hello 資源類型為資源提供者，使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="d43cb-150">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="d43cb-151">hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="d43cb-152">資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。</span><span class="sxs-lookup"><span data-stu-id="d43cb-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="d43cb-153">tooget hello 可用的 API 版本的資源類型，使用：</span><span class="sxs-lookup"><span data-stu-id="d43cb-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="d43cb-154">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="d43cb-155">資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。</span><span class="sxs-lookup"><span data-stu-id="d43cb-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="d43cb-156">此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="d43cb-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="d43cb-157">資源類型的 tooget hello 支援位置使用。</span><span class="sxs-lookup"><span data-stu-id="d43cb-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="d43cb-158">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="d43cb-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="d43cb-159">入口網站</span><span class="sxs-lookup"><span data-stu-id="d43cb-159">Portal</span></span>

<span data-ttu-id="d43cb-160">所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶中，都選取 toosee**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="d43cb-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![選取 [訂用帳戶]](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="d43cb-162">選擇 hello 訂用帳戶 tooview。</span><span class="sxs-lookup"><span data-stu-id="d43cb-162">Choose hello subscription tooview.</span></span>

![指定訂用帳戶](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="d43cb-164">選取**資源提供者**和檢視 hello 可用的資源提供者清單。</span><span class="sxs-lookup"><span data-stu-id="d43cb-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![顯示資源提供者](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="d43cb-166">註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="d43cb-167">註冊的 hello 範圍一律是 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43cb-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="d43cb-168">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d43cb-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="d43cb-169">不過，您可能需要 toomanually 註冊一些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="d43cb-170">tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="d43cb-171">這項作業包含在 hello 參與者和擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d43cb-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="d43cb-172">tooregister 資源提供者中，選取**註冊**。</span><span class="sxs-lookup"><span data-stu-id="d43cb-172">tooregister a resource provider, select **Register**.</span></span>

![註冊資源提供者](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="d43cb-174">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d43cb-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="d43cb-175">選取 為特定資源提供者，toosee 資訊**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="d43cb-175">toosee information for a particular resource provider, select **More services**.</span></span>

![選取 [更多服務]](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="d43cb-177">搜尋**資源總管**和選取從 hello 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="d43cb-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![選取 [資源總管]](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="d43cb-179">選取 [提供者]。</span><span class="sxs-lookup"><span data-stu-id="d43cb-179">Select **Providers**.</span></span>

![選取 [提供者]](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="d43cb-181">選取 hello 資源提供者和資源類型的 tooview。</span><span class="sxs-lookup"><span data-stu-id="d43cb-181">Select hello resource provider and resource type that you want tooview.</span></span>

![選取 [資源類型]](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="d43cb-183">資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。</span><span class="sxs-lookup"><span data-stu-id="d43cb-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="d43cb-184">此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="d43cb-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="d43cb-185">hello 資源總管會顯示 hello 資源類型的有效位置。</span><span class="sxs-lookup"><span data-stu-id="d43cb-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![顯示位置](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="d43cb-187">hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。</span><span class="sxs-lookup"><span data-stu-id="d43cb-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="d43cb-188">資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。</span><span class="sxs-lookup"><span data-stu-id="d43cb-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="d43cb-189">hello 資源總管會顯示 hello 資源類型的有效應用程式開發介面版本。</span><span class="sxs-lookup"><span data-stu-id="d43cb-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![顯示 API 版本](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="d43cb-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d43cb-191">Next steps</span></span>
* <span data-ttu-id="d43cb-192">toolearn 有關建立資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d43cb-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d43cb-193">toolearn 有關部署資源，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="d43cb-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="d43cb-194">tooview hello 作業為資源提供者，請參閱[Azure REST API](/rest/api/)。</span><span class="sxs-lookup"><span data-stu-id="d43cb-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

