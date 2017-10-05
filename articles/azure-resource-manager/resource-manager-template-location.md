---
title: "Azure 範本中的資源位置 | Microsoft Docs"
description: "示範如何設定 Azure Resource Manager 範本中資源的位置"
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
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="e0b02-103">設定 Azure Resource Manager 範本中的資源位置</span><span class="sxs-lookup"><span data-stu-id="e0b02-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="e0b02-104">在部署範本時，您必須為每個資源提供一個位置。</span><span class="sxs-lookup"><span data-stu-id="e0b02-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="e0b02-105">本主題示範如何決定可供訂用帳戶使用的每個資源類型位置。</span><span class="sxs-lookup"><span data-stu-id="e0b02-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="e0b02-106">決定支援的位置</span><span class="sxs-lookup"><span data-stu-id="e0b02-106">Determine supported locations</span></span>

<span data-ttu-id="e0b02-107">如需支援每個資源類型位置的完整清單，請參閱[依區域提供的產品](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="e0b02-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="e0b02-108">不過，您的訂用帳戶可能無法存取該清單中所有位置。</span><span class="sxs-lookup"><span data-stu-id="e0b02-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="e0b02-109">若要檢視供您的訂用帳戶使用的自訂位置清單，請使用 Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="e0b02-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="e0b02-110">下列範例使用 PowerShell 來取得 `Microsoft.Web\sites` 資源類型的位置︰</span><span class="sxs-lookup"><span data-stu-id="e0b02-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="e0b02-111">下列範例使用 Azure CLI 2.0 來取得 `Microsoft.Web\sites` 資源類型的位置：</span><span class="sxs-lookup"><span data-stu-id="e0b02-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="e0b02-112">在範本中設定位置</span><span class="sxs-lookup"><span data-stu-id="e0b02-112">Set location in template</span></span>

<span data-ttu-id="e0b02-113">決定支援資源的位置之後，您需要在範本中設定該位置。</span><span class="sxs-lookup"><span data-stu-id="e0b02-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="e0b02-114">設定此值最簡單的方式是在支援資源類型的位置建立一個資源群組，而且將每個位置設定為 `[resourceGroup().location]`。</span><span class="sxs-lookup"><span data-stu-id="e0b02-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="e0b02-115">您可以將範本重新部署到不同位置的資源群組，而且無需變更範本中的任何值或參數。</span><span class="sxs-lookup"><span data-stu-id="e0b02-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="e0b02-116">下列範例顯示部署到與資源群組相同位置的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e0b02-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

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

<span data-ttu-id="e0b02-117">如果您需要在範本中採硬式編碼來指定位置，請提供其中一個支援區域的名稱。</span><span class="sxs-lookup"><span data-stu-id="e0b02-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="e0b02-118">下列範例顯示一律會部署到美國中北部的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e0b02-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e0b02-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0b02-119">Next steps</span></span>
* <span data-ttu-id="e0b02-120">如需如何建立範本的建議，請參閱 [建立 Azure Resource Manager 範本的最佳做法](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="e0b02-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

