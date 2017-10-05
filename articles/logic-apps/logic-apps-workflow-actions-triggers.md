---
title: "工作流程動作和觸發程序 - Azure Logic Apps | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="2dae5-102">Azure Logic Apps 的工作流程動作和觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="2dae5-103">邏輯應用程式是由觸發程序和動作所組成。</span><span class="sxs-lookup"><span data-stu-id="2dae5-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="2dae5-104">觸發程序有六種類型。</span><span class="sxs-lookup"><span data-stu-id="2dae5-104">There are six types of triggers.</span></span> <span data-ttu-id="2dae5-105">每種類型各有不同的介面和行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="2dae5-106">透過查看[工作流程定義語言](logic-apps-workflow-definition-language.md)的詳細資料，您還可以深入了解其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2dae5-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="2dae5-107">請繼續閱讀以深入了解觸發程序和動作，以及如何使用它們來建置邏輯應用程式，以改善商務程序和工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="2dae5-108">觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-108">Triggers</span></span>  

<span data-ttu-id="2dae5-109">觸發程序會指定可起始邏輯應用程式工作流程執行的呼叫。</span><span class="sxs-lookup"><span data-stu-id="2dae5-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="2dae5-110">以下是兩種可起始工作流程執行的不同方式︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="2dae5-111">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-111">A polling trigger</span></span>  

