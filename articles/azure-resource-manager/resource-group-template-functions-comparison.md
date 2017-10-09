---
title: "aaaAzure 資源管理員範本函式-比較 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toocompare 值中的 hello 函式 toouse。"
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的比較函式

Resource Manager 提供了幾個用來在範本中進行比較的函式。

* [equals](#equals)
* [greater](#greater)
* [greaterOrEquals](#greaterorequals)
* [less](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>equals
`equals(arg1, arg2)`

檢查兩個值是否彼此相等。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數、字串、陣列或物件 |hello 第一個值 toocheck 相等。 |
| arg2 |是 |整數、字串、陣列或物件 |hello 第二個值 toocheck 相等。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 值是否相等; 否則**False**。

### <a name="remarks"></a>備註

hello equals 函式常用以 hello`condition`元素 tootest 是否部署資源。

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a>範例

hello 範例範本會檢查不同類型的值相等。 所有的 hello 預設值為 true，則傳回。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | True |
| checkArrays | Bool | True |
| checkObjects | Bool | True |


hello 下列範例會使用[不](resource-group-template-functions-logical.md#not)與**等於**。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

上述範例中的 hello hello 輸出為：

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkNotEquals | Bool | True |


## <a name="greater"></a>greater
`greater(arg1, arg2)`

檢查是否大於第二個值的 hello hello 第一個值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數或字串 |hello hello 大於比較的第一個值。 |
| arg2 |是 |整數或字串 |hello hello 大於比較的第二個值。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 第一個值是大於 hello 第二個值; 否則如果**False**。

### <a name="example"></a>範例

hello 範例範本會檢查 hello 某個值是否大於 hello 其他。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

檢查 hello 第一個值是否大於或等於 toohello 第二個值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數或字串 |hello hello 大於或等於比較的第一個值。 |
| arg2 |是 |整數或字串 |hello hello 大於或等於比較的第二個值。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 第一個值是否大於或等於 toohello 第二個值; 否則**False**。

### <a name="example"></a>範例

hello 範例範本會在 hello 的一個值是否大於或等於 toohello 其他檢查。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |



## <a name="less"></a>less
`less(arg1, arg2)`

檢查是否 hello 第一個值小於 hello 第二個值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數或字串 |hello hello 小於比較的第一個值。 |
| arg2 |是 |整數或字串 |hello hello 小於比較的第二個值。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 第一個值是否小於 hello 第二個值; 否則**False**。

### <a name="example"></a>範例

hello 範例範本會檢查 hello 某個值是否小於其他 hello。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

檢查 hello 第一個值是否小於或等於 toohello 第二個值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數或字串 |hello hello 較少的第一個值或等號比較。 |
| arg2 |是 |整數或字串 |hello hello 小於第二個值或等號比較。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 第一個值是否小於或等於 toohello 第二個值，否則**False**。

### <a name="example"></a>範例

hello 範例範本會檢查 hello 某個值是否小於或等於其他 toohello。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |



## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

