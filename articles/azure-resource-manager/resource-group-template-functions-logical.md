---
title: "aaaAzure 資源管理員範本函式-邏輯 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toodetermine 邏輯值中的 hello 函式 toouse。"
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的邏輯函式

Resource Manager 提供了幾個用來在範本中進行比較的函式。

* [and](#and)
* [bool](#bool)
* [if](#if)
* [not](#not)
* [or](#or)

## <a name="and"></a>和
`and(arg1, arg2)`

檢查兩個參數值是否為 true。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |布林值 |hello 第一個值 toocheck 是否為 true。 |
| arg2 |是 |布林值 |hello 第二個值 toocheck 是否為 true。 |

### <a name="return-value"></a>傳回值

如果兩個值都是 true，則傳回 **True**，否則會傳回 **False**。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse 邏輯函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

上述範例中的 hello hello 輸出為：

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | True |
| notExampleOutput | Bool | False |


## <a name="bool"></a>布林
`bool(arg1)`

轉換 hello 參數 tooa 布林值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |字串或整數 |hello 值 tooconvert tooa 布林值。 |

### <a name="return-value"></a>傳回值
Hello 的布林值轉換值。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse bool 的字串或整數。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| trueString | Bool | True |
| falseString | Bool | False |
| trueInt | Bool | True |
| falseInt | Bool | False |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

根據條件是 true 或 false 傳回值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| condition |是 |布林值 |hello 值 toocheck，是否為 true。 |
| trueValue |是 | 字串、int、物件或陣列 |hello 值 tooreturn hello 條件為 true 時。 |
| falseValue |是 | 字串、int、物件或陣列 |hello 值 tooreturn 時 hello 條件為 false。 |

### <a name="return-value"></a>傳回值

當第一個參數是 **True** 時，傳回第二個參數；否則會傳回第三個參數。

### <a name="remarks"></a>備註

您可以使用這個函式 tooconditionally 集合之資源屬性。 hello 下列範例不完整的範本，但是它會顯示 hello 相關部分，有條件地設定 hello 可用性設定組。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse hello`if`函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

上述範例中的 hello hello 輸出為：

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| yesOutput | String | yes |
| noOutput | String | no |


## <a name="not"></a>否
`not(arg1)`

將轉換的布林值 tooits 相反值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |布林值 |hello 值 tooconvert。 |


### <a name="return-value"></a>傳回值

當參數是 **False** 時，傳回 **True**。 當參數是 **True** 時，傳回 **False**。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse 邏輯函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

上述範例中的 hello hello 輸出為：

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | True |
| notExampleOutput | Bool | False |

hello 下列範例會使用**不**與[等於](resource-group-template-functions-comparison.md#equals)。

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


## <a name="or"></a>或
`or(arg1, arg2)`

檢查任一個參數值是否為 true。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |布林值 |hello 第一個值 toocheck 是否為 true。 |
| arg2 |是 |布林值 |hello 第二個值 toocheck 是否為 true。 |

### <a name="return-value"></a>傳回值

如果任一值為 ture，傳回 **True**，否則會傳回 **False**。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse 邏輯函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

上述範例中的 hello hello 輸出為：

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | True |
| notExampleOutput | Bool | False |


## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

