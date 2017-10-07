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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>設定 Azure Resource Manager 範本中的資源位置
在部署範本時，您必須為每個資源提供一個位置。 本主題會顯示的每個資源的訂用帳戶可用 tooyour toodetermine hello 位置的型別。

## <a name="determine-supported-locations"></a>決定支援的位置

如需支援每個資源類型位置的完整清單，請參閱[依區域提供的產品](https://azure.microsoft.com/regions/services/)。 不過，您的訂用帳戶可能沒有存取 tooall hello 位置，該清單中。 toosee 自訂清單的位置是使用 tooyour 訂用帳戶，使用 Azure PowerShell 或 Azure CLI。 

hello 下列範例會使用 PowerShell tooget hello 位置 hello`Microsoft.Web\sites`資源類型：

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

hello 下列範例會使用 Azure CLI 2.0 tooget hello 位置 hello`Microsoft.Web\sites`資源類型：

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>在範本中設定位置

決定之後 hello 支援資源的位置，您需要 tooset 該位置在範本中。 hello 的 toocreate 資源群組中的位置，以支援 hello 資源類型，則這個值是最簡單的方式 tooset 和設定每個位置太`[resourceGroup().location]`。 您可以重新部署 hello 範本 tooresource 群組在不同的位置，並不會變更 hello 範本或參數中的任何值。 

hello 下列範例顯示已部署的 toohello 儲存體帳戶與 hello 資源群組相同的位置：

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

如果您需要 toohardcode hello 位置在範本中，提供的其中一個支援的 hello 區域 hello 名稱。 hello 下列範例會顯示儲存體帳戶永遠部署 tooNorth 美國中部：

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

## <a name="next-steps"></a>後續步驟
* 如需有關如何建議 toocreate 範本，請參閱[最佳作法來建立 Azure 資源管理員範本](resource-manager-template-best-practices.md)。

