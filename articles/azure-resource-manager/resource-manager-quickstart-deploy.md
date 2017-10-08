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
# <a name="deploy-resources-tooazure"></a>部署資源 tooAzure

本主題說明如何 toodeploy 資源 tooyour Azure 訂用帳戶。 您可以使用 Azure PowerShell 或 Azure CLI toodeploy 資源管理員範本可定義您方案的 hello 基礎結構。

如簡介 tooconcepts 的資源管理員，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。

## <a name="steps-for-deployment"></a>部署步驟

本主題假設您要部署的 hello[範例儲存範本](#example-storage-template)本主題中。 您可以使用不同的範本，但不同於本主題中所顯示 hello 您傳遞的參數。

建立範本之後, hello 部署範本的一般步驟如下：

1. 登入 tooyour 帳戶
2. 選取 hello 訂用帳戶 toouse （只在如果您有多個訂用帳戶，而且您想 toouse 不 hello 預設訂用帳戶的其中一個必要）
3. 建立資源群組
4. 部署 hello 範本
5. 檢查部署狀態

hello 下列各節說明如何 tooperform 那些步驟[PowerShell](#powershell)或[Azure CLI](#azure-cli)。

## <a name="powershell"></a>PowerShell

1. tooinstall Azure PowerShell，請參閱[開始使用 Azure PowerShell cmdlet](/powershell/azure/overview)。

2. tooquickly 開始進行部署，請使用下列 cmdlet 的 hello:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  hello`Set-AzureRmContext`預設訂用帳戶以外 toouse 訂用帳戶時，將只需要 cmdlet。 toosee 所有訂用帳戶，以及其識別碼，使用：

  ```powershell
  Get-AzureRmSubscription
  ```

3. hello 部署可能需要幾分鐘的時間 toocomplete。 部署完成時，您會看到類似以下的訊息：

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. 資源群組和儲存體帳戶所 toosee 部署 tooyour 訂用帳戶，使用：

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. 部署範本時，您可以指定範本參數作為 PowerShell 參數。 hello 先前範例未包含任何範本參數，所以使用 hello hello 範本中的預設值。 toodeploy 另一個儲存體帳戶，而且提供 hello 儲存體名稱前置詞和 hello 儲存體帳戶 SKU，使用參數值：

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  現在，您的資源群組中有兩個儲存體帳戶。 

## <a name="azure-cli"></a>Azure CLI

1. tooinstall Azure CLI，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2)。

2. tooquickly 開始部署，請使用下列命令的 hello:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  hello`az account set`預設訂用帳戶以外 toouse 訂用帳戶時，將只需要命令。 toosee 所有訂用帳戶，以及其識別碼，使用：

  ```azurecli
  az account list
  ```

3. hello 部署可能需要幾分鐘的時間 toocomplete。 部署完成時，您會看到類似以下的訊息：

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. 資源群組和儲存體帳戶所 toosee 部署 tooyour 訂用帳戶，使用：

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. 部署範本時，您可以指定範本參數作為 PowerShell 參數。 hello 先前範例未包含任何範本參數，所以使用 hello hello 範本中的預設值。 toodeploy 另一個儲存體帳戶，而且提供 hello 儲存體名稱前置詞和 hello 儲存體帳戶 SKU，使用參數值：

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  現在，您的資源群組中有兩個儲存體帳戶。 

## <a name="example-storage-template"></a>範例儲存體範本

使用下列範例範本 toodeploy 儲存體帳戶 tooyour 訂用帳戶的 hello:

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

## <a name="next-steps"></a>後續步驟

* 如需使用 PowerShell toodeploy 範本的詳細資訊，請參閱[部署資源與資源管理員範本和 Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy)。
* 如需使用 Azure CLI toodeploy 範本的詳細資訊，請參閱[部署資源，資源管理員範本與 Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli)。



