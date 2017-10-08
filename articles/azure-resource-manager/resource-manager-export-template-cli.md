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
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>使用 Azure CLI 來匯出 Azure Resource Manager 範本

資源管理員可讓您 tooexport Resource Manager 範本使用從您的訂用帳戶中現有的資源。 您可以使用該產生的範本 toolearn，有關 hello 範本語法或 tooautomate hello 重新部署方案視需要。

它是重要 toonote 有兩個不同的方式 tooexport 範本：

* 您可以匯出您用於部署的 hello 實際範本。 hello 匯出的範本包含所有 hello 參數和變數，如同它們是出現在 hello 原始範本。 當您需要 tooretrieve 範本時，這個方法就很有幫助。
* 您可以匯出代表 hello hello 資源群組的目前狀態的範本。 hello 匯出的範本不根據您用於部署的任何範本。 相反地，它會建立 hello 資源群組的快照集的範本。 hello 匯出的範本有許多的硬式編碼值，可能不一樣多的參數，因為您通常會定義。 當您修改了 hello 資源群組，則這個方法會很有用。 現在，您需要 toocapture hello 資源群組，做為範本。

本主題說明這兩種方法。

## <a name="deploy-a-solution"></a>部署解決方案

這兩個 tooillustrate 方法匯出範本，讓我們開始部署方案 tooyour 訂用帳戶。 如果您想 tooexport 您訂用帳戶中已經有資源群組，您沒有 toodeploy 此解決方案。 不過，hello 本文其餘部分是指 toohello 範本，針對此解決方案。 hello 範例指令碼會將部署的儲存體帳戶。

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>從部署歷程記錄儲存範本

您也可以使用 hello 部署歷程記錄中擷取範本[az 群組部署匯出](/cli/azure/group/deployment#export)命令。 下列範例會將儲存 hello 範本您先前部署的 hello:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

它會傳回 hello 範本。 複製 hello JSON，並儲存成檔案。 請注意，它會是您用於部署的 hello 確切範本。 hello 參數和變數符合從 GitHub hello 範本。 您可以重新部署此範本。


## <a name="export-resource-group-as-template"></a>匯出資源群組以作為範本

而不是從 hello 部署歷程記錄中擷取範本，您可以擷取使用 hello 代表 hello 的資源群組的目前狀態的範本[az 群組匯出](/cli/azure/group#export)命令。 當您已經進行許多變更 tooyour 資源群組，並沒有現有的範本代表 hello 的所有變更，您可以使用此命令。

```azurecli
az group export --name ExampleGroup
```

它會傳回 hello 範本。 複製 hello JSON，並儲存成檔案。 請注意，不同於在 GitHub 中的 hello 範本。 它有不同的參數，而且沒有任何變數。 hello 儲存 SKU 和位置是硬式編碼 toovalues。 hello 下列範例顯示 hello 匯出的範本，但是您的範本有稍微不同的參數名稱：

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

您可以重新部署此範本，但需要猜測 hello 儲存體帳戶的唯一名稱。 您的參數名稱 hello 有些許不同。

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>自訂匯出的範本

您可以修改此範本 toomake 它更容易 toouse 而且更有彈性。 如需更多位置，變更 hello 位置屬性 toouse tooallow hello 與 hello 資源群組相同的位置：

```json
"location": "[resourceGroup().location]",
```

tooavoid 具有 tooguess 唯一性儲存體帳戶名稱，移除 hello 參數 hello 儲存體帳戶名稱。 新增儲存體名稱尾碼的參數，以及儲存體 SKU︰

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

加入建構 hello 儲存體帳戶名稱與 hello uniqueString 函式的變數：

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

設定 hello hello 儲存體帳戶 toohello 變數名稱：

```json
"name": "[variables('storageAccountName')]",
```

設定 hello SKU toohello 參數：

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

您的範本現在如下所示：

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

重新部署 hello 修改的範本。

## <a name="next-steps"></a>後續步驟
* 如需使用 hello 入口 tooexport 範本資訊，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。
* toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。
* 如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。