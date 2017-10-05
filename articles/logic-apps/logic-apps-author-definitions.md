---
title: "使用 JSON 定義工作流程 - Azure Logic Apps | Microsoft Docs"
description: "如何以 JSON 撰寫 Logic Apps 的工作流程定義"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="fb4b8-103">使用 JSON 建立邏輯應用程式的工作流程定義</span><span class="sxs-lookup"><span data-stu-id="fb4b8-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="fb4b8-104">您可以使用簡單、宣告式的 JSON 語言建立 [Azure Logic Apps](logic-apps-what-are-logic-apps.md) 的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="fb4b8-105">如果您還沒有這麼做，請先檢閱[如何使用邏輯應用程式設計工具建立第一個邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="fb4b8-106">此外，請參閱[工作流程定義語言的完整參考](http://aka.ms/logicappsdocs)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="fb4b8-107">對清單重複執行步驟</span><span class="sxs-lookup"><span data-stu-id="fb4b8-107">Repeat steps over a list</span></span>

<span data-ttu-id="fb4b8-108">若要逐一查看有多達 10,000 個項目的陣列，並針對每個項目執行動作，請使用 [foreach 類型](logic-apps-loops-and-scopes.md)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="fb4b8-109">若發生錯誤時會處理失敗</span><span class="sxs-lookup"><span data-stu-id="fb4b8-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="fb4b8-110">通常，您想要包括*補救步驟* — 如果*且唯有*當一或多個呼叫失敗時執行的一些邏輯。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="fb4b8-111">此範例會從各種地方取得資料，但如果呼叫失敗，我們想要在某處 POST 訊息，方便稍後追蹤該失敗。：</span><span class="sxs-lookup"><span data-stu-id="fb4b8-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="fb4b8-112">若要指定 `postToErrorMessageQueue` 僅在 `readData` 已 `Failed` 之後才會執行，使用 `runAfter` 屬性，例如，指定可能值的清單，以便 `runAfter` 可能是 `["Succeeded", "Failed"]`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="fb4b8-113">最後，因為此範例現在會處理錯誤，我們不再將執行結果標示為 `Failed`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="fb4b8-114">因為我們在此範例中新增處理此失敗的步驟，執行結果為 `Succeeded`，雖然其中一個步驟 `Failed`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="fb4b8-115">平行執行兩個以上步驟</span><span class="sxs-lookup"><span data-stu-id="fb4b8-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="fb4b8-116">若要平行執行多個動作，`runAfter` 屬性在執行階段必須相同。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="fb4b8-117">在此範例中，`branch1` 和 `branch2` 設定為在 `readData` 之後執行。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="fb4b8-118">如此一來，這兩個分支會以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="fb4b8-119">兩個分支的時間戳記完全相同。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-119">The timestamp for both branches is identical.</span></span>

