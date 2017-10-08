---
title: "aaaAzure 資源管理員範本函式-資源 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 tooretrieve 值中的 hello 函式 toouse 相關資源。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的資源函式

資源管理員提供下列函數來取得資源值 hello:

* [listKeys 和 list{Value}](#listkeys)
* [提供者](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [訂用帳戶](#subscription)

tooget 值參數、 變數或 hello 目前部署中，請參閱[部署值函式](resource-group-template-functions-deployment.md)。

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys 和 list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

傳回 hello 任何支援 hello 清單作業的資源類型的值。 hello 最常見的用法是`listKeys`。 

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| resourceName 或 resourceIdentifier |是 |字串 |Hello 資源的唯一識別碼。 |
| apiVersion |是 |字串 |資源執行階段狀態的 API 版本。 一般來說，在 hello 格式**yyyy-mm-dd**。 |

### <a name="return-value"></a>傳回值

hello 傳回來自 Listkey 物件具有下列格式的 hello:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

其他 list 函式具有不同的傳回格式。 在函式、 toosee hello 格式包含在 hello 輸出區段 hello 範例範本中所示。 

### <a name="remarks"></a>備註

開頭為 **list** 的任何作業都可在您的範本中用為函式。 hello 可用的作業包括不僅 Listkey，但等作業也`list`， `listAdminKeys`，和`listStatus`。 不過，您無法使用**清單**需要在 hello 中的值的作業要求本文。 比方說，hello[清單帳戶 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS)作業需要要求主體參數喜歡*signedExpiry*，因此您無法在樣板內使用它。

toodetermine 哪些資源類型都有清單作業，您有下列選項的 hello:

* 檢視 hello [REST API 作業](/rest/api/)資源提供者，以及尋找清單作業。 例如，儲存體帳戶有 hello [Listkey 作業](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)。
* 使用 hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet。 hello 下列範例會取得所有儲存體帳戶的清單作業：

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* 使用下列 Azure CLI 命令 toofilter 只 hello 列出作業的 hello:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

使用任一個 hello 指定 hello 資源[resourceId 函數](#resourceid)，或 hello 格式`{providerNamespace}/{resourceType}/{resourceName}`。


### <a name="example"></a>範例

hello 下列範例顯示如何 tooreturn hello 主要和次要金鑰從 hello 的儲存體帳戶會輸出一節。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>提供者
`providers(providerNamespace, [resourceType])`

傳回資源提供者和其所支援資源類型的相關資訊。 如果您未提供資源類型，hello 函式會傳回所有支援的 hello 型別 hello 資源提供者。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| providerNamespace |是 |字串 |Hello 提供者命名空間 |
| resourceType |否 |字串 |指定命名空間內 hello 資源 hello 型別。 |

### <a name="return-value"></a>傳回值

每個支援的型別會傳回在 hello 下列格式： 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Hello 排序陣列傳回不保證值。

### <a name="example"></a>範例

hello 下列範例顯示如何 toouse hello 提供者函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

hello 上述範例會傳回物件中 hello 下列格式：

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

傳回代表資源執行階段狀態的物件。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| resourceName 或 resourceIdentifier |是 |string |資源的名稱或唯一識別碼。 |
| apiVersion |否 |字串 |API 版的 hello 指定的資源。 Hello 資源不會提供相同的範本中時包含此參數。 一般來說，在 hello 格式**yyyy-mm-dd**。 |

### <a name="return-value"></a>傳回值

每個資源類型傳回 hello 參考函式的不同屬性。 hello 函式不會傳回單一的預先定義的格式。 資源類型，toosee hello 屬性傳回 hello 中的 hello 物件輸出區段中 hello 範例所示。

### <a name="remarks"></a>備註

hello 參考函式衍生其值從執行階段的狀態，並因此不能用在 hello 變數區段。 它可以用於範本的 outputs 區段中。 

利用 hello 參考的函式，您隱含地宣告一個資源依存於另一個資源如果 hello 參考資源相同的範本內佈建。 您不需要 tooalso 使用 hello dependsOn 屬性。 hello 函式之前不會評估 hello 參照的資源已完成部署。

toosee hello 屬性名稱和值的資源類型，建立傳回 hello 輸出區段中的 hello 物件的範本。 如果您有現有的資源，該類型時，您的範本會傳回 hello 物件而不會部署任何新的資源。 

一般而言，您可以使用 hello**參考**函式 tooreturn 特定值的物件，例如 hello blob 端點 URI 或完整的網域名稱。

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>範例

hello toodeploy 和參考 hello 資源相同的範本，使用：

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

hello 上述範例會傳回物件中 hello 下列格式：

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

hello 下列範例會參考未部署此範本中的儲存體帳戶。 hello 儲存體帳戶已經存在於 hello 相同資源群組。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

傳回代表 hello 目前的資源群組的物件。 

### <a name="return-value"></a>傳回值

hello 傳回的物件處於 hello 下列格式：

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>備註

Hello resourceGroup 函式的常見用法是在 hello toocreate 資源與 hello 資源群組相同的位置。 hello 下列範例會使用 hello 資源群組位置 tooassign hello 位置的網站。

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>範例

hello 下列範本會傳回 hello hello 資源群組的屬性。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

hello 上述範例會傳回物件中 hello 下列格式：

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

傳回 hello 資源的唯一識別碼。 Hello 資源名稱模稜兩可或 hello 內不會佈建時，會使用此函式相同的範本。 

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| subscriptionId |否 |字串 (GUID 格式) |預設值為 hello 目前訂用帳戶。 當您需要 tooretrieve 其他訂用帳戶中的資源時，請指定這個值。 |
| resourceGroupName |否 |字串 |預設值為目前資源群組。 當您需要 tooretrieve 另一個資源群組中的資源時，請指定這個值。 |
| resourceType |是 |字串 |資源的類型 (包括資源提供者命名空間)。 |
| resourceName1 |是 |string |資源的名稱。 |
| resourceName2 |否 |string |如果是巢狀資源，則為下一個資源名稱區段。 |

### <a name="return-value"></a>傳回值

hello 識別碼會傳入 hello 下列格式：

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>備註

hello 參數所指定的值取決於 hello 資源是在 hello 與 hello 目前部署的相同訂用帳戶和資源群組。

tooget hello 資源識別碼 hello 的儲存體帳戶的相同訂用帳戶和資源群組中，使用：

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

儲存體帳戶中的 tooget hello 資源識別碼 hello 相同訂用帳戶，但不同的資源群組，請使用：

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

使用不同訂用帳戶和資源群組中的儲存體帳戶的 tooget hello 的資源 ID:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello 資源資料庫識別碼，在不同的資源群組中，使用：

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

通常，您需要 toouse 此函式時使用替代的資源群組中的儲存體帳戶或虛擬網路。 hello 下列範例顯示如何從外部的資源群組的資源可以輕鬆地加以使用：

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>範例

hello 下列範例會傳回儲存體帳戶的 hello 資源識別碼 hello 資源群組中：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| sameRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | String | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>訂用帳戶
`subscription()`

傳回有關 hello 目前部署的 hello 訂用帳戶的詳細資料。 

### <a name="return-value"></a>傳回值

hello 函式會傳回下列格式的 hello:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>範例

hello 下列範例顯示 hello 訂用帳戶函式，呼叫 hello 輸出區段中。 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

