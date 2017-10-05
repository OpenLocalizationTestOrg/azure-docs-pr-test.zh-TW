---
title: "在工作流程中建立迴圈和範圍，或解除批次 (debatch) 資料 - Azure Logic Apps | Microsoft Docs"
description: "在 Azure Logic Apps 中建立迴圈來逐一查看資料、將動作群組為範圍，或者解除批次資料，以便啟動更多工作流程。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="79256-103">Logic Apps 迴圈、範圍和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="79256-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="79256-104">Logic Apps 提供數種方法來處理工作流程中的陣列、集合、批次和迴圈。</span><span class="sxs-lookup"><span data-stu-id="79256-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="79256-105">ForEach 迴圈和陣列</span><span class="sxs-lookup"><span data-stu-id="79256-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="79256-106">Logic Apps 可讓您在一組資料上進行迴圈，並為每個項目執行動作。</span><span class="sxs-lookup"><span data-stu-id="79256-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="79256-107">這可透過 `foreach` 動作來達成。</span><span class="sxs-lookup"><span data-stu-id="79256-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="79256-108">在設計工具中，您可以指定要新增一個 for each 迴圈。</span><span class="sxs-lookup"><span data-stu-id="79256-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="79256-109">在選取您希望反覆查看的陣列之後，就可以新增動作。</span><span class="sxs-lookup"><span data-stu-id="79256-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="79256-110">目前您受限於每個 foreach 迴圈只能有一個動作，但在未來幾週內，將會提高此限制。</span><span class="sxs-lookup"><span data-stu-id="79256-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="79256-111">一旦進入迴圈之後，您就可以開始指定應針對陣列的每個值執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="79256-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="79256-112">如果使用程式碼檢視，您就可以指定 for each 迴圈，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79256-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="79256-113">這是 for each 迴圈的範例，可針對每個包含「microsoft.com」的電子郵件地址傳送傳送電子郵件︰</span><span class="sxs-lookup"><span data-stu-id="79256-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="79256-114">`foreach` 動作可以反覆查看陣列，最多 5,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="79256-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="79256-115">預設會平行執行每個反覆運算。</span><span class="sxs-lookup"><span data-stu-id="79256-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="79256-116">循序 ForEach 迴圈</span><span class="sxs-lookup"><span data-stu-id="79256-116">Sequential ForEach loops</span></span>

<span data-ttu-id="79256-117">若要啟用要循序執行的 foreach 迴圈，應該新增 `Sequential` 作業選項。</span><span class="sxs-lookup"><span data-stu-id="79256-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="79256-118">Until 迴圈</span><span class="sxs-lookup"><span data-stu-id="79256-118">Until loop</span></span>
  
  <span data-ttu-id="79256-119">您可以執行某個動作或一系列動作，直到符合某個條件為止。</span><span class="sxs-lookup"><span data-stu-id="79256-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="79256-120">對於此迴圈的最常見案例是呼叫端點，直到您取得所需的回應為止。</span><span class="sxs-lookup"><span data-stu-id="79256-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="79256-121">在設計工具中，您可以指定要新增一個 until 迴圈。</span><span class="sxs-lookup"><span data-stu-id="79256-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="79256-122">在迴圈中新增動作之後，您就可以設定結束條件以及迴圈限制。</span><span class="sxs-lookup"><span data-stu-id="79256-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="79256-123">迴圈循環之間有 1 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="79256-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="79256-124">如果使用程式碼檢視，您可以指定 until 迴圈，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79256-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="79256-125">這個範例會呼叫 HTTP 端點，直到回應主體具有「已完成」的值為止。</span><span class="sxs-lookup"><span data-stu-id="79256-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="79256-126">它將會在符合下列其中一種情況時完成</span><span class="sxs-lookup"><span data-stu-id="79256-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="79256-127">HTTP 回應具有「已完成」的狀態</span><span class="sxs-lookup"><span data-stu-id="79256-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="79256-128">已嘗試 1 小時的時間</span><span class="sxs-lookup"><span data-stu-id="79256-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="79256-129">已執行過 100 次的迴圈</span><span class="sxs-lookup"><span data-stu-id="79256-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="79256-130">SplitOn 和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="79256-130">SplitOn and debatching</span></span>

<span data-ttu-id="79256-131">觸發程序有時可能會接收到您想要解除批次處理並針對每個項目啟動工作流程的項目陣列。</span><span class="sxs-lookup"><span data-stu-id="79256-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="79256-132">這可透過 `spliton` 命令來完成。</span><span class="sxs-lookup"><span data-stu-id="79256-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="79256-133">根據預設，如果您的觸發程序 Swagger 指定的承載是一個陣列，即會新增 `spliton` ，並針對每個項目開始執行。</span><span class="sxs-lookup"><span data-stu-id="79256-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="79256-134">SplitOn 只會新增至觸發程序。</span><span class="sxs-lookup"><span data-stu-id="79256-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="79256-135">這可以在定義程式碼檢視中手動設定或覆寫。</span><span class="sxs-lookup"><span data-stu-id="79256-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="79256-136">SplitOn 目前可以解除批次處理陣列，最多 5,000 個項目。</span><span class="sxs-lookup"><span data-stu-id="79256-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="79256-137">您無法具有 `spliton` 並同時實作同步回應模式。</span><span class="sxs-lookup"><span data-stu-id="79256-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="79256-138">若所呼叫的任何工作流程除了 `spliton` 之外還有 `response` 動作，將會以非同步方式執行並傳送立即 `202 Accepted` 回應。</span><span class="sxs-lookup"><span data-stu-id="79256-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="79256-139">SplitOn 可以指定於程式碼檢視中，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="79256-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="79256-140">這會收到項目陣列，並在每一列上解除批次處理。</span><span class="sxs-lookup"><span data-stu-id="79256-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="79256-141">範圍</span><span class="sxs-lookup"><span data-stu-id="79256-141">Scopes</span></span>

<span data-ttu-id="79256-142">可能可以使用 scope 來將一系列動作群組在一起。</span><span class="sxs-lookup"><span data-stu-id="79256-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="79256-143">這特別適合用來實作例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="79256-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="79256-144">在設計工具中，您可以新增範圍，並開始在其內部新增任何動作。</span><span class="sxs-lookup"><span data-stu-id="79256-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="79256-145">您可以在程式碼檢視中定義範圍，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="79256-145">You can define scopes in code-view like the following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```