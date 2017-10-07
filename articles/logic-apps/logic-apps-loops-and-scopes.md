---
title: "aaaCreate 迴圈和範圍，或 debatch 中工作流程-Azure 邏輯應用程式資料 |Microsoft 文件"
description: "建立動作群組成範圍的資料，透過迴圈 tooiterate 或 debatch 資料 toostart Azure 邏輯應用程式中的多個工作流程。"
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
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="fd079-103">Logic Apps 迴圈、範圍和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="fd079-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="fd079-104">邏輯應用程式提供方式 toowork 陣列、 集合、 批次，與工作流程內迴圈的數目。</span><span class="sxs-lookup"><span data-stu-id="fd079-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="fd079-105">ForEach 迴圈和陣列</span><span class="sxs-lookup"><span data-stu-id="fd079-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="fd079-106">邏輯應用程式可讓您對資料集的 tooloop 和每個項目執行的動作。</span><span class="sxs-lookup"><span data-stu-id="fd079-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="fd079-107">這是可透過 hello`foreach`動作。</span><span class="sxs-lookup"><span data-stu-id="fd079-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="fd079-108">在 hello 設計工具中，您可以指定 tooadd for each 迴圈。</span><span class="sxs-lookup"><span data-stu-id="fd079-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="fd079-109">選取您想 tooiterate 透過 hello 陣列之後, 您就可以開始加入動作。</span><span class="sxs-lookup"><span data-stu-id="fd079-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="fd079-110">您目前是有限的 tooonly 一個動作，每個 「 foreach 迴圈 」，但 hello 即將週中，將會提高此限制。</span><span class="sxs-lookup"><span data-stu-id="fd079-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="fd079-111">一次 hello 迴圈中，您可以開始的 toospecify 應該會發生什麼在 hello 陣列的每個值。</span><span class="sxs-lookup"><span data-stu-id="fd079-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="fd079-112">如果使用程式碼檢視，您就可以指定 for each 迴圈，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd079-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="fd079-113">這是 for each 迴圈的範例，可針對每個包含「microsoft.com」的電子郵件地址傳送傳送電子郵件︰</span><span class="sxs-lookup"><span data-stu-id="fd079-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="fd079-114">A`foreach`動作可以逐一查看 too5，000 資料列組成的陣列。</span><span class="sxs-lookup"><span data-stu-id="fd079-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="fd079-115">預設會平行執行每個反覆運算。</span><span class="sxs-lookup"><span data-stu-id="fd079-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="fd079-116">循序 ForEach 迴圈</span><span class="sxs-lookup"><span data-stu-id="fd079-116">Sequential ForEach loops</span></span>

<span data-ttu-id="fd079-117">foreach 迴圈 tooexecute 循序 hello 的 tooenable`Sequential`應加入作業選項。</span><span class="sxs-lookup"><span data-stu-id="fd079-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="fd079-118">Until 迴圈</span><span class="sxs-lookup"><span data-stu-id="fd079-118">Until loop</span></span>
  
  <span data-ttu-id="fd079-119">您可以執行某個動作或一系列動作，直到符合某個條件為止。</span><span class="sxs-lookup"><span data-stu-id="fd079-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="fd079-120">hello 最常見的案例呼叫端點直到取得所需的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="fd079-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="fd079-121">在 hello 設計工具中，您可以指定 tooadd until 迴圈。</span><span class="sxs-lookup"><span data-stu-id="fd079-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="fd079-122">在新增之後 hello 迴圈內的動作，您可以設定 hello 結束條件，以及 hello 迴圈限制。</span><span class="sxs-lookup"><span data-stu-id="fd079-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="fd079-123">迴圈循環之間有 1 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="fd079-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="fd079-124">如果使用程式碼檢視，您可以指定 until 迴圈，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd079-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="fd079-125">這是呼叫的 HTTP 端點，直到 hello 值 'Completed' hello 回應主體的範例。</span><span class="sxs-lookup"><span data-stu-id="fd079-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="fd079-126">它將會在符合下列其中一種情況時完成</span><span class="sxs-lookup"><span data-stu-id="fd079-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="fd079-127">HTTP 回應具有「已完成」的狀態</span><span class="sxs-lookup"><span data-stu-id="fd079-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="fd079-128">已嘗試 1 小時的時間</span><span class="sxs-lookup"><span data-stu-id="fd079-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="fd079-129">已執行過 100 次的迴圈</span><span class="sxs-lookup"><span data-stu-id="fd079-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="fd079-130">SplitOn 和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="fd079-130">SplitOn and debatching</span></span>

<span data-ttu-id="fd079-131">有時觸發程序可能會收到項目，toodebatch 並啟動工作流程，每個項目的陣列。</span><span class="sxs-lookup"><span data-stu-id="fd079-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="fd079-132">這可以透過 hello 完成`spliton`命令。</span><span class="sxs-lookup"><span data-stu-id="fd079-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="fd079-133">根據預設，如果您的觸發程序 Swagger 指定的承載是一個陣列，即會新增 `spliton` ，並針對每個項目開始執行。</span><span class="sxs-lookup"><span data-stu-id="fd079-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="fd079-134">SplitOn 只能加入 tooa 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="fd079-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="fd079-135">這可以在定義程式碼檢視中手動設定或覆寫。</span><span class="sxs-lookup"><span data-stu-id="fd079-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="fd079-136">目前 SplitOn 可以 debatch too5，000 項目組成的陣列。</span><span class="sxs-lookup"><span data-stu-id="fd079-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="fd079-137">您不能有`spliton`和也實作 hello 同步回應模式。</span><span class="sxs-lookup"><span data-stu-id="fd079-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="fd079-138">呼叫的任何工作流程具有`response`此外動作太`spliton`會以非同步方式執行，並傳送立即`202 Accepted`回應。</span><span class="sxs-lookup"><span data-stu-id="fd079-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="fd079-139">SplitOn 可以指定程式碼檢視中，為下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="fd079-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="fd079-140">這會收到項目陣列，並在每一列上解除批次處理。</span><span class="sxs-lookup"><span data-stu-id="fd079-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="fd079-141">範圍</span><span class="sxs-lookup"><span data-stu-id="fd079-141">Scopes</span></span>

<span data-ttu-id="fd079-142">很可能 toogroup 一系列動作一起使用的範圍。</span><span class="sxs-lookup"><span data-stu-id="fd079-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="fd079-143">這特別適合用來實作例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="fd079-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="fd079-144">Hello 設計工具中，您可以加入新的領域，並開始新增在其內部的任何動作。</span><span class="sxs-lookup"><span data-stu-id="fd079-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="fd079-145">您可以在 hello 如下的程式碼檢視中定義範圍：</span><span class="sxs-lookup"><span data-stu-id="fd079-145">You can define scopes in code-view like hello following:</span></span>


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