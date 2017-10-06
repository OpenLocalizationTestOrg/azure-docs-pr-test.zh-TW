---
title: "aaaDefine JSON-Azure 邏輯應用程式的工作流程 |Microsoft 文件"
description: "如何 toowrite 工作流程定義，在 JSON 中的 logic apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>使用 JSON 建立邏輯應用程式的工作流程定義

您可以使用簡單、宣告式的 JSON 語言建立 [Azure Logic Apps](logic-apps-what-are-logic-apps.md) 的工作流程定義。 如果您還沒有這麼做，先檢閱[如何 toocreate 第一個邏輯應用程式與邏輯應用程式的設計工具](logic-apps-create-a-logic-app.md)。 此外，請參閱 hello[完整的 hello 工作流程定義語言參考](http://aka.ms/logicappsdocs)。

## <a name="repeat-steps-over-a-list"></a>對清單重複執行步驟

陣列，其中沒有 too10，000 項目和每個項目執行的動作，請使用 hello 透過 tooiterate [foreach 類型](logic-apps-loops-and-scopes.md)。

## <a name="handle-failures-if-something-goes-wrong"></a>若發生錯誤時會處理失敗

一般而言，您想 tooinclude*補救步驟*-執行一些邏輯*如果且只有*一或多個呼叫會失敗。 這個範例會取得資料，從不同位置，但是，如果 hello 呼叫失敗，我們要 tooPOST 訊息某處，我們可以稍後追蹤該失敗：  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify，`postToErrorMessageQueue`才會執行`readData`具有`Failed`，使用 hello`runAfter`屬性，例如 toospecify 一份可能的值，以便`runAfter`可能`["Succeeded", "Failed"]`。

最後，因為此範例中現在會處理 hello 錯誤，我們不再標示 hello 以執行`Failed`。 由於新增 hello 步驟處理此失敗，在此範例中，執行 hello 具有`Succeeded`雖然一個步驟`Failed`。

## <a name="execute-two-or-more-steps-in-parallel"></a>平行執行兩個以上步驟

toorun 以平行方式，多個動作 hello`runAfter`屬性必須在執行階段對等。 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

在此範例中，同時`branch1`和`branch2`設定之後 toorun `readData`。 如此一來，這兩個分支會以平行方式執行。 這兩個分支的 hello 時間戳記是相同的。

![平行](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>聯結兩個平行分支

您可以加入兩個動作以平行方式所設定的 toorun 的新增項目 toohello `runAfter` hello 先前範例所示的屬性。

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![平行](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>將對應的清單項目 tooa 不同的組態

接下來，假設我們想要根據屬性值 hello tooget 不同的內容。 我們可以做為參數建立值 toodestinations 的對應：  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

在此情況下，我們先取得文章清單。 Hello 類別目錄做為參數定義為基礎，hello 第二個步驟會使用對應 toolook 向上 hello URL 取得 hello 內容。

某些時間 toonote: 

*   hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection)函式會檢查是否 hello 類別目錄比對一個 hello 已知定義的類別。

*   我們取得 hello 類別之後，我們可以提取 hello hello 對應使用方括號中的項目：`parameters[...]`

## <a name="process-strings"></a>處理序字串

您可以使用各種函式 toomanipulate 字串。 例如，假設我們有我們想要 toopass tooa 系統，但我們不保險正確處理字元編碼的字串。 其中一個選項是 toobase64 將此字串編碼。 不過，在 URL 中，逸出 tooavoid 我們 tooreplace 的幾個字元。 

我們也想 hello 順序名稱的子字串，因為不會使用 hello 前五個字元。

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Toooutside 內運作：

1. 取得 hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello orderer 名稱，因此我們取回 hello 的總字元數。

2. 減 5，因為我們要較短的字串。

3. 實際上，採取 hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)。 我們開始索引`5`並移 hello hello 字串的其餘部分。

4. 轉換此子字串 tooa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64)字串。

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)所有的 hello`+`字元與`-`字元。

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)所有的 hello`/`字元與`_`字元。

## <a name="work-with-date-times"></a>使用日期時間

日期時間可能會很有用，特別是當您嘗試從資料來源不自然支援 toopull 資料*觸發程序*。 您也可以使用日期時間算出各步驟花費的時間。

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

在此範例中，我們會擷取 hello `startTime` hello 上一個步驟。 然後我們取得 hello 目前的時間，並減去一秒：

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

您可以使用其他的時間單位，例如 `minutes` 或 `hours`。 最後，我們可以比較這兩個值。 Hello 第一個值是否小於第二個值 hello，則超過 1 秒後經過 hello 先訂單。

tooformat 日期，我們可以使用字串格式器。 例如，tooget hello rfc1123 格式，我們使用[ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。 toolearn 關於日期格式，請參閱[工作流程定義語言](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。

## <a name="deployment-parameters-for-different-environments"></a>不同環境的部署參數

通常，部署生命週期中會有開發環境、預備環境及生產環境。 例如，您可能會使用 hello 相同的定義，在所有這些環境中，但使用不同的資料庫。 同樣地，您可能會想 toouse hello 相同定義跨越不同地區的高可用性，但想要每個邏輯應用程式執行個體 tootalk toothat 區域的資料庫。
此案例中不同於在參數*執行階段*位置，您應該改用 hello`trigger()`函式如 hello 先前範例所示。

您可以從基本定義開始，如下範例所示：

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

在實際的 hello`PUT`要求 hello logic apps，您可以提供 hello 參數`uri`。 預設值不再存在，因此 hello 邏輯應用程式承載需要此參數：

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

在每個環境中，您可以提供不同的值為 hello`connection`參數。 

所有 hello 您有建立及管理邏輯應用程式的選項，請參閱 hello [REST API 文件](https://msdn.microsoft.com/library/azure/mt643787.aspx)。 