-   <span data-ttu-id="2dae5-112">推送觸發程序 - 藉由呼叫[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="2dae5-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="2dae5-113">所有觸發程序都包含下列最上層元素︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="2dae5-114">觸發程序類型和其輸入</span><span class="sxs-lookup"><span data-stu-id="2dae5-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="2dae5-115">您可以使用下列類型的觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="2dae5-116">**要求** \- 讓邏輯應用程式成為可供您呼叫的端點</span><span class="sxs-lookup"><span data-stu-id="2dae5-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="2dae5-117">**循環** \- 根據定義的排程來引發</span><span class="sxs-lookup"><span data-stu-id="2dae5-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="2dae5-118">**HTTP** \- 輪詢 HTTP Web 端點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="2dae5-119">HTTP 端點必須符合特定觸發合約 \- 不論是藉由使用 202\-非同步模式或藉由傳回陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="2dae5-120">**ApiConnection** \- 如同 HTTP 觸發程序一般地輪詢，不過，它會利用 [Microsoft 管理的 API](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="2dae5-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="2dae5-121">**HTTPWebhook** \- 如同手動觸發程序一般地開啟端點，不過，它也會對指定的 URL 進行呼叫以便註冊和取消註冊</span><span class="sxs-lookup"><span data-stu-id="2dae5-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="2dae5-122">**ApiConnectionWebhook** \- 藉由利用 Microsoft 管理的 API 以如同 HTTPWebhook 觸發程序的方式運作</span><span class="sxs-lookup"><span data-stu-id="2dae5-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="2dae5-123">每種觸發程序類型都會有一組不同的行為定義**輸入**。</span><span class="sxs-lookup"><span data-stu-id="2dae5-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="2dae5-124">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-124">Request trigger</span></span>  

<span data-ttu-id="2dae5-125">此觸發程序可做為端點，供您透過 HTTP 要求進行呼叫，以叫用邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="2dae5-126">要求觸發程序看起來就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="2dae5-127">此外，還有一個稱為**結構描述**的選擇性屬性：</span><span class="sxs-lookup"><span data-stu-id="2dae5-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="2dae5-128">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-128">Element name</span></span>|<span data-ttu-id="2dae5-129">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-129">Required</span></span>|<span data-ttu-id="2dae5-130">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="2dae5-131">結構描述</span><span class="sxs-lookup"><span data-stu-id="2dae5-131">schema</span></span>|<span data-ttu-id="2dae5-132">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-132">No</span></span>|<span data-ttu-id="2dae5-133">會驗證連入要求的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="2dae5-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="2dae5-134">適用於協助後續工作流程步驟了解要參考哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="2dae5-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="2dae5-135">若要叫用此端點，您必須呼叫 listCallbackUrl API。</span><span class="sxs-lookup"><span data-stu-id="2dae5-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="2dae5-136">請參閱[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)。</span><span class="sxs-lookup"><span data-stu-id="2dae5-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="2dae5-137">循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-137">Recurrence trigger</span></span>  

<span data-ttu-id="2dae5-138">循環觸發程序是會根據定義的排程來執行的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2dae5-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="2dae5-139">這類觸發程序看起來可能就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="2dae5-140">如您所見，這是很簡單的工作流程執行方式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="2dae5-141">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-141">Element name</span></span>|<span data-ttu-id="2dae5-142">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-142">Required</span></span>|<span data-ttu-id="2dae5-143">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="2dae5-144">frequency</span><span class="sxs-lookup"><span data-stu-id="2dae5-144">frequency</span></span>|<span data-ttu-id="2dae5-145">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-145">Yes</span></span>|<span data-ttu-id="2dae5-146">觸發程序的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="2dae5-146">How often the trigger executes.</span></span> <span data-ttu-id="2dae5-147">只能使用下列其中一個可能值︰秒、分鐘、小時、天、週、月或年</span><span class="sxs-lookup"><span data-stu-id="2dae5-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="2dae5-148">interval</span><span class="sxs-lookup"><span data-stu-id="2dae5-148">interval</span></span>|<span data-ttu-id="2dae5-149">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-149">Yes</span></span>|<span data-ttu-id="2dae5-150">給定循環頻率的間隔</span><span class="sxs-lookup"><span data-stu-id="2dae5-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="2dae5-151">startTime</span><span class="sxs-lookup"><span data-stu-id="2dae5-151">startTime</span></span>|<span data-ttu-id="2dae5-152">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-152">No</span></span>|<span data-ttu-id="2dae5-153">如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。</span><span class="sxs-lookup"><span data-stu-id="2dae5-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="2dae5-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="2dae5-154">timeZone</span></span>|<span data-ttu-id="2dae5-155">no</span><span class="sxs-lookup"><span data-stu-id="2dae5-155">no</span></span>|<span data-ttu-id="2dae5-156">如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。</span><span class="sxs-lookup"><span data-stu-id="2dae5-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="2dae5-157">您也可以將觸發程序排程在未來某個時間點開始執行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="2dae5-158">例如，如果您想要在每週一啟動每週報告，則可以藉由建立下列觸發程序將邏輯應用程式排程在每週一啟動︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="2dae5-159">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-159">HTTP trigger</span></span>  

<span data-ttu-id="2dae5-160">HTTP 觸發程序會輪詢指定端點，然後檢查回應以判斷是否應執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="2dae5-161">輸入物件會採用一組建構 HTTP 呼叫時所需的參數︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="2dae5-162">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-162">Element name</span></span>|<span data-ttu-id="2dae5-163">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-163">Required</span></span>|<span data-ttu-id="2dae5-164">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-164">Description</span></span>|<span data-ttu-id="2dae5-165">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="2dae5-166">method</span><span class="sxs-lookup"><span data-stu-id="2dae5-166">method</span></span>|<span data-ttu-id="2dae5-167">yes</span><span class="sxs-lookup"><span data-stu-id="2dae5-167">yes</span></span>|<span data-ttu-id="2dae5-168">可以是下列其中一種 HTTP 方法︰GET、POST、PUT、DELETE、PATCH 或 HEAD</span><span class="sxs-lookup"><span data-stu-id="2dae5-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="2dae5-169">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-169">String</span></span>|  
|<span data-ttu-id="2dae5-170">uri</span><span class="sxs-lookup"><span data-stu-id="2dae5-170">uri</span></span>|<span data-ttu-id="2dae5-171">yes</span><span class="sxs-lookup"><span data-stu-id="2dae5-171">yes</span></span>|<span data-ttu-id="2dae5-172">所呼叫的 http 或 https 端點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="2dae5-173">最大值為 2 KB。</span><span class="sxs-lookup"><span data-stu-id="2dae5-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="2dae5-174">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-174">String</span></span>|  
|<span data-ttu-id="2dae5-175">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-175">queries</span></span>|<span data-ttu-id="2dae5-176">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-176">No</span></span>|<span data-ttu-id="2dae5-177">物件，代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="2dae5-178">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="2dae5-179">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-179">Object</span></span>|  
|<span data-ttu-id="2dae5-180">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-180">headers</span></span>|<span data-ttu-id="2dae5-181">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-181">No</span></span>|<span data-ttu-id="2dae5-182">物件，代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-183">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="2dae5-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="2dae5-184">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-184">Object</span></span>|  
|<span data-ttu-id="2dae5-185">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-185">body</span></span>|<span data-ttu-id="2dae5-186">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-186">No</span></span>|<span data-ttu-id="2dae5-187">物件，代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="2dae5-188">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-188">Object</span></span>|  
|<span data-ttu-id="2dae5-189">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="2dae5-189">retryPolicy</span></span>|<span data-ttu-id="2dae5-190">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-190">No</span></span>|<span data-ttu-id="2dae5-191">物件，可讓您自訂 4xx 或 5xx 錯誤的重試行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="2dae5-192">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-192">Object</span></span>|  
|<span data-ttu-id="2dae5-193">驗證</span><span class="sxs-lookup"><span data-stu-id="2dae5-193">authentication</span></span>|<span data-ttu-id="2dae5-194">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-194">No</span></span>|<span data-ttu-id="2dae5-195">代表應該用來驗證要求的方法。</span><span class="sxs-lookup"><span data-stu-id="2dae5-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="2dae5-196">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。</span><span class="sxs-lookup"><span data-stu-id="2dae5-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="2dae5-197">除了排程器外，還有一個支援的屬性︰`authority`。根據預設，在未指定時這個值會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="2dae5-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="2dae5-198">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-198">Object</span></span>|  
  
<span data-ttu-id="2dae5-199">HTTP 觸發程序要求 HTTP API 必須符合特定模式，才能與邏輯應用程式良好搭配運作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="2dae5-200">它需要下列欄位：</span><span class="sxs-lookup"><span data-stu-id="2dae5-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="2dae5-201">Response</span><span class="sxs-lookup"><span data-stu-id="2dae5-201">Response</span></span>|<span data-ttu-id="2dae5-202">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="2dae5-203">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2dae5-203">Status code</span></span>|<span data-ttu-id="2dae5-204">狀態碼 200 \(確定\) 會導致執行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="2dae5-205">其他任何狀態碼則不會導致執行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="2dae5-206">Retry\-after 標頭</span><span class="sxs-lookup"><span data-stu-id="2dae5-206">Retry\-after header</span></span>|<span data-ttu-id="2dae5-207">邏輯應用程式再次輪詢端點前所需經過的秒數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="2dae5-208">位置標頭</span><span class="sxs-lookup"><span data-stu-id="2dae5-208">Location header</span></span>|<span data-ttu-id="2dae5-209">在下一個輪詢間隔時所要呼叫的 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="2dae5-210">如果未指定，則會使用原本的 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="2dae5-211">以下是不同要求類型所具有之不同行為的一些範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="2dae5-212">Response code</span><span class="sxs-lookup"><span data-stu-id="2dae5-212">Response code</span></span>|<span data-ttu-id="2dae5-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="2dae5-213">Retry\-After</span></span>|<span data-ttu-id="2dae5-214">行為</span><span class="sxs-lookup"><span data-stu-id="2dae5-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="2dae5-215">200</span><span class="sxs-lookup"><span data-stu-id="2dae5-215">200</span></span>|<span data-ttu-id="2dae5-216">無\(\)</span><span class="sxs-lookup"><span data-stu-id="2dae5-216">\(none\)</span></span>|<span data-ttu-id="2dae5-217">非有效觸發程序，必須有 Retry\-After，否則引擎永遠不會輪詢下一個要求。</span><span class="sxs-lookup"><span data-stu-id="2dae5-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="2dae5-218">202</span><span class="sxs-lookup"><span data-stu-id="2dae5-218">202</span></span>|<span data-ttu-id="2dae5-219">60</span><span class="sxs-lookup"><span data-stu-id="2dae5-219">60</span></span>|<span data-ttu-id="2dae5-220">不會觸發工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-220">Do not trigger the workflow.</span></span> <span data-ttu-id="2dae5-221">會在一分鐘內開始下一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="2dae5-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="2dae5-222">200</span><span class="sxs-lookup"><span data-stu-id="2dae5-222">200</span></span>|<span data-ttu-id="2dae5-223">10</span><span class="sxs-lookup"><span data-stu-id="2dae5-223">10</span></span>|<span data-ttu-id="2dae5-224">執行工作流程，並在 10 秒後再次檢查是否有其他內容。</span><span class="sxs-lookup"><span data-stu-id="2dae5-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="2dae5-225">400</span><span class="sxs-lookup"><span data-stu-id="2dae5-225">400</span></span>|<span data-ttu-id="2dae5-226">無\(\)</span><span class="sxs-lookup"><span data-stu-id="2dae5-226">\(none\)</span></span>|<span data-ttu-id="2dae5-227">不正確的要求，不會執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="2dae5-228">如果未定義任何**重試原則**，則會使用預設原則。</span><span class="sxs-lookup"><span data-stu-id="2dae5-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="2dae5-229">在達到重試次數後，觸發程序就會失效。</span><span class="sxs-lookup"><span data-stu-id="2dae5-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="2dae5-230">500</span><span class="sxs-lookup"><span data-stu-id="2dae5-230">500</span></span>|<span data-ttu-id="2dae5-231">無\(\)</span><span class="sxs-lookup"><span data-stu-id="2dae5-231">\(none\)</span></span>|<span data-ttu-id="2dae5-232">伺服器錯誤，不會執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="2dae5-233">如果未定義任何**重試原則**，則會使用預設原則。</span><span class="sxs-lookup"><span data-stu-id="2dae5-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="2dae5-234">在達到重試次數後，觸發程序就會失效。</span><span class="sxs-lookup"><span data-stu-id="2dae5-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="2dae5-235">HTTP 觸發程序的輸出看起來就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="2dae5-236">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-236">Element name</span></span>|<span data-ttu-id="2dae5-237">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-237">Description</span></span>|<span data-ttu-id="2dae5-238">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="2dae5-239">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-239">headers</span></span>|<span data-ttu-id="2dae5-240">http 回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-240">The headers of the http response.</span></span>|<span data-ttu-id="2dae5-241">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-241">Object</span></span>|  
|<span data-ttu-id="2dae5-242">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-242">body</span></span>|<span data-ttu-id="2dae5-243">http 回應的主體。</span><span class="sxs-lookup"><span data-stu-id="2dae5-243">The body of the http response.</span></span>|<span data-ttu-id="2dae5-244">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="2dae5-245">API 連線觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-245">API Connection trigger</span></span>  

<span data-ttu-id="2dae5-246">API 連線觸發程序和 HTTP 觸發程序的相似之處在於其基本功能。</span><span class="sxs-lookup"><span data-stu-id="2dae5-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="2dae5-247">然而，用於識別動作的參數卻不相同。</span><span class="sxs-lookup"><span data-stu-id="2dae5-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="2dae5-248">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="2dae5-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="2dae5-249">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-249">Element name</span></span>|<span data-ttu-id="2dae5-250">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-250">Required</span></span>|<span data-ttu-id="2dae5-251">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-251">Type</span></span>|<span data-ttu-id="2dae5-252">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-253">主機</span><span class="sxs-lookup"><span data-stu-id="2dae5-253">host</span></span>|<span data-ttu-id="2dae5-254">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-254">Yes</span></span>||<span data-ttu-id="2dae5-255">ApiApp 所裝載的閘道和識別碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="2dae5-256">method</span><span class="sxs-lookup"><span data-stu-id="2dae5-256">method</span></span>|<span data-ttu-id="2dae5-257">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-257">Yes</span></span>|<span data-ttu-id="2dae5-258">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-258">String</span></span>|<span data-ttu-id="2dae5-259">可以是下列其中一種 HTTP 方法︰**GET**、**POST**、**PUT**、**DELETE**、**PATCH** 或 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="2dae5-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="2dae5-260">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-260">queries</span></span>|<span data-ttu-id="2dae5-261">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-261">No</span></span>|<span data-ttu-id="2dae5-262">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-262">Object</span></span>|<span data-ttu-id="2dae5-263">代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="2dae5-264">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="2dae5-265">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-265">headers</span></span>|<span data-ttu-id="2dae5-266">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-266">No</span></span>|<span data-ttu-id="2dae5-267">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-267">Object</span></span>|<span data-ttu-id="2dae5-268">代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-269">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="2dae5-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="2dae5-270">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-270">body</span></span>|<span data-ttu-id="2dae5-271">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-271">No</span></span>|<span data-ttu-id="2dae5-272">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-272">Object</span></span>|<span data-ttu-id="2dae5-273">代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="2dae5-274">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="2dae5-274">retryPolicy</span></span>|<span data-ttu-id="2dae5-275">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-275">No</span></span>|<span data-ttu-id="2dae5-276">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-276">Object</span></span>|<span data-ttu-id="2dae5-277">可讓您自訂 4xx 或 5xx 錯誤的重試行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="2dae5-278">驗證</span><span class="sxs-lookup"><span data-stu-id="2dae5-278">authentication</span></span>|<span data-ttu-id="2dae5-279">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-279">No</span></span>|<span data-ttu-id="2dae5-280">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-280">Object</span></span>|<span data-ttu-id="2dae5-281">代表應該用來驗證要求的方法。</span><span class="sxs-lookup"><span data-stu-id="2dae5-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="2dae5-282">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="2dae5-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="2dae5-283">主機的屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="2dae5-284">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-284">Element name</span></span>|<span data-ttu-id="2dae5-285">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-285">Required</span></span>|<span data-ttu-id="2dae5-286">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="2dae5-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="2dae5-287">api runtimeUrl</span></span>|<span data-ttu-id="2dae5-288">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-288">Yes</span></span>|<span data-ttu-id="2dae5-289">Managed API 的端點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="2dae5-290">連線名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-290">connection name</span></span>||<span data-ttu-id="2dae5-291">必須是名為 `$connection` 之參數的參考，並且是工作流程所使用之 Managed API 連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="2dae5-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="2dae5-292">API 連線觸發程序的輸出如下︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="2dae5-293">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-293">Element name</span></span>|<span data-ttu-id="2dae5-294">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-294">Type</span></span>|<span data-ttu-id="2dae5-295">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="2dae5-296">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-296">headers</span></span>|<span data-ttu-id="2dae5-297">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-297">Object</span></span>|<span data-ttu-id="2dae5-298">http 回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="2dae5-299">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-299">body</span></span>|<span data-ttu-id="2dae5-300">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-300">Object</span></span>|<span data-ttu-id="2dae5-301">http 回應的主體。</span><span class="sxs-lookup"><span data-stu-id="2dae5-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="2dae5-302">HTTPWebhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="2dae5-303">HTTPWebhook 觸發程序會如同手動觸發程序一般地開啟端點，不過，HTTPWebhook 觸發程序還會對指定的 URL 進行呼叫以便註冊和取消註冊。</span><span class="sxs-lookup"><span data-stu-id="2dae5-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="2dae5-304">HTTPWebhook 觸發程序看起來可能就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="2dae5-305">這些區段之中有許多是選擇性的，而且 Webhook 的行為取決於提供或省略了哪些區段。</span><span class="sxs-lookup"><span data-stu-id="2dae5-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="2dae5-306">Webhook 的屬性如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="2dae5-307">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-307">Element name</span></span>|<span data-ttu-id="2dae5-308">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-308">Required</span></span>|<span data-ttu-id="2dae5-309">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="2dae5-310">訂閱</span><span class="sxs-lookup"><span data-stu-id="2dae5-310">subscribe</span></span>|<span data-ttu-id="2dae5-311">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-311">No</span></span>|<span data-ttu-id="2dae5-312">在觸發程序建立並執行初始註冊時，所呼叫的連出要求。</span><span class="sxs-lookup"><span data-stu-id="2dae5-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="2dae5-313">取消訂閱</span><span class="sxs-lookup"><span data-stu-id="2dae5-313">unsubscribe</span></span>|<span data-ttu-id="2dae5-314">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-314">No</span></span>|<span data-ttu-id="2dae5-315">刪除觸發程序時的連出要求。</span><span class="sxs-lookup"><span data-stu-id="2dae5-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="2dae5-316">**訂閱**是為了開始接聽事件所產生的連出呼叫。</span><span class="sxs-lookup"><span data-stu-id="2dae5-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="2dae5-317">此呼叫會使用一般 HTTP 動作所使用的同一組參數來啟動。</span><span class="sxs-lookup"><span data-stu-id="2dae5-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="2dae5-318">工作流程在任何時候以任何方式進行變更 (例如，每當認證輪替時)，或觸發程序的輸入參數變更時，就會產生連出呼叫。</span><span class="sxs-lookup"><span data-stu-id="2dae5-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="2dae5-319">為了支援這個呼叫，所以有了一個新函式︰`@listCallbackUrl()`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="2dae5-320">這個函式會針對此工作流程中的這個特定觸發程序傳回唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="2dae5-321">它代表使用服務 REST 之端點的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="2dae5-322">**取消訂閱**受到呼叫的時機是當作業將此觸發程序轉譯為無效時，包括︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="2dae5-323">刪除或停用觸發程序</span><span class="sxs-lookup"><span data-stu-id="2dae5-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="2dae5-324">刪除或停用工作流程</span><span class="sxs-lookup"><span data-stu-id="2dae5-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="2dae5-325">刪除或停用訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2dae5-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="2dae5-326">邏輯應用程式會自動呼叫取消訂閱動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="2dae5-327">此函式的參數和 HTTP 觸發程序的相同。</span><span class="sxs-lookup"><span data-stu-id="2dae5-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="2dae5-328">HTTPWebhook 觸發程序的輸出是連入要求的內容︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="2dae5-329">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-329">Element name</span></span>|<span data-ttu-id="2dae5-330">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-330">Type</span></span>|<span data-ttu-id="2dae5-331">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="2dae5-332">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-332">headers</span></span>|<span data-ttu-id="2dae5-333">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-333">Object</span></span>|<span data-ttu-id="2dae5-334">http 要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="2dae5-335">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-335">body</span></span>|<span data-ttu-id="2dae5-336">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-336">Object</span></span>|<span data-ttu-id="2dae5-337">http 要求的主體。</span><span class="sxs-lookup"><span data-stu-id="2dae5-337">The body of the http request.</span></span>|  

<span data-ttu-id="2dae5-338">對於 Webhook 動作的限制可透過和 [HTTP 非同步限制](#asynchronous-limits)相同的方式來指定。</span><span class="sxs-lookup"><span data-stu-id="2dae5-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="2dae5-339">條件</span><span class="sxs-lookup"><span data-stu-id="2dae5-339">Conditions</span></span>  

<span data-ttu-id="2dae5-340">對於任何觸發程序，您都可以使用一或多個條件來判斷是否應該執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="2dae5-341">例如：</span><span class="sxs-lookup"><span data-stu-id="2dae5-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="2dae5-342">在此案例中，報告只會在工作流程的 `sendReports` 參數設定為 true 時觸發。</span><span class="sxs-lookup"><span data-stu-id="2dae5-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="2dae5-343">最後，條件可能會參考觸發程序的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="2dae5-344">例如，您只能在網站傳回狀態碼 500 時啟動工作流程，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="2dae5-345">若有任何運算式 \(以任何方式\) 參考觸發程序的狀態碼，預設行為 \(只在 200 \(確定\) 時觸發\) 會遭到取代。</span><span class="sxs-lookup"><span data-stu-id="2dae5-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="2dae5-346">例如，如果您想要同時對狀態碼 200 和狀態碼 201 觸發，則需要納入 `@or(equals(triggers().code, 200),equals(triggers().code,201))` 作為條件。</span><span class="sxs-lookup"><span data-stu-id="2dae5-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="2dae5-347">為要求啟動多個執行</span><span class="sxs-lookup"><span data-stu-id="2dae5-347">Start multiple runs for a request</span></span>

<span data-ttu-id="2dae5-348">若要為單一要求啟動多個執行，`splitOn` 會適用於，例如，當您想要輪詢的端點可在輪詢間隔之間具有多個新項目時。</span><span class="sxs-lookup"><span data-stu-id="2dae5-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="2dae5-349">透過 `splitOn`，您可在包含項目陣列 (您想要使用其中各項來啟動觸發程序的執行) 的回應承載內指定屬性。</span><span class="sxs-lookup"><span data-stu-id="2dae5-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="2dae5-350">例如，假設您有一個會傳回下列回應的 API︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="2dae5-351">您的邏輯應用程式只需要資料列內容，因此您可以如下列範例這樣建構觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="2dae5-352">然後，在工作流程定義中，`@triggerBody().name` 會針對第一個執行傳回 `mycoolrow`，並針對第二個執行傳回 `another row`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="2dae5-353">觸發程序的輸出看起來就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="2dae5-354">因此，如果您使用 `SplitOn`，就無法取得陣列 (在此案例中是指 `Status` 欄位) 外部的屬性。</span><span class="sxs-lookup"><span data-stu-id="2dae5-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="2dae5-355">在此範例中，我們使用 `?` 運算子，以便可以在 `Rows` 屬性不存在時避免失敗。</span><span class="sxs-lookup"><span data-stu-id="2dae5-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="2dae5-356">單一執行的執行個體</span><span class="sxs-lookup"><span data-stu-id="2dae5-356">Single run instance</span></span>

<span data-ttu-id="2dae5-357">您可以將擁有循環屬性的觸發程序，設定為只在所有作用中執行皆已完成的情況下引發。</span><span class="sxs-lookup"><span data-stu-id="2dae5-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="2dae5-358">如果在仍有進行中執行時發生了排程的循環，觸發程序將會略過並等待，直到下一個排程的循環間隔時才再次檢查。</span><span class="sxs-lookup"><span data-stu-id="2dae5-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="2dae5-359">您可以透過作業選項進行此設定︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="2dae5-360">類型和輸入</span><span class="sxs-lookup"><span data-stu-id="2dae5-360">Types and inputs</span></span>  

<span data-ttu-id="2dae5-361">動作有許多類型，且各有各的獨特行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="2dae5-362">集合動作可在自身當中包含其他許多動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="2dae5-363">標準動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-363">Standard actions</span></span>  

-   <span data-ttu-id="2dae5-364">**HTTP** 這個動作會呼叫 HTTP Web 端點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="2dae5-365">**ApiConnection** \- 這個動作的行為就像 HTTP 動作，但會使用 Microsoft 管理的 API。</span><span class="sxs-lookup"><span data-stu-id="2dae5-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="2dae5-366">**ApiConnectionWebhook** \- 像 HTTPWebhook，但使用 Microsoft 管理的 API。</span><span class="sxs-lookup"><span data-stu-id="2dae5-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="2dae5-367">**回應** \- 這個動作會定義連入呼叫的回應。</span><span class="sxs-lookup"><span data-stu-id="2dae5-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="2dae5-368">**等候** \- 這個簡單的動作會等候固定時間量或直到某個特定時間。</span><span class="sxs-lookup"><span data-stu-id="2dae5-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="2dae5-369">**工作流程** \- 這個動作代表巢狀工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="2dae5-370">**函式** \- 這個動作代表 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="2dae5-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="2dae5-371">集合動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-371">Collection actions</span></span>

-   <span data-ttu-id="2dae5-372">**範圍** \- 這個動作是其他動作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="2dae5-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="2dae5-373">**條件** \- 這個動作會評估運算式，並執行對應的結果分支。</span><span class="sxs-lookup"><span data-stu-id="2dae5-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="2dae5-374">**ForEach** \- 這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="2dae5-375">**直到** \- 這個迴圈動作會執行內部動作，直到有條件的結果為 true。</span><span class="sxs-lookup"><span data-stu-id="2dae5-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="2dae5-376">每種動作類型都有一組可定義動作行為的不同**輸入**。</span><span class="sxs-lookup"><span data-stu-id="2dae5-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="2dae5-377">HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-377">HTTP action</span></span>  

<span data-ttu-id="2dae5-378">HTTP 動作會呼叫指定端點，然後檢查回應以判斷是否應執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="2dae5-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="2dae5-379">**輸入**物件會採用一組建構 HTTP 呼叫時所需的參數︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="2dae5-380">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-380">Element name</span></span>|<span data-ttu-id="2dae5-381">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-381">Required</span></span>|<span data-ttu-id="2dae5-382">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-382">Type</span></span>|<span data-ttu-id="2dae5-383">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-384">method</span><span class="sxs-lookup"><span data-stu-id="2dae5-384">method</span></span>|<span data-ttu-id="2dae5-385">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-385">Yes</span></span>|<span data-ttu-id="2dae5-386">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-386">String</span></span>|<span data-ttu-id="2dae5-387">可以是下列其中一種 HTTP 方法︰**GET**、**POST**、**PUT**、**DELETE**、**PATCH** 或 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="2dae5-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="2dae5-388">uri</span><span class="sxs-lookup"><span data-stu-id="2dae5-388">uri</span></span>|<span data-ttu-id="2dae5-389">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-389">Yes</span></span>|<span data-ttu-id="2dae5-390">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-390">String</span></span>|<span data-ttu-id="2dae5-391">所呼叫的 http 或 https 端點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="2dae5-392">最大長度為 2 KB。</span><span class="sxs-lookup"><span data-stu-id="2dae5-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="2dae5-393">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-393">queries</span></span>|<span data-ttu-id="2dae5-394">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-394">No</span></span>|<span data-ttu-id="2dae5-395">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-395">Object</span></span>|<span data-ttu-id="2dae5-396">代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="2dae5-397">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="2dae5-398">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-398">headers</span></span>|<span data-ttu-id="2dae5-399">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-399">No</span></span>|<span data-ttu-id="2dae5-400">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-400">Object</span></span>|<span data-ttu-id="2dae5-401">代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-402">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="2dae5-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="2dae5-403">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-403">body</span></span>|<span data-ttu-id="2dae5-404">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-404">No</span></span>|<span data-ttu-id="2dae5-405">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-405">Object</span></span>|<span data-ttu-id="2dae5-406">代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="2dae5-407">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="2dae5-407">retryPolicy</span></span>|<span data-ttu-id="2dae5-408">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-408">No</span></span>|<span data-ttu-id="2dae5-409">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-409">Object</span></span>|<span data-ttu-id="2dae5-410">可讓您自訂 4xx 或 5xx 錯誤的重試行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="2dae5-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="2dae5-411">operationsOptions</span></span>|<span data-ttu-id="2dae5-412">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-412">No</span></span>|<span data-ttu-id="2dae5-413">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-413">String</span></span>|<span data-ttu-id="2dae5-414">定義一組要覆寫的特殊行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="2dae5-415">驗證</span><span class="sxs-lookup"><span data-stu-id="2dae5-415">authentication</span></span>|<span data-ttu-id="2dae5-416">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-416">No</span></span>|<span data-ttu-id="2dae5-417">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-417">Object</span></span>|<span data-ttu-id="2dae5-418">代表應該用來驗證要求的方法。</span><span class="sxs-lookup"><span data-stu-id="2dae5-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="2dae5-419">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。</span><span class="sxs-lookup"><span data-stu-id="2dae5-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="2dae5-420">除了排程器外，還有一個支援的屬性︰`authority`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="2dae5-421">根據預設，在未指定時這會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="2dae5-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="2dae5-422">HTTP 動作 \(和 API 連線\) 動作支援重試原則。</span><span class="sxs-lookup"><span data-stu-id="2dae5-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="2dae5-423">重試原則適用於間歇性失敗，其典型是 HTTP 狀態碼 408、429 與 5xx，以及任何連線例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2dae5-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="2dae5-424">此原則使用所定義的 *retryPolicy* 物件來進行描述，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="2dae5-425">重試間隔是以 ISO 8601 格式來指定。</span><span class="sxs-lookup"><span data-stu-id="2dae5-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="2dae5-426">此間隔的最小值 (也是預設值) 為 20 秒，最大值為 1 小時。</span><span class="sxs-lookup"><span data-stu-id="2dae5-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="2dae5-427">最大重試計數 (也是預設值) 為 4 小時。</span><span class="sxs-lookup"><span data-stu-id="2dae5-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="2dae5-428">如果未指定重試原則定義，則會使用 `fixed` 策略與預設重試計數和間隔值。</span><span class="sxs-lookup"><span data-stu-id="2dae5-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="2dae5-429">若要停用重試原則，請將其類型設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="2dae5-430">例如，下列動作會在有間歇性失敗時重試擷取最新消息兩次，總共會執行三次，每次嘗試之間會延遲 30 秒︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="2dae5-431">非同步模式</span><span class="sxs-lookup"><span data-stu-id="2dae5-431">Asynchronous patterns</span></span>

<span data-ttu-id="2dae5-432">根據預設，所有 HTTP 型動作皆支援標準的非同步作業模式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="2dae5-433">因此，如果遠端伺服器指出已接受處理要求，並產生 202 \(已接受\) 回應，Logic Apps 引擎會持續輪詢回應之 location 標頭中指定的 URL，直到到達終止狀態 \(非\-202 回應\)。</span><span class="sxs-lookup"><span data-stu-id="2dae5-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="2dae5-434">若要停用先前所述的非同步行為，請在動作輸入中設定 `DisableAsyncPattern` 選項。</span><span class="sxs-lookup"><span data-stu-id="2dae5-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="2dae5-435">在此案例中，動作的輸出是根據伺服器所傳來的初始 202 回應。</span><span class="sxs-lookup"><span data-stu-id="2dae5-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="2dae5-436">非同步限制</span><span class="sxs-lookup"><span data-stu-id="2dae5-436">Asynchronous Limits</span></span>

<span data-ttu-id="2dae5-437">非同步模式可限制在其持續時間內，也可以限制在特定時間間隔內。</span><span class="sxs-lookup"><span data-stu-id="2dae5-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="2dae5-438">如果在時間間隔經過後仍未到達終止狀態，動作的狀態會標示為 `Cancelled`，而狀態碼為 `ActionTimedOut`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="2dae5-439">限制逾時是以 ISO 8601 格式來指定。</span><span class="sxs-lookup"><span data-stu-id="2dae5-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="2dae5-440">使用下列語法即可指定限制︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="2dae5-441">API 連線</span><span class="sxs-lookup"><span data-stu-id="2dae5-441">API Connection</span></span>  

<span data-ttu-id="2dae5-442">API 連線是參考 Microsoft 管理之連接器的動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="2dae5-443">這個動作需要有效連線的參考，以及關於所需 API 及參數的資訊。</span><span class="sxs-lookup"><span data-stu-id="2dae5-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="2dae5-444">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-444">Element name</span></span>|<span data-ttu-id="2dae5-445">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-445">Required</span></span>|<span data-ttu-id="2dae5-446">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-446">Type</span></span>|<span data-ttu-id="2dae5-447">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-448">主機</span><span class="sxs-lookup"><span data-stu-id="2dae5-448">host</span></span>|<span data-ttu-id="2dae5-449">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-449">Yes</span></span>|<span data-ttu-id="2dae5-450">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-450">Object</span></span>|<span data-ttu-id="2dae5-451">代表連接器資訊，例如 runtimeUrl 和連線物件的參考</span><span class="sxs-lookup"><span data-stu-id="2dae5-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="2dae5-452">method</span><span class="sxs-lookup"><span data-stu-id="2dae5-452">method</span></span>|<span data-ttu-id="2dae5-453">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-453">Yes</span></span>|<span data-ttu-id="2dae5-454">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-454">String</span></span>|<span data-ttu-id="2dae5-455">可以是下列其中一種 HTTP 方法︰**GET**、**POST**、**PUT**、**DELETE**、**PATCH** 或 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="2dae5-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="2dae5-456">路徑</span><span class="sxs-lookup"><span data-stu-id="2dae5-456">path</span></span>|<span data-ttu-id="2dae5-457">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-457">Yes</span></span>|<span data-ttu-id="2dae5-458">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-458">String</span></span>|<span data-ttu-id="2dae5-459">API 作業的路徑。</span><span class="sxs-lookup"><span data-stu-id="2dae5-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="2dae5-460">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-460">queries</span></span>|<span data-ttu-id="2dae5-461">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-461">No</span></span>|<span data-ttu-id="2dae5-462">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-462">Object</span></span>|<span data-ttu-id="2dae5-463">代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="2dae5-464">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="2dae5-465">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-465">headers</span></span>|<span data-ttu-id="2dae5-466">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-466">No</span></span>|<span data-ttu-id="2dae5-467">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-467">Object</span></span>|<span data-ttu-id="2dae5-468">代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-469">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="2dae5-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="2dae5-470">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-470">body</span></span>|<span data-ttu-id="2dae5-471">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-471">No</span></span>|<span data-ttu-id="2dae5-472">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-472">Object</span></span>|<span data-ttu-id="2dae5-473">代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="2dae5-474">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="2dae5-474">retryPolicy</span></span>|<span data-ttu-id="2dae5-475">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-475">No</span></span>|<span data-ttu-id="2dae5-476">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-476">Object</span></span>|<span data-ttu-id="2dae5-477">可讓您自訂 4xx 或 5xx 錯誤的重試行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="2dae5-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="2dae5-478">operationsOptions</span></span>|<span data-ttu-id="2dae5-479">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-479">No</span></span>|<span data-ttu-id="2dae5-480">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-480">String</span></span>|<span data-ttu-id="2dae5-481">定義一組要覆寫的特殊行為。</span><span class="sxs-lookup"><span data-stu-id="2dae5-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="2dae5-482">API 連線 Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="2dae5-483">對於 Webhook 動作的限制可透過和 [HTTP 非同步限制](#asynchronous-limits)相同的方式來指定。</span><span class="sxs-lookup"><span data-stu-id="2dae5-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="2dae5-484">回應動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-484">Response action</span></span>  

<span data-ttu-id="2dae5-485">這個動作類型包含來自 HTTP 要求的整個回應承載，並納入 statusCode、主體和標頭︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="2dae5-486">回應動作有其他動作所不適用的特殊限制。</span><span class="sxs-lookup"><span data-stu-id="2dae5-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="2dae5-487">具體而言：</span><span class="sxs-lookup"><span data-stu-id="2dae5-487">Specifically:</span></span>  
  
-   <span data-ttu-id="2dae5-488">定義中不能有平行的回應動作，因為連入要求必須有確定性回應。</span><span class="sxs-lookup"><span data-stu-id="2dae5-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="2dae5-489">如果連入要求在收到回應後觸達回應動作，系統會將動作視為失敗 \(衝突\)，因此，執行會是 `Failed`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="2dae5-490">具有回應動作的工作流程在其觸發程序中不能有 `splitOn`，因為一個呼叫就會導致許多個執行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="2dae5-491">因此，當流程是 PUT 且造成不正確的要求時，便應就此進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2dae5-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="2dae5-492">等候動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-492">Wait action</span></span>  

<span data-ttu-id="2dae5-493">`wait` 動作會在一段指定間隔內暫停工作流程的執行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="2dae5-494">例如，若要等候 15 分鐘，您可以使用此程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="2dae5-495">或者，若要等候直到特定時間點，您可以使用此範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="2dae5-496">等候持續時間可使用**間隔**物件或**直到**物件 (但不可同時使用兩者) 來指定。</span><span class="sxs-lookup"><span data-stu-id="2dae5-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="2dae5-497">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-497">Name</span></span>|<span data-ttu-id="2dae5-498">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-498">Required</span></span>|<span data-ttu-id="2dae5-499">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-499">Type</span></span>|<span data-ttu-id="2dae5-500">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-501">interval</span><span class="sxs-lookup"><span data-stu-id="2dae5-501">interval</span></span>|<span data-ttu-id="2dae5-502">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-502">No</span></span>|<span data-ttu-id="2dae5-503">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-503">Object</span></span>|<span data-ttu-id="2dae5-504">以時間量為基礎的等候持續時間。</span><span class="sxs-lookup"><span data-stu-id="2dae5-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="2dae5-505">間隔單位</span><span class="sxs-lookup"><span data-stu-id="2dae5-505">interval unit</span></span>|<span data-ttu-id="2dae5-506">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-506">Yes</span></span>|<span data-ttu-id="2dae5-507">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-507">String</span></span>|<span data-ttu-id="2dae5-508">下列其中一個間隔︰秒、分鐘、小時、天、週、月、年。</span><span class="sxs-lookup"><span data-stu-id="2dae5-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="2dae5-509">間隔計數</span><span class="sxs-lookup"><span data-stu-id="2dae5-509">interval count</span></span>|<span data-ttu-id="2dae5-510">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-510">Yes</span></span>|<span data-ttu-id="2dae5-511">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-511">String</span></span>|<span data-ttu-id="2dae5-512">以指定內部單位為基礎的持續時間。</span><span class="sxs-lookup"><span data-stu-id="2dae5-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="2dae5-513">直到</span><span class="sxs-lookup"><span data-stu-id="2dae5-513">until</span></span>|<span data-ttu-id="2dae5-514">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-514">No</span></span>|<span data-ttu-id="2dae5-515">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-515">Object</span></span>|<span data-ttu-id="2dae5-516">以時間點為基礎的等候持續時間。</span><span class="sxs-lookup"><span data-stu-id="2dae5-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="2dae5-517">直到時間戳記</span><span class="sxs-lookup"><span data-stu-id="2dae5-517">until timestamp</span></span>|<span data-ttu-id="2dae5-518">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-518">Yes</span></span>|<span data-ttu-id="2dae5-519">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-519">String</span></span>|<span data-ttu-id="2dae5-520">字串 | 等候到期時的 UTC 時間點。</span><span class="sxs-lookup"><span data-stu-id="2dae5-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="2dae5-521">查詢動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-521">Query action</span></span>

<span data-ttu-id="2dae5-522">`query` 動作可讓您根據條件來篩選陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="2dae5-523">例如，若要選取大於 2 的數字，您可以使用︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="2dae5-524">`query` 動作的輸出是一個陣列，其中具有輸入陣列中符合條件的元素。</span><span class="sxs-lookup"><span data-stu-id="2dae5-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="2dae5-525">如果沒有任何值符合 `where` 條件，則結果為空白陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="2dae5-526">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-526">Name</span></span>|<span data-ttu-id="2dae5-527">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-527">Required</span></span>|<span data-ttu-id="2dae5-528">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-528">Type</span></span>|<span data-ttu-id="2dae5-529">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="2dae5-530">from</span><span class="sxs-lookup"><span data-stu-id="2dae5-530">from</span></span>|<span data-ttu-id="2dae5-531">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-531">Yes</span></span>|<span data-ttu-id="2dae5-532">陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-532">Array</span></span>|<span data-ttu-id="2dae5-533">來源陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-533">The source array.</span></span>|
|<span data-ttu-id="2dae5-534">其中</span><span class="sxs-lookup"><span data-stu-id="2dae5-534">where</span></span>|<span data-ttu-id="2dae5-535">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-535">Yes</span></span>|<span data-ttu-id="2dae5-536">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-536">String</span></span>|<span data-ttu-id="2dae5-537">要套用到來源陣列各個元素的條件。</span><span class="sxs-lookup"><span data-stu-id="2dae5-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="2dae5-538">選取動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-538">Select action</span></span>

<span data-ttu-id="2dae5-539">`select` 動作可讓您將陣列的每個元素預測為新的值。</span><span class="sxs-lookup"><span data-stu-id="2dae5-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="2dae5-540">例如，若要將數字的陣列轉換為物件的陣列，您可以使用︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="2dae5-541">`select` 動作的輸出是基數為與輸入陣列相同的陣列，其中每個轉換的元素均由 `select` 屬性定義。</span><span class="sxs-lookup"><span data-stu-id="2dae5-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="2dae5-542">如果輸入是空的陣列，則輸出也是空的陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="2dae5-543">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-543">Name</span></span>|<span data-ttu-id="2dae5-544">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-544">Required</span></span>|<span data-ttu-id="2dae5-545">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-545">Type</span></span>|<span data-ttu-id="2dae5-546">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="2dae5-547">from</span><span class="sxs-lookup"><span data-stu-id="2dae5-547">from</span></span>|<span data-ttu-id="2dae5-548">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-548">Yes</span></span>|<span data-ttu-id="2dae5-549">陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-549">Array</span></span>|<span data-ttu-id="2dae5-550">來源陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-550">The source array.</span></span>|
|<span data-ttu-id="2dae5-551">選取</span><span class="sxs-lookup"><span data-stu-id="2dae5-551">select</span></span>|<span data-ttu-id="2dae5-552">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-552">Yes</span></span>|<span data-ttu-id="2dae5-553">任意</span><span class="sxs-lookup"><span data-stu-id="2dae5-553">Any</span></span>|<span data-ttu-id="2dae5-554">要套用到來源陣列各個元素的預測。</span><span class="sxs-lookup"><span data-stu-id="2dae5-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="2dae5-555">終止動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-555">Terminate action</span></span>

<span data-ttu-id="2dae5-556">終止動作會停止執行工作流程、中止任何進行中的動作，並略過任何剩餘的動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="2dae5-557">例如，若要終止狀態為**失敗**的執行，您可以使用下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="2dae5-558">已完成的動作不受終止動作所影響。</span><span class="sxs-lookup"><span data-stu-id="2dae5-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="2dae5-559">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-559">Name</span></span>|<span data-ttu-id="2dae5-560">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-560">Required</span></span>|<span data-ttu-id="2dae5-561">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-561">Type</span></span>|<span data-ttu-id="2dae5-562">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="2dae5-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="2dae5-563">runStatus</span></span>|<span data-ttu-id="2dae5-564">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-564">Yes</span></span>|<span data-ttu-id="2dae5-565">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-565">String</span></span>|<span data-ttu-id="2dae5-566">目標執行狀態。</span><span class="sxs-lookup"><span data-stu-id="2dae5-566">The target run status.</span></span> <span data-ttu-id="2dae5-567">**失敗**或**取消**。</span><span class="sxs-lookup"><span data-stu-id="2dae5-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="2dae5-568">runError</span><span class="sxs-lookup"><span data-stu-id="2dae5-568">runError</span></span>|<span data-ttu-id="2dae5-569">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-569">No</span></span>|<span data-ttu-id="2dae5-570">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-570">Object</span></span>|<span data-ttu-id="2dae5-571">錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2dae5-571">The error details.</span></span> <span data-ttu-id="2dae5-572">在 **runStatus** 設為**失敗**時才支援。</span><span class="sxs-lookup"><span data-stu-id="2dae5-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="2dae5-573">runError 代碼</span><span class="sxs-lookup"><span data-stu-id="2dae5-573">runError code</span></span>|<span data-ttu-id="2dae5-574">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-574">No</span></span>|<span data-ttu-id="2dae5-575">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-575">String</span></span>|<span data-ttu-id="2dae5-576">執行錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-576">The run error code.</span></span>|
|<span data-ttu-id="2dae5-577">runError 訊息</span><span class="sxs-lookup"><span data-stu-id="2dae5-577">runError message</span></span>|<span data-ttu-id="2dae5-578">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-578">No</span></span>|<span data-ttu-id="2dae5-579">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-579">String</span></span>|<span data-ttu-id="2dae5-580">執行錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2dae5-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="2dae5-581">撰寫動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-581">Compose action</span></span>

<span data-ttu-id="2dae5-582">撰寫動作可讓您建構任意物件。</span><span class="sxs-lookup"><span data-stu-id="2dae5-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="2dae5-583">撰寫動作的輸出是其輸入的評估結果。</span><span class="sxs-lookup"><span data-stu-id="2dae5-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="2dae5-584">例如，您可以使用撰寫動作合併多個動作的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="2dae5-585">**撰寫**動作可用來建構任何輸出，包括物件、陣列以及邏輯應用程式原生支援的其他任何類型，例如 XML 和二進位檔。</span><span class="sxs-lookup"><span data-stu-id="2dae5-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="2dae5-586">資料表動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-586">Table action</span></span>

<span data-ttu-id="2dae5-587">`table` 可讓您將項目的陣列轉換為 **CSV** 或 **HTML** 資料表。</span><span class="sxs-lookup"><span data-stu-id="2dae5-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="2dae5-588">假設 @triggerBody() 是</span><span class="sxs-lookup"><span data-stu-id="2dae5-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="2dae5-589">並且讓動作定義為</span><span class="sxs-lookup"><span data-stu-id="2dae5-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="2dae5-590">以上會產生</span><span class="sxs-lookup"><span data-stu-id="2dae5-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="2dae5-591">id</span><span class="sxs-lookup"><span data-stu-id="2dae5-591">id</span></span></th><th><span data-ttu-id="2dae5-592">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="2dae5-593">0</span><span class="sxs-lookup"><span data-stu-id="2dae5-593">0</span></span></td><td><span data-ttu-id="2dae5-594">apples</span><span class="sxs-lookup"><span data-stu-id="2dae5-594">apples</span></span></td></tr><tr><td><span data-ttu-id="2dae5-595">1</span><span class="sxs-lookup"><span data-stu-id="2dae5-595">1</span></span></td><td><span data-ttu-id="2dae5-596">oranges</span><span class="sxs-lookup"><span data-stu-id="2dae5-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="2dae5-597">"</span><span class="sxs-lookup"><span data-stu-id="2dae5-597">"</span></span>

<span data-ttu-id="2dae5-598">為了自訂資料表，您可以明確指定資料行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="2dae5-599">例如：</span><span class="sxs-lookup"><span data-stu-id="2dae5-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="2dae5-600">以上會產生</span><span class="sxs-lookup"><span data-stu-id="2dae5-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="2dae5-601">產生識別碼</span><span class="sxs-lookup"><span data-stu-id="2dae5-601">produce id</span></span></th><th><span data-ttu-id="2dae5-602">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="2dae5-603">0</span><span class="sxs-lookup"><span data-stu-id="2dae5-603">0</span></span></td><td><span data-ttu-id="2dae5-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="2dae5-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="2dae5-605">1</span><span class="sxs-lookup"><span data-stu-id="2dae5-605">1</span></span></td><td><span data-ttu-id="2dae5-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="2dae5-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="2dae5-607">"</span><span class="sxs-lookup"><span data-stu-id="2dae5-607">"</span></span>

<span data-ttu-id="2dae5-608">如果 `from` 屬性值為空的陣列，則輸出為空的資料表。</span><span class="sxs-lookup"><span data-stu-id="2dae5-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="2dae5-609">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-609">Name</span></span>|<span data-ttu-id="2dae5-610">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-610">Required</span></span>|<span data-ttu-id="2dae5-611">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-611">Type</span></span>|<span data-ttu-id="2dae5-612">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="2dae5-613">from</span><span class="sxs-lookup"><span data-stu-id="2dae5-613">from</span></span>|<span data-ttu-id="2dae5-614">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-614">Yes</span></span>|<span data-ttu-id="2dae5-615">陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-615">Array</span></span>|<span data-ttu-id="2dae5-616">來源陣列。</span><span class="sxs-lookup"><span data-stu-id="2dae5-616">The source array.</span></span>|
|<span data-ttu-id="2dae5-617">format</span><span class="sxs-lookup"><span data-stu-id="2dae5-617">format</span></span>|<span data-ttu-id="2dae5-618">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-618">Yes</span></span>|<span data-ttu-id="2dae5-619">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-619">String</span></span>|<span data-ttu-id="2dae5-620">格式，**CSV** 或 **HTML**。</span><span class="sxs-lookup"><span data-stu-id="2dae5-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="2dae5-621">columns</span><span class="sxs-lookup"><span data-stu-id="2dae5-621">columns</span></span>|<span data-ttu-id="2dae5-622">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-622">No</span></span>|<span data-ttu-id="2dae5-623">陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-623">Array</span></span>|<span data-ttu-id="2dae5-624">資料行。</span><span class="sxs-lookup"><span data-stu-id="2dae5-624">The columns.</span></span> <span data-ttu-id="2dae5-625">允許覆寫資料表的預設圖形。</span><span class="sxs-lookup"><span data-stu-id="2dae5-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="2dae5-626">資料行標頭</span><span class="sxs-lookup"><span data-stu-id="2dae5-626">column header</span></span>|<span data-ttu-id="2dae5-627">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-627">No</span></span>|<span data-ttu-id="2dae5-628">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-628">String</span></span>|<span data-ttu-id="2dae5-629">資料行的標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-629">The header of the column.</span></span>|
|<span data-ttu-id="2dae5-630">資料行值</span><span class="sxs-lookup"><span data-stu-id="2dae5-630">column value</span></span>|<span data-ttu-id="2dae5-631">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-631">Yes</span></span>|<span data-ttu-id="2dae5-632">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-632">String</span></span>|<span data-ttu-id="2dae5-633">資料行的值。</span><span class="sxs-lookup"><span data-stu-id="2dae5-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="2dae5-634">工作流程動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-634">Workflow action</span></span>   

|<span data-ttu-id="2dae5-635">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-635">Name</span></span>|<span data-ttu-id="2dae5-636">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-636">Required</span></span>|<span data-ttu-id="2dae5-637">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-637">Type</span></span>|<span data-ttu-id="2dae5-638">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-639">主機識別碼</span><span class="sxs-lookup"><span data-stu-id="2dae5-639">host id</span></span>|<span data-ttu-id="2dae5-640">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-640">Yes</span></span>|<span data-ttu-id="2dae5-641">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-641">String</span></span>|<span data-ttu-id="2dae5-642">您想要呼叫之工作流程的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="2dae5-643">主機 triggerName</span><span class="sxs-lookup"><span data-stu-id="2dae5-643">host triggerName</span></span>|<span data-ttu-id="2dae5-644">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-644">Yes</span></span>|<span data-ttu-id="2dae5-645">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-645">String</span></span>|<span data-ttu-id="2dae5-646">您想要叫用之觸發程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="2dae5-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="2dae5-647">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-647">queries</span></span>|<span data-ttu-id="2dae5-648">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-648">No</span></span>|<span data-ttu-id="2dae5-649">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-649">Object</span></span>|<span data-ttu-id="2dae5-650">代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="2dae5-651">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="2dae5-652">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-652">headers</span></span>|<span data-ttu-id="2dae5-653">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-653">No</span></span>|<span data-ttu-id="2dae5-654">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-654">Object</span></span>|<span data-ttu-id="2dae5-655">代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-656">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="2dae5-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="2dae5-657">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-657">body</span></span>|<span data-ttu-id="2dae5-658">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-658">No</span></span>|<span data-ttu-id="2dae5-659">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-659">Object</span></span>|<span data-ttu-id="2dae5-660">代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="2dae5-661">系統會檢查工作流程 \(更具體地說是觸發程序\) 的存取權，也就是說，您需要工作流程的存取權。</span><span class="sxs-lookup"><span data-stu-id="2dae5-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="2dae5-662">`workflow` 動作的輸出是根據您在子工作流程之 `response` 動作中所做的定義。</span><span class="sxs-lookup"><span data-stu-id="2dae5-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="2dae5-663">如果您尚未定義任何 `response` 動作，輸出會是空的。</span><span class="sxs-lookup"><span data-stu-id="2dae5-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="2dae5-664">函式動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-664">Function action</span></span>   

|<span data-ttu-id="2dae5-665">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-665">Name</span></span>|<span data-ttu-id="2dae5-666">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-666">Required</span></span>|<span data-ttu-id="2dae5-667">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-667">Type</span></span>|<span data-ttu-id="2dae5-668">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-669">函式識別碼</span><span class="sxs-lookup"><span data-stu-id="2dae5-669">function id</span></span>|<span data-ttu-id="2dae5-670">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-670">Yes</span></span>|<span data-ttu-id="2dae5-671">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-671">String</span></span>|<span data-ttu-id="2dae5-672">您想要叫用之函式的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="2dae5-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="2dae5-673">method</span><span class="sxs-lookup"><span data-stu-id="2dae5-673">method</span></span>|<span data-ttu-id="2dae5-674">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-674">No</span></span>|<span data-ttu-id="2dae5-675">String</span><span class="sxs-lookup"><span data-stu-id="2dae5-675">String</span></span>|<span data-ttu-id="2dae5-676">用來叫用函式的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="2dae5-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="2dae5-677">若未指定，則其預設值為 `POST`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="2dae5-678">查詢</span><span class="sxs-lookup"><span data-stu-id="2dae5-678">queries</span></span>|<span data-ttu-id="2dae5-679">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-679">No</span></span>|<span data-ttu-id="2dae5-680">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-680">Object</span></span>|<span data-ttu-id="2dae5-681">代表要新增至 URL 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2dae5-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="2dae5-682">例如，`"queries" : { "api-version": "2015-02-01" }` 會將 `?api-version=2015-02-01` 新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="2dae5-683">headers</span><span class="sxs-lookup"><span data-stu-id="2dae5-683">headers</span></span>|<span data-ttu-id="2dae5-684">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-684">No</span></span>|<span data-ttu-id="2dae5-685">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-685">Object</span></span>|<span data-ttu-id="2dae5-686">代表傳送至要求的每個標頭。</span><span class="sxs-lookup"><span data-stu-id="2dae5-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="2dae5-687">例如，若要對要求設定語言和類型︰`"headers" : { "Accept-Language": "en-us" }`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="2dae5-688">body</span><span class="sxs-lookup"><span data-stu-id="2dae5-688">body</span></span>|<span data-ttu-id="2dae5-689">否</span><span class="sxs-lookup"><span data-stu-id="2dae5-689">No</span></span>|<span data-ttu-id="2dae5-690">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-690">Object</span></span>|<span data-ttu-id="2dae5-691">代表傳送至端點的承載。</span><span class="sxs-lookup"><span data-stu-id="2dae5-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="2dae5-692">當您儲存邏輯應用程式時，我們會對所參考的函式執行某些檢查︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="2dae5-693">您必須具有該函式的存取權。</span><span class="sxs-lookup"><span data-stu-id="2dae5-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="2dae5-694">僅允許使用標準 HTTP 觸發程序或一般 JSON Webhook 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2dae5-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="2dae5-695">它不應定義任何路由。</span><span class="sxs-lookup"><span data-stu-id="2dae5-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="2dae5-696">只允許使用「函式」和「匿名」授權層級。</span><span class="sxs-lookup"><span data-stu-id="2dae5-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="2dae5-697">系統會在執行階段擷取、快取及使用觸發程序 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="2dae5-698">因此，若有任何作業讓快取的 URL 失效，動作就會在執行階段失敗。</span><span class="sxs-lookup"><span data-stu-id="2dae5-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="2dae5-699">若要解決這個問題，請再次儲存邏輯應用程式，這會讓邏輯應用程式再次擷取及快取觸發程序 URL。</span><span class="sxs-lookup"><span data-stu-id="2dae5-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="2dae5-700">集合動作 (範圍和迴圈)</span><span class="sxs-lookup"><span data-stu-id="2dae5-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="2dae5-701">某些動作類型可以在自身當中包含動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="2dae5-702">集合內的參考動作可直接在集合外部參考。</span><span class="sxs-lookup"><span data-stu-id="2dae5-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="2dae5-703">如果您在某個範圍中定義了 `http`，`@body('http')` 仍會在工作流程中的任何位置保持有效。</span><span class="sxs-lookup"><span data-stu-id="2dae5-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="2dae5-704">集合內的動作只能對相同集合內的其他動作執行 `runAfter`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="2dae5-705">範圍動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-705">Scope action</span></span>

<span data-ttu-id="2dae5-706">`scope` 動作可讓您以邏輯方式將工作流程中的動作群組起來。</span><span class="sxs-lookup"><span data-stu-id="2dae5-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="2dae5-707">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-707">Name</span></span>|<span data-ttu-id="2dae5-708">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-708">Required</span></span>|<span data-ttu-id="2dae5-709">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-709">Type</span></span>|<span data-ttu-id="2dae5-710">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-711">動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-711">actions</span></span>|<span data-ttu-id="2dae5-712">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-712">Yes</span></span>|<span data-ttu-id="2dae5-713">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-713">Object</span></span>|<span data-ttu-id="2dae5-714">要在範圍內執行的內部動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-714">Inner actions to execute within the scope</span></span>|

```json
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

## <a name="foreach-action"></a><span data-ttu-id="2dae5-715">ForEach 動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-715">ForEach action</span></span>

<span data-ttu-id="2dae5-716">這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="2dae5-717">根據預設，foreach 迴圈會以平行方式執行 (一次 20 個平行執行)。</span><span class="sxs-lookup"><span data-stu-id="2dae5-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="2dae5-718">您可以使用 `operationOptions` 參數設定執行規則。</span><span class="sxs-lookup"><span data-stu-id="2dae5-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="2dae5-719">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-719">Name</span></span>|<span data-ttu-id="2dae5-720">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-720">Required</span></span>|<span data-ttu-id="2dae5-721">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-721">Type</span></span>|<span data-ttu-id="2dae5-722">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-723">動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-723">actions</span></span>|<span data-ttu-id="2dae5-724">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-724">Yes</span></span>|<span data-ttu-id="2dae5-725">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-725">Object</span></span>|<span data-ttu-id="2dae5-726">要在迴圈內執行的內部動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="2dae5-727">foreach</span><span class="sxs-lookup"><span data-stu-id="2dae5-727">foreach</span></span>|<span data-ttu-id="2dae5-728">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-728">Yes</span></span>|<span data-ttu-id="2dae5-729">字串</span><span class="sxs-lookup"><span data-stu-id="2dae5-729">string</span></span>|<span data-ttu-id="2dae5-730">要逐一查看的陣列</span><span class="sxs-lookup"><span data-stu-id="2dae5-730">The array to iterate over</span></span>|
|<span data-ttu-id="2dae5-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="2dae5-731">operationOptions</span></span>|<span data-ttu-id="2dae5-732">no</span><span class="sxs-lookup"><span data-stu-id="2dae5-732">no</span></span>|<span data-ttu-id="2dae5-733">string</span><span class="sxs-lookup"><span data-stu-id="2dae5-733">string</span></span>|<span data-ttu-id="2dae5-734">行為的任何作業選項。</span><span class="sxs-lookup"><span data-stu-id="2dae5-734">Any operation options for behavior.</span></span> <span data-ttu-id="2dae5-735">目前僅支援 `sequential` 來循序執行反覆運算 (預設行為是平行)</span><span class="sxs-lookup"><span data-stu-id="2dae5-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
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
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="2dae5-736">直到動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-736">Until action</span></span>

<span data-ttu-id="2dae5-737">這個迴圈動作會執行內部動作，直到有條件的結果為 true。</span><span class="sxs-lookup"><span data-stu-id="2dae5-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="2dae5-738">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-738">Name</span></span>|<span data-ttu-id="2dae5-739">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-739">Required</span></span>|<span data-ttu-id="2dae5-740">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-740">Type</span></span>|<span data-ttu-id="2dae5-741">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-742">動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-742">actions</span></span>|<span data-ttu-id="2dae5-743">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-743">Yes</span></span>|<span data-ttu-id="2dae5-744">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-744">Object</span></span>|<span data-ttu-id="2dae5-745">要在迴圈內執行的內部動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="2dae5-746">expression</span><span class="sxs-lookup"><span data-stu-id="2dae5-746">expression</span></span>|<span data-ttu-id="2dae5-747">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-747">Yes</span></span>|<span data-ttu-id="2dae5-748">string</span><span class="sxs-lookup"><span data-stu-id="2dae5-748">string</span></span>|<span data-ttu-id="2dae5-749">要在每次反覆運算之後評估的運算式</span><span class="sxs-lookup"><span data-stu-id="2dae5-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="2dae5-750">limit</span><span class="sxs-lookup"><span data-stu-id="2dae5-750">limit</span></span>|<span data-ttu-id="2dae5-751">yes</span><span class="sxs-lookup"><span data-stu-id="2dae5-751">yes</span></span>|<span data-ttu-id="2dae5-752">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-752">Object</span></span>|<span data-ttu-id="2dae5-753">迴圈的限制 - 必須定義至少一項限制</span><span class="sxs-lookup"><span data-stu-id="2dae5-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="2dae5-754">計數</span><span class="sxs-lookup"><span data-stu-id="2dae5-754">count</span></span>|<span data-ttu-id="2dae5-755">no</span><span class="sxs-lookup"><span data-stu-id="2dae5-755">no</span></span>|<span data-ttu-id="2dae5-756">int</span><span class="sxs-lookup"><span data-stu-id="2dae5-756">int</span></span>|<span data-ttu-id="2dae5-757">可執行之反覆運算次數的限制</span><span class="sxs-lookup"><span data-stu-id="2dae5-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="2dae5-758">timeout</span><span class="sxs-lookup"><span data-stu-id="2dae5-758">timeout</span></span>|<span data-ttu-id="2dae5-759">no</span><span class="sxs-lookup"><span data-stu-id="2dae5-759">no</span></span>|<span data-ttu-id="2dae5-760">字串</span><span class="sxs-lookup"><span data-stu-id="2dae5-760">string</span></span>|<span data-ttu-id="2dae5-761">此動作應執行迴圈多久的逾時值。</span><span class="sxs-lookup"><span data-stu-id="2dae5-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="2dae5-762">ISO 8601 格式</span><span class="sxs-lookup"><span data-stu-id="2dae5-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="2dae5-763">條件 - If 動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-763">Conditions - If Action</span></span>

<span data-ttu-id="2dae5-764">`If` 動作可讓您評估條件，並根據運算式是否評估為 `true` 來執行分支。</span><span class="sxs-lookup"><span data-stu-id="2dae5-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="2dae5-765">名稱</span><span class="sxs-lookup"><span data-stu-id="2dae5-765">Name</span></span>|<span data-ttu-id="2dae5-766">必要</span><span class="sxs-lookup"><span data-stu-id="2dae5-766">Required</span></span>|<span data-ttu-id="2dae5-767">類型</span><span class="sxs-lookup"><span data-stu-id="2dae5-767">Type</span></span>|<span data-ttu-id="2dae5-768">說明</span><span class="sxs-lookup"><span data-stu-id="2dae5-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="2dae5-769">動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-769">actions</span></span>|<span data-ttu-id="2dae5-770">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-770">Yes</span></span>|<span data-ttu-id="2dae5-771">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-771">Object</span></span>|<span data-ttu-id="2dae5-772">運算式評估為 `true` 時要執行的內部動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="2dae5-773">expression</span><span class="sxs-lookup"><span data-stu-id="2dae5-773">expression</span></span>|<span data-ttu-id="2dae5-774">是</span><span class="sxs-lookup"><span data-stu-id="2dae5-774">Yes</span></span>|<span data-ttu-id="2dae5-775">字串</span><span class="sxs-lookup"><span data-stu-id="2dae5-775">string</span></span>|<span data-ttu-id="2dae5-776">要評估的運算式</span><span class="sxs-lookup"><span data-stu-id="2dae5-776">The expression to evaluate</span></span>|
|<span data-ttu-id="2dae5-777">else</span><span class="sxs-lookup"><span data-stu-id="2dae5-777">else</span></span>|<span data-ttu-id="2dae5-778">no</span><span class="sxs-lookup"><span data-stu-id="2dae5-778">no</span></span>|<span data-ttu-id="2dae5-779">Object</span><span class="sxs-lookup"><span data-stu-id="2dae5-779">Object</span></span>|<span data-ttu-id="2dae5-780">運算式評估為 `false` 時要執行的內部動作</span><span class="sxs-lookup"><span data-stu-id="2dae5-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="2dae5-781">下表說明條件如何在動作中使用運算式的範例︰</span><span class="sxs-lookup"><span data-stu-id="2dae5-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="2dae5-782">JSON 值</span><span class="sxs-lookup"><span data-stu-id="2dae5-782">JSON value</span></span>|<span data-ttu-id="2dae5-783">結果</span><span class="sxs-lookup"><span data-stu-id="2dae5-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="2dae5-784">會評估為 true 的任何值都會導致此條件成立。</span><span class="sxs-lookup"><span data-stu-id="2dae5-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="2dae5-785">僅支援布林運算式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="2dae5-786">若要將其他類型轉換成布林值，請使用函式 `empty`、`equals`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="2dae5-787">支援比較函式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-787">Comparison functions are supported.</span></span> <span data-ttu-id="2dae5-788">對於這裡的範例，只有當 act1 的輸出大於閾值時，才會執行動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="2dae5-789">邏輯函式也支援建立巢狀布林運算式。</span><span class="sxs-lookup"><span data-stu-id="2dae5-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="2dae5-790">在此案例中，當 act1 的輸出高於閾值或低於 100 時，便會執行動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="2dae5-791">您可以使用陣列函式來檢查陣列是否有任何項目。</span><span class="sxs-lookup"><span data-stu-id="2dae5-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="2dae5-792">在此案例中，當錯誤陣列空白時，便會執行動作。</span><span class="sxs-lookup"><span data-stu-id="2dae5-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="2dae5-793">錯誤 - 不是有效條件，因為條件必須有 @。</span><span class="sxs-lookup"><span data-stu-id="2dae5-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="2dae5-794">如果條件評估成功，條件會標示為 `Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="2dae5-795">`actions` 或 `else` 物件內的動作在執行並成功後會評估為 `Succeeded`，執行但失敗後會評估為 `Failed`，當該分支未執行時會評估為 `Skipped`。</span><span class="sxs-lookup"><span data-stu-id="2dae5-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dae5-796">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dae5-796">Next steps</span></span>

[<span data-ttu-id="2dae5-797">工作流程服務 REST API</span><span class="sxs-lookup"><span data-stu-id="2dae5-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
