---
title: "Azure 資源提供者和資源類型 | Microsoft Docs"
description: "說明支援資源管理員、其結構描述及可用 API 版本的資源提供者，以及可裝載資源的區域。"
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="4c51a-103">資源提供者和類型</span><span class="sxs-lookup"><span data-stu-id="4c51a-103">Resource providers and types</span></span>

<span data-ttu-id="4c51a-104">部署資源時，您經常需要擷取有關資源提供者和類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="4c51a-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="4c51a-105">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="4c51a-105">In this article, you learn to:</span></span>

* <span data-ttu-id="4c51a-106">在 Azure 中檢視所有資源提供者</span><span class="sxs-lookup"><span data-stu-id="4c51a-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="4c51a-107">檢查資源提供者的註冊狀態</span><span class="sxs-lookup"><span data-stu-id="4c51a-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="4c51a-108">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="4c51a-108">Register a resource provider</span></span>
* <span data-ttu-id="4c51a-109">檢視資源提供者的資源類型</span><span class="sxs-lookup"><span data-stu-id="4c51a-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="4c51a-110">檢視資源類型的有效位置</span><span class="sxs-lookup"><span data-stu-id="4c51a-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="4c51a-111">檢視資源類型的有效 API 版本</span><span class="sxs-lookup"><span data-stu-id="4c51a-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="4c51a-112">您可以透過入口網站、PowerShell 或 Azure CLI 執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4c51a-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="4c51a-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c51a-113">PowerShell</span></span>

<span data-ttu-id="4c51a-114">若要查看 Azure 中的所有資源提供者，以及您訂用帳戶的登錄狀態，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="4c51a-115">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="4c51a-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="4c51a-116">註冊資源提供者可將您的訂用帳戶設定為可搭配資源提供者使用。</span><span class="sxs-lookup"><span data-stu-id="4c51a-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="4c51a-117">註冊範圍一律是訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c51a-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="4c51a-118">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="4c51a-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="4c51a-119">不過，您可能需要手動註冊某些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="4c51a-120">若要註冊資源提供者，您必須有權執行資源提供者的 `/register/action` 作業。</span><span class="sxs-lookup"><span data-stu-id="4c51a-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="4c51a-121">這項作業包含在「參與者」和「擁有者」角色中。</span><span class="sxs-lookup"><span data-stu-id="4c51a-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="4c51a-122">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="4c51a-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="4c51a-123">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="4c51a-124">若要查看特定資源提供者的資訊，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="4c51a-125">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="4c51a-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="4c51a-126">若要查看資源提供者的資源類型，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="4c51a-127">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="4c51a-128">API 版本會對應至資源提供者所發行的 REST API 作業版本。</span><span class="sxs-lookup"><span data-stu-id="4c51a-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="4c51a-129">當資源提供者啟用新功能時，它會發行新版本的 REST API。</span><span class="sxs-lookup"><span data-stu-id="4c51a-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="4c51a-130">若要取得資源類型的可用 API 版本，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="4c51a-131">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="4c51a-132">所有區域都支援資源管理員，但您部署的資源可能無法在所有區域中受到支援。</span><span class="sxs-lookup"><span data-stu-id="4c51a-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="4c51a-133">此外，您的訂用帳戶上可能會有一些限制，以防止您使用某些支援該資源的區域。</span><span class="sxs-lookup"><span data-stu-id="4c51a-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="4c51a-134">若要取得資源類型支援的位置，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="4c51a-135">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="4c51a-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c51a-136">Azure CLI</span></span>
<span data-ttu-id="4c51a-137">若要查看 Azure 中的所有資源提供者，以及您訂用帳戶的登錄狀態，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="4c51a-138">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="4c51a-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="4c51a-139">註冊資源提供者可將您的訂用帳戶設定為可搭配資源提供者使用。</span><span class="sxs-lookup"><span data-stu-id="4c51a-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="4c51a-140">註冊範圍一律是訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c51a-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="4c51a-141">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="4c51a-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="4c51a-142">不過，您可能需要手動註冊某些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="4c51a-143">若要註冊資源提供者，您必須有權執行資源提供者的 `/register/action` 作業。</span><span class="sxs-lookup"><span data-stu-id="4c51a-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="4c51a-144">這項作業包含在「參與者」和「擁有者」角色中。</span><span class="sxs-lookup"><span data-stu-id="4c51a-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="4c51a-145">它會傳回一則訊息說明註冊持續進行中。</span><span class="sxs-lookup"><span data-stu-id="4c51a-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="4c51a-146">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="4c51a-147">若要查看特定資源提供者的資訊，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="4c51a-148">傳回的結果類似於：</span><span class="sxs-lookup"><span data-stu-id="4c51a-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="4c51a-149">若要查看資源提供者的資源類型，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="4c51a-150">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="4c51a-151">API 版本會對應至資源提供者所發行的 REST API 作業版本。</span><span class="sxs-lookup"><span data-stu-id="4c51a-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="4c51a-152">當資源提供者啟用新功能時，它會發行新版本的 REST API。</span><span class="sxs-lookup"><span data-stu-id="4c51a-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="4c51a-153">若要取得資源類型的可用 API 版本，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="4c51a-154">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="4c51a-155">所有區域都支援資源管理員，但您部署的資源可能無法在所有區域中受到支援。</span><span class="sxs-lookup"><span data-stu-id="4c51a-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="4c51a-156">此外，您的訂用帳戶上可能會有一些限制，以防止您使用某些支援該資源的區域。</span><span class="sxs-lookup"><span data-stu-id="4c51a-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="4c51a-157">若要取得資源類型支援的位置，請使用：</span><span class="sxs-lookup"><span data-stu-id="4c51a-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="4c51a-158">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="4c51a-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="4c51a-159">入口網站</span><span class="sxs-lookup"><span data-stu-id="4c51a-159">Portal</span></span>

