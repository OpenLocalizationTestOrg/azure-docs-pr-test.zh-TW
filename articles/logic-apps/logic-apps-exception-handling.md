---
title: "aaaError （& s) 例外狀況處理-Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="0289e-103">處理 Azure Logic Apps 中的錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="0289e-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="0289e-104">Azure 邏輯應用程式提供豐富的工具和模式 toohelp 您確定您的整合是強固且彈性地防止失敗。</span><span class="sxs-lookup"><span data-stu-id="0289e-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="0289e-105">任何整合架構其中 hello 挑戰，可確保確定 tooappropriately 控制代碼的停機時間，或從相依系統問題。</span><span class="sxs-lookup"><span data-stu-id="0289e-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="0289e-106">邏輯應用程式會處理錯誤的第一級的體驗，讓您 hello 需 tooact 上例外狀況和錯誤在工作流程中的工具。</span><span class="sxs-lookup"><span data-stu-id="0289e-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="0289e-107">重試原則</span><span class="sxs-lookup"><span data-stu-id="0289e-107">Retry policies</span></span>

<span data-ttu-id="0289e-108">重試原則是 hello 最基本的例外狀況和錯誤處理的類型。</span><span class="sxs-lookup"><span data-stu-id="0289e-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="0289e-109">如果初始的要求已逾時或失敗 (429 會導致任何要求或 5xx 回應)，此原則會定義 hello 動作是否應該重試。</span><span class="sxs-lookup"><span data-stu-id="0289e-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="0289e-110">根據預設，所有動作會在 20 秒的間隔內另外再試 4 次。</span><span class="sxs-lookup"><span data-stu-id="0289e-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="0289e-111">因此，如果收到 hello 第一個要求`500 Internal Server Error`20 秒的回應，hello 工作流程引擎暫停，並嘗試再次 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="0289e-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="0289e-112">如果所有重試之後, hello 回應仍是例外狀況或失敗，hello 工作流程會繼續和標記 hello 做為動作狀態`Failed`。</span><span class="sxs-lookup"><span data-stu-id="0289e-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="0289e-113">您可以設定的重試原則在 hello**輸入**特定動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="0289e-114">例如，您可以設定重試原則 tootry 4 次最多 1 小時間隔。</span><span class="sxs-lookup"><span data-stu-id="0289e-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="0289e-115">如需輸入屬性的完整詳細資料，請參閱[工作流程動作與觸發程序][retryPolicyMSDN]。</span><span class="sxs-lookup"><span data-stu-id="0289e-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="0289e-116">如果您想要您 HTTP 動作 tooretry 4 次，並等候 10 分鐘後，每個嘗試之間，您可以使用下列定義 hello:</span><span class="sxs-lookup"><span data-stu-id="0289e-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="0289e-117">如需有關支援語法的詳細資訊，請參閱 hello[重試原則工作流程動作和觸發程序 」 一節][retryPolicyMSDN]。</span><span class="sxs-lookup"><span data-stu-id="0289e-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="0289e-118">攔截 hello RunAfter 屬性的失敗</span><span class="sxs-lookup"><span data-stu-id="0289e-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="0289e-119">邏輯應用程式的每個動作宣告 hello 動作啟動，例如工作流程中排序 hello 步驟前必須完成的動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="0289e-120">在 hello 動作定義中，這種排序稱為 hello`runAfter`屬性。</span><span class="sxs-lookup"><span data-stu-id="0289e-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="0289e-121">這個屬性是物件，描述哪些動作和動作狀態執行 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="0289e-122">根據預設，所有的動作，透過 hello 邏輯應用程式的設計工具加入設定太`runAfter`如果 hello hello 上一個步驟前一個步驟`Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="0289e-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="0289e-123">不過，您可以自訂此值 toofire 動作當上一個動作都有`Failed`， `Skipped`，或一組可能的這些值。</span><span class="sxs-lookup"><span data-stu-id="0289e-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="0289e-124">如果您想 tooadd 項目 tooa 指定 Service Bus 主題的特定動作之後`Insert_Row`失敗，您可以使用下列的 hello`runAfter`組態：</span><span class="sxs-lookup"><span data-stu-id="0289e-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="0289e-125">請注意 hello`runAfter`屬性如果 hello 設定 toofire`Insert_Row`動作`Failed`。</span><span class="sxs-lookup"><span data-stu-id="0289e-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="0289e-126">如果 hello 動作狀態是 toorun hello 動作`Succeeded`， `Failed`，或`Skipped`，使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="0289e-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="0289e-127">前一個動作失敗之後所執行並順利完成的動作會標示為 `Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="0289e-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="0289e-128">這意味著如果您已成功在工作流程時，攔截所有失敗 hello 執行本身標示為`Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="0289e-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="0289e-129">範圍和結果 tooevaluate 動作</span><span class="sxs-lookup"><span data-stu-id="0289e-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="0289e-130">您可以在個別的動作之後執行的 toohow 類似，您可以也動作組成群組內[範圍](../logic-apps/logic-apps-loops-and-scopes.md)，其做為動作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="0289e-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="0289e-131">領域都是適合用來組織您的邏輯應用程式的動作，以及用於在領域的 hello 狀態上執行彙總的評估。</span><span class="sxs-lookup"><span data-stu-id="0289e-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="0289e-132">在範圍中的所有動作都完成後，請 hello 範圍本身會接收狀態。</span><span class="sxs-lookup"><span data-stu-id="0289e-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="0289e-133">hello 領域狀態決定以 hello 做為測試回合的相同準則。</span><span class="sxs-lookup"><span data-stu-id="0289e-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="0289e-134">如果執行分支中的 hello 最後一個動作是`Failed`或`Aborted`，hello 狀態是`Failed`。</span><span class="sxs-lookup"><span data-stu-id="0289e-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="0289e-135">toofire hello 範圍內發生任何失敗的特定動作，您可以使用`runAfter`範圍標示為`Failed`。</span><span class="sxs-lookup"><span data-stu-id="0289e-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="0289e-136">如果*任何*hello 範圍中的動作失敗、 執行之後的範圍可讓您建立單一動作 toocatch 失敗。</span><span class="sxs-lookup"><span data-stu-id="0289e-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="0289e-137">取得 hello 內容失敗，將結果</span><span class="sxs-lookup"><span data-stu-id="0289e-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="0289e-138">雖然攔截失敗從範圍非常有用，您可能也想內容 toohelp 您了解確切的動作失敗，任何錯誤或已傳回狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0289e-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="0289e-139">hello`@result()`工作流程函式提供有關 hello 結果的範圍中的所有動作內容。</span><span class="sxs-lookup"><span data-stu-id="0289e-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="0289e-140">`@result()`接受單一參數，領域名稱，並傳回所有 hello 動作會從該範圍內的陣列。</span><span class="sxs-lookup"><span data-stu-id="0289e-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="0289e-141">這些動作物件包含相同屬性，hello hello`@actions()`輸出物件，包括動作的開始時間、 動作的結束時間、 動作狀態、 輸入動作、 動作相互關聯識別碼和動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="0289e-142">toosend 內容中無法在範圍內的任何動作，您可以輕易地配對`@result()`函式與`runAfter`。</span><span class="sxs-lookup"><span data-stu-id="0289e-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="0289e-143">tooexecute 動作*每個*範圍中的動作，`Failed`結果 tooactions 篩選 hello 陣列失敗，您所能配對`@result()`與**[篩選陣列](../connectors/connectors-native-query.md)**動作和 **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** 迴圈。</span><span class="sxs-lookup"><span data-stu-id="0289e-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="0289e-144">您可以使用 hello 篩選的結果的陣列，並使用 hello 每個失敗執行的動作**ForEach**迴圈。</span><span class="sxs-lookup"><span data-stu-id="0289e-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="0289e-145">以下是範例，後面接著 hello 範圍內傳送 HTTP POST 要求與 hello 回應主體失敗的任何動作的詳細說明`My_Scope`。</span><span class="sxs-lookup"><span data-stu-id="0289e-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="0289e-146">以下是會發生什麼情況的詳細逐步解說 toodescribe:</span><span class="sxs-lookup"><span data-stu-id="0289e-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="0289e-147">tooget hello 結果內的所有動作`My_Scope`，hello**篩選陣列**動作篩選條件`@result('My_Scope')`。</span><span class="sxs-lookup"><span data-stu-id="0289e-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="0289e-148">hello 條件**篩選陣列**可以是任何`@result()`也有狀態相等的項目`Failed`。</span><span class="sxs-lookup"><span data-stu-id="0289e-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="0289e-149">這種狀況篩選 hello 陣列的所有動作結果`My_Scope`tooan 陣列只含失敗的動作結果。</span><span class="sxs-lookup"><span data-stu-id="0289e-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="0289e-150">執行**每個**動作 hello**篩選陣列**輸出。</span><span class="sxs-lookup"><span data-stu-id="0289e-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="0289e-151">此步驟會對之前篩選的每個失敗動作結果執行動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="0289e-152">如果在 hello 範圍內的單一動作失敗、 hello hello 中的動作`foreach`只執行一次。</span><span class="sxs-lookup"><span data-stu-id="0289e-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="0289e-153">許多失敗動作會對每個失敗造成一個動作。</span><span class="sxs-lookup"><span data-stu-id="0289e-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="0289e-154">HTTP POST 傳送嗨`foreach`回應主體的項目或`@item()['outputs']['body']`。</span><span class="sxs-lookup"><span data-stu-id="0289e-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="0289e-155">hello`@result()`項目 圖形是 hello 相同為 hello`@actions()`圖形，並可以剖析 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="0289e-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="0289e-156">包含兩個具有 hello 失敗的動作名稱的自訂標頭`@item()['name']`hello 失敗執行的用戶端追蹤 ID `@item()['clientTrackingId']`。</span><span class="sxs-lookup"><span data-stu-id="0289e-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="0289e-157">如需參考，以下是在單一範例`@result()`項目，顯示 hello `name`， `body`，和`clientTrackingId`剖析的 hello 前一個範例中的屬性。</span><span class="sxs-lookup"><span data-stu-id="0289e-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="0289e-158">在 `foreach` 之外，`@result()` 會傳回這些物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="0289e-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="0289e-159">tooperform 不同的例外狀況處理模式，您可以使用先前顯示的 hello 運算式。</span><span class="sxs-lookup"><span data-stu-id="0289e-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="0289e-160">您可能會選擇 tooexecute 單一的例外狀況處理可接受 hello 整個篩選的陣列失敗次數、 hello 範圍外的動作，並移除 hello `foreach`。</span><span class="sxs-lookup"><span data-stu-id="0289e-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="0289e-161">您也可以包含其他有用的屬性，從 hello`@result()`先前所示的回應。</span><span class="sxs-lookup"><span data-stu-id="0289e-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="0289e-162">Azure 診斷和遙測</span><span class="sxs-lookup"><span data-stu-id="0289e-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="0289e-163">hello 先前模式很好的方法 toohandle 錯誤和例外狀況，在執行中，但您也可以識別並回應 tooerrors 執行本身的 hello 與無關。</span><span class="sxs-lookup"><span data-stu-id="0289e-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="0289e-164">[Azure 診斷](../logic-apps/logic-apps-monitor-your-logic-apps.md)提供簡單的方式 toosend，所有的工作流程 （包括所有執行和動作的狀態） 的事件 tooan Azure 儲存體帳戶或 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="0289e-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="0289e-165">tooevaluate 執行狀態，您可以監視 hello 記錄檔和度量，或將它們發佈至任何您偏好的監視工具。</span><span class="sxs-lookup"><span data-stu-id="0289e-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="0289e-166">其中一個可能的選項是 toostream 所有 hello 事件至 Azure 事件中心透過[Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="0289e-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="0289e-167">在 Stream Analytics 中，您可以撰寫任何異常、 平均值或失敗關閉的即時查詢從 hello 診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0289e-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="0289e-168">串流分析可輕鬆地輸出 tooother 資料來源，例如佇列、 主題、 SQL、 Azure Cosmos DB、 和 Power BI。</span><span class="sxs-lookup"><span data-stu-id="0289e-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0289e-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0289e-169">Next Steps</span></span>

* [<span data-ttu-id="0289e-170">看看客戶如何使用 Azure Logic Apps 建置錯誤處理</span><span class="sxs-lookup"><span data-stu-id="0289e-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="0289e-171">尋找其他 Logic Apps 範例和案例</span><span class="sxs-lookup"><span data-stu-id="0289e-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="0289e-172">了解 toocreate 自動化部署邏輯應用程式的方式</span><span class="sxs-lookup"><span data-stu-id="0289e-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="0289e-173">使用 Visual Studio 建置和部署邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0289e-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
