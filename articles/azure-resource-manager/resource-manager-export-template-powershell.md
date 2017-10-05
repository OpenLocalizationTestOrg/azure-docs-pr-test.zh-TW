---
title: "使用 Azure PowerShell 來匯出 Resource Manager 範本 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Azure PowerShell 從資源群組匯出範本。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="1d05e-103">使用 PowerShell 來匯出 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1d05e-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="1d05e-104">Resource Manager 可讓您從您的訂用帳戶中現有的資源匯出 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="1d05e-105">您可以使用產生的範本了解範本語法，或視需要自動重新部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d05e-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="1d05e-106">請務必注意，有兩種不同的方式可匯出範本︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="1d05e-107">您可以匯出用於部署的實際範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="1d05e-108">匯出的範本包含與原始範本完全相同的所有參數和變數。</span><span class="sxs-lookup"><span data-stu-id="1d05e-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="1d05e-109">當您需要擷取範本時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="1d05e-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="1d05e-110">您可以匯出代表資源群組目前狀態的範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="1d05e-111">匯出的範本不是以任何用於部署的範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="1d05e-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="1d05e-112">反而，它所建立的範本是資源群組的快照。</span><span class="sxs-lookup"><span data-stu-id="1d05e-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="1d05e-113">匯出的範本會有許多硬式編碼值，但數量可能不如您通常會定義的參數數量。</span><span class="sxs-lookup"><span data-stu-id="1d05e-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="1d05e-114">當您已修改資源群組時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="1d05e-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="1d05e-115">現在，您需要擷取做為範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1d05e-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="1d05e-116">本主題說明這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="1d05e-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="1d05e-117">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="1d05e-117">Deploy a solution</span></span>

<span data-ttu-id="1d05e-118">為了說明這兩種用來匯出範本的方法，一開始先讓我們將解決方案部署到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d05e-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="1d05e-119">如果您的訂用帳戶中已有想要匯出的資源群組，就不需要部署此解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d05e-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="1d05e-120">不過，本文其餘部分會參考此解決方案的範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="1d05e-121">指令碼範例會部署儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d05e-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="1d05e-122">從部署歷程記錄儲存範本</span><span class="sxs-lookup"><span data-stu-id="1d05e-122">Save template from deployment history</span></span>

<span data-ttu-id="1d05e-123">您可以使用 [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) 命令來從部署歷程記錄中擷取範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="1d05e-124">下列範例會儲存您先前部署的範本︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="1d05e-125">它會傳回範本的位置。</span><span class="sxs-lookup"><span data-stu-id="1d05e-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="1d05e-126">開啟檔案，並請注意它正是您用於部署的範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="1d05e-127">其參數和變數會與 GitHub 中的範本相符。</span><span class="sxs-lookup"><span data-stu-id="1d05e-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="1d05e-128">您可以重新部署此範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="1d05e-129">匯出資源群組以作為範本</span><span class="sxs-lookup"><span data-stu-id="1d05e-129">Export resource group as template</span></span>

<span data-ttu-id="1d05e-130">您不必從部署歷程記錄擷取範本，而是可以使用 [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) 命令來擷取範本，以代表資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="1d05e-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="1d05e-131">當您對資源群組做了許多變更，且現有的範本均無法完全呈現這些變更時，就可以使用這個命令。</span><span class="sxs-lookup"><span data-stu-id="1d05e-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="1d05e-132">它會傳回範本的位置。</span><span class="sxs-lookup"><span data-stu-id="1d05e-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="1d05e-133">開啟檔案，並請注意它與 GitHub 中的範本不同。</span><span class="sxs-lookup"><span data-stu-id="1d05e-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="1d05e-134">它有不同的參數，而且沒有任何變數。</span><span class="sxs-lookup"><span data-stu-id="1d05e-134">It has different parameters and no variables.</span></span> <span data-ttu-id="1d05e-135">儲存體 SKU 和位置皆已硬式編碼為值。</span><span class="sxs-lookup"><span data-stu-id="1d05e-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="1d05e-136">下列範例會顯示所匯出的範本，但您的範本會有稍微不同的參數名稱︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="1d05e-137">您可以重新部署此範本，但必須猜測儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="1d05e-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="1d05e-138">您的參數名稱會稍微不同。</span><span class="sxs-lookup"><span data-stu-id="1d05e-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="1d05e-139">自訂匯出的範本</span><span class="sxs-lookup"><span data-stu-id="1d05e-139">Customize exported template</span></span>

<span data-ttu-id="1d05e-140">您可以修改此範本，讓它變得更方便使用且更有彈性。</span><span class="sxs-lookup"><span data-stu-id="1d05e-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="1d05e-141">若要允許更多位置，請將 location 屬性變更為使用與資源群組相同的位置︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="1d05e-142">為了避免必須猜測儲存體帳戶的唯一名稱，請移除儲存體帳戶名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="1d05e-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="1d05e-143">新增儲存體名稱尾碼的參數，以及儲存體 SKU︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="1d05e-144">新增變數，以便使用 uniqueString 函式來建構儲存體帳戶名稱︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="1d05e-145">將儲存體帳戶名稱設定為變數︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="1d05e-146">將 SKU 設定為參數︰</span><span class="sxs-lookup"><span data-stu-id="1d05e-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="1d05e-147">您的範本現在如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d05e-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="1d05e-148">重新部署修改過的範本。</span><span class="sxs-lookup"><span data-stu-id="1d05e-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d05e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d05e-149">Next steps</span></span>
* <span data-ttu-id="1d05e-150">如需使用入口網站來匯出範本的相關資訊，請參閱[從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="1d05e-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="1d05e-151">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="1d05e-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="1d05e-152">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="1d05e-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