<span data-ttu-id="4c51a-160">訂用帳戶若要查看 Azure 中的所有資源提供者，以及您訂用帳戶的登錄狀態，請選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="4c51a-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![選取 [訂用帳戶]](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="4c51a-162">選擇要檢視的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c51a-162">Choose the subscription to view.</span></span>

![指定訂用帳戶](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="4c51a-164">選取**資源提供者**並檢視可用資源提供者的清單。</span><span class="sxs-lookup"><span data-stu-id="4c51a-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![顯示資源提供者](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="4c51a-166">註冊資源提供者可將您的訂用帳戶設定為可搭配資源提供者使用。</span><span class="sxs-lookup"><span data-stu-id="4c51a-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="4c51a-167">註冊範圍一律是訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c51a-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="4c51a-168">許多資源提供者都會預設為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="4c51a-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="4c51a-169">不過，您可能需要手動註冊某些資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="4c51a-170">若要註冊資源提供者，您必須有權執行資源提供者的 `/register/action` 作業。</span><span class="sxs-lookup"><span data-stu-id="4c51a-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="4c51a-171">這項作業包含在「參與者」和「擁有者」角色中。</span><span class="sxs-lookup"><span data-stu-id="4c51a-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="4c51a-172">若要註冊資源提供者，請選取 [註冊]。</span><span class="sxs-lookup"><span data-stu-id="4c51a-172">To register a resource provider, select **Register**.</span></span>

![註冊資源提供者](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="4c51a-174">當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。</span><span class="sxs-lookup"><span data-stu-id="4c51a-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="4c51a-175">若要查看特定資源提供者的資訊，請選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="4c51a-175">To see information for a particular resource provider, select **More services**.</span></span>

![選取 [更多服務]](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="4c51a-177">搜尋**資源總管**並從可用的選項加以選取。</span><span class="sxs-lookup"><span data-stu-id="4c51a-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![選取 [資源總管]](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="4c51a-179">選取 [提供者]。</span><span class="sxs-lookup"><span data-stu-id="4c51a-179">Select **Providers**.</span></span>

![選取 [提供者]](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="4c51a-181">選取資源提供者和您想要檢視的資源類型。</span><span class="sxs-lookup"><span data-stu-id="4c51a-181">Select the resource provider and resource type that you want to view.</span></span>

![選取 [資源類型]](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="4c51a-183">所有區域都支援資源管理員，但您部署的資源可能無法在所有區域中受到支援。</span><span class="sxs-lookup"><span data-stu-id="4c51a-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="4c51a-184">此外，您的訂用帳戶上可能會有一些限制，以防止您使用某些支援該資源的區域。</span><span class="sxs-lookup"><span data-stu-id="4c51a-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="4c51a-185">資源總管會顯示資源類型的有效位置。</span><span class="sxs-lookup"><span data-stu-id="4c51a-185">The resource explorer displays valid locations for the resource type.</span></span>

![顯示位置](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="4c51a-187">API 版本會對應至資源提供者所發行的 REST API 作業版本。</span><span class="sxs-lookup"><span data-stu-id="4c51a-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="4c51a-188">當資源提供者啟用新功能時，它會發行新版本的 REST API。</span><span class="sxs-lookup"><span data-stu-id="4c51a-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="4c51a-189">資源總管會顯示資源類型的有效 API 版本。</span><span class="sxs-lookup"><span data-stu-id="4c51a-189">The resource explorer displays valid API versions for the resource type.</span></span>

![顯示 API 版本](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="4c51a-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c51a-191">Next steps</span></span>
* <span data-ttu-id="4c51a-192">若要了解如何建立資源管理員範本，請參閱 [編寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="4c51a-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4c51a-193">若要了解如何部署資源，請參閱 [使用 Azure 資源管理員範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="4c51a-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="4c51a-194">若要檢視資源提供者的作業，請參閱 [Azure REST API](/rest/api/)。</span><span class="sxs-lookup"><span data-stu-id="4c51a-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

