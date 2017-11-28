---
title: "錯誤和例外狀況處理 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps 中的錯誤和例外狀況處理模式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="5b527-103">處理 Azure Logic Apps 中的錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="5b527-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="5b527-104">Azure Logic Apps 提供了豐富的工具和模式，以協助確保您的整合穩固且具有彈性，不怕故障。</span><span class="sxs-lookup"><span data-stu-id="5b527-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="5b527-105">任何整合架構都會帶來挑戰，讓您難以確定是否可適當地處理相依系統的停機或問題。</span><span class="sxs-lookup"><span data-stu-id="5b527-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="5b527-106">Logic Apps 讓處理錯誤成為一種頂級享受，賦予您所需工具來處理工作流程內的例外狀況和錯誤。</span><span class="sxs-lookup"><span data-stu-id="5b527-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="5b527-107">重試原則</span><span class="sxs-lookup"><span data-stu-id="5b527-107">Retry policies</span></span>

<span data-ttu-id="5b527-108">重試原則是最基本的例外狀況和錯誤處理類型。</span><span class="sxs-lookup"><span data-stu-id="5b527-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="5b527-109">如果初始要求逾時或失敗 (任何造成 429 或 5xx 回應的要求)，此原則會定義是否應該重試動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="5b527-110">根據預設，所有動作會在 20 秒的間隔內另外再試 4 次。</span><span class="sxs-lookup"><span data-stu-id="5b527-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="5b527-111">因此，如果第一個要求收到 `500 Internal Server Error` 回應，工作流程引擎就會暫停 20 秒，然後再一次嘗試要求。</span><span class="sxs-lookup"><span data-stu-id="5b527-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="5b527-112">如果在經過所有重試後回應仍是例外狀況或失敗，工作流程會繼續，並將動作狀態標示為 `Failed`。</span><span class="sxs-lookup"><span data-stu-id="5b527-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="5b527-113">您可以在特定動作的**輸入**中設定重試原則。</span><span class="sxs-lookup"><span data-stu-id="5b527-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="5b527-114">例如，您可以設定重試原則，以在 1 小時的間隔內嘗試多達 4 次。</span><span class="sxs-lookup"><span data-stu-id="5b527-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="5b527-115">如需輸入屬性的完整詳細資料，請參閱[工作流程動作與觸發程序][retryPolicyMSDN]。</span><span class="sxs-lookup"><span data-stu-id="5b527-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="5b527-116">如果您想要 HTTP 動作重試 4 次，並在每次嘗試之間等候 10 分鐘，您會使用下列定義︰</span><span class="sxs-lookup"><span data-stu-id="5b527-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="5b527-117">如需受支援語法的詳細資訊，請參閱[工作流程動作和觸發程序中的 retry-policy 區段][retryPolicyMSDN]。</span><span class="sxs-lookup"><span data-stu-id="5b527-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="5b527-118">使用 RunAfter 屬性來擷取失敗</span><span class="sxs-lookup"><span data-stu-id="5b527-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="5b527-119">每個邏輯應用程式動作都會宣告要讓此動作啟動必須先完成哪些動作，就像是將工作流程中的步驟排序。</span><span class="sxs-lookup"><span data-stu-id="5b527-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="5b527-120">在動作定義中，此排序稱為 `runAfter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5b527-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="5b527-121">此屬性是會說明哪些動作和動作狀態會執行此動作的物件。</span><span class="sxs-lookup"><span data-stu-id="5b527-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="5b527-122">根據預設，所有透過邏輯應用程式設計工具新增的動作都會設定為如果上一個步驟 `Succeeded`，則在上一個步驟之後執行 (`runAfter`)。</span><span class="sxs-lookup"><span data-stu-id="5b527-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="5b527-123">不過，您可以自訂此值，以在先前的動作是 `Failed`、`Skipped` 或這兩個值的可能組合時引發動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="5b527-124">如果您想要在特定動作 `Insert_Row` 失敗之後於指定的服務匯流排主題新增項目，您可以使用下列 `runAfter` 組態︰</span><span class="sxs-lookup"><span data-stu-id="5b527-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="5b527-125">請注意，`runAfter` 屬性會設定為在 `Insert_Row` 動作是 `Failed` 時引發。</span><span class="sxs-lookup"><span data-stu-id="5b527-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="5b527-126">若要在動作狀態是 `Succeeded`、`Failed` 或 `Skipped` 時執行動作，請使用此語法︰</span><span class="sxs-lookup"><span data-stu-id="5b527-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="5b527-127">前一個動作失敗之後所執行並順利完成的動作會標示為 `Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="5b527-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="5b527-128">此行為表示如果您成功擷取到工作流程中的所有失敗，該次執行本身會標示為 `Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="5b527-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="5b527-129">用以評估動作的範圍和結果</span><span class="sxs-lookup"><span data-stu-id="5b527-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="5b527-130">和您可以在個別動作之後進行的執行方式類似，您也可以將多個動作群組到某個[範圍](../logic-apps/logic-apps-loops-and-scopes.md)內，其可做為這些動作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="5b527-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="5b527-131">範圍適合用來組織邏輯應用程式動作，以及用來對某一範圍的狀態執行彙總評估。</span><span class="sxs-lookup"><span data-stu-id="5b527-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="5b527-132">範圍本身會在範圍中的所有動作都已完成之後收到狀態。</span><span class="sxs-lookup"><span data-stu-id="5b527-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="5b527-133">範圍狀態會由執行時的相同條件來決定。</span><span class="sxs-lookup"><span data-stu-id="5b527-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="5b527-134">如果執行分支中的最後一個動作是 `Failed` 或 `Aborted`，狀態會是 `Failed`。</span><span class="sxs-lookup"><span data-stu-id="5b527-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="5b527-135">若要針對範圍內發生的任何失敗引發特定動作，您可以搭配標示為 `Failed` 的範圍使用 `runAfter`。</span><span class="sxs-lookup"><span data-stu-id="5b527-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="5b527-136">若範圍內的「任何」動作失敗，在範圍失敗之後執行可讓您建立一項動作以擷取失敗。</span><span class="sxs-lookup"><span data-stu-id="5b527-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="5b527-137">透過結果取得失敗的內容</span><span class="sxs-lookup"><span data-stu-id="5b527-137">Getting the context of failures with results</span></span>

