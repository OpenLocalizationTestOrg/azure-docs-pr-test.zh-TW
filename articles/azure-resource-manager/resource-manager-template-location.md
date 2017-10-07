---
title: "在範本中的 aaaAzure 資源位置 |Microsoft 文件"
description: "示範如何 tooset Azure Resource Manager 範本中的資源的位置"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="1b476-103">設定 Azure Resource Manager 範本中的資源位置</span><span class="sxs-lookup"><span data-stu-id="1b476-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="1b476-104">在部署範本時，您必須為每個資源提供一個位置。</span><span class="sxs-lookup"><span data-stu-id="1b476-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="1b476-105">本主題會顯示的每個資源的訂用帳戶可用 tooyour toodetermine hello 位置的型別。</span><span class="sxs-lookup"><span data-stu-id="1b476-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="1b476-106">決定支援的位置</span><span class="sxs-lookup"><span data-stu-id="1b476-106">Determine supported locations</span></span>

<span data-ttu-id="1b476-107">如需支援每個資源類型位置的完整清單，請參閱[依區域提供的產品](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="1b476-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="1b476-108">不過，您的訂用帳戶可能沒有存取 tooall hello 位置，該清單中。</span><span class="sxs-lookup"><span data-stu-id="1b476-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="1b476-109">toosee 自訂清單的位置是使用 tooyour 訂用帳戶，使用 Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="1b476-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="1b476-110">hello 下列範例會使用 PowerShell tooget hello 位置 hello`Microsoft.Web\sites`資源類型：</span><span class="sxs-lookup"><span data-stu-id="1b476-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="1b476-111">hello 下列範例會使用 Azure CLI 2.0 tooget hello 位置 hello`Microsoft.Web\sites`資源類型：</span><span class="sxs-lookup"><span data-stu-id="1b476-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="1b476-112">在範本中設定位置</span><span class="sxs-lookup"><span data-stu-id="1b476-112">Set location in template</span></span>

<span data-ttu-id="1b476-113">決定之後 hello 支援資源的位置，您需要 tooset 該位置在範本中。</span><span class="sxs-lookup"><span data-stu-id="1b476-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="1b476-114">hello 的 toocreate 資源群組中的位置，以支援 hello 資源類型，則這個值是最簡單的方式 tooset 和設定每個位置太`[resourceGroup().location]`。</span><span class="sxs-lookup"><span data-stu-id="1b476-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="1b476-115">您可以重新部署 hello 範本 tooresource 群組在不同的位置，並不會變更 hello 範本或參數中的任何值。</span><span class="sxs-lookup"><span data-stu-id="1b476-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="1b476-116">hello 下列範例顯示已部署的 toohello 儲存體帳戶與 hello 資源群組相同的位置：</span><span class="sxs-lookup"><span data-stu-id="1b476-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="1b476-117">如果您需要 toohardcode hello 位置在範本中，提供的其中一個支援的 hello 區域 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1b476-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="1b476-118">hello 下列範例會顯示儲存體帳戶永遠部署 tooNorth 美國中部：</span><span class="sxs-lookup"><span data-stu-id="1b476-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="1b476-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b476-119">Next steps</span></span>
* <span data-ttu-id="1b476-120">如需有關如何建議 toocreate 範本，請參閱[最佳作法來建立 Azure 資源管理員範本](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="1b476-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

