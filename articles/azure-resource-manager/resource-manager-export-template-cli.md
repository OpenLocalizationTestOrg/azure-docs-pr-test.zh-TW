---
title: "使用 Azure CLI aaaExport Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure 資源管理員和 Azure CLI tooexport 資源群組中的範本。"
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
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="3af81-103">使用 Azure CLI 來匯出 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3af81-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="3af81-104">資源管理員可讓您 tooexport Resource Manager 範本使用從您的訂用帳戶中現有的資源。</span><span class="sxs-lookup"><span data-stu-id="3af81-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="3af81-105">您可以使用該產生的範本 toolearn，有關 hello 範本語法或 tooautomate hello 重新部署方案視需要。</span><span class="sxs-lookup"><span data-stu-id="3af81-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="3af81-106">它是重要 toonote 有兩個不同的方式 tooexport 範本：</span><span class="sxs-lookup"><span data-stu-id="3af81-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="3af81-107">您可以匯出您用於部署的 hello 實際範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="3af81-108">hello 匯出的範本包含所有 hello 參數和變數，如同它們是出現在 hello 原始範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="3af81-109">當您需要 tooretrieve 範本時，這個方法就很有幫助。</span><span class="sxs-lookup"><span data-stu-id="3af81-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="3af81-110">您可以匯出代表 hello hello 資源群組的目前狀態的範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="3af81-111">hello 匯出的範本不根據您用於部署的任何範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="3af81-112">相反地，它會建立 hello 資源群組的快照集的範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="3af81-113">hello 匯出的範本有許多的硬式編碼值，可能不一樣多的參數，因為您通常會定義。</span><span class="sxs-lookup"><span data-stu-id="3af81-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="3af81-114">當您修改了 hello 資源群組，則這個方法會很有用。</span><span class="sxs-lookup"><span data-stu-id="3af81-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="3af81-115">現在，您需要 toocapture hello 資源群組，做為範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="3af81-116">本主題說明這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="3af81-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="3af81-117">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="3af81-117">Deploy a solution</span></span>

<span data-ttu-id="3af81-118">這兩個 tooillustrate 方法匯出範本，讓我們開始部署方案 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3af81-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="3af81-119">如果您想 tooexport 您訂用帳戶中已經有資源群組，您沒有 toodeploy 此解決方案。</span><span class="sxs-lookup"><span data-stu-id="3af81-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="3af81-120">不過，hello 本文其餘部分是指 toohello 範本，針對此解決方案。</span><span class="sxs-lookup"><span data-stu-id="3af81-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="3af81-121">hello 範例指令碼會將部署的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3af81-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="3af81-122">從部署歷程記錄儲存範本</span><span class="sxs-lookup"><span data-stu-id="3af81-122">Save template from deployment history</span></span>

<span data-ttu-id="3af81-123">您也可以使用 hello 部署歷程記錄中擷取範本[az 群組部署匯出](/cli/azure/group/deployment#export)命令。</span><span class="sxs-lookup"><span data-stu-id="3af81-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="3af81-124">下列範例會將儲存 hello 範本您先前部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="3af81-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="3af81-125">它會傳回 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-125">It returns hello template.</span></span> <span data-ttu-id="3af81-126">複製 hello JSON，並儲存成檔案。</span><span class="sxs-lookup"><span data-stu-id="3af81-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="3af81-127">請注意，它會是您用於部署的 hello 確切範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="3af81-128">hello 參數和變數符合從 GitHub hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="3af81-129">您可以重新部署此範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="3af81-130">匯出資源群組以作為範本</span><span class="sxs-lookup"><span data-stu-id="3af81-130">Export resource group as template</span></span>

<span data-ttu-id="3af81-131">而不是從 hello 部署歷程記錄中擷取範本，您可以擷取使用 hello 代表 hello 的資源群組的目前狀態的範本[az 群組匯出](/cli/azure/group#export)命令。</span><span class="sxs-lookup"><span data-stu-id="3af81-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="3af81-132">當您已經進行許多變更 tooyour 資源群組，並沒有現有的範本代表 hello 的所有變更，您可以使用此命令。</span><span class="sxs-lookup"><span data-stu-id="3af81-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="3af81-133">它會傳回 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-133">It returns hello template.</span></span> <span data-ttu-id="3af81-134">複製 hello JSON，並儲存成檔案。</span><span class="sxs-lookup"><span data-stu-id="3af81-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="3af81-135">請注意，不同於在 GitHub 中的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="3af81-136">它有不同的參數，而且沒有任何變數。</span><span class="sxs-lookup"><span data-stu-id="3af81-136">It has different parameters and no variables.</span></span> <span data-ttu-id="3af81-137">hello 儲存 SKU 和位置是硬式編碼 toovalues。</span><span class="sxs-lookup"><span data-stu-id="3af81-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="3af81-138">hello 下列範例顯示 hello 匯出的範本，但是您的範本有稍微不同的參數名稱：</span><span class="sxs-lookup"><span data-stu-id="3af81-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="3af81-139">您可以重新部署此範本，但需要猜測 hello 儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="3af81-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="3af81-140">您的參數名稱 hello 有些許不同。</span><span class="sxs-lookup"><span data-stu-id="3af81-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="3af81-141">自訂匯出的範本</span><span class="sxs-lookup"><span data-stu-id="3af81-141">Customize exported template</span></span>

<span data-ttu-id="3af81-142">您可以修改此範本 toomake 它更容易 toouse 而且更有彈性。</span><span class="sxs-lookup"><span data-stu-id="3af81-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="3af81-143">如需更多位置，變更 hello 位置屬性 toouse tooallow hello 與 hello 資源群組相同的位置：</span><span class="sxs-lookup"><span data-stu-id="3af81-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="3af81-144">tooavoid 具有 tooguess 唯一性儲存體帳戶名稱，移除 hello 參數 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3af81-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="3af81-145">新增儲存體名稱尾碼的參數，以及儲存體 SKU︰</span><span class="sxs-lookup"><span data-stu-id="3af81-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="3af81-146">加入建構 hello 儲存體帳戶名稱與 hello uniqueString 函式的變數：</span><span class="sxs-lookup"><span data-stu-id="3af81-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="3af81-147">設定 hello hello 儲存體帳戶 toohello 變數名稱：</span><span class="sxs-lookup"><span data-stu-id="3af81-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="3af81-148">設定 hello SKU toohello 參數：</span><span class="sxs-lookup"><span data-stu-id="3af81-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="3af81-149">您的範本現在如下所示：</span><span class="sxs-lookup"><span data-stu-id="3af81-149">Your template now looks like:</span></span>

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

<span data-ttu-id="3af81-150">重新部署 hello 修改的範本。</span><span class="sxs-lookup"><span data-stu-id="3af81-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3af81-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3af81-151">Next steps</span></span>
* <span data-ttu-id="3af81-152">如需使用 hello 入口 tooexport 範本資訊，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="3af81-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="3af81-153">toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="3af81-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="3af81-154">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="3af81-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>