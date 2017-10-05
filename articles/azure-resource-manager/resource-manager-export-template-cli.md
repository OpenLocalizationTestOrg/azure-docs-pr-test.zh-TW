---
title: "使用 Azure CLI 來匯出 Resource Manager 範本 | Microsoft Docs"
description: "使用 Azure Resource Manager 和 Azure CLI 從資源群組匯出範本。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="11bb1-103">使用 Azure CLI 來匯出 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="11bb1-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="11bb1-104">Resource Manager 可讓您從您的訂用帳戶中現有的資源匯出 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="11bb1-105">您可以使用產生的範本了解範本語法，或視需要自動重新部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="11bb1-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="11bb1-106">請務必注意，有兩種不同的方式可匯出範本︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="11bb1-107">您可以匯出用於部署的實際範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="11bb1-108">匯出的範本包含與原始範本完全相同的所有參數和變數。</span><span class="sxs-lookup"><span data-stu-id="11bb1-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="11bb1-109">當您需要擷取範本時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="11bb1-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="11bb1-110">您可以匯出代表資源群組目前狀態的範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="11bb1-111">匯出的範本不是以任何用於部署的範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="11bb1-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="11bb1-112">反而，它所建立的範本是資源群組的快照。</span><span class="sxs-lookup"><span data-stu-id="11bb1-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="11bb1-113">匯出的範本會有許多硬式編碼值，但數量可能不如您通常會定義的參數數量。</span><span class="sxs-lookup"><span data-stu-id="11bb1-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="11bb1-114">當您已修改資源群組時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="11bb1-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="11bb1-115">現在，您需要擷取做為範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="11bb1-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="11bb1-116">本主題說明這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="11bb1-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="11bb1-117">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="11bb1-117">Deploy a solution</span></span>

<span data-ttu-id="11bb1-118">為了說明這兩種用來匯出範本的方法，一開始先讓我們將解決方案部署到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="11bb1-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="11bb1-119">如果您的訂用帳戶中已有想要匯出的資源群組，就不需要部署此解決方案。</span><span class="sxs-lookup"><span data-stu-id="11bb1-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="11bb1-120">不過，本文其餘部分會參考此解決方案的範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="11bb1-121">指令碼範例會部署儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="11bb1-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="11bb1-122">從部署歷程記錄儲存範本</span><span class="sxs-lookup"><span data-stu-id="11bb1-122">Save template from deployment history</span></span>

<span data-ttu-id="11bb1-123">您可以使用 [az group deployment export](/cli/azure/group/deployment#export) 命令，從部署歷程記錄中擷取範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="11bb1-124">下列範例會儲存您先前部署的範本︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="11bb1-125">它會傳回範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-125">It returns the template.</span></span> <span data-ttu-id="11bb1-126">複製 JSON，並儲存為檔案。</span><span class="sxs-lookup"><span data-stu-id="11bb1-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="11bb1-127">請注意，它正是您用於部署的範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="11bb1-128">其參數和變數會與 GitHub 中的範本相符。</span><span class="sxs-lookup"><span data-stu-id="11bb1-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="11bb1-129">您可以重新部署此範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="11bb1-130">匯出資源群組以作為範本</span><span class="sxs-lookup"><span data-stu-id="11bb1-130">Export resource group as template</span></span>

<span data-ttu-id="11bb1-131">您不必從部署歷程記錄擷取範本，而可以使用 [az group export](/cli/azure/group#export) 命令來擷取範本，以代表資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="11bb1-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="11bb1-132">當您對資源群組做了許多變更，且現有的範本均無法完全呈現這些變更時，就可以使用這個命令。</span><span class="sxs-lookup"><span data-stu-id="11bb1-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="11bb1-133">它會傳回範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-133">It returns the template.</span></span> <span data-ttu-id="11bb1-134">複製 JSON，並儲存為檔案。</span><span class="sxs-lookup"><span data-stu-id="11bb1-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="11bb1-135">請注意，它與 GitHub 中的範本不同。</span><span class="sxs-lookup"><span data-stu-id="11bb1-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="11bb1-136">它有不同的參數，而且沒有任何變數。</span><span class="sxs-lookup"><span data-stu-id="11bb1-136">It has different parameters and no variables.</span></span> <span data-ttu-id="11bb1-137">儲存體 SKU 和位置皆已硬式編碼為值。</span><span class="sxs-lookup"><span data-stu-id="11bb1-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="11bb1-138">下列範例會顯示所匯出的範本，但您的範本會有稍微不同的參數名稱︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="11bb1-139">您可以重新部署此範本，但必須猜測儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="11bb1-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="11bb1-140">您的參數名稱會稍微不同。</span><span class="sxs-lookup"><span data-stu-id="11bb1-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="11bb1-141">自訂匯出的範本</span><span class="sxs-lookup"><span data-stu-id="11bb1-141">Customize exported template</span></span>

<span data-ttu-id="11bb1-142">您可以修改此範本，讓它變得更方便使用且更有彈性。</span><span class="sxs-lookup"><span data-stu-id="11bb1-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="11bb1-143">若要允許更多位置，請將 location 屬性變更為使用與資源群組相同的位置︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="11bb1-144">為了避免必須猜測儲存體帳戶的唯一名稱，請移除儲存體帳戶名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="11bb1-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="11bb1-145">新增儲存體名稱尾碼的參數，以及儲存體 SKU︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="11bb1-146">新增變數，以便使用 uniqueString 函式來建構儲存體帳戶名稱︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="11bb1-147">將儲存體帳戶名稱設定為變數︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="11bb1-148">將 SKU 設定為參數︰</span><span class="sxs-lookup"><span data-stu-id="11bb1-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="11bb1-149">您的範本現在如下所示：</span><span class="sxs-lookup"><span data-stu-id="11bb1-149">Your template now looks like:</span></span>

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

<span data-ttu-id="11bb1-150">重新部署修改過的範本。</span><span class="sxs-lookup"><span data-stu-id="11bb1-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11bb1-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11bb1-151">Next steps</span></span>
* <span data-ttu-id="11bb1-152">如需使用入口網站來匯出範本的相關資訊，請參閱[從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="11bb1-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="11bb1-153">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="11bb1-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="11bb1-154">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="11bb1-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>