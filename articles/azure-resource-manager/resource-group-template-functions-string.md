---
title: "資源管理員範本函式 aaaAzure-字串 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toowork，字串中的 hello 函式 toouse。"
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的字串函式

資源管理員提供下列函數使用字串 hello:

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [length](#length)
* [padLeft](#padleft)
* [replace](#replace)
* [skip](#skip)
* [分割](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [字串](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [修剪](#trim)
* [uniqueString](#uniquestring)
* [uri](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>base64
`base64(inputString)`

傳回 hello hello 輸入字串的 base64 表示法。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| inputString |是 |字串 |hello 值 tooreturn 為 base64 表示法。 |

### <a name="return-value"></a>傳回值

字串，包含 hello base64 表示法。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello base64 函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

將轉換的 base64 表示法 tooa JSON 物件。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| base64Value |是 |字串 |hello base64 表示法 tooconvert tooa JSON 物件。 |

### <a name="return-value"></a>傳回值

JSON 物件。

### <a name="examples"></a>範例

hello 下列範例會使用 hello base64ToJson 函式 tooconvert base64 值：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

將 base64 表示法 tooa 字串轉換。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| base64Value |是 |字串 |hello base64 表示法 tooconvert tooa 字串。 |

### <a name="return-value"></a>傳回值

已轉換字串 hello 的 base64 值。

### <a name="examples"></a>範例

hello 下列範例會使用 hello base64ToString 函式 tooconvert base64 值：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

結合多個字串值和傳回 hello 串連字串，或結合多個陣列並傳回串連的 hello 陣列。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |字串或陣列 |hello 串連的第一個值。 |
| 其他引數 |否 |字串 |串連的其他值 (循序順序)。 |

### <a name="return-value"></a>傳回值
串連值的字串或陣列。

### <a name="examples"></a>範例

hello 下列範例將說明如何 toocombine 兩個字串值，並傳回串連的字串。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| concatOutput | String | prefix-5yj4yjf5mbg72 |

hello 下列範例顯示兩個 toocombine 的陣列。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| return | 陣列 | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

<a id="contains" />

## <a name="contains"></a>contains
`contains (container, itemToFind)`

檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| container |是 |陣列、物件或字串 |包含 hello 值 toofind hello 值。 |
| itemToFind |是 |字串或整數 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

**True** hello 項目是否找到則為**False**。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse 包含與不同類型：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| stringTrue | Bool | True |
| stringFalse | Bool | False |
| objectTrue | Bool | True |
| objectFalse | Bool | False |
| arrayTrue | Bool | True |
| arrayFalse | Bool | False |

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

將轉換值 tooa 資料 URI。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToConvert |是 |字串 |hello 值 tooconvert tooa 資料 URI。 |

### <a name="return-value"></a>傳回值

格式化為資料 URI 的字串。

### <a name="examples"></a>範例

下列範例中的 hello 值 tooa 資料 URI 轉換，並且將 URI tooa 字串資料轉換：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| dataUriOutput | String | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | String | Hello, World! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

轉換資料的 URI 格式化值 tooa 字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |是 |字串 |hello 資料 URI 值 tooconvert。 |

### <a name="return-value"></a>傳回值

字串，包含 hello 轉換值。

### <a name="examples"></a>範例

下列範例中的 hello 值 tooa 資料 URI 轉換，並且將 URI tooa 字串資料轉換：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| dataUriOutput | String | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | String | Hello, World! |

<a id="empty" /> 

## <a name="empty"></a>empty
`empty(itemToTest)`

判斷陣列、物件或字串是否空白。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| itemToTest |是 |陣列、物件或字串 |hello 值 toocheck，如果是空白。 |

### <a name="return-value"></a>傳回值

傳回**True** hello 值是空的否則如果**False**。

### <a name="examples"></a>範例

下列範例會檢查是否是空的陣列、 物件和字串 hello。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayEmpty | Bool | True |
| objectEmpty | Bool | True |
| stringEmpty | Bool | True |

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

判斷字串結尾是否為值。 hello 比較不區分大小寫。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToSearch |是 |字串 |包含 hello 項目 toofind hello 值。 |
| stringToFind |是 |字串 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

**True** hello 最後一個字元或字元字串 hello 符合 hello 值; 否則**False**。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello startsWith 和 endsWith 函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

傳回 hello hello 字串的第一個字元或 hello 陣列的第一個項目。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 值 tooretrieve hello 第一個項目或字元。 |

### <a name="return-value"></a>傳回值

字串 hello 第一個字元或 hello 型別 （字串、 int、 陣列或物件） 的 hello 陣列中的第一個項目。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello 與陣列和字串的第一個函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | String | one |
| stringOutput | String | O |

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

傳回 hello 值在字串內的第一個位置。 hello 比較不區分大小寫。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToSearch |是 |字串 |包含 hello 項目 toofind hello 值。 |
| stringToFind |是 |字串 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

整數，代表 hello 項目 toofind hello 位置。 hello 值是以零為起始的。 如果找不到 hello 項目，則傳回-1。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello indexOf 和 lastIndexOf 函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

傳回最後一個 hello 字串的字元或 hello hello 陣列的最後一個項目。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 值 tooretrieve hello 最後一個項目或字元。 |

### <a name="return-value"></a>傳回值

Hello 最後一個字元，或 hello 型別 （字串、 int、 陣列或物件） hello 陣列中的最後一個項目的字串。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello 與陣列和字串的最後一個函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | String | three |
| stringOutput | String | e |

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

傳回 hello 值在字串內的最後一個位置。 hello 比較不區分大小寫。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToSearch |是 |字串 |包含 hello 項目 toofind hello 值。 |
| stringToFind |是 |字串 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

整數，代表 hello 項目 toofind hello 最後一個位置。 hello 值是以零為起始的。 如果找不到 hello 項目，則傳回-1。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello indexOf 和 lastIndexOf 函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>length
`length(string)`

傳回字串或陣列中的項目中的 hello 的字元數。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 取得 hello 元素數的陣列 toouse 或 hello 字串 toouse 取得 hello 的字元數。 |

### <a name="return-value"></a>傳回值

整數。 

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse 與陣列和字串的長度：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

<a id="padleft" />

## <a name="padleft"></a>padLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

藉由新增直到到達 hello 總指定的長度的字元 toohello 左傳回靠右對齊的字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| valueToPad |是 |字串或整數 |hello 值 tooright-對齊。 |
| totalLength |是 |int |傳回字串 hello 總數目 hello 中的字元。 |
| paddingCharacter |否 |單一字元 |hello 字元 toouse 左填補 hello 總長度為止。 hello 預設值是一個空格。 |

如果 hello 原始字串的長度超過 hello toopad 字元數目，就會不加入任何字元。

### <a name="return-value"></a>傳回值

字串至少 hello 指定字元的數。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toopad hello 使用者提供參數值加 hello 零字元直到達到 hello 的總字元數。 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| stringOutput | String | 0000000123 |

<a id="replace" />

## <a name="replace"></a>取代
`replace(originalString, oldString, newString)`

傳回具備由另一個字串取代的一個字串之所有執行個體的新字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| originalString |是 |字串 |hello 具有一個字串，取代成另一個字串的所有執行個體的值。 |
| oldString |是 |字串 |hello 字串 toobe 從 hello 原始字串中移除。 |
| newString |是 |字串 |取代 hello hello 字串 tooadd 移除字串。 |

### <a name="return-value"></a>傳回值

Hello 的字串取代字元。

### <a name="examples"></a>範例

hello 下列範例會顯示所有 tooremove 都虛線從 hello 使用者提供的字串的方式和 tooreplace 一部分 hello 以另一個字串的字串。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| firstOutput | String | 1231231234 |
| secodeOutput | String | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Hello 會指定所有 hello 元素的字元數或陣列後 hello 都指定的項目數目之後，傳回所有 hello 字元的字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| originalValue |是 |陣列或字串 |hello 陣列或字串 toouse 跳過。 |
| numberToSkip |是 |int |hello tooskip 項目或字元數目。 如果此值為 0 或更少，所有 hello 項目，或傳回 hello 值中的字元。 如果大於 hello hello 陣列或字串的長度，就會傳回空陣列或字串。 |

### <a name="return-value"></a>傳回值

陣列或字串。

### <a name="examples"></a>範例

下列範例會略過 hello hello hello 陣列中指定的項目數目和 hello 的字串中指定的字元數。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | 陣列 | ["three"] |
| stringOutput | String | two three |

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

傳回字串陣列，其中包含 hello 子字串 hello 的輸入字串 hello 所分隔指定的分隔符號。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| inputString |是 |字串 |hello 字串 toosplit。 |
| 分隔符號 |是 |字串或字串陣列 |將分割 hello 字串 hello 分隔符號 toouse。 |

### <a name="return-value"></a>傳回值

字串的陣列。

### <a name="examples"></a>範例

hello 下例 hello 輸入的字串分割以逗點，並以逗號或分號分隔。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| firstOutput | 陣列 | ["one", "two", "three"] |
| secondOutput | 陣列 | ["one", "two", "three"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

判斷字串開頭是否為值。 hello 比較不區分大小寫。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToSearch |是 |字串 |包含 hello 項目 toofind hello 值。 |
| stringToFind |是 |字串 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

**True** hello 第一個字元或字元字串 hello 符合 hello 值; 否則**False**。

### <a name="examples"></a>範例

hello 下列範例顯示如何 toouse hello startsWith 和 endsWith 函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

<a id="string" />

## <a name="string"></a>字串
`string(valueToConvert)`

轉換 hello 指定值 tooa 字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| valueToConvert |是 | 任意 |hello 值 tooconvert toostring。 任何類型的值均可轉換，包括物件和陣列。 |

### <a name="return-value"></a>傳回值

Hello 轉換值的字串。

### <a name="examples"></a>範例

hello 下列範例顯示如何 tooconvert 不同類型的值 toostrings:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| objectOutput | String | {"valueA":10,"valueB":"Example Text"} |
| arrayOutput | String | ["a","b","c"] |
| intOutput | String | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

傳回子字串開始於指定的 hello 字元位置，並包含 hello 指定的字元數。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToParse |是 |字串 |擷取子字串的哪個 hello hello 的原始字串。 |
| startIndex |否 |int |hello 以零為起始起始字元位置 hello 的子字串。 |
| length |否 |int |hello hello 的子字串的字元數。 必須參考 tooa hello 字串內的位置。 |

### <a name="return-value"></a>傳回值

hello 子字串。

### <a name="remarks"></a>備註

hello 函式失敗時的子字串 hello 超出 hello hello 字串的結尾。 下列範例中的 hello 因 hello 錯誤 「 hello 索引和長度參數必須參考 tooa hello 字串內的位置。 hello 索引參數: '0'，hello 長度參數: '11' hello hello 字串參數的長度: '10'。 」。

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>範例

下列範例中的 hello 自參數來擷取子字串。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| substringOutput | String | two |


<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

傳回字串 hello 與指定從 hello 開頭的字元數 hello 字串，或以 hello 陣列指定從 hello 開頭 hello 陣列元素數目。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| originalValue |是 |陣列或字串 |hello 陣列或字串 tootake hello 中的項目。 |
| numberToTake |是 |int |hello tootake 項目或字元數目。 如果此值為 0 或更小的值，則會傳回空白陣列或字串。 如果它大於指定之陣列或字串 hello hello 長度，則會傳回所有 hello 陣列或字串中的 hello 項目。 |

### <a name="return-value"></a>傳回值

陣列或字串。

### <a name="examples"></a>範例

下列範例會採用 hello hello 指定 hello 陣列中的項目和從字串的字元數目。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | 陣列 | ["one", "two"] |
| stringOutput | String | on |

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

轉換 hello 指定字串 toolower 案例。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToChange |是 |字串 |hello 值 tooconvert toolower 案例。 |

### <a name="return-value"></a>傳回值

hello 字串轉換 toolower 案例。

### <a name="examples"></a>範例

下列範例中的 hello 將轉換的參數值 toolower 案例和 tooupper 案例。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| toLowerOutput | String | one two three |
| toUpperOutput | String | ONE TWO THREE |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

轉換 hello 指定字串 tooupper 案例。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToChange |是 |字串 |hello 值 tooconvert tooupper 案例。 |

### <a name="return-value"></a>傳回值

hello 字串轉換 tooupper 案例。

### <a name="examples"></a>範例

下列範例中的 hello 將轉換的參數值 toolower 案例和 tooupper 案例。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| toLowerOutput | String | one two three |
| toUpperOutput | String | ONE TWO THREE |

<a id="trim" />

## <a name="trim"></a>修剪
`trim (stringToTrim)`

移除所有開頭和尾端空白字元 hello 從指定的字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToTrim |是 |字串 |hello 值 tootrim。 |

### <a name="return-value"></a>傳回值

hello 不含字串開頭和尾端空白字元。

### <a name="examples"></a>範例

hello 下列範例會修剪 hello hello 參數的空格字元。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| 傳回 | String | one two three |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

建立根據 hello 值做為參數提供具決定性的雜湊字串。 

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| baseString |是 |字串 |hello 值用於 hello 雜湊函式 toocreate 的唯一字串。 |
| 視需要，也會使用其他參數 |否 |字串 |您可以將許多字串為指定的唯一性 hello 層級的所需的 toocreate hello 值。 |

### <a name="remarks"></a>備註

當您需要 toocreate 資源的唯一名稱，此函式是很有幫助。 您提供的唯一性的 hello 結果的 hello 範圍限制的參數值。 您可以指定 hello 名稱是否唯一下 toosubscription、 資源群組或部署。 

hello 傳回值不是隨機的字串，但而 hello 雜湊函式的結果。 hello 傳回值為 13 個字元。 它不是全域唯一的。 您可能想 toocombine hello 值與前置詞的命名慣例 toocreate 有意義的名稱。 hello 下列範例顯示 hello hello 傳回值格式。 hello 實際值會因 hello 提供的參數。

    tcvhiyu5h2o5o

hello 遵循範例顯示如何 toouse uniqueString toocreate 的唯一值通常使用層級。

唯一的限定範圍的 toosubscription

```json
"[uniqueString(subscription().subscriptionId)]"
```

唯一的限定範圍的 tooresource 群組

```json
"[uniqueString(resourceGroup().id)]"
```

資源群組的唯一已設定領域的 toodeployment

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

hello 下列範例顯示如何 toocreate 儲存體帳戶的唯一名稱根據您的資源群組。 Hello 資源群組內，hello 名稱不是唯一如果建構 hello 相同的方式。

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>傳回值

包含 13 個字元的字串。

### <a name="examples"></a>範例

下列範例中的 hello uniquestring 從傳回的結果：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>uri
`uri (baseUri, relativeUri)`

藉由結合 hello baseUri 和 hello relativeUri 字串建立的絕對 URI。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| baseUri |是 |字串 |hello 基底 uri 的字串。 |
| relativeUri |是 |字串 |hello 相對 uri 字串 tooadd toohello 基底 uri 字串。 |

hello 值 hello **baseUri**參數可以包含特定的檔案，但建構 hello URI 時，系統會使用 hello 基底路徑。 例如，傳遞`http://contoso.com/resources/azuredeploy.json`做為基底 URI 中的 hello baseUri 參數結果`http://contoso.com/resources/`。

### <a name="return-value"></a>傳回值

字串，代表 hello hello 基底和相對值的絕對 URI。

### <a name="examples"></a>範例

hello 下列範例顯示如何 tooconstruct 連結 tooa 巢狀的範本為基礎的 hello 父樣板的 hello 值。

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

將 URI 編碼。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| stringToEncode |是 |字串 |hello 值 tooencode。 |

### <a name="return-value"></a>傳回值

Hello URI 的字串編碼值。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

傳回 URI 編碼值的字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| uriEncodedString |是 |字串 |hello URI 編碼值 tooconvert tooa 字串。 |

### <a name="return-value"></a>傳回值

URI 編碼值的解碼字串。

### <a name="examples"></a>範例

下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |


## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

