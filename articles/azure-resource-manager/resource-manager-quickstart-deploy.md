---
title: "將資源部署到 Azure | Microsoft Docs"
description: "使用 Azure PowerShell 或 Azure CLI 將資源部署到 Azure。 資源會定義在 Resource Manager 範本中。"
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
ms.openlocfilehash: 19d5ec337a18b1a159de05ed611b2ccd0c15c592
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="8dcfd-104">將資源部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="8dcfd-104">Deploy resources to Azure</span></span>

<span data-ttu-id="8dcfd-105">本主題說明如何將資源部署到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="8dcfd-106">您可以使用 Azure PowerShell 或 Azure CLI 來部署定義解決方案基礎結構的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="8dcfd-107">如需 Resource Manager 的概念簡介，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="8dcfd-108">部署步驟</span><span class="sxs-lookup"><span data-stu-id="8dcfd-108">Steps for deployment</span></span>

<span data-ttu-id="8dcfd-109">本主題假設您會在本主題中部署此[範例儲存體範本](#example-storage-template)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="8dcfd-110">您可以使用不同的範本，但所傳遞的參數會與本主題中所示的不同。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="8dcfd-111">建立範本之後，部署範本的一般步驟包括：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="8dcfd-112">登入您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8dcfd-112">Log in to your account</span></span>
2. <span data-ttu-id="8dcfd-113">選取要使用的訂用帳戶 (只有當您有多個訂用帳戶，且您想要使用非預設訂用帳戶時，才需要執行此步驟)</span><span class="sxs-lookup"><span data-stu-id="8dcfd-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="8dcfd-114">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="8dcfd-114">Create a resource group</span></span>
4. <span data-ttu-id="8dcfd-115">部署範本</span><span class="sxs-lookup"><span data-stu-id="8dcfd-115">Deploy the template</span></span>
5. <span data-ttu-id="8dcfd-116">檢查部署狀態</span><span class="sxs-lookup"><span data-stu-id="8dcfd-116">Check your deployment status</span></span>

<span data-ttu-id="8dcfd-117">下列各節說明如何使用 [PowerShell](#powershell) 或 [Azure CLI](#azure-cli) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="8dcfd-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dcfd-118">PowerShell</span></span>

1. <span data-ttu-id="8dcfd-119">若要安裝 Azure PowerShell，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="8dcfd-120">若要快速開始部署，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="8dcfd-121">只有當您想要使用預設訂用帳戶以外的訂用帳戶時，才需要使用 `Set-AzureRmContext` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="8dcfd-122">若要查看您的所有訂用帳戶及其 ID，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="8dcfd-123">部署需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="8dcfd-124">部署完成時，您會看到類似以下的訊息：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="8dcfd-125">若要查看您的資源群組和儲存體帳戶是否已部署到您的訂用帳戶，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="8dcfd-126">部署範本時，您可以指定範本參數作為 PowerShell 參數。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="8dcfd-127">先前的範例並未包含任何範本參數，因此會使用範本中的預設值。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="8dcfd-128">若要部署另一個儲存體帳戶，並為儲存體名稱前置詞和儲存體帳戶 SKU 提供參數值，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="8dcfd-129">現在，您的資源群組中有兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="8dcfd-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8dcfd-130">Azure CLI</span></span>

1. <span data-ttu-id="8dcfd-131">若要安裝 Azure CLI，請參閱[安裝 Azure CLI 2.0 (英文)](/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="8dcfd-132">若要快速開始部署，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="8dcfd-133">只有當您想要使用預設訂用帳戶以外的訂用帳戶時，才需要使用 `az account set` 命令。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="8dcfd-134">若要查看您的所有訂用帳戶及其 ID，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="8dcfd-135">部署需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="8dcfd-136">部署完成時，您會看到類似以下的訊息：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="8dcfd-137">若要查看您的資源群組和儲存體帳戶是否已部署到您的訂用帳戶，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="8dcfd-138">部署範本時，您可以指定範本參數作為 PowerShell 參數。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="8dcfd-139">先前的範例並未包含任何範本參數，因此會使用範本中的預設值。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="8dcfd-140">若要部署另一個儲存體帳戶，並為儲存體名稱前置詞和儲存體帳戶 SKU 提供參數值，請使用：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="8dcfd-141">現在，您的資源群組中有兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="8dcfd-142">範例儲存體範本</span><span class="sxs-lookup"><span data-stu-id="8dcfd-142">Example storage template</span></span>

<span data-ttu-id="8dcfd-143">請使用下列範例範本將儲存體帳戶部署到您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="8dcfd-143">Use the following example template to deploy a storage account to your subscription:</span></span>

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
        "description": "The value to use for starting the storage account name."
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
        "description": "The type of replication to use for the storage account."
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

## <a name="next-steps"></a><span data-ttu-id="8dcfd-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8dcfd-144">Next steps</span></span>

* <span data-ttu-id="8dcfd-145">如需有關使用 PowerShell 來部署範本的詳細資訊，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="8dcfd-146">如需有關使用 Azure CLI 來部署範本的詳細資訊，請參閱[使用 Resource Manager 範本與 Azure CLI 部署資源](/azure/azure-resource-manager/resource-group-template-deploy-cli)。</span><span class="sxs-lookup"><span data-stu-id="8dcfd-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



