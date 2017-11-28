---
title: "aaaWorkflow 動作和觸發程序-Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="af0c2-102">Azure Logic Apps 的工作流程動作和觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="af0c2-103">邏輯應用程式是由觸發程序和動作所組成。</span><span class="sxs-lookup"><span data-stu-id="af0c2-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="af0c2-104">觸發程序有六種類型。</span><span class="sxs-lookup"><span data-stu-id="af0c2-104">There are six types of triggers.</span></span> <span data-ttu-id="af0c2-105">每種類型各有不同的介面和行為。</span><span class="sxs-lookup"><span data-stu-id="af0c2-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="af0c2-106">您也可以了解其他詳細資料藉由查看 hello 詳細資料的 hello[工作流程定義語言](logic-apps-workflow-definition-language.md)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="af0c2-107">深入了解觸發程序和動作和您如何使用它們 toobuild 邏輯應用程式 tooimprove toolearn 上讀取，您的商務程序和工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="af0c2-108">觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-108">Triggers</span></span>  

<span data-ttu-id="af0c2-109">觸發程序指定 hello 呼叫可以起始邏輯應用程式工作流程的執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="af0c2-110">以下是 hello 兩種不同方式 tooinitiate 執行的工作流程：</span><span class="sxs-lookup"><span data-stu-id="af0c2-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="af0c2-111">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-111">A polling trigger</span></span>  