<span data-ttu-id="5b527-138">雖然從範圍擷取失敗很實用，但您可能也想要取得內容以協助您了解實際上有哪些動作失敗，以及所傳回的任何錯誤或狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5b527-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="5b527-139">`@result()` 工作流程函式會提供有關範圍內所有動作結果的內容。</span><span class="sxs-lookup"><span data-stu-id="5b527-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="5b527-140">`@result()` 採用單一參數、範圍名稱，並且會傳回該範圍內產生之所有動作的陣列。</span><span class="sxs-lookup"><span data-stu-id="5b527-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="5b527-141">這些動作物件包含和 `@actions()` 物件相同的屬性，包括動作開始時間、動作結束時間、動作狀態、動作輸入、動作相互關聯識別碼和動作輸出。</span><span class="sxs-lookup"><span data-stu-id="5b527-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="5b527-142">若要傳送在範圍內失敗之任何動作的內容，您可以輕易地配對 `@result()` 函式與 `runAfter`。</span><span class="sxs-lookup"><span data-stu-id="5b527-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="5b527-143">若要對範圍中 `Failed` 的 For each 動作執行動作，篩選失敗動作的結果陣列，您可以配對 `@result()` 與**[篩選陣列](../connectors/connectors-native-query.md)**動作和 **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** 迴圈。</span><span class="sxs-lookup"><span data-stu-id="5b527-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="5b527-144">您可以取得篩選後的結果陣列，並使用 **ForEach** 迴圈對每個失敗執行動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="5b527-145">以下範例 (隨後並有詳細說明) 會傳送 HTTP POST 要求，其中含有任何在範圍 `My_Scope` 內失敗之動作的回應本文。</span><span class="sxs-lookup"><span data-stu-id="5b527-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="5b527-146">以下是說明整個情形的詳細逐步解說︰</span><span class="sxs-lookup"><span data-stu-id="5b527-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="5b527-147">若要取得 `My_Scope` 內所有動作的結果，**篩選陣列**動作會篩選 `@result('My_Scope')`。</span><span class="sxs-lookup"><span data-stu-id="5b527-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="5b527-148">**篩選陣列**的條件是狀態等於 `Failed` 的任何 `@result()` 項目。</span><span class="sxs-lookup"><span data-stu-id="5b527-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="5b527-149">此條件會將具有 `My_Scope` 之所有動作結果的陣列，篩選為只剩失敗動作結果的陣列。</span><span class="sxs-lookup"><span data-stu-id="5b527-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="5b527-150">對**篩選後陣列**的輸出執行 **For Each** 動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="5b527-151">此步驟會對之前篩選的每個失敗動作結果執行動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="5b527-152">如果範圍中的單一動作失敗，`foreach` 中的動作只會執行一次。</span><span class="sxs-lookup"><span data-stu-id="5b527-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="5b527-153">許多失敗動作會對每個失敗造成一個動作。</span><span class="sxs-lookup"><span data-stu-id="5b527-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="5b527-154">在 `foreach` 項目的回應本文上傳送 HTTP POST，或傳送 `@item()['outputs']['body']`。</span><span class="sxs-lookup"><span data-stu-id="5b527-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="5b527-155">`@result()` 項目圖形和 `@actions()` 圖形相同，並可透過相同方式剖析。</span><span class="sxs-lookup"><span data-stu-id="5b527-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="5b527-156">包含兩個具有失敗動作名稱 `@item()['name']` 和失敗執行用戶端追蹤識別碼 `@item()['clientTrackingId']` 的自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="5b527-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="5b527-157">供您參考，以下範例是單一 `@result()` 項目，會顯示前一個範例中剖析的 `name`、`body` 和 `clientTrackingId` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5b527-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="5b527-158">在 `foreach` 之外，`@result()` 會傳回這些物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="5b527-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="5b527-159">若要執行不同的例外狀況處理模式，您可以使用上述運算式。</span><span class="sxs-lookup"><span data-stu-id="5b527-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="5b527-160">您可以選擇在範圍之外執行單一的例外狀況處理動作，以接受整個篩選後的失敗陣列並移除 `foreach`。</span><span class="sxs-lookup"><span data-stu-id="5b527-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="5b527-161">您也可以包含上述 `@result()` 回應中的其他有用屬性。</span><span class="sxs-lookup"><span data-stu-id="5b527-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="5b527-162">Azure 診斷和遙測</span><span class="sxs-lookup"><span data-stu-id="5b527-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="5b527-163">上述模式非常適合處理執行內的錯誤和例外狀況，但您也可以識別和回應與執行本身無關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5b527-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="5b527-164">[Azure 診斷](../logic-apps/logic-apps-monitor-your-logic-apps.md) 提供了簡單的方法讓您將所有工作流程事件 (包括所有執行和動作狀態) 傳送至 Azure 儲存體帳戶或 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="5b527-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="5b527-165">若要評估執行狀態，您可以監視記錄和度量，或將它們發佈至您偏好使用的任何監視工具。</span><span class="sxs-lookup"><span data-stu-id="5b527-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="5b527-166">其中一個可能的選項是透過 Azure 事件中樞將所有事件串流到 [串流分析](https://azure.microsoft.com/services/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="5b527-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="5b527-167">在串流分析中，您可以將診斷記錄中任何異常、平均或失敗的即時查詢取消。</span><span class="sxs-lookup"><span data-stu-id="5b527-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="5b527-168">串流分析可以輕鬆地輸出至其他資料來源，例如佇列、主題、SQL、Azure Cosmos DB 和 Power BI。</span><span class="sxs-lookup"><span data-stu-id="5b527-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b527-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b527-169">Next Steps</span></span>

* [<span data-ttu-id="5b527-170">看看客戶如何使用 Azure Logic Apps 建置錯誤處理</span><span class="sxs-lookup"><span data-stu-id="5b527-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="5b527-171">尋找其他 Logic Apps 範例和案例</span><span class="sxs-lookup"><span data-stu-id="5b527-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="5b527-172">了解如何建立邏輯應用程式的自動化部署</span><span class="sxs-lookup"><span data-stu-id="5b527-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="5b527-173">使用 Visual Studio 建置和部署邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="5b527-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
