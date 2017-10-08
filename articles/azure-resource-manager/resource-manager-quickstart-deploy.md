---
title: "aaaDeploy 資源 tooAzure |Microsoft 文件"
description: "使用 Azure PowerShell 或 Azure CLI toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="30c10-104">部署資源 tooAzure</span><span class="sxs-lookup"><span data-stu-id="30c10-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="30c10-105">本主題說明如何 toodeploy 資源 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="30c10-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="30c10-106">您可以使用 Azure PowerShell 或 Azure CLI toodeploy 資源管理員範本可定義您方案的 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="30c10-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="30c10-107">如簡介 tooconcepts 的資源管理員，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="30c10-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="30c10-108">部署步驟</span><span class="sxs-lookup"><span data-stu-id="30c10-108">Steps for deployment</span></span>

<span data-ttu-id="30c10-109">本主題假設您要部署的 hello[範例儲存範本](#example-storage-template)本主題中。</span><span class="sxs-lookup"><span data-stu-id="30c10-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="30c10-110">您可以使用不同的範本，但不同於本主題中所顯示 hello 您傳遞的參數。</span><span class="sxs-lookup"><span data-stu-id="30c10-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="30c10-111">建立範本之後, hello 部署範本的一般步驟如下：</span><span class="sxs-lookup"><span data-stu-id="30c10-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="30c10-112">登入 tooyour 帳戶</span><span class="sxs-lookup"><span data-stu-id="30c10-112">Log in tooyour account</span></span>
2. <span data-ttu-id="30c10-113">選取 hello 訂用帳戶 toouse （只在如果您有多個訂用帳戶，而且您想 toouse 不 hello 預設訂用帳戶的其中一個必要）</span><span class="sxs-lookup"><span data-stu-id="30c10-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="30c10-114">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="30c10-114">Create a resource group</span></span>
4. <span data-ttu-id="30c10-115">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="30c10-115">Deploy hello template</span></span>
5. <span data-ttu-id="30c10-116">檢查部署狀態</span><span class="sxs-lookup"><span data-stu-id="30c10-116">Check your deployment status</span></span>

<span data-ttu-id="30c10-117">hello 下列各節說明如何 tooperform 那些步驟[PowerShell](#powershell)或[Azure CLI](#azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="30c10-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="30c10-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30c10-118">PowerShell</span></span>

1. <span data-ttu-id="30c10-119">tooinstall Azure PowerShell，請參閱[開始使用 Azure PowerShell cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="30c10-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="30c10-120">tooquickly 開始進行部署，請使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="30c10-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="30c10-121">hello`Set-AzureRmContext`預設訂用帳戶以外 toouse 訂用帳戶時，將只需要 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="30c10-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="30c10-122">toosee 所有訂用帳戶，以及其識別碼，使用：</span><span class="sxs-lookup"><span data-stu-id="30c10-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="30c10-123">hello 部署可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="30c10-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="30c10-124">部署完成時，您會看到類似以下的訊息：</span><span class="sxs-lookup"><span data-stu-id="30c10-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="30c10-125">資源群組和儲存體帳戶所 toosee 部署 tooyour 訂用帳戶，使用：</span><span class="sxs-lookup"><span data-stu-id="30c10-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="30c10-126">部署範本時，您可以指定範本參數作為 PowerShell 參數。</span><span class="sxs-lookup"><span data-stu-id="30c10-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="30c10-127">hello 先前範例未包含任何範本參數，所以使用 hello hello 範本中的預設值。</span><span class="sxs-lookup"><span data-stu-id="30c10-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="30c10-128">toodeploy 另一個儲存體帳戶，而且提供 hello 儲存體名稱前置詞和 hello 儲存體帳戶 SKU，使用參數值：</span><span class="sxs-lookup"><span data-stu-id="30c10-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="30c10-129">現在，您的資源群組中有兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="30c10-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="30c10-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30c10-130">Azure CLI</span></span>

1. <span data-ttu-id="30c10-131">tooinstall Azure CLI，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="30c10-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="30c10-132">tooquickly 開始部署，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="30c10-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="30c10-133">hello`az account set`預設訂用帳戶以外 toouse 訂用帳戶時，將只需要命令。</span><span class="sxs-lookup"><span data-stu-id="30c10-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="30c10-134">toosee 所有訂用帳戶，以及其識別碼，使用：</span><span class="sxs-lookup"><span data-stu-id="30c10-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="30c10-135">hello 部署可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="30c10-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="30c10-136">部署完成時，您會看到類似以下的訊息：</span><span class="sxs-lookup"><span data-stu-id="30c10-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="30c10-137">資源群組和儲存體帳戶所 toosee 部署 tooyour 訂用帳戶，使用：</span><span class="sxs-lookup"><span data-stu-id="30c10-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="30c10-138">部署範本時，您可以指定範本參數作為 PowerShell 參數。</span><span class="sxs-lookup"><span data-stu-id="30c10-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="30c10-139">hello 先前範例未包含任何範本參數，所以使用 hello hello 範本中的預設值。</span><span class="sxs-lookup"><span data-stu-id="30c10-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="30c10-140">toodeploy 另一個儲存體帳戶，而且提供 hello 儲存體名稱前置詞和 hello 儲存體帳戶 SKU，使用參數值：</span><span class="sxs-lookup"><span data-stu-id="30c10-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="30c10-141">現在，您的資源群組中有兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="30c10-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="30c10-142">範例儲存體範本</span><span class="sxs-lookup"><span data-stu-id="30c10-142">Example storage template</span></span>

<span data-ttu-id="30c10-143">使用下列範例範本 toodeploy 儲存體帳戶 tooyour 訂用帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="30c10-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="30c10-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30c10-144">Next steps</span></span>

* <span data-ttu-id="30c10-145">如需使用 PowerShell toodeploy 範本的詳細資訊，請參閱[部署資源與資源管理員範本和 Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="30c10-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="30c10-146">如需使用 Azure CLI toodeploy 範本的詳細資訊，請參閱[部署資源，資源管理員範本與 Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli)。</span><span class="sxs-lookup"><span data-stu-id="30c10-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