-   <span data-ttu-id="af0c2-112">推入觸發程序的呼叫 hello[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="af0c2-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="af0c2-113">所有觸發程序都包含下列最上層元素︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="af0c2-114">觸發程序類型和其輸入</span><span class="sxs-lookup"><span data-stu-id="af0c2-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="af0c2-115">您可以使用下列類型的觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="af0c2-116">**要求**\-您 toocall 的端點可讓 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="af0c2-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="af0c2-117">**循環** \- 根據定義的排程來引發</span><span class="sxs-lookup"><span data-stu-id="af0c2-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="af0c2-118">**HTTP** \- 輪詢 HTTP Web 端點。</span><span class="sxs-lookup"><span data-stu-id="af0c2-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="af0c2-119">hello HTTP 結束點必須符合 tooa 特定觸發合約\-使用 202\-非同步模式，或藉由傳回陣列</span><span class="sxs-lookup"><span data-stu-id="af0c2-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="af0c2-120">**ApiConnection** \-像 hello HTTP 輪詢觸發，不過，它會利用 hello [Microsoft 管理 Api](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="af0c2-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="af0c2-121">**HTTPWebhook** \-會開啟一個端點，類似 toohello 手動觸發程序，不過，它也會呼叫 tooa 出指定 URL tooregister 和取消註冊</span><span class="sxs-lookup"><span data-stu-id="af0c2-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="af0c2-122">**ApiConnectionWebhook** \-運作一樣 hello HTTPWebhook 觸發程序，利用 hello Microsoft 管理 Api</span><span class="sxs-lookup"><span data-stu-id="af0c2-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="af0c2-123">每種觸發程序類型都會有一組不同的行為定義**輸入**。</span><span class="sxs-lookup"><span data-stu-id="af0c2-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="af0c2-124">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-124">Request trigger</span></span>  

<span data-ttu-id="af0c2-125">這個觸發程序做為端點，透過 HTTP 要求 tooinvoke 呼叫應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="af0c2-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="af0c2-126">要求觸發程序看起來就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="af0c2-127">此外，還有一個稱為**結構描述**的選擇性屬性：</span><span class="sxs-lookup"><span data-stu-id="af0c2-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="af0c2-128">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-128">Element name</span></span>|<span data-ttu-id="af0c2-129">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-129">Required</span></span>|<span data-ttu-id="af0c2-130">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="af0c2-131">結構描述</span><span class="sxs-lookup"><span data-stu-id="af0c2-131">schema</span></span>|<span data-ttu-id="af0c2-132">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-132">No</span></span>|<span data-ttu-id="af0c2-133">JSON 結構描述驗證 hello 連入要求。</span><span class="sxs-lookup"><span data-stu-id="af0c2-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="af0c2-134">很有用，可幫助知道哪些屬性 tooreference 後續的工作流程步驟。</span><span class="sxs-lookup"><span data-stu-id="af0c2-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="af0c2-135">tooinvoke 此端點，您需要 toocall hello *listCallbackUrl*應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="af0c2-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="af0c2-136">請參閱[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="af0c2-137">循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-137">Recurrence trigger</span></span>  

<span data-ttu-id="af0c2-138">循環觸發程序是會根據定義的排程來執行的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="af0c2-139">這類觸發程序看起來可能就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="af0c2-140">如您所見，它是簡單的方式 toorun 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="af0c2-141">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-141">Element name</span></span>|<span data-ttu-id="af0c2-142">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-142">Required</span></span>|<span data-ttu-id="af0c2-143">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="af0c2-144">frequency</span><span class="sxs-lookup"><span data-stu-id="af0c2-144">frequency</span></span>|<span data-ttu-id="af0c2-145">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-145">Yes</span></span>|<span data-ttu-id="af0c2-146">頻率 hello 執行觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-146">How often hello trigger executes.</span></span> <span data-ttu-id="af0c2-147">只能使用下列其中一個可能值︰秒、分鐘、小時、天、週、月或年</span><span class="sxs-lookup"><span data-stu-id="af0c2-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="af0c2-148">interval</span><span class="sxs-lookup"><span data-stu-id="af0c2-148">interval</span></span>|<span data-ttu-id="af0c2-149">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-149">Yes</span></span>|<span data-ttu-id="af0c2-150">Hello 給 hello 循環頻率間隔</span><span class="sxs-lookup"><span data-stu-id="af0c2-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="af0c2-151">startTime</span><span class="sxs-lookup"><span data-stu-id="af0c2-151">startTime</span></span>|<span data-ttu-id="af0c2-152">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-152">No</span></span>|<span data-ttu-id="af0c2-153">如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。</span><span class="sxs-lookup"><span data-stu-id="af0c2-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="af0c2-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="af0c2-154">timeZone</span></span>|<span data-ttu-id="af0c2-155">no</span><span class="sxs-lookup"><span data-stu-id="af0c2-155">no</span></span>|<span data-ttu-id="af0c2-156">如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。</span><span class="sxs-lookup"><span data-stu-id="af0c2-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="af0c2-157">您也可以排定觸發程序 toostart 執行在 hello 未來在某個時間點。</span><span class="sxs-lookup"><span data-stu-id="af0c2-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="af0c2-158">例如，如果您想要每週會報告每週的星期一 toostart 您可以排定 hello 邏輯應用程式 toostart 每星期一藉由建立 hello 下列觸發程序：</span><span class="sxs-lookup"><span data-stu-id="af0c2-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="af0c2-159">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-159">HTTP trigger</span></span>  

<span data-ttu-id="af0c2-160">HTTP 觸發程序輪詢指定的端點，並檢查 hello 回應 toodetermine，是否應該要執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="af0c2-161">hello 輸入物件會使用參數需要 tooconstruct HTTP 呼叫 hello 組：</span><span class="sxs-lookup"><span data-stu-id="af0c2-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="af0c2-162">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-162">Element name</span></span>|<span data-ttu-id="af0c2-163">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-163">Required</span></span>|<span data-ttu-id="af0c2-164">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-164">Description</span></span>|<span data-ttu-id="af0c2-165">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="af0c2-166">method</span><span class="sxs-lookup"><span data-stu-id="af0c2-166">method</span></span>|<span data-ttu-id="af0c2-167">yes</span><span class="sxs-lookup"><span data-stu-id="af0c2-167">yes</span></span>|<span data-ttu-id="af0c2-168">可以是其中一個 hello 遵循 HTTP 方法： GET、 POST、 PUT、 DELETE、 修補程式或標頭</span><span class="sxs-lookup"><span data-stu-id="af0c2-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="af0c2-169">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-169">String</span></span>|  
|<span data-ttu-id="af0c2-170">uri</span><span class="sxs-lookup"><span data-stu-id="af0c2-170">uri</span></span>|<span data-ttu-id="af0c2-171">yes</span><span class="sxs-lookup"><span data-stu-id="af0c2-171">yes</span></span>|<span data-ttu-id="af0c2-172">hello http 或 https 端點時所呼叫。</span><span class="sxs-lookup"><span data-stu-id="af0c2-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="af0c2-173">最大值為 2 KB。</span><span class="sxs-lookup"><span data-stu-id="af0c2-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="af0c2-174">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-174">String</span></span>|  
|<span data-ttu-id="af0c2-175">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-175">queries</span></span>|<span data-ttu-id="af0c2-176">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-176">No</span></span>|<span data-ttu-id="af0c2-177">物件，代表 hello 查詢參數 tooadd toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="af0c2-178">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="af0c2-179">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-179">Object</span></span>|  
|<span data-ttu-id="af0c2-180">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-180">headers</span></span>|<span data-ttu-id="af0c2-181">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-181">No</span></span>|<span data-ttu-id="af0c2-182">物件，表示每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-183">例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="af0c2-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="af0c2-184">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-184">Object</span></span>|  
|<span data-ttu-id="af0c2-185">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-185">body</span></span>|<span data-ttu-id="af0c2-186">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-186">No</span></span>|<span data-ttu-id="af0c2-187">物件，表示傳送 toohello 端點的 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="af0c2-188">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-188">Object</span></span>|  
|<span data-ttu-id="af0c2-189">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="af0c2-189">retryPolicy</span></span>|<span data-ttu-id="af0c2-190">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-190">No</span></span>|<span data-ttu-id="af0c2-191">物件，可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。</span><span class="sxs-lookup"><span data-stu-id="af0c2-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="af0c2-192">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-192">Object</span></span>|  
|<span data-ttu-id="af0c2-193">驗證</span><span class="sxs-lookup"><span data-stu-id="af0c2-193">authentication</span></span>|<span data-ttu-id="af0c2-194">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-194">No</span></span>|<span data-ttu-id="af0c2-195">代表 hello 要求的 hello 方法應該進行驗證。</span><span class="sxs-lookup"><span data-stu-id="af0c2-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="af0c2-196">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="af0c2-197">除了排程器外，還有一個支援的屬性︰`authority`。根據預設，在未指定時這個值會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="af0c2-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="af0c2-198">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-198">Object</span></span>|  
  
<span data-ttu-id="af0c2-199">hello HTTP 觸發程序需要使用與邏輯應用程式特定的模式 toowork hello HTTP API tooconform。</span><span class="sxs-lookup"><span data-stu-id="af0c2-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="af0c2-200">它需要 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="af0c2-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="af0c2-201">Response</span><span class="sxs-lookup"><span data-stu-id="af0c2-201">Response</span></span>|<span data-ttu-id="af0c2-202">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="af0c2-203">狀態碼</span><span class="sxs-lookup"><span data-stu-id="af0c2-203">Status code</span></span>|<span data-ttu-id="af0c2-204">狀態碼 200\(確定\)toocause 執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="af0c2-205">其他任何狀態碼則不會導致執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="af0c2-206">Retry\-after 標頭</span><span class="sxs-lookup"><span data-stu-id="af0c2-206">Retry\-after header</span></span>|<span data-ttu-id="af0c2-207">Hello 邏輯應用程式會再次輪詢 hello 端點之前的秒數。</span><span class="sxs-lookup"><span data-stu-id="af0c2-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="af0c2-208">位置標頭</span><span class="sxs-lookup"><span data-stu-id="af0c2-208">Location header</span></span>|<span data-ttu-id="af0c2-209">hello URL toocall hello 下一次輪詢間隔。</span><span class="sxs-lookup"><span data-stu-id="af0c2-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="af0c2-210">如果未指定，會使用 hello 原始 URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="af0c2-211">以下是不同要求類型所具有之不同行為的一些範例︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="af0c2-212">Response code</span><span class="sxs-lookup"><span data-stu-id="af0c2-212">Response code</span></span>|<span data-ttu-id="af0c2-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="af0c2-213">Retry\-After</span></span>|<span data-ttu-id="af0c2-214">行為</span><span class="sxs-lookup"><span data-stu-id="af0c2-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="af0c2-215">200</span><span class="sxs-lookup"><span data-stu-id="af0c2-215">200</span></span>|<span data-ttu-id="af0c2-216">無\(\)</span><span class="sxs-lookup"><span data-stu-id="af0c2-216">\(none\)</span></span>|<span data-ttu-id="af0c2-217">不是有效觸發，重試\-之後輪詢 hello 下一個要求永遠不會是必要項目，或其他 hello 引擎。</span><span class="sxs-lookup"><span data-stu-id="af0c2-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="af0c2-218">202</span><span class="sxs-lookup"><span data-stu-id="af0c2-218">202</span></span>|<span data-ttu-id="af0c2-219">60</span><span class="sxs-lookup"><span data-stu-id="af0c2-219">60</span></span>|<span data-ttu-id="af0c2-220">不會觸發 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="af0c2-221">hello 下一次嘗試就會發生在一分鐘內。</span><span class="sxs-lookup"><span data-stu-id="af0c2-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="af0c2-222">200</span><span class="sxs-lookup"><span data-stu-id="af0c2-222">200</span></span>|<span data-ttu-id="af0c2-223">10</span><span class="sxs-lookup"><span data-stu-id="af0c2-223">10</span></span>|<span data-ttu-id="af0c2-224">執行 hello 流程時，並在 10 秒後再次檢查詳細內容。</span><span class="sxs-lookup"><span data-stu-id="af0c2-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="af0c2-225">400</span><span class="sxs-lookup"><span data-stu-id="af0c2-225">400</span></span>|<span data-ttu-id="af0c2-226">無\(\)</span><span class="sxs-lookup"><span data-stu-id="af0c2-226">\(none\)</span></span>|<span data-ttu-id="af0c2-227">不正確的要求，不會執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="af0c2-228">如果沒有任何**重試原則**定義，則會使用 hello 預設原則。</span><span class="sxs-lookup"><span data-stu-id="af0c2-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="af0c2-229">已達到重試的 hello 次數之後，hello 觸發程序都不再有效。</span><span class="sxs-lookup"><span data-stu-id="af0c2-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="af0c2-230">500</span><span class="sxs-lookup"><span data-stu-id="af0c2-230">500</span></span>|<span data-ttu-id="af0c2-231">無\(\)</span><span class="sxs-lookup"><span data-stu-id="af0c2-231">\(none\)</span></span>|<span data-ttu-id="af0c2-232">伺服器錯誤時，不會執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="af0c2-233">如果沒有任何**重試原則**定義，則會使用 hello 預設原則。</span><span class="sxs-lookup"><span data-stu-id="af0c2-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="af0c2-234">已達到重試的 hello 次數之後，hello 觸發程序都不再有效。</span><span class="sxs-lookup"><span data-stu-id="af0c2-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="af0c2-235">hello HTTP 觸發程序的輸出類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="af0c2-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="af0c2-236">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-236">Element name</span></span>|<span data-ttu-id="af0c2-237">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-237">Description</span></span>|<span data-ttu-id="af0c2-238">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="af0c2-239">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-239">headers</span></span>|<span data-ttu-id="af0c2-240">hello http 回應的 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-240">hello headers of hello http response.</span></span>|<span data-ttu-id="af0c2-241">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-241">Object</span></span>|  
|<span data-ttu-id="af0c2-242">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-242">body</span></span>|<span data-ttu-id="af0c2-243">hello hello http 回應主體。</span><span class="sxs-lookup"><span data-stu-id="af0c2-243">hello body of hello http response.</span></span>|<span data-ttu-id="af0c2-244">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="af0c2-245">API 連線觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-245">API Connection trigger</span></span>  

<span data-ttu-id="af0c2-246">hello API 連線觸發程序是在其基本功能類似 toohello 的 HTTP 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="af0c2-247">不過，hello 參數識別 hello 動作是不同的。</span><span class="sxs-lookup"><span data-stu-id="af0c2-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="af0c2-248">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="af0c2-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="af0c2-249">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-249">Element name</span></span>|<span data-ttu-id="af0c2-250">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-250">Required</span></span>|<span data-ttu-id="af0c2-251">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-251">Type</span></span>|<span data-ttu-id="af0c2-252">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-253">主機</span><span class="sxs-lookup"><span data-stu-id="af0c2-253">host</span></span>|<span data-ttu-id="af0c2-254">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-254">Yes</span></span>||<span data-ttu-id="af0c2-255">hello ApiApp 裝載閘道和識別碼。</span><span class="sxs-lookup"><span data-stu-id="af0c2-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="af0c2-256">method</span><span class="sxs-lookup"><span data-stu-id="af0c2-256">method</span></span>|<span data-ttu-id="af0c2-257">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-257">Yes</span></span>|<span data-ttu-id="af0c2-258">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-258">String</span></span>|<span data-ttu-id="af0c2-259">可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**</span><span class="sxs-lookup"><span data-stu-id="af0c2-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="af0c2-260">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-260">queries</span></span>|<span data-ttu-id="af0c2-261">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-261">No</span></span>|<span data-ttu-id="af0c2-262">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-262">Object</span></span>|<span data-ttu-id="af0c2-263">代表 hello 查詢參數 toobe 加入 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="af0c2-264">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="af0c2-265">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-265">headers</span></span>|<span data-ttu-id="af0c2-266">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-266">No</span></span>|<span data-ttu-id="af0c2-267">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-267">Object</span></span>|<span data-ttu-id="af0c2-268">代表每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-269">例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="af0c2-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="af0c2-270">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-270">body</span></span>|<span data-ttu-id="af0c2-271">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-271">No</span></span>|<span data-ttu-id="af0c2-272">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-272">Object</span></span>|<span data-ttu-id="af0c2-273">表示傳送 toohello 端點的 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="af0c2-274">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="af0c2-274">retryPolicy</span></span>|<span data-ttu-id="af0c2-275">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-275">No</span></span>|<span data-ttu-id="af0c2-276">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-276">Object</span></span>|<span data-ttu-id="af0c2-277">可讓您 toocustomize hello 重試行 4xx 或 5xx 錯誤。</span><span class="sxs-lookup"><span data-stu-id="af0c2-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="af0c2-278">驗證</span><span class="sxs-lookup"><span data-stu-id="af0c2-278">authentication</span></span>|<span data-ttu-id="af0c2-279">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-279">No</span></span>|<span data-ttu-id="af0c2-280">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-280">Object</span></span>|<span data-ttu-id="af0c2-281">代表 hello 要求的 hello 方法應該進行驗證。</span><span class="sxs-lookup"><span data-stu-id="af0c2-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="af0c2-282">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="af0c2-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="af0c2-283">主機的 hello 屬性包括：</span><span class="sxs-lookup"><span data-stu-id="af0c2-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="af0c2-284">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-284">Element name</span></span>|<span data-ttu-id="af0c2-285">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-285">Required</span></span>|<span data-ttu-id="af0c2-286">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="af0c2-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="af0c2-287">api runtimeUrl</span></span>|<span data-ttu-id="af0c2-288">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-288">Yes</span></span>|<span data-ttu-id="af0c2-289">hello 端點 hello 的受管理應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="af0c2-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="af0c2-290">連線名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-290">connection name</span></span>||<span data-ttu-id="af0c2-291">必須參考 tooa 參數呼叫`$connection`和 hello hello 工作流程使用的受管理的 hello API 連線名稱。</span><span class="sxs-lookup"><span data-stu-id="af0c2-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="af0c2-292">hello API 連線觸發程序的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="af0c2-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="af0c2-293">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-293">Element name</span></span>|<span data-ttu-id="af0c2-294">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-294">Type</span></span>|<span data-ttu-id="af0c2-295">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="af0c2-296">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-296">headers</span></span>|<span data-ttu-id="af0c2-297">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-297">Object</span></span>|<span data-ttu-id="af0c2-298">hello http 回應的 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="af0c2-299">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-299">body</span></span>|<span data-ttu-id="af0c2-300">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-300">Object</span></span>|<span data-ttu-id="af0c2-301">hello hello http 回應主體。</span><span class="sxs-lookup"><span data-stu-id="af0c2-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="af0c2-302">HTTPWebhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="af0c2-303">hello HTTPWebhook 觸發程序會開啟端點，類似 toohello 手動觸發程序，但 hello HTTPWebhook 觸發程序也會呼叫 tooa 出指定 URL tooregister 及取消註冊。</span><span class="sxs-lookup"><span data-stu-id="af0c2-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="af0c2-304">HTTPWebhook 觸發程序看起來可能就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="af0c2-305">許多這些區段是選擇性的並且 hello Webhook hello 行為取決於哪些區段會提供或省略。</span><span class="sxs-lookup"><span data-stu-id="af0c2-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="af0c2-306">Webhook hello 屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="af0c2-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="af0c2-307">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-307">Element name</span></span>|<span data-ttu-id="af0c2-308">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-308">Required</span></span>|<span data-ttu-id="af0c2-309">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="af0c2-310">訂閱</span><span class="sxs-lookup"><span data-stu-id="af0c2-310">subscribe</span></span>|<span data-ttu-id="af0c2-311">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-311">No</span></span>|<span data-ttu-id="af0c2-312">hello 傳出 hello 觸發程序會建立並執行 hello 初始註冊時所呼叫的要求。</span><span class="sxs-lookup"><span data-stu-id="af0c2-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="af0c2-313">取消訂閱</span><span class="sxs-lookup"><span data-stu-id="af0c2-313">unsubscribe</span></span>|<span data-ttu-id="af0c2-314">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-314">No</span></span>|<span data-ttu-id="af0c2-315">hello 刪除 hello 觸發程序時，連出要求。</span><span class="sxs-lookup"><span data-stu-id="af0c2-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="af0c2-316">**訂閱**hello 連出 toostart 接聽 tooevents 所做的呼叫。</span><span class="sxs-lookup"><span data-stu-id="af0c2-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="af0c2-317">此呼叫會啟動以 hello 執行相同的 hello 標準 HTTP 動作的參數集合。</span><span class="sxs-lookup"><span data-stu-id="af0c2-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="af0c2-318">進行任何時間 hello 這個傳出呼叫工作流程以任何方式，例如，每當 hello 認證會復原變更，或 hello 觸發程序的輸入參數的變更。</span><span class="sxs-lookup"><span data-stu-id="af0c2-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="af0c2-319">此呼叫 toosupport，有一個新的函式： `@listCallbackUrl()`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="af0c2-320">這個函式會針對此工作流程中的這個特定觸發程序傳回唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="af0c2-321">它代表 hello 使用 hello REST 服務的 hello 端點的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="af0c2-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="af0c2-322">**取消訂閱**受到呼叫的時機是當作業將此觸發程序轉譯為無效時，包括︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="af0c2-323">刪除或停用 hello 觸發程序</span><span class="sxs-lookup"><span data-stu-id="af0c2-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="af0c2-324">刪除或停用 hello 工作流程</span><span class="sxs-lookup"><span data-stu-id="af0c2-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="af0c2-325">刪除或停用 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="af0c2-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="af0c2-326">hello 邏輯應用程式會自動呼叫 hello 取消動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="af0c2-327">hello 參數 toothis 函式會將相同 hello 為 hello HTTP 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="af0c2-328">hello hello HTTPWebhook 觸發程序的輸出是 hello hello 連入要求內容：</span><span class="sxs-lookup"><span data-stu-id="af0c2-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="af0c2-329">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-329">Element name</span></span>|<span data-ttu-id="af0c2-330">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-330">Type</span></span>|<span data-ttu-id="af0c2-331">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="af0c2-332">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-332">headers</span></span>|<span data-ttu-id="af0c2-333">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-333">Object</span></span>|<span data-ttu-id="af0c2-334">hello http 要求的 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="af0c2-335">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-335">body</span></span>|<span data-ttu-id="af0c2-336">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-336">Object</span></span>|<span data-ttu-id="af0c2-337">hello hello http 要求主體。</span><span class="sxs-lookup"><span data-stu-id="af0c2-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="af0c2-338">Webhook 動作的限制可以在 hello 中指定相同的方式[HTTP 非同步限制](#asynchronous-limits)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="af0c2-339">條件</span><span class="sxs-lookup"><span data-stu-id="af0c2-339">Conditions</span></span>  

<span data-ttu-id="af0c2-340">任何觸發程序，您可以使用一或多個條件 toodetermine 是否 hello 工作流程應執行或未執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="af0c2-341">例如：</span><span class="sxs-lookup"><span data-stu-id="af0c2-341">For example:</span></span>  

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

<span data-ttu-id="af0c2-342">在此情況下，hello 報表時 hello 工作流程的唯一觸發程序`sendReports`參數設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="af0c2-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="af0c2-343">最後，條件可能會參考 hello hello 觸發程序的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="af0c2-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="af0c2-344">例如，您只能在網站傳回狀態碼 500 時啟動工作流程，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="af0c2-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="af0c2-345">當任何運算式參考 hello hello 觸發程序的狀態碼\(以任何方式\)，hello 預設行為\(觸發程序只能在 200\(確定\)\)取代。</span><span class="sxs-lookup"><span data-stu-id="af0c2-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="af0c2-346">例如，如果您想 tootrigger 狀態碼 200 和狀態碼 「 201 上的，您有 tooinclude:`@or(equals(triggers().code, 200),equals(triggers().code,201))`做為您的條件。</span><span class="sxs-lookup"><span data-stu-id="af0c2-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="af0c2-347">為要求啟動多個執行</span><span class="sxs-lookup"><span data-stu-id="af0c2-347">Start multiple runs for a request</span></span>

<span data-ttu-id="af0c2-348">針對單一要求中，多個回合關閉 tookick`splitOn`非常有用，例如，當您想 toopoll 可以有多個新項目，輪詢間隔之間的端點。</span><span class="sxs-lookup"><span data-stu-id="af0c2-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="af0c2-349">與`splitOn`，指定 hello 屬性內包含的項目，其中每個您想要的 hello 陣列的 hello 回應裝載 toouse toostart hello 觸發程序執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="af0c2-350">例如，假設您有應用程式開發介面會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="af0c2-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="af0c2-351">邏輯應用程式只需要 hello 資料列內容，因此您可以建構在觸發程序，如下列範例：</span><span class="sxs-lookup"><span data-stu-id="af0c2-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="af0c2-352">然後，在 hello 工作流程定義、`@triggerBody().name`傳回`mycoolrow`hello 第一次執行，並`another row`hello 第二個執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="af0c2-353">hello 觸發程序的輸出看起來像此範例中：</span><span class="sxs-lookup"><span data-stu-id="af0c2-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="af0c2-354">因此，如果您使用`SplitOn`，您無法取得 hello 內容以外的 hello 陣列在此情況下，hello`Status`欄位。</span><span class="sxs-lookup"><span data-stu-id="af0c2-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="af0c2-355">在此範例中，我們使用 hello`?`運算子 toobe 無法 tooavoid 失敗如果 hello`Rows`屬性不存在。</span><span class="sxs-lookup"><span data-stu-id="af0c2-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="af0c2-356">單一執行的執行個體</span><span class="sxs-lookup"><span data-stu-id="af0c2-356">Single run instance</span></span>

<span data-ttu-id="af0c2-357">您可以設定具有循環屬性 tooonly 火災，如果已完成所有作用中執行的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="af0c2-358">如果正在執行時，就會發生排程的循環，hello 觸發程序會略過，並等待，直到 hello 下一個排程的循環間隔 toocheck 一次。</span><span class="sxs-lookup"><span data-stu-id="af0c2-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="af0c2-359">您可以設定此設定，透過 hello 作業選項：</span><span class="sxs-lookup"><span data-stu-id="af0c2-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="af0c2-360">類型和輸入</span><span class="sxs-lookup"><span data-stu-id="af0c2-360">Types and inputs</span></span>  

<span data-ttu-id="af0c2-361">動作有許多類型，且各有各的獨特行為。</span><span class="sxs-lookup"><span data-stu-id="af0c2-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="af0c2-362">集合動作可在自身當中包含其他許多動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="af0c2-363">標準動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-363">Standard actions</span></span>  

-   <span data-ttu-id="af0c2-364">**HTTP** 這個動作會呼叫 HTTP Web 端點。</span><span class="sxs-lookup"><span data-stu-id="af0c2-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="af0c2-365">**ApiConnection** \-此動作的行為方式與 hello HTTP 動作，但使用 hello Microsoft 管理的 Api。</span><span class="sxs-lookup"><span data-stu-id="af0c2-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="af0c2-366">**ApiConnectionWebhook** \-像 HTTPWebhook，但使用 hello Microsoft 管理的 Api。</span><span class="sxs-lookup"><span data-stu-id="af0c2-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="af0c2-367">**回應** \- 這個動作會定義連入呼叫的回應。</span><span class="sxs-lookup"><span data-stu-id="af0c2-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="af0c2-368">**等候** \- 這個簡單的動作會等候固定時間量或直到某個特定時間。</span><span class="sxs-lookup"><span data-stu-id="af0c2-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="af0c2-369">**工作流程** \- 這個動作代表巢狀工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="af0c2-370">**函式** \- 這個動作代表 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="af0c2-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="af0c2-371">集合動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-371">Collection actions</span></span>

-   <span data-ttu-id="af0c2-372">**範圍** \- 這個動作是其他動作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="af0c2-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="af0c2-373">**條件**\-這個動作會評估運算式，並執行 hello 對應的結果分支。</span><span class="sxs-lookup"><span data-stu-id="af0c2-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="af0c2-374">**ForEach** \- 這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="af0c2-375">**直到**\-此迴圈的動作會執行內部的動作，直到條件結果 tootrue。</span><span class="sxs-lookup"><span data-stu-id="af0c2-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="af0c2-376">每種動作類型都有一組可定義動作行為的不同**輸入**。</span><span class="sxs-lookup"><span data-stu-id="af0c2-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="af0c2-377">HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-377">HTTP action</span></span>  

<span data-ttu-id="af0c2-378">HTTP 動作呼叫指定的端點，並檢查 hello 回應 toodetermine，是否應該執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="af0c2-379">hello**輸入**物件會使用參數需要的 tooconstruct hello HTTP 呼叫 hello 組：</span><span class="sxs-lookup"><span data-stu-id="af0c2-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="af0c2-380">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-380">Element name</span></span>|<span data-ttu-id="af0c2-381">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-381">Required</span></span>|<span data-ttu-id="af0c2-382">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-382">Type</span></span>|<span data-ttu-id="af0c2-383">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-384">method</span><span class="sxs-lookup"><span data-stu-id="af0c2-384">method</span></span>|<span data-ttu-id="af0c2-385">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-385">Yes</span></span>|<span data-ttu-id="af0c2-386">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-386">String</span></span>|<span data-ttu-id="af0c2-387">可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**</span><span class="sxs-lookup"><span data-stu-id="af0c2-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="af0c2-388">uri</span><span class="sxs-lookup"><span data-stu-id="af0c2-388">uri</span></span>|<span data-ttu-id="af0c2-389">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-389">Yes</span></span>|<span data-ttu-id="af0c2-390">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-390">String</span></span>|<span data-ttu-id="af0c2-391">hello http 或 https 端點時所呼叫。</span><span class="sxs-lookup"><span data-stu-id="af0c2-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="af0c2-392">最大長度為 2 KB。</span><span class="sxs-lookup"><span data-stu-id="af0c2-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="af0c2-393">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-393">queries</span></span>|<span data-ttu-id="af0c2-394">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-394">No</span></span>|<span data-ttu-id="af0c2-395">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-395">Object</span></span>|<span data-ttu-id="af0c2-396">代表 hello 查詢參數 tooadd toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="af0c2-397">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="af0c2-398">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-398">headers</span></span>|<span data-ttu-id="af0c2-399">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-399">No</span></span>|<span data-ttu-id="af0c2-400">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-400">Object</span></span>|<span data-ttu-id="af0c2-401">代表每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-402">例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="af0c2-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="af0c2-403">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-403">body</span></span>|<span data-ttu-id="af0c2-404">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-404">No</span></span>|<span data-ttu-id="af0c2-405">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-405">Object</span></span>|<span data-ttu-id="af0c2-406">表示傳送 toohello 端點的 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="af0c2-407">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="af0c2-407">retryPolicy</span></span>|<span data-ttu-id="af0c2-408">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-408">No</span></span>|<span data-ttu-id="af0c2-409">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-409">Object</span></span>|<span data-ttu-id="af0c2-410">可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。</span><span class="sxs-lookup"><span data-stu-id="af0c2-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="af0c2-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="af0c2-411">operationsOptions</span></span>|<span data-ttu-id="af0c2-412">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-412">No</span></span>|<span data-ttu-id="af0c2-413">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-413">String</span></span>|<span data-ttu-id="af0c2-414">定義特殊的行為 toooverride hello 組。</span><span class="sxs-lookup"><span data-stu-id="af0c2-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="af0c2-415">驗證</span><span class="sxs-lookup"><span data-stu-id="af0c2-415">authentication</span></span>|<span data-ttu-id="af0c2-416">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-416">No</span></span>|<span data-ttu-id="af0c2-417">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-417">Object</span></span>|<span data-ttu-id="af0c2-418">代表 hello 要求的 hello 方法應該進行驗證。</span><span class="sxs-lookup"><span data-stu-id="af0c2-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="af0c2-419">如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="af0c2-420">除了排程器外，還有一個支援的屬性︰`authority`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="af0c2-421">根據預設，在未指定時這會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="af0c2-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="af0c2-422">HTTP 動作 \(和 API 連線\) 動作支援重試原則。</span><span class="sxs-lookup"><span data-stu-id="af0c2-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="af0c2-423">重試原則會套用 toointermittent 失敗，是做為特性與 HTTP 狀態碼 408、 429 和 5xx，加法 tooany 連線例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af0c2-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="af0c2-424">說明此原則使用 hello *retryPolicy*物件定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="af0c2-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="af0c2-425">hello ISO 8601 格式指定 hello 重試間隔。</span><span class="sxs-lookup"><span data-stu-id="af0c2-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="af0c2-426">在此時間間隔具有預設的 20 秒，最小值，而 hello 最大值為一小時。</span><span class="sxs-lookup"><span data-stu-id="af0c2-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="af0c2-427">hello 預設值和最大重試計數為四個小時。</span><span class="sxs-lookup"><span data-stu-id="af0c2-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="af0c2-428">如果未指定 hello 重試原則定義，`fixed`策略會搭配預設重試計數和間隔值。</span><span class="sxs-lookup"><span data-stu-id="af0c2-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="af0c2-429">toodisable hello 重試原則，將其類型設定太`None`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="af0c2-430">例如，hello 下列動作重試擷取 hello 最新消息兩次，如果有斷斷續續地發生失敗，總共有三個執行中，每個嘗試之間會有 30 秒延遲：</span><span class="sxs-lookup"><span data-stu-id="af0c2-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="af0c2-431">非同步模式</span><span class="sxs-lookup"><span data-stu-id="af0c2-431">Asynchronous patterns</span></span>

<span data-ttu-id="af0c2-432">根據預設，所有以 HTTP 為基礎的動作支援 hello 標準的非同步作業模式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="af0c2-433">因此如果 hello 遠端伺服器指出該 hello 要求已接受以進行處理，202 的\(接受\)回應 hello Logic Apps 引擎會持續輪詢 hello 直到到達終端機 hello 回應的位置標頭中指定的 URL狀態\(非\-202 回應\)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="af0c2-434">toodisable hello 非同步行為先前所述，設定`DisableAsyncPattern`hello 動作輸入中的選項。</span><span class="sxs-lookup"><span data-stu-id="af0c2-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="af0c2-435">在此情況下，hello 動作的 hello 輸出根據 hello 初始 202 回應 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="af0c2-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="af0c2-436">非同步限制</span><span class="sxs-lookup"><span data-stu-id="af0c2-436">Asynchronous Limits</span></span>

<span data-ttu-id="af0c2-437">非同步模式可限制其持續時間 tooa 特定時間間隔中。</span><span class="sxs-lookup"><span data-stu-id="af0c2-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="af0c2-438">如果 hello 時間間隔超過期限而未到達終止狀態，將會標示 hello hello 動作狀態`Cancelled`的代碼`ActionTimedOut`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="af0c2-439">採用 ISO 8601 格式指定 hello 限制逾時。</span><span class="sxs-lookup"><span data-stu-id="af0c2-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="af0c2-440">限制可以指定以 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="af0c2-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="af0c2-441">API 連線</span><span class="sxs-lookup"><span data-stu-id="af0c2-441">API Connection</span></span>  

<span data-ttu-id="af0c2-442">API 連線是參考 Microsoft 管理之連接器的動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="af0c2-443">這個動作需要參考 tooa 有效連接，以及有關 hello API 和所需的參數。</span><span class="sxs-lookup"><span data-stu-id="af0c2-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="af0c2-444">元素名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-444">Element name</span></span>|<span data-ttu-id="af0c2-445">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-445">Required</span></span>|<span data-ttu-id="af0c2-446">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-446">Type</span></span>|<span data-ttu-id="af0c2-447">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-448">主機</span><span class="sxs-lookup"><span data-stu-id="af0c2-448">host</span></span>|<span data-ttu-id="af0c2-449">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-449">Yes</span></span>|<span data-ttu-id="af0c2-450">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-450">Object</span></span>|<span data-ttu-id="af0c2-451">表示 hello 連接器資訊，例如 hello runtimeUrl 和參考 toohello 連接物件</span><span class="sxs-lookup"><span data-stu-id="af0c2-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="af0c2-452">method</span><span class="sxs-lookup"><span data-stu-id="af0c2-452">method</span></span>|<span data-ttu-id="af0c2-453">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-453">Yes</span></span>|<span data-ttu-id="af0c2-454">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-454">String</span></span>|<span data-ttu-id="af0c2-455">可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**</span><span class="sxs-lookup"><span data-stu-id="af0c2-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="af0c2-456">路徑</span><span class="sxs-lookup"><span data-stu-id="af0c2-456">path</span></span>|<span data-ttu-id="af0c2-457">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-457">Yes</span></span>|<span data-ttu-id="af0c2-458">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-458">String</span></span>|<span data-ttu-id="af0c2-459">hello 應用程式開發介面作業的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="af0c2-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="af0c2-460">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-460">queries</span></span>|<span data-ttu-id="af0c2-461">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-461">No</span></span>|<span data-ttu-id="af0c2-462">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-462">Object</span></span>|<span data-ttu-id="af0c2-463">代表 hello 查詢參數 tooadd toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="af0c2-464">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="af0c2-465">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-465">headers</span></span>|<span data-ttu-id="af0c2-466">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-466">No</span></span>|<span data-ttu-id="af0c2-467">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-467">Object</span></span>|<span data-ttu-id="af0c2-468">代表每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-469">例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="af0c2-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="af0c2-470">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-470">body</span></span>|<span data-ttu-id="af0c2-471">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-471">No</span></span>|<span data-ttu-id="af0c2-472">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-472">Object</span></span>|<span data-ttu-id="af0c2-473">表示傳送 toohello 端點的 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="af0c2-474">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="af0c2-474">retryPolicy</span></span>|<span data-ttu-id="af0c2-475">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-475">No</span></span>|<span data-ttu-id="af0c2-476">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-476">Object</span></span>|<span data-ttu-id="af0c2-477">可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。</span><span class="sxs-lookup"><span data-stu-id="af0c2-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="af0c2-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="af0c2-478">operationsOptions</span></span>|<span data-ttu-id="af0c2-479">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-479">No</span></span>|<span data-ttu-id="af0c2-480">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-480">String</span></span>|<span data-ttu-id="af0c2-481">定義特殊的行為 toooverride hello 組。</span><span class="sxs-lookup"><span data-stu-id="af0c2-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="af0c2-482">API 連線 Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-482">API Connection webhook action</span></span>

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

<span data-ttu-id="af0c2-483">Webhook 動作的限制可以在 hello 中指定相同的方式[HTTP 非同步限制](#asynchronous-limits)。</span><span class="sxs-lookup"><span data-stu-id="af0c2-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="af0c2-484">回應動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-484">Response action</span></span>  

<span data-ttu-id="af0c2-485">此動作的類型包含從 HTTP 要求的 hello 整個回應內容，並包含 statusCode、 本文和標頭：</span><span class="sxs-lookup"><span data-stu-id="af0c2-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="af0c2-486">hello 回應動作有特殊限制不適用 tooother 動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="af0c2-487">具體而言：</span><span class="sxs-lookup"><span data-stu-id="af0c2-487">Specifically:</span></span>  
  
-   <span data-ttu-id="af0c2-488">回應動作無法平行定義中，因為具決定性的回應 toohello 連入要求為必要項。</span><span class="sxs-lookup"><span data-stu-id="af0c2-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="af0c2-489">如果收到回應 hello 連入要求之後，將到達回應動作，hello 動作會被視為失敗\(衝突\)，且如此一來，執行 hello `Failed`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="af0c2-490">具有回應動作的工作流程在其觸發程序中不能有 `splitOn`，因為一個呼叫就會導致許多個執行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="af0c2-491">如此一來，這應該驗證 hello 資料流程時 PUT 和不正確的要求可能的原因。</span><span class="sxs-lookup"><span data-stu-id="af0c2-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="af0c2-492">等候動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-492">Wait action</span></span>  

<span data-ttu-id="af0c2-493">hello`wait`動作暫止工作流程執行 hello 指定時間間隔。</span><span class="sxs-lookup"><span data-stu-id="af0c2-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="af0c2-494">例如，toowait 15 分鐘，您可以使用此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="af0c2-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="af0c2-495">或者，toowait 特定時間點，直到您可以使用此範例：</span><span class="sxs-lookup"><span data-stu-id="af0c2-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="af0c2-496">hello 等候持續時間可能是使用可以指定 hello**間隔**物件或 hello**直到**物件，但非兩者。</span><span class="sxs-lookup"><span data-stu-id="af0c2-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="af0c2-497">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-497">Name</span></span>|<span data-ttu-id="af0c2-498">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-498">Required</span></span>|<span data-ttu-id="af0c2-499">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-499">Type</span></span>|<span data-ttu-id="af0c2-500">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-501">interval</span><span class="sxs-lookup"><span data-stu-id="af0c2-501">interval</span></span>|<span data-ttu-id="af0c2-502">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-502">No</span></span>|<span data-ttu-id="af0c2-503">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-503">Object</span></span>|<span data-ttu-id="af0c2-504">hello 等候一段時間為基礎的持續時間。</span><span class="sxs-lookup"><span data-stu-id="af0c2-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="af0c2-505">間隔單位</span><span class="sxs-lookup"><span data-stu-id="af0c2-505">interval unit</span></span>|<span data-ttu-id="af0c2-506">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-506">Yes</span></span>|<span data-ttu-id="af0c2-507">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-507">String</span></span>|<span data-ttu-id="af0c2-508">下列其中一個間隔︰秒、分鐘、小時、天、週、月、年。</span><span class="sxs-lookup"><span data-stu-id="af0c2-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="af0c2-509">間隔計數</span><span class="sxs-lookup"><span data-stu-id="af0c2-509">interval count</span></span>|<span data-ttu-id="af0c2-510">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-510">Yes</span></span>|<span data-ttu-id="af0c2-511">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-511">String</span></span>|<span data-ttu-id="af0c2-512">根據給定內部單位 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="af0c2-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="af0c2-513">直到</span><span class="sxs-lookup"><span data-stu-id="af0c2-513">until</span></span>|<span data-ttu-id="af0c2-514">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-514">No</span></span>|<span data-ttu-id="af0c2-515">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-515">Object</span></span>|<span data-ttu-id="af0c2-516">hello 等候以時間為基礎的點上的持續時間。</span><span class="sxs-lookup"><span data-stu-id="af0c2-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="af0c2-517">直到時間戳記</span><span class="sxs-lookup"><span data-stu-id="af0c2-517">until timestamp</span></span>|<span data-ttu-id="af0c2-518">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-518">Yes</span></span>|<span data-ttu-id="af0c2-519">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-519">String</span></span>|<span data-ttu-id="af0c2-520">字串 &#124; hello hello 等候到期時的 UTC 時間點。</span><span class="sxs-lookup"><span data-stu-id="af0c2-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="af0c2-521">查詢動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-521">Query action</span></span>

<span data-ttu-id="af0c2-522">hello`query`動作可讓您篩選條件所根據的陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="af0c2-523">例如，tooselect 數字大於 2，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="af0c2-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="af0c2-524">hello 輸出 hello`query`動作是陣列，其中具有 hello 輸入陣列中滿足 hello 條件的項目。</span><span class="sxs-lookup"><span data-stu-id="af0c2-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="af0c2-525">如果沒有任何值滿足 hello`where`條件，hello 結果為空陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="af0c2-526">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-526">Name</span></span>|<span data-ttu-id="af0c2-527">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-527">Required</span></span>|<span data-ttu-id="af0c2-528">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-528">Type</span></span>|<span data-ttu-id="af0c2-529">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="af0c2-530">from</span><span class="sxs-lookup"><span data-stu-id="af0c2-530">from</span></span>|<span data-ttu-id="af0c2-531">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-531">Yes</span></span>|<span data-ttu-id="af0c2-532">陣列</span><span class="sxs-lookup"><span data-stu-id="af0c2-532">Array</span></span>|<span data-ttu-id="af0c2-533">hello 來源陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-533">hello source array.</span></span>|
|<span data-ttu-id="af0c2-534">其中</span><span class="sxs-lookup"><span data-stu-id="af0c2-534">where</span></span>|<span data-ttu-id="af0c2-535">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-535">Yes</span></span>|<span data-ttu-id="af0c2-536">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-536">String</span></span>|<span data-ttu-id="af0c2-537">hello 條件 tooapply tooeach hello 來源陣列元素。</span><span class="sxs-lookup"><span data-stu-id="af0c2-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="af0c2-538">選取動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-538">Select action</span></span>

<span data-ttu-id="af0c2-539">hello`select`動作可讓您在規劃新的值陣列的每個項目。</span><span class="sxs-lookup"><span data-stu-id="af0c2-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="af0c2-540">例如，tooconvert 的數字讀入陣列物件的陣列，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="af0c2-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="af0c2-541">hello 的 hello 輸出`select`動作是陣列，其中具有 hello 由相同的基數為 hello 輸入的陣列，其中每個元素轉換成定義的 hello`select`屬性。</span><span class="sxs-lookup"><span data-stu-id="af0c2-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="af0c2-542">Hello 輸入是空的陣列，如果 hello 輸出也會為空陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="af0c2-543">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-543">Name</span></span>|<span data-ttu-id="af0c2-544">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-544">Required</span></span>|<span data-ttu-id="af0c2-545">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-545">Type</span></span>|<span data-ttu-id="af0c2-546">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="af0c2-547">from</span><span class="sxs-lookup"><span data-stu-id="af0c2-547">from</span></span>|<span data-ttu-id="af0c2-548">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-548">Yes</span></span>|<span data-ttu-id="af0c2-549">陣列</span><span class="sxs-lookup"><span data-stu-id="af0c2-549">Array</span></span>|<span data-ttu-id="af0c2-550">hello 來源陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-550">hello source array.</span></span>|
|<span data-ttu-id="af0c2-551">選取</span><span class="sxs-lookup"><span data-stu-id="af0c2-551">select</span></span>|<span data-ttu-id="af0c2-552">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-552">Yes</span></span>|<span data-ttu-id="af0c2-553">任意</span><span class="sxs-lookup"><span data-stu-id="af0c2-553">Any</span></span>|<span data-ttu-id="af0c2-554">hello 投影 tooapply tooeach hello 來源陣列元素。</span><span class="sxs-lookup"><span data-stu-id="af0c2-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="af0c2-555">終止動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-555">Terminate action</span></span>

<span data-ttu-id="af0c2-556">hello 終止動作停止執行 hello 工作流程執行時，中止執行中的任何動作，並略過任何其餘的動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="af0c2-557">比方說，tooterminate 狀態執行**失敗**，您可以使用下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="af0c2-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="af0c2-558">已完成的動作不會受到 hello 終止動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="af0c2-559">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-559">Name</span></span>|<span data-ttu-id="af0c2-560">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-560">Required</span></span>|<span data-ttu-id="af0c2-561">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-561">Type</span></span>|<span data-ttu-id="af0c2-562">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="af0c2-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="af0c2-563">runStatus</span></span>|<span data-ttu-id="af0c2-564">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-564">Yes</span></span>|<span data-ttu-id="af0c2-565">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-565">String</span></span>|<span data-ttu-id="af0c2-566">hello 目標執行狀態。</span><span class="sxs-lookup"><span data-stu-id="af0c2-566">hello target run status.</span></span> <span data-ttu-id="af0c2-567">**失敗**或**取消**。</span><span class="sxs-lookup"><span data-stu-id="af0c2-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="af0c2-568">runError</span><span class="sxs-lookup"><span data-stu-id="af0c2-568">runError</span></span>|<span data-ttu-id="af0c2-569">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-569">No</span></span>|<span data-ttu-id="af0c2-570">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-570">Object</span></span>|<span data-ttu-id="af0c2-571">hello 錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="af0c2-571">hello error details.</span></span> <span data-ttu-id="af0c2-572">只支援當**runStatus**設定得**失敗**。</span><span class="sxs-lookup"><span data-stu-id="af0c2-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="af0c2-573">runError 代碼</span><span class="sxs-lookup"><span data-stu-id="af0c2-573">runError code</span></span>|<span data-ttu-id="af0c2-574">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-574">No</span></span>|<span data-ttu-id="af0c2-575">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-575">String</span></span>|<span data-ttu-id="af0c2-576">hello 執行錯誤的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af0c2-576">hello run error code.</span></span>|
|<span data-ttu-id="af0c2-577">runError 訊息</span><span class="sxs-lookup"><span data-stu-id="af0c2-577">runError message</span></span>|<span data-ttu-id="af0c2-578">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-578">No</span></span>|<span data-ttu-id="af0c2-579">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-579">String</span></span>|<span data-ttu-id="af0c2-580">hello 執行錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="af0c2-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="af0c2-581">撰寫動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-581">Compose action</span></span>

<span data-ttu-id="af0c2-582">hello 撰寫動作可讓您建構任意的物件。</span><span class="sxs-lookup"><span data-stu-id="af0c2-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="af0c2-583">hello hello 輸出撰寫動作是 hello 結果評估其輸入。</span><span class="sxs-lookup"><span data-stu-id="af0c2-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="af0c2-584">例如，您可以使用 hello 撰寫多個動作的動作 toomerge 輸出：</span><span class="sxs-lookup"><span data-stu-id="af0c2-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="af0c2-585">hello**撰寫**動作可以使用的 tooconstruct 任何輸出，包括物件、 陣列和任何其他原生支援的邏輯應用程式，例如 XML 和二進位的型別。</span><span class="sxs-lookup"><span data-stu-id="af0c2-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="af0c2-586">資料表動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-586">Table action</span></span>

<span data-ttu-id="af0c2-587">hello`table`可讓您的項目插入陣列 tooconvert **CSV**或**HTML**資料表。</span><span class="sxs-lookup"><span data-stu-id="af0c2-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="af0c2-588">假設 @triggerBody() 是</span><span class="sxs-lookup"><span data-stu-id="af0c2-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="af0c2-589">並讓 hello 動作定義為</span><span class="sxs-lookup"><span data-stu-id="af0c2-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="af0c2-590">會產生上述 hello</span><span class="sxs-lookup"><span data-stu-id="af0c2-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="af0c2-591">id</span><span class="sxs-lookup"><span data-stu-id="af0c2-591">id</span></span></th><th><span data-ttu-id="af0c2-592">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="af0c2-593">0</span><span class="sxs-lookup"><span data-stu-id="af0c2-593">0</span></span></td><td><span data-ttu-id="af0c2-594">apples</span><span class="sxs-lookup"><span data-stu-id="af0c2-594">apples</span></span></td></tr><tr><td><span data-ttu-id="af0c2-595">1</span><span class="sxs-lookup"><span data-stu-id="af0c2-595">1</span></span></td><td><span data-ttu-id="af0c2-596">oranges</span><span class="sxs-lookup"><span data-stu-id="af0c2-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="af0c2-597">"</span><span class="sxs-lookup"><span data-stu-id="af0c2-597">"</span></span>

<span data-ttu-id="af0c2-598">在順序 toocustomize hello 資料表中，您可以明確地指定 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="af0c2-599">例如：</span><span class="sxs-lookup"><span data-stu-id="af0c2-599">For example:</span></span>

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

<span data-ttu-id="af0c2-600">會產生上述 hello</span><span class="sxs-lookup"><span data-stu-id="af0c2-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="af0c2-601">產生識別碼</span><span class="sxs-lookup"><span data-stu-id="af0c2-601">produce id</span></span></th><th><span data-ttu-id="af0c2-602">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="af0c2-603">0</span><span class="sxs-lookup"><span data-stu-id="af0c2-603">0</span></span></td><td><span data-ttu-id="af0c2-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="af0c2-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="af0c2-605">1</span><span class="sxs-lookup"><span data-stu-id="af0c2-605">1</span></span></td><td><span data-ttu-id="af0c2-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="af0c2-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="af0c2-607">"</span><span class="sxs-lookup"><span data-stu-id="af0c2-607">"</span></span>

<span data-ttu-id="af0c2-608">如果 hello`from`屬性值為空陣列，hello 輸出，則為空的資料表。</span><span class="sxs-lookup"><span data-stu-id="af0c2-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="af0c2-609">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-609">Name</span></span>|<span data-ttu-id="af0c2-610">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-610">Required</span></span>|<span data-ttu-id="af0c2-611">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-611">Type</span></span>|<span data-ttu-id="af0c2-612">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="af0c2-613">from</span><span class="sxs-lookup"><span data-stu-id="af0c2-613">from</span></span>|<span data-ttu-id="af0c2-614">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-614">Yes</span></span>|<span data-ttu-id="af0c2-615">陣列</span><span class="sxs-lookup"><span data-stu-id="af0c2-615">Array</span></span>|<span data-ttu-id="af0c2-616">hello 來源陣列。</span><span class="sxs-lookup"><span data-stu-id="af0c2-616">hello source array.</span></span>|
|<span data-ttu-id="af0c2-617">format</span><span class="sxs-lookup"><span data-stu-id="af0c2-617">format</span></span>|<span data-ttu-id="af0c2-618">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-618">Yes</span></span>|<span data-ttu-id="af0c2-619">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-619">String</span></span>|<span data-ttu-id="af0c2-620">hello 格式，或是**CSV**或**HTML**。</span><span class="sxs-lookup"><span data-stu-id="af0c2-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="af0c2-621">columns</span><span class="sxs-lookup"><span data-stu-id="af0c2-621">columns</span></span>|<span data-ttu-id="af0c2-622">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-622">No</span></span>|<span data-ttu-id="af0c2-623">陣列</span><span class="sxs-lookup"><span data-stu-id="af0c2-623">Array</span></span>|<span data-ttu-id="af0c2-624">hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="af0c2-624">hello columns.</span></span> <span data-ttu-id="af0c2-625">允許 hello 資料表 toooverride hello 預設的圖形。</span><span class="sxs-lookup"><span data-stu-id="af0c2-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="af0c2-626">資料行標頭</span><span class="sxs-lookup"><span data-stu-id="af0c2-626">column header</span></span>|<span data-ttu-id="af0c2-627">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-627">No</span></span>|<span data-ttu-id="af0c2-628">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-628">String</span></span>|<span data-ttu-id="af0c2-629">hello 資料行標頭的 hello。</span><span class="sxs-lookup"><span data-stu-id="af0c2-629">hello header of hello column.</span></span>|
|<span data-ttu-id="af0c2-630">資料行值</span><span class="sxs-lookup"><span data-stu-id="af0c2-630">column value</span></span>|<span data-ttu-id="af0c2-631">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-631">Yes</span></span>|<span data-ttu-id="af0c2-632">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-632">String</span></span>|<span data-ttu-id="af0c2-633">hello hello 資料行值。</span><span class="sxs-lookup"><span data-stu-id="af0c2-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="af0c2-634">工作流程動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-634">Workflow action</span></span>   

|<span data-ttu-id="af0c2-635">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-635">Name</span></span>|<span data-ttu-id="af0c2-636">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-636">Required</span></span>|<span data-ttu-id="af0c2-637">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-637">Type</span></span>|<span data-ttu-id="af0c2-638">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-639">主機識別碼</span><span class="sxs-lookup"><span data-stu-id="af0c2-639">host id</span></span>|<span data-ttu-id="af0c2-640">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-640">Yes</span></span>|<span data-ttu-id="af0c2-641">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-641">String</span></span>|<span data-ttu-id="af0c2-642">您想 toocall hello 工作流程 hello 資源 ID。</span><span class="sxs-lookup"><span data-stu-id="af0c2-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="af0c2-643">主機 triggerName</span><span class="sxs-lookup"><span data-stu-id="af0c2-643">host triggerName</span></span>|<span data-ttu-id="af0c2-644">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-644">Yes</span></span>|<span data-ttu-id="af0c2-645">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-645">String</span></span>|<span data-ttu-id="af0c2-646">hello 想 tooinvoke hello 觸發程序名稱。</span><span class="sxs-lookup"><span data-stu-id="af0c2-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="af0c2-647">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-647">queries</span></span>|<span data-ttu-id="af0c2-648">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-648">No</span></span>|<span data-ttu-id="af0c2-649">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-649">Object</span></span>|<span data-ttu-id="af0c2-650">代表 hello 查詢參數 tooadd toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="af0c2-651">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="af0c2-652">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-652">headers</span></span>|<span data-ttu-id="af0c2-653">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-653">No</span></span>|<span data-ttu-id="af0c2-654">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-654">Object</span></span>|<span data-ttu-id="af0c2-655">代表每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-656">例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="af0c2-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="af0c2-657">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-657">body</span></span>|<span data-ttu-id="af0c2-658">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-658">No</span></span>|<span data-ttu-id="af0c2-659">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-659">Object</span></span>|<span data-ttu-id="af0c2-660">表示傳送 toohello 端點 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="af0c2-661">Hello 工作流程上進行存取檢查\(更具體來說，hello 觸發程序\)，表示您需要存取 toohello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="af0c2-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="af0c2-662">hello 輸出從 hello`workflow`動作根據您定義在 hello `response` hello 子工作流程中的動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="af0c2-663">如果未定義任何`response`動作，然後 hello 輸出是空的。</span><span class="sxs-lookup"><span data-stu-id="af0c2-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="af0c2-664">函式動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-664">Function action</span></span>   

|<span data-ttu-id="af0c2-665">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-665">Name</span></span>|<span data-ttu-id="af0c2-666">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-666">Required</span></span>|<span data-ttu-id="af0c2-667">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-667">Type</span></span>|<span data-ttu-id="af0c2-668">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-669">函式識別碼</span><span class="sxs-lookup"><span data-stu-id="af0c2-669">function id</span></span>|<span data-ttu-id="af0c2-670">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-670">Yes</span></span>|<span data-ttu-id="af0c2-671">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-671">String</span></span>|<span data-ttu-id="af0c2-672">您想 tooinvoke 的 hello 函式 hello 資源 ID。</span><span class="sxs-lookup"><span data-stu-id="af0c2-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="af0c2-673">method</span><span class="sxs-lookup"><span data-stu-id="af0c2-673">method</span></span>|<span data-ttu-id="af0c2-674">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-674">No</span></span>|<span data-ttu-id="af0c2-675">String</span><span class="sxs-lookup"><span data-stu-id="af0c2-675">String</span></span>|<span data-ttu-id="af0c2-676">hello HTTP 方法使用 tooinvoke hello 函式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="af0c2-677">若未指定，則其預設值為 `POST`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="af0c2-678">查詢</span><span class="sxs-lookup"><span data-stu-id="af0c2-678">queries</span></span>|<span data-ttu-id="af0c2-679">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-679">No</span></span>|<span data-ttu-id="af0c2-680">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-680">Object</span></span>|<span data-ttu-id="af0c2-681">代表 hello 查詢參數 tooadd toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="af0c2-682">例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="af0c2-683">headers</span><span class="sxs-lookup"><span data-stu-id="af0c2-683">headers</span></span>|<span data-ttu-id="af0c2-684">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-684">No</span></span>|<span data-ttu-id="af0c2-685">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-685">Object</span></span>|<span data-ttu-id="af0c2-686">代表每個 toohello 要求會傳送 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="af0c2-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="af0c2-687">例如，tooset hello 語言和類型的要求： `"headers" : { "Accept-Language": "en-us" }`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="af0c2-688">body</span><span class="sxs-lookup"><span data-stu-id="af0c2-688">body</span></span>|<span data-ttu-id="af0c2-689">否</span><span class="sxs-lookup"><span data-stu-id="af0c2-689">No</span></span>|<span data-ttu-id="af0c2-690">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-690">Object</span></span>|<span data-ttu-id="af0c2-691">表示傳送 toohello 端點 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="af0c2-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="af0c2-692">當您儲存 hello 邏輯應用程式時，我們會執行某些檢查參考的 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="af0c2-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="af0c2-693">您需要 toohave access toohello 函式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="af0c2-694">僅允許使用標準 HTTP 觸發程序或一般 JSON Webhook 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af0c2-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="af0c2-695">它不應定義任何路由。</span><span class="sxs-lookup"><span data-stu-id="af0c2-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="af0c2-696">只允許使用「函式」和「匿名」授權層級。</span><span class="sxs-lookup"><span data-stu-id="af0c2-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="af0c2-697">擷取、 快取，且在執行階段使用 hello 觸發程序 URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="af0c2-698">因此如果任何作業會導致快取的 hello URL 無效，hello 動作便會在執行階段。</span><span class="sxs-lookup"><span data-stu-id="af0c2-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="af0c2-699">此 toowork 儲存 hello 邏輯應用程式，這將導致邏輯應用程式 tooretrieve 並再次快取 hello 觸發程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="af0c2-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="af0c2-700">集合動作 (範圍和迴圈)</span><span class="sxs-lookup"><span data-stu-id="af0c2-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="af0c2-701">某些動作類型可以在自身當中包含動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="af0c2-702">在集合中的參考動作，可直接之外 hello 集合參考。</span><span class="sxs-lookup"><span data-stu-id="af0c2-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="af0c2-703">如果您在某個範圍中定義了 `http`，`@body('http')` 仍會在工作流程中的任何位置保持有效。</span><span class="sxs-lookup"><span data-stu-id="af0c2-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="af0c2-704">在集合中的動作可以`runAfter`內其他動作 hello 相同的集合。</span><span class="sxs-lookup"><span data-stu-id="af0c2-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="af0c2-705">範圍動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-705">Scope action</span></span>

<span data-ttu-id="af0c2-706">hello`scope`動作可讓您以邏輯方式群組動作工作流程中的。</span><span class="sxs-lookup"><span data-stu-id="af0c2-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="af0c2-707">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-707">Name</span></span>|<span data-ttu-id="af0c2-708">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-708">Required</span></span>|<span data-ttu-id="af0c2-709">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-709">Type</span></span>|<span data-ttu-id="af0c2-710">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-711">動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-711">actions</span></span>|<span data-ttu-id="af0c2-712">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-712">Yes</span></span>|<span data-ttu-id="af0c2-713">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-713">Object</span></span>|<span data-ttu-id="af0c2-714">內部動作 tooexecute hello 範圍內</span><span class="sxs-lookup"><span data-stu-id="af0c2-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="af0c2-715">ForEach 動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-715">ForEach action</span></span>

<span data-ttu-id="af0c2-716">這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。</span><span class="sxs-lookup"><span data-stu-id="af0c2-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="af0c2-717">根據預設，平行 （20 執行以平行方式一次） 執行 hello foreach 迴圈 」。</span><span class="sxs-lookup"><span data-stu-id="af0c2-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="af0c2-718">您可以設定執行規則使用 hello`operationOptions`參數。</span><span class="sxs-lookup"><span data-stu-id="af0c2-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="af0c2-719">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-719">Name</span></span>|<span data-ttu-id="af0c2-720">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-720">Required</span></span>|<span data-ttu-id="af0c2-721">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-721">Type</span></span>|<span data-ttu-id="af0c2-722">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-723">動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-723">actions</span></span>|<span data-ttu-id="af0c2-724">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-724">Yes</span></span>|<span data-ttu-id="af0c2-725">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-725">Object</span></span>|<span data-ttu-id="af0c2-726">Hello 迴圈內的內部動作 tooexecute</span><span class="sxs-lookup"><span data-stu-id="af0c2-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="af0c2-727">foreach</span><span class="sxs-lookup"><span data-stu-id="af0c2-727">foreach</span></span>|<span data-ttu-id="af0c2-728">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-728">Yes</span></span>|<span data-ttu-id="af0c2-729">字串</span><span class="sxs-lookup"><span data-stu-id="af0c2-729">string</span></span>|<span data-ttu-id="af0c2-730">透過 hello 陣列 tooiterate</span><span class="sxs-lookup"><span data-stu-id="af0c2-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="af0c2-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="af0c2-731">operationOptions</span></span>|<span data-ttu-id="af0c2-732">no</span><span class="sxs-lookup"><span data-stu-id="af0c2-732">no</span></span>|<span data-ttu-id="af0c2-733">string</span><span class="sxs-lookup"><span data-stu-id="af0c2-733">string</span></span>|<span data-ttu-id="af0c2-734">行為的任何作業選項。</span><span class="sxs-lookup"><span data-stu-id="af0c2-734">Any operation options for behavior.</span></span> <span data-ttu-id="af0c2-735">目前只支援`sequential`tooexecute 反覆項目以循序方式 （預設行為是平行）</span><span class="sxs-lookup"><span data-stu-id="af0c2-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="af0c2-736">直到動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-736">Until action</span></span>

<span data-ttu-id="af0c2-737">此迴圈的動作會執行內部的動作，直到條件結果 tootrue 為止。</span><span class="sxs-lookup"><span data-stu-id="af0c2-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="af0c2-738">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-738">Name</span></span>|<span data-ttu-id="af0c2-739">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-739">Required</span></span>|<span data-ttu-id="af0c2-740">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-740">Type</span></span>|<span data-ttu-id="af0c2-741">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-742">動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-742">actions</span></span>|<span data-ttu-id="af0c2-743">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-743">Yes</span></span>|<span data-ttu-id="af0c2-744">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-744">Object</span></span>|<span data-ttu-id="af0c2-745">Hello 迴圈內的內部動作 tooexecute</span><span class="sxs-lookup"><span data-stu-id="af0c2-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="af0c2-746">expression</span><span class="sxs-lookup"><span data-stu-id="af0c2-746">expression</span></span>|<span data-ttu-id="af0c2-747">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-747">Yes</span></span>|<span data-ttu-id="af0c2-748">字串</span><span class="sxs-lookup"><span data-stu-id="af0c2-748">string</span></span>|<span data-ttu-id="af0c2-749">每個反覆項目之後的 hello 運算式 tooevaluate</span><span class="sxs-lookup"><span data-stu-id="af0c2-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="af0c2-750">limit</span><span class="sxs-lookup"><span data-stu-id="af0c2-750">limit</span></span>|<span data-ttu-id="af0c2-751">yes</span><span class="sxs-lookup"><span data-stu-id="af0c2-751">yes</span></span>|<span data-ttu-id="af0c2-752">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-752">Object</span></span>|<span data-ttu-id="af0c2-753">必須定義 hello 迴圈-至少一個限制的 hello 限制</span><span class="sxs-lookup"><span data-stu-id="af0c2-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="af0c2-754">計數</span><span class="sxs-lookup"><span data-stu-id="af0c2-754">count</span></span>|<span data-ttu-id="af0c2-755">no</span><span class="sxs-lookup"><span data-stu-id="af0c2-755">no</span></span>|<span data-ttu-id="af0c2-756">int</span><span class="sxs-lookup"><span data-stu-id="af0c2-756">int</span></span>|<span data-ttu-id="af0c2-757">hello toohello 數目限制可以執行的反覆項目</span><span class="sxs-lookup"><span data-stu-id="af0c2-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="af0c2-758">timeout</span><span class="sxs-lookup"><span data-stu-id="af0c2-758">timeout</span></span>|<span data-ttu-id="af0c2-759">no</span><span class="sxs-lookup"><span data-stu-id="af0c2-759">no</span></span>|<span data-ttu-id="af0c2-760">字串</span><span class="sxs-lookup"><span data-stu-id="af0c2-760">string</span></span>|<span data-ttu-id="af0c2-761">hello 多久它應該循環逾時。</span><span class="sxs-lookup"><span data-stu-id="af0c2-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="af0c2-762">ISO 8601 格式</span><span class="sxs-lookup"><span data-stu-id="af0c2-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="af0c2-763">條件 - If 動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-763">Conditions - If Action</span></span>

<span data-ttu-id="af0c2-764">hello`If`動作可讓您評估條件，以及執行分支，根據是否 hello 運算式評估太`true`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="af0c2-765">名稱</span><span class="sxs-lookup"><span data-stu-id="af0c2-765">Name</span></span>|<span data-ttu-id="af0c2-766">必要</span><span class="sxs-lookup"><span data-stu-id="af0c2-766">Required</span></span>|<span data-ttu-id="af0c2-767">類型</span><span class="sxs-lookup"><span data-stu-id="af0c2-767">Type</span></span>|<span data-ttu-id="af0c2-768">說明</span><span class="sxs-lookup"><span data-stu-id="af0c2-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="af0c2-769">動作</span><span class="sxs-lookup"><span data-stu-id="af0c2-769">actions</span></span>|<span data-ttu-id="af0c2-770">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-770">Yes</span></span>|<span data-ttu-id="af0c2-771">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-771">Object</span></span>|<span data-ttu-id="af0c2-772">當運算式評估過的內部動作 tooexecute`true`</span><span class="sxs-lookup"><span data-stu-id="af0c2-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="af0c2-773">expression</span><span class="sxs-lookup"><span data-stu-id="af0c2-773">expression</span></span>|<span data-ttu-id="af0c2-774">是</span><span class="sxs-lookup"><span data-stu-id="af0c2-774">Yes</span></span>|<span data-ttu-id="af0c2-775">字串</span><span class="sxs-lookup"><span data-stu-id="af0c2-775">string</span></span>|<span data-ttu-id="af0c2-776">hello 運算式 tooevaluate</span><span class="sxs-lookup"><span data-stu-id="af0c2-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="af0c2-777">else</span><span class="sxs-lookup"><span data-stu-id="af0c2-777">else</span></span>|<span data-ttu-id="af0c2-778">no</span><span class="sxs-lookup"><span data-stu-id="af0c2-778">no</span></span>|<span data-ttu-id="af0c2-779">Object</span><span class="sxs-lookup"><span data-stu-id="af0c2-779">Object</span></span>|<span data-ttu-id="af0c2-780">當運算式評估過的內部動作 tooexecute`false`</span><span class="sxs-lookup"><span data-stu-id="af0c2-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="af0c2-781">hello 下表顯示條件如何在動作中使用運算式的範例：</span><span class="sxs-lookup"><span data-stu-id="af0c2-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="af0c2-782">JSON 值</span><span class="sxs-lookup"><span data-stu-id="af0c2-782">JSON value</span></span>|<span data-ttu-id="af0c2-783">結果</span><span class="sxs-lookup"><span data-stu-id="af0c2-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="af0c2-784">會評估 tootrue 任何值會導致此狀況 toopass。</span><span class="sxs-lookup"><span data-stu-id="af0c2-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="af0c2-785">僅支援布林運算式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="af0c2-786">其他 tooconvert 類型 tooBoolean，使用函數`empty`， `equals`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="af0c2-787">支援比較函式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-787">Comparison functions are supported.</span></span> <span data-ttu-id="af0c2-788">如 hello 範例，hello 動作時才執行 act1 hello 輸出大於 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="af0c2-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="af0c2-789">邏輯函數也會支援的 toocreate 巢狀布林運算式。</span><span class="sxs-lookup"><span data-stu-id="af0c2-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="af0c2-790">在此情況下，hello 動作執行 hello 臨界值高於或低於 100 的 act1 hello 輸出時。</span><span class="sxs-lookup"><span data-stu-id="af0c2-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="af0c2-791">如果陣列沒有任何項目，您可以使用陣列函式 toocheck。</span><span class="sxs-lookup"><span data-stu-id="af0c2-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="af0c2-792">在此情況下，hello 動作執行時 hello 錯誤陣列是空的。</span><span class="sxs-lookup"><span data-stu-id="af0c2-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="af0c2-793">錯誤 - 不是有效條件，因為條件必須有 @。</span><span class="sxs-lookup"><span data-stu-id="af0c2-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="af0c2-794">如果條件評估成功，hello 條件標示為`Succeeded`。</span><span class="sxs-lookup"><span data-stu-id="af0c2-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="af0c2-795">動作內任一 hello`actions`或`else`物件的評估太`Succeeded`時執行，且成功，`Failed`時執行，且失敗，或`Skipped`時不會執行該分支。</span><span class="sxs-lookup"><span data-stu-id="af0c2-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af0c2-796">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af0c2-796">Next steps</span></span>

[<span data-ttu-id="af0c2-797">工作流程服務 REST API</span><span class="sxs-lookup"><span data-stu-id="af0c2-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
