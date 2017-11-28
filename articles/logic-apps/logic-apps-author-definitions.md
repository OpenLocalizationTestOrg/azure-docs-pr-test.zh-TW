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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="5e4f4-103">使用 JSON 建立邏輯應用程式的工作流程定義</span><span class="sxs-lookup"><span data-stu-id="5e4f4-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="5e4f4-104">您可以使用簡單、宣告式的 JSON 語言建立 [Azure Logic Apps](logic-apps-what-are-logic-apps.md) 的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="5e4f4-105">如果您還沒有這麼做，先檢閱[如何 toocreate 第一個邏輯應用程式與邏輯應用程式的設計工具](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5e4f4-106">此外，請參閱 hello[完整的 hello 工作流程定義語言參考](http://aka.ms/logicappsdocs)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="5e4f4-107">對清單重複執行步驟</span><span class="sxs-lookup"><span data-stu-id="5e4f4-107">Repeat steps over a list</span></span>

<span data-ttu-id="5e4f4-108">陣列，其中沒有 too10，000 項目和每個項目執行的動作，請使用 hello 透過 tooiterate [foreach 類型](logic-apps-loops-and-scopes.md)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="5e4f4-109">若發生錯誤時會處理失敗</span><span class="sxs-lookup"><span data-stu-id="5e4f4-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="5e4f4-110">一般而言，您想 tooinclude*補救步驟*-執行一些邏輯*如果且只有*一或多個呼叫會失敗。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="5e4f4-111">這個範例會取得資料，從不同位置，但是，如果 hello 呼叫失敗，我們要 tooPOST 訊息某處，我們可以稍後追蹤該失敗：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="5e4f4-112">toospecify，`postToErrorMessageQueue`才會執行`readData`具有`Failed`，使用 hello`runAfter`屬性，例如 toospecify 一份可能的值，以便`runAfter`可能`["Succeeded", "Failed"]`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="5e4f4-113">最後，因為此範例中現在會處理 hello 錯誤，我們不再標示 hello 以執行`Failed`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="5e4f4-114">由於新增 hello 步驟處理此失敗，在此範例中，執行 hello 具有`Succeeded`雖然一個步驟`Failed`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="5e4f4-115">平行執行兩個以上步驟</span><span class="sxs-lookup"><span data-stu-id="5e4f4-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="5e4f4-116">toorun 以平行方式，多個動作 hello`runAfter`屬性必須在執行階段對等。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="5e4f4-117">在此範例中，同時`branch1`和`branch2`設定之後 toorun `readData`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="5e4f4-118">如此一來，這兩個分支會以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="5e4f4-119">這兩個分支的 hello 時間戳記是相同的。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-119">hello timestamp for both branches is identical.</span></span>

![平行](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="5e4f4-121">聯結兩個平行分支</span><span class="sxs-lookup"><span data-stu-id="5e4f4-121">Join two parallel branches</span></span>

<span data-ttu-id="5e4f4-122">您可以加入兩個動作以平行方式所設定的 toorun 的新增項目 toohello `runAfter` hello 先前範例所示的屬性。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="5e4f4-124">將對應的清單項目 tooa 不同的組態</span><span class="sxs-lookup"><span data-stu-id="5e4f4-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="5e4f4-125">接下來，假設我們想要根據屬性值 hello tooget 不同的內容。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="5e4f4-126">我們可以做為參數建立值 toodestinations 的對應：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="5e4f4-127">在此情況下，我們先取得文章清單。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="5e4f4-128">Hello 類別目錄做為參數定義為基礎，hello 第二個步驟會使用對應 toolook 向上 hello URL 取得 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="5e4f4-129">某些時間 toonote:</span><span class="sxs-lookup"><span data-stu-id="5e4f4-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="5e4f4-130">hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection)函式會檢查是否 hello 類別目錄比對一個 hello 已知定義的類別。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="5e4f4-131">我們取得 hello 類別之後，我們可以提取 hello hello 對應使用方括號中的項目：`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="5e4f4-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="5e4f4-132">處理序字串</span><span class="sxs-lookup"><span data-stu-id="5e4f4-132">Process strings</span></span>

<span data-ttu-id="5e4f4-133">您可以使用各種函式 toomanipulate 字串。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="5e4f4-134">例如，假設我們有我們想要 toopass tooa 系統，但我們不保險正確處理字元編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="5e4f4-135">其中一個選項是 toobase64 將此字串編碼。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="5e4f4-136">不過，在 URL 中，逸出 tooavoid 我們 tooreplace 的幾個字元。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="5e4f4-137">我們也想 hello 順序名稱的子字串，因為不會使用 hello 前五個字元。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="5e4f4-138">Toooutside 內運作：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="5e4f4-139">取得 hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello orderer 名稱，因此我們取回 hello 的總字元數。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="5e4f4-140">減 5，因為我們要較短的字串。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="5e4f4-141">實際上，採取 hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="5e4f4-142">我們開始索引`5`並移 hello hello 字串的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="5e4f4-143">轉換此子字串 tooa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64)字串。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="5e4f4-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)所有的 hello`+`字元與`-`字元。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="5e4f4-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)所有的 hello`/`字元與`_`字元。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="5e4f4-146">使用日期時間</span><span class="sxs-lookup"><span data-stu-id="5e4f4-146">Work with Date Times</span></span>

<span data-ttu-id="5e4f4-147">日期時間可能會很有用，特別是當您嘗試從資料來源不自然支援 toopull 資料*觸發程序*。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="5e4f4-148">您也可以使用日期時間算出各步驟花費的時間。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="5e4f4-149">在此範例中，我們會擷取 hello `startTime` hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="5e4f4-150">然後我們取得 hello 目前的時間，並減去一秒：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="5e4f4-151">您可以使用其他的時間單位，例如 `minutes` 或 `hours`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="5e4f4-152">最後，我們可以比較這兩個值。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="5e4f4-153">Hello 第一個值是否小於第二個值 hello，則超過 1 秒後經過 hello 先訂單。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="5e4f4-154">tooformat 日期，我們可以使用字串格式器。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="5e4f4-155">例如，tooget hello rfc1123 格式，我們使用[ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="5e4f4-156">toolearn 關於日期格式，請參閱[工作流程定義語言](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="5e4f4-157">不同環境的部署參數</span><span class="sxs-lookup"><span data-stu-id="5e4f4-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="5e4f4-158">通常，部署生命週期中會有開發環境、預備環境及生產環境。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="5e4f4-159">例如，您可能會使用 hello 相同的定義，在所有這些環境中，但使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="5e4f4-160">同樣地，您可能會想 toouse hello 相同定義跨越不同地區的高可用性，但想要每個邏輯應用程式執行個體 tootalk toothat 區域的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="5e4f4-161">此案例中不同於在參數*執行階段*位置，您應該改用 hello`trigger()`函式如 hello 先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="5e4f4-162">您可以從基本定義開始，如下範例所示：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="5e4f4-163">在實際的 hello`PUT`要求 hello logic apps，您可以提供 hello 參數`uri`。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="5e4f4-164">預設值不再存在，因此 hello 邏輯應用程式承載需要此參數：</span><span class="sxs-lookup"><span data-stu-id="5e4f4-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="5e4f4-165">在每個環境中，您可以提供不同的值為 hello`connection`參數。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="5e4f4-166">所有 hello 您有建立及管理邏輯應用程式的選項，請參閱 hello [REST API 文件](https://msdn.microsoft.com/library/azure/mt643787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e4f4-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