![平行](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="fb4b8-121">聯結兩個平行分支</span><span class="sxs-lookup"><span data-stu-id="fb4b8-121">Join two parallel branches</span></span>

<span data-ttu-id="fb4b8-122">透過先前範例中的方式在 `runAfter` 屬性新增項目，即可聯結設定為平行執行的兩個動作。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="fb4b8-124">將清單項目對應至不同的組態</span><span class="sxs-lookup"><span data-stu-id="fb4b8-124">Map list items to a different configuration</span></span>

<span data-ttu-id="fb4b8-125">接下來，假設我們想要根據屬性的值取得不同的內容。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="fb4b8-126">我們可以建立值與目的地的對應做為參數：</span><span class="sxs-lookup"><span data-stu-id="fb4b8-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="fb4b8-127">在此情況下，我們先取得文章清單。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="fb4b8-128">根據已定義為參數的類別，第二個步驟會使用對應查詢 URL 來取得內容。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="fb4b8-129">這裡要注意的某些時間︰</span><span class="sxs-lookup"><span data-stu-id="fb4b8-129">Some times to note here:</span></span> 

*   <span data-ttu-id="fb4b8-130">[ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) 函式會檢查類別是否符合其中一個已知的定義類別。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="fb4b8-131">在取得類別後，我們可以使用方括號從對應提取項目：`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="fb4b8-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="fb4b8-132">處理序字串</span><span class="sxs-lookup"><span data-stu-id="fb4b8-132">Process strings</span></span>

<span data-ttu-id="fb4b8-133">您可以使用不同的函式來操作字串。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="fb4b8-134">例如，假設我們有想要傳遞到系統上的字串，但我們並不十分熟悉字元編碼的正確處理。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="fb4b8-135">一種作法是以 base64 將此字串編碼。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="fb4b8-136">不過，為了避免在 URL 中逸出，我們要取代幾個字元。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="fb4b8-137">我們也想要訂單名稱的子字串，因為不會用到前五個字元。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="fb4b8-138">使用從內到外︰</span><span class="sxs-lookup"><span data-stu-id="fb4b8-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="fb4b8-139">取得訂購者名稱的 [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length)，以便我們傳回字元總數。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="fb4b8-140">減 5，因為我們要較短的字串。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="fb4b8-141">實際取得 [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="fb4b8-142">我們從索引 `5` 開始，並取得字串的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="fb4b8-143">將這個子字串轉換成 [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) 字串。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="fb4b8-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) 所有 `+` 字元換成 `-` 字元。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="fb4b8-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) 所有 `/` 字元換成 `_` 字元。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="fb4b8-146">使用日期時間</span><span class="sxs-lookup"><span data-stu-id="fb4b8-146">Work with Date Times</span></span>

<span data-ttu-id="fb4b8-147">日期時間很有用，特別是在嘗試從不支援的觸發程序的資料來源提取資料時。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="fb4b8-148">您也可以使用日期時間算出各步驟花費的時間。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="fb4b8-149">在此範例中，我們從前一個步驟擷取 `startTime`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="fb4b8-150">然後我們會取得目前的時間，並減去一秒︰</span><span class="sxs-lookup"><span data-stu-id="fb4b8-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="fb4b8-151">您可以使用其他的時間單位，例如 `minutes` 或 `hours`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="fb4b8-152">最後，我們可以比較這兩個值。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="fb4b8-153">如果第一個值小於第二個值，則自從訂單最初提交以來已超過一秒。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="fb4b8-154">若要格式化日期，我們可以使用字串格式子。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="fb4b8-155">例如，若要取得 RFC1123，我們使用 [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="fb4b8-156">若要深入了解日期格式設定，請參閱[工作流程定義語言](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="fb4b8-157">不同環境的部署參數</span><span class="sxs-lookup"><span data-stu-id="fb4b8-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="fb4b8-158">通常，部署生命週期中會有開發環境、預備環境及生產環境。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="fb4b8-159">例如，您可以在所有這些環境中使用相同的定義，但使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="fb4b8-160">同樣地，您可能想要跨不同的區域使用相同的定義，以發揮高可用性，但希望每個邏輯應用程式執行個體與該區域資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="fb4b8-161">這種情況與在執行階段採用參數不同，相反地，您應該如先前範例所示使用 `trigger()` 函式。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="fb4b8-162">您可以從基本定義開始，如下範例所示：</span><span class="sxs-lookup"><span data-stu-id="fb4b8-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="fb4b8-163">在邏輯應用程式的實際 `PUT` 要求中，您可以提供參數 `uri`。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="fb4b8-164">因為預設值不存在，邏輯應用程式承載需要此參數︰</span><span class="sxs-lookup"><span data-stu-id="fb4b8-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="fb4b8-165">在每個環境中，您可以提供不同的值給 `connection` 參數。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="fb4b8-166">如需有關建立及管理邏輯應用程式的所有可用選項，請參閱 [REST API 文件](https://msdn.microsoft.com/library/azure/mt643787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fb4b8-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
