---
title: "aaaAzure Resource Manager 範本函式-陣列和物件 |Microsoft 文件"
description: "描述使用陣列和物件的 Azure Resource Manager 範本中的 hello 函式 toouse。"
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 範本的陣列和物件函式 

Resource Manager 提供了幾個用來使用陣列和物件的函式。

* [array](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

請參閱 tooget 值，以分隔的字串值的陣列[分割](resource-group-template-functions-string.md#split)。

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

將轉換 hello 值 tooan 陣列。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| convertToArray |是 |整數、字串、陣列或物件 |hello 值 tooconvert tooan 陣列。 |

### <a name="return-value"></a>傳回值

陣列。

### <a name="example"></a>範例

hello 下列範例顯示如何 toouse hello 與不同類型的陣列函式。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| intOutput | 陣列 | [1] |
| stringOutput | 陣列 | ["a"] |
| objectOutput | 陣列 | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

從 hello 參數中傳回第一個非 null 值。 空白字串、空白陣列和空白物件不是 null。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數、字串、陣列或物件 |hello 第一個值 tootest 為 null 的。 |
| 其他引數 |否 |整數、字串、陣列或物件 |將 tootest 額外的值為 null 的。 |

### <a name="return-value"></a>傳回值

hello hello 第一個非 null 參數值，它可以是字串、 int、 陣列或物件。 如果所有參數都是 null，則傳回 null。 

### <a name="example"></a>範例

hello 下列範例顯示不同用法 coalesce hello 輸出。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| stringOutput | String | 預設值 |
| intOutput | int | 1 |
| objectOutput | Object | {"first": "default"} |
| arrayOutput | 陣列 | [1] |
| emptyOutput | Bool | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

結合多個陣列並傳回串連的 hello 陣列，或結合多個字串值，並傳回 hello 串連字串。 

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 第一個陣列或字串串連。 |
| 其他引數 |否 |陣列或字串 |串連的其他陣列或字串 (循序順序)。 |

此函式可以接受任意數目的引數，並且可以接受字串或陣列以進行 hello 參數。

### <a name="return-value"></a>傳回值
串連值的字串或陣列。

### <a name="example"></a>範例

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

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| container |是 |陣列、物件或字串 |包含 hello 值 toofind hello 值。 |
| itemToFind |是 |字串或整數 |hello 值 toofind。 |

### <a name="return-value"></a>傳回值

**True** hello 項目是否找到則為**False**。

### <a name="example"></a>範例

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

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

建立從 hello 參數的陣列。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |字串、整數、陣列或物件 |hello hello 陣列中的第一個值。 |
| 其他引數 |否 |字串、整數、陣列或物件 |Hello 陣列中的其他值。 |

### <a name="return-value"></a>傳回值

陣列。

### <a name="example"></a>範例

下列範例會示範如何 hello toouse createArray 與不同類型：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
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
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| stringArray | 陣列 | ["a", "b", "c"] |
| intArray | 陣列 | [1, 2, 3] |
| objectArray | 陣列 | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | 陣列 | [["one", "two", "three"]] |

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

### <a name="example"></a>範例

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

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

傳回 hello hello 陣列的第一個項目或 hello 字串的第一個字元。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 值 tooretrieve hello 第一個項目或字元。 |

### <a name="return-value"></a>傳回值

hello hello 在陣列中，第一個項目類型 （字串、 int、 陣列或物件） 或 hello 第一個字元的字串。

### <a name="example"></a>範例

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

<a id="intersection" />

## <a name="intersection"></a>交集
`intersection(arg1, arg2, arg3, ...)`

從 hello 參數中傳回的單一陣列或物件 hello 通用項目。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或物件 |hello 第一個值 toouse 尋找通用項目。 |
| arg2 |是 |陣列或物件 |hello 第二個值 toouse 尋找通用項目。 |
| 其他引數 |否 |陣列或物件 |其他值 toouse 尋找通用項目。 |

### <a name="return-value"></a>傳回值

陣列或物件與 hello 通用項目。

### <a name="example"></a>範例

下列範例會顯示與 toouse 交集的陣列和物件 hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "three": "c"} |
| arrayOutput | 陣列 | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

傳回 JSON 物件。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |字串 |hello 值 tooconvert tooJSON。 |


### <a name="return-value"></a>傳回值

字串或空的物件，指定從 hello 的 hello JSON 物件時**null**指定。

### <a name="example"></a>範例

下列範例會顯示與 toouse 交集的陣列和物件 hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| jsonOutput | Object | {"a": "b"} |
| nullOutput | Boolean | True |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

傳回 hello hello 陣列的最後一個項目或 hello 字串的最後一個字元。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 值 tooretrieve hello 最後一個項目或字元。 |

### <a name="return-value"></a>傳回值

hello hello 在陣列中，最後一個項目類型 （字串、 int、 陣列或物件） 或 hello 最後一個字元的字串。

### <a name="example"></a>範例

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

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

傳回 hello 的元素數目，為陣列或字串中的字元。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或字串 |hello 取得 hello 元素數的陣列 toouse 或 hello 字串 toouse 取得 hello 的字元數。 |

### <a name="return-value"></a>傳回值

整數。 

### <a name="example"></a>範例

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

建立資源時，您可以使用此函式以陣列 toospecify hello 的反覆項目數目。 在下列範例的 hello，hello 參數**siteNames**建立 hello 網站時，會參考名稱 toouse tooan 陣列。

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

如需有關在此陣列中使用函式的詳細資訊，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

傳回 hello 從整數的陣列或以逗號分隔的整數清單的最小值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數的陣列，或以逗號分隔的整數清單 |hello 集合 tooget hello 最小值。 |

### <a name="return-value"></a>傳回值

整數，代表 hello 最小值。

### <a name="example"></a>範例

下列範例會示範如何 hello toouse 最小值與整數清單和陣列：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max(arg1)`

傳回 hello 從整數的陣列或以逗號分隔的整數清單的最大值。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |整數的陣列，或以逗號分隔的整數清單 |hello 集合 tooget hello 最大值。 |

### <a name="return-value"></a>傳回值

整數，代表 hello 最大值。

### <a name="example"></a>範例

下列範例會示範如何 hello toouse 陣列與整數清單的最大值：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

從起始整數建立整數陣列，且其中包含一些項目。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| startingInteger |是 |int |hello hello 陣列中的第一個整數。 |
| numberofElements |是 |int |hello hello 陣列中的整數數目。 |

### <a name="return-value"></a>傳回值

整數陣列。

### <a name="example"></a>範例

hello 下列範例顯示如何 toouse hello 範圍函式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| rangeOutput | 陣列 | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Hello hello 陣列中指定數目或 hello hello 字串中指定數字之後會傳回所有 hello 字元的字串之後，傳回所有 hello 元素的陣列。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| originalValue |是 |陣列或字串 |hello 陣列或字串 toouse 跳過。 |
| numberToSkip |是 |int |hello tooskip 項目或字元數目。 如果此值為 0 或更少，所有 hello 項目，或傳回 hello 值中的字元。 如果大於 hello hello 陣列或字串的長度，就會傳回空陣列或字串。 |

### <a name="return-value"></a>傳回值

陣列或字串。

### <a name="example"></a>範例

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

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

傳回以 hello 陣列指定的項目數從 hello hello 陣列的開頭或字串 hello 與指定的 hello hello 字串的開頭字元數。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| originalValue |是 |陣列或字串 |hello 陣列或字串 tootake hello 中的項目。 |
| numberToTake |是 |int |hello tootake 項目或字元數目。 如果此值為 0 或更小的值，則會傳回空白陣列或字串。 如果它大於指定之陣列或字串 hello hello 長度，則會傳回所有 hello 陣列或字串中的 hello 項目。 |

### <a name="return-value"></a>傳回值

陣列或字串。

### <a name="example"></a>範例

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

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

從 hello 參數中傳回的單一陣列或物件的所有項目。 重複的值或索引鍵只會納入一次。

### <a name="parameters"></a>參數

| 參數 | 必要 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| arg1 |是 |陣列或物件 |hello 第一個值 toouse 加入項目。 |
| arg2 |是 |陣列或物件 |hello 第二個值 toouse 加入項目。 |
| 其他引數 |否 |陣列或物件 |其他值 toouse 加入項目。 |

### <a name="return-value"></a>傳回值

陣列或物件。

### <a name="example"></a>範例

下列範例所示 toouse 聯集的陣列和物件 hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

hello 輸出範例與 hello 預設值是從上述 hello:

| 名稱 | 類型 | 值 |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | 陣列 | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。
* toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

