---
title: "aaaAzure 資源管理員範本函式-部署 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 tooretrieve 部署資訊中的 hello 函式 toouse。"
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的部署函式 

資源管理員提供 hello 下列函數來取得從 hello 範本的區段值和值相關的 toohello 部署：

* [部署](#deployment)
* [參數](#parameters)
* [變數](#variables)

tooget 或值的資源、 資源群組訂閱，請參閱[資源函式](resource-group-template-functions-resource.md)。

<a id="deployment" />

## <a name="deployment"></a>部署
`deployment()`

傳回 hello 目前的部署作業的相關資訊。

### <a name="return-value"></a>傳回值

此函數會傳回部署期間所傳入的 hello 物件。 依是否 hello 部署物件會傳遞為連結或內嵌物件中傳回物件的 hello hello 內容有所不同。 當 hello 部署物件時，會傳遞內嵌，例如使用 hello **-TemplateFile**參數在 Azure PowerShell toopoint tooa 本機檔案中，傳回的物件具有下列格式的 hello hello:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

當 hello 物件傳遞為連結，例如當使用 hello **-TemplateUri**參數 toopoint tooa 遠端物件、 hello 物件會傳入 hello 下列格式： 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>備註

您可以使用 hello hello 父範本的 URI 為基礎的 deployment() toolink tooanother 範本。

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>範例

hello 下列範例會傳回 hello 部署物件：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

hello 上述範例會傳回下列物件的 hello:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>參數
`parameters(parameterName)`

傳回參數值。 hello 指定的參數名稱必須 hello 範本 hello 參數區段中定義。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| parameterName |是 |字串 |hello 參數 tooreturn hello 名稱。 |

### <a name="return-value"></a>傳回值

hello hello 值指定參數。

### <a name="remarks"></a>備註

一般而言，您可以使用參數 tooset 資源值。 hello 下列範例會設定網站 toohello 參數值在部署期間所傳入的 hello 名稱。

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>範例

hello 下列範例示範簡化的使用 hello 參數函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| stringOutput | String | 選項 1 |
| intOutput | int | 1 |
| objectOutput | Object | {"one": "a", "two": "b"} |
| arrayOutput | 陣列 | [1, 2, 3] |
| crossOutput | String | 選項 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

傳回 hello 變數的值。 hello 指定的變數名稱必須 hello 變數 hello 範本區段中定義。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| variableName |是 |String |hello 變數 tooreturn hello 名稱。 |

### <a name="return-value"></a>傳回值

hello hello 指定變數的值。

### <a name="remarks"></a>備註

一般而言，您使用變數 toosimplify 範本可以建構複雜的值一次。 hello 下列範例會建構儲存體帳戶的唯一名稱。

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>範例

hello 範例範本會傳回不同的變數值。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| exampleOutput1 | String | myVariable |
| exampleOutput2 | 陣列 | [1, 2, 3, 4] |
| exampleOutput3 | String | myVariable |
| exampleOutput4 |  Object | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

