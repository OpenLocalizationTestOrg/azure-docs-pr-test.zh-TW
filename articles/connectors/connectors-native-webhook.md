---
title: "適用於 Azure Logic Apps 的 webhook 連接器 | Microsoft Docs"
description: "如何使用 webhook 動作和觸發程序，從邏輯應用程式執行類似篩選陣列的動作"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: fbfef291334109c6dcfcde80741874549fb7929f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-webhook-connector"></a><span data-ttu-id="44bc3-103">開始使用 webhook 連接器</span><span class="sxs-lookup"><span data-stu-id="44bc3-103">Get started with the webhook connector</span></span>

<span data-ttu-id="44bc3-104">透過使用 webhook 動作和觸發程序，您可以啟動、暫停和繼續流程來執行這些工作︰</span><span class="sxs-lookup"><span data-stu-id="44bc3-104">With the webhook action and trigger, you can start, pause, and resume flows to perform these tasks:</span></span>

* <span data-ttu-id="44bc3-105">收到項目時，即從 [Azure 事件中樞](https://github.com/logicappsio/EventHubAPI) 觸發</span><span class="sxs-lookup"><span data-stu-id="44bc3-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span></span>
* <span data-ttu-id="44bc3-106">等待核准再繼續工作流程</span><span class="sxs-lookup"><span data-stu-id="44bc3-106">Wait for an approval before continuing a workflow</span></span>

<span data-ttu-id="44bc3-107">深入了解關於[如何建立支援 webhook 的自訂 API](../logic-apps/logic-apps-create-api-app.md)。</span><span class="sxs-lookup"><span data-stu-id="44bc3-107">Learn more about [how to create custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="use-the-webhook-trigger"></a><span data-ttu-id="44bc3-108">使用 webhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="44bc3-108">Use the webhook trigger</span></span>

<span data-ttu-id="44bc3-109">[觸發程序](connectors-overview.md)是啟動邏輯應用程式工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="44bc3-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span></span> <span data-ttu-id="44bc3-110">webhook 觸發程序是以事件為基礎，而不是依賴對新項目進行輪詢。</span><span class="sxs-lookup"><span data-stu-id="44bc3-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span></span> <span data-ttu-id="44bc3-111">如同[要求觸發程序](connectors-native-reqres.md)一般，邏輯應用程式會觸發事件發生的瞬間。</span><span class="sxs-lookup"><span data-stu-id="44bc3-111">Like the [request trigger](connectors-native-reqres.md), the logic app fires the instant that an event happens.</span></span> <span data-ttu-id="44bc3-112">webhook 觸發程序會註冊服務的*回呼 URL*，並依需求使用該 URL 來觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="44bc3-112">The webhook trigger registers a *callback URL* to a service and uses that URL to fire the logic app as needed.</span></span>

<span data-ttu-id="44bc3-113">以下是如何在邏輯應用程式設計工具中設定 HTTP 觸發程序的範例。</span><span class="sxs-lookup"><span data-stu-id="44bc3-113">Here's an example that shows how to set up an HTTP trigger in the Logic App Designer.</span></span> <span data-ttu-id="44bc3-114">這個步驟假設您已部署或正在存取的 API 會遵循[邏輯應用程式中的 webhook 訂閱和取消訂閱模式](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)。</span><span class="sxs-lookup"><span data-stu-id="44bc3-114">The steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span></span> <span data-ttu-id="44bc3-115">每當邏輯應用程式隨新的 webhook 儲存或由停用切換為啟用時，就會進行訂閱呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bc3-115">The subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled to enabled.</span></span> <span data-ttu-id="44bc3-116">每當系統移除並儲存邏輯應用程式 webhook 觸發程序時，就會進行取消訂閱呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bc3-116">The unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled to disabled.</span></span>

<span data-ttu-id="44bc3-117">**新增 webhook 觸發程序**</span><span class="sxs-lookup"><span data-stu-id="44bc3-117">**To add the webhook trigger**</span></span>

1. <span data-ttu-id="44bc3-118">將 **HTTP Webhook** 觸發程序新增為邏輯應用程式中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="44bc3-118">Add the **HTTP Webhook** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="44bc3-119">填入 webhook 訂閱和取消訂閱呼叫的參數。</span><span class="sxs-lookup"><span data-stu-id="44bc3-119">Fill in the parameters for the webhook subscribe and unsubscribe calls.</span></span>

   <span data-ttu-id="44bc3-120">此步驟所遵循的模式與 [HTTP 動作](connectors-native-http.md)格式相同。</span><span class="sxs-lookup"><span data-stu-id="44bc3-120">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![HTTP 觸發程序](./media/connectors-native-webhook/using-trigger.png)

3. <span data-ttu-id="44bc3-122">加入至少一個動作。</span><span class="sxs-lookup"><span data-stu-id="44bc3-122">Add at least one action.</span></span>
4. <span data-ttu-id="44bc3-123">按一下 [儲存] 來發佈邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="44bc3-123">Click **Save** to publish the logic app.</span></span> <span data-ttu-id="44bc3-124">此步驟會呼叫含有觸發此邏輯應用程式所需的回呼 URL 訂閱端點。</span><span class="sxs-lookup"><span data-stu-id="44bc3-124">This step calls the subscribe endpoint with the callback URL needed to trigger this logic app.</span></span>
5. <span data-ttu-id="44bc3-125">每當服務對回呼 URL 發出 `HTTP POST` 時，就會觸發邏輯應用程式，並包含要求中所傳遞的任何資料。</span><span class="sxs-lookup"><span data-stu-id="44bc3-125">Whenever the service makes an `HTTP POST` to the callback URL, the logic app fires, and includes any data passed into the request.</span></span>

## <a name="use-the-webhook-action"></a><span data-ttu-id="44bc3-126">使用 webhook 動作</span><span class="sxs-lookup"><span data-stu-id="44bc3-126">Use the webhook action</span></span>

<span data-ttu-id="44bc3-127">[「動作」](connectors-overview.md)是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="44bc3-127">An [*action*](connectors-overview.md) is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="44bc3-128">Webhook 動作會註冊服務的*回呼 URL*，並等到呼叫該 URL 後再繼續。</span><span class="sxs-lookup"><span data-stu-id="44bc3-128">A webhook action registers a *callback URL* with a service and waits until the URL is called before resuming.</span></span> <span data-ttu-id="44bc3-129">[傳送核准電子郵件](connectors-create-api-office365-outlook.md)是遵循這個模式的連接器範例。</span><span class="sxs-lookup"><span data-stu-id="44bc3-129">The ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span></span> <span data-ttu-id="44bc3-130">您可以透過 webhook 動作將此模式擴充到任何服務。</span><span class="sxs-lookup"><span data-stu-id="44bc3-130">You can extend this pattern into any service through the webhook action.</span></span> 

<span data-ttu-id="44bc3-131">以下是如何在邏輯應用程式設計工具中設定 webhook 動作的範例。</span><span class="sxs-lookup"><span data-stu-id="44bc3-131">Here's an example that shows how to set up a webhook action in the Logic App Designer.</span></span> <span data-ttu-id="44bc3-132">這些步驟假設您已部署或正在存取的 API 會遵循[邏輯應用程式中的 webhook 訂閱和取消訂閱模式](../logic-apps/logic-apps-create-api-app.md#webhook-actions)。</span><span class="sxs-lookup"><span data-stu-id="44bc3-132">These steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span></span> <span data-ttu-id="44bc3-133">每當邏輯應用程式執行 webhook 動作時，就會進行訂閱呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bc3-133">The subscribe call is made when a logic app executes the webhook action.</span></span> <span data-ttu-id="44bc3-134">每當執行在等待回應時取消，或在邏輯應用程式逾時前取消，就會進行取消訂閱呼叫。</span><span class="sxs-lookup"><span data-stu-id="44bc3-134">The unsubscribe call is made when a run is canceled while waiting for a response, or before the logic app times out.</span></span>

<span data-ttu-id="44bc3-135">**若要新增 webhook 動作**</span><span class="sxs-lookup"><span data-stu-id="44bc3-135">**To add a webhook action**</span></span>

1. <span data-ttu-id="44bc3-136">選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="44bc3-136">Choose **New Step** > **Add an action**.</span></span>

2. <span data-ttu-id="44bc3-137">在搜尋方塊中，輸入 "webhook" 以找出 **HTTP Webhook** 動作。</span><span class="sxs-lookup"><span data-stu-id="44bc3-137">In the search box, type "webhook" to find the **HTTP Webhook** action.</span></span>

    ![選取查詢動作](./media/connectors-native-webhook/using-action-1.png)

3. <span data-ttu-id="44bc3-139">填入 webhook 訂閱和取消訂閱呼叫的參數</span><span class="sxs-lookup"><span data-stu-id="44bc3-139">Fill in the parameters for the webhook subscribe and unsubscribe calls</span></span>

   <span data-ttu-id="44bc3-140">此步驟所遵循的模式與 [HTTP 動作](connectors-native-http.md)格式相同。</span><span class="sxs-lookup"><span data-stu-id="44bc3-140">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![完整查詢動作](./media/connectors-native-webhook/using-action-2.png)
   
   <span data-ttu-id="44bc3-142">在執行階段中，邏輯應用程式會進行該步驟之後呼叫訂閱端點。</span><span class="sxs-lookup"><span data-stu-id="44bc3-142">At runtime, the logic app calls the subscribe endpoint after reaching that step.</span></span>

4. <span data-ttu-id="44bc3-143">按一下 [儲存] 來發佈邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="44bc3-143">Click **Save** to publish the logic app.</span></span>

## <a name="technical-details"></a><span data-ttu-id="44bc3-144">技術詳細資訊</span><span class="sxs-lookup"><span data-stu-id="44bc3-144">Technical details</span></span>

<span data-ttu-id="44bc3-145">以下是更多關於 webhook 支援的觸發程序和動作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="44bc3-145">Here are more details about the triggers and actions that webhook supports.</span></span>

## <a name="webhook-triggers"></a><span data-ttu-id="44bc3-146">WebHook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="44bc3-146">Webhook triggers</span></span>

| <span data-ttu-id="44bc3-147">動作</span><span class="sxs-lookup"><span data-stu-id="44bc3-147">Action</span></span> | <span data-ttu-id="44bc3-148">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44bc3-149">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="44bc3-149">HTTP Webhook</span></span> |<span data-ttu-id="44bc3-150">訂閱服務的回呼 URL，就能視需要呼叫該 URL 以觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="44bc3-150">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span> |

### <a name="trigger-details"></a><span data-ttu-id="44bc3-151">觸發程序詳細資料</span><span class="sxs-lookup"><span data-stu-id="44bc3-151">Trigger details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="44bc3-152">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="44bc3-152">HTTP Webhook</span></span>

<span data-ttu-id="44bc3-153">訂閱服務的回呼 URL，就能視需要呼叫該 URL 以觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="44bc3-153">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span>
<span data-ttu-id="44bc3-154">代表必要欄位 * 。</span><span class="sxs-lookup"><span data-stu-id="44bc3-154">An * means required field.</span></span>

| <span data-ttu-id="44bc3-155">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-155">Display Name</span></span> | <span data-ttu-id="44bc3-156">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-156">Property Name</span></span> | <span data-ttu-id="44bc3-157">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44bc3-158">訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="44bc3-158">Subscribe Method*</span></span> |<span data-ttu-id="44bc3-159">方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-159">method</span></span> |<span data-ttu-id="44bc3-160">用於訂閱要求的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-160">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="44bc3-161">訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="44bc3-161">Subscribe URI*</span></span> |<span data-ttu-id="44bc3-162">uri</span><span class="sxs-lookup"><span data-stu-id="44bc3-162">uri</span></span> |<span data-ttu-id="44bc3-163">用於訂閱要求的 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="44bc3-163">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="44bc3-164">取消訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="44bc3-164">Unsubscribe Method*</span></span> |<span data-ttu-id="44bc3-165">方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-165">method</span></span> |<span data-ttu-id="44bc3-166">用於取消訂閱要求的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-166">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="44bc3-167">取消訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="44bc3-167">Unsubscribe URI*</span></span> |<span data-ttu-id="44bc3-168">uri</span><span class="sxs-lookup"><span data-stu-id="44bc3-168">uri</span></span> |<span data-ttu-id="44bc3-169">用於取消訂閱要求的 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="44bc3-169">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="44bc3-170">訂閱本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-170">Subscribe Body</span></span> |<span data-ttu-id="44bc3-171">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-171">body</span></span> |<span data-ttu-id="44bc3-172">訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-172">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="44bc3-173">訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-173">Subscribe Headers</span></span> |<span data-ttu-id="44bc3-174">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-174">headers</span></span> |<span data-ttu-id="44bc3-175">訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-175">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="44bc3-176">訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-176">Subscribe Authentication</span></span> |<span data-ttu-id="44bc3-177">驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-177">authentication</span></span> |<span data-ttu-id="44bc3-178">訂閱要使用的 HTTP 驗證。</span><span class="sxs-lookup"><span data-stu-id="44bc3-178">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="44bc3-179">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="44bc3-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="44bc3-180">取消訂閱頁面</span><span class="sxs-lookup"><span data-stu-id="44bc3-180">Unsubscribe Body</span></span> |<span data-ttu-id="44bc3-181">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-181">body</span></span> |<span data-ttu-id="44bc3-182">取消訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-182">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="44bc3-183">取消訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-183">Unsubscribe Headers</span></span> |<span data-ttu-id="44bc3-184">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-184">headers</span></span> |<span data-ttu-id="44bc3-185">取消訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-185">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="44bc3-186">取消訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-186">Unsubscribe Authentication</span></span> |<span data-ttu-id="44bc3-187">驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-187">authentication</span></span> |<span data-ttu-id="44bc3-188">取消訂閱要使用的 HTTP 驗證。</span><span class="sxs-lookup"><span data-stu-id="44bc3-188">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="44bc3-189">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="44bc3-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="44bc3-190">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="44bc3-190">**Output Details**</span></span>

<span data-ttu-id="44bc3-191">Webhook 要求</span><span class="sxs-lookup"><span data-stu-id="44bc3-191">Webhook request</span></span>

| <span data-ttu-id="44bc3-192">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-192">Property Name</span></span> | <span data-ttu-id="44bc3-193">資料類型</span><span class="sxs-lookup"><span data-stu-id="44bc3-193">Data Type</span></span> | <span data-ttu-id="44bc3-194">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44bc3-195">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-195">Headers</span></span> |<span data-ttu-id="44bc3-196">物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-196">object</span></span> |<span data-ttu-id="44bc3-197">Webhook 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-197">Webhook request headers</span></span> |
| <span data-ttu-id="44bc3-198">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-198">Body</span></span> |<span data-ttu-id="44bc3-199">物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-199">object</span></span> |<span data-ttu-id="44bc3-200">Webhook 要求物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-200">Webhook request object</span></span> |
| <span data-ttu-id="44bc3-201">狀態碼</span><span class="sxs-lookup"><span data-stu-id="44bc3-201">Status Code</span></span> |<span data-ttu-id="44bc3-202">int</span><span class="sxs-lookup"><span data-stu-id="44bc3-202">int</span></span> |<span data-ttu-id="44bc3-203">Webhook 要求狀態碼</span><span class="sxs-lookup"><span data-stu-id="44bc3-203">Webhook request status code</span></span> |

## <a name="webhook-actions"></a><span data-ttu-id="44bc3-204">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="44bc3-204">Webhook actions</span></span>

| <span data-ttu-id="44bc3-205">動作</span><span class="sxs-lookup"><span data-stu-id="44bc3-205">Action</span></span> | <span data-ttu-id="44bc3-206">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44bc3-207">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="44bc3-207">HTTP Webhook</span></span> |<span data-ttu-id="44bc3-208">訂閱服務的回呼 URL，就能視需要呼叫繼續工作流程步驟的 URL。</span><span class="sxs-lookup"><span data-stu-id="44bc3-208">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span> |

### <a name="action-details"></a><span data-ttu-id="44bc3-209">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="44bc3-209">Action details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="44bc3-210">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="44bc3-210">HTTP Webhook</span></span>

<span data-ttu-id="44bc3-211">訂閱服務的回呼 URL，就能視需要呼叫繼續工作流程步驟的 URL。</span><span class="sxs-lookup"><span data-stu-id="44bc3-211">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span>
<span data-ttu-id="44bc3-212">代表必要欄位 * 。</span><span class="sxs-lookup"><span data-stu-id="44bc3-212">An * means required field.</span></span>

| <span data-ttu-id="44bc3-213">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-213">Display Name</span></span> | <span data-ttu-id="44bc3-214">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-214">Property Name</span></span> | <span data-ttu-id="44bc3-215">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44bc3-216">訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="44bc3-216">Subscribe Method*</span></span> |<span data-ttu-id="44bc3-217">方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-217">method</span></span> |<span data-ttu-id="44bc3-218">用於訂閱要求的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-218">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="44bc3-219">訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="44bc3-219">Subscribe URI*</span></span> |<span data-ttu-id="44bc3-220">uri</span><span class="sxs-lookup"><span data-stu-id="44bc3-220">uri</span></span> |<span data-ttu-id="44bc3-221">用於訂閱要求的 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="44bc3-221">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="44bc3-222">取消訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="44bc3-222">Unsubscribe Method*</span></span> |<span data-ttu-id="44bc3-223">方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-223">method</span></span> |<span data-ttu-id="44bc3-224">用於取消訂閱要求的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="44bc3-224">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="44bc3-225">取消訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="44bc3-225">Unsubscribe URI*</span></span> |<span data-ttu-id="44bc3-226">uri</span><span class="sxs-lookup"><span data-stu-id="44bc3-226">uri</span></span> |<span data-ttu-id="44bc3-227">用於取消訂閱要求的 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="44bc3-227">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="44bc3-228">訂閱本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-228">Subscribe Body</span></span> |<span data-ttu-id="44bc3-229">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-229">body</span></span> |<span data-ttu-id="44bc3-230">訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-230">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="44bc3-231">訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-231">Subscribe Headers</span></span> |<span data-ttu-id="44bc3-232">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-232">headers</span></span> |<span data-ttu-id="44bc3-233">訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-233">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="44bc3-234">訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-234">Subscribe Authentication</span></span> |<span data-ttu-id="44bc3-235">驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-235">authentication</span></span> |<span data-ttu-id="44bc3-236">訂閱要使用的 HTTP 驗證。</span><span class="sxs-lookup"><span data-stu-id="44bc3-236">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="44bc3-237">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="44bc3-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="44bc3-238">取消訂閱頁面</span><span class="sxs-lookup"><span data-stu-id="44bc3-238">Unsubscribe Body</span></span> |<span data-ttu-id="44bc3-239">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-239">body</span></span> |<span data-ttu-id="44bc3-240">取消訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="44bc3-240">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="44bc3-241">取消訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-241">Unsubscribe Headers</span></span> |<span data-ttu-id="44bc3-242">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-242">headers</span></span> |<span data-ttu-id="44bc3-243">取消訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-243">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="44bc3-244">取消訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-244">Unsubscribe Authentication</span></span> |<span data-ttu-id="44bc3-245">驗證</span><span class="sxs-lookup"><span data-stu-id="44bc3-245">authentication</span></span> |<span data-ttu-id="44bc3-246">取消訂閱要使用的 HTTP 驗證。</span><span class="sxs-lookup"><span data-stu-id="44bc3-246">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="44bc3-247">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="44bc3-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="44bc3-248">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="44bc3-248">**Output Details**</span></span>

<span data-ttu-id="44bc3-249">Webhook 要求</span><span class="sxs-lookup"><span data-stu-id="44bc3-249">Webhook request</span></span>

| <span data-ttu-id="44bc3-250">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="44bc3-250">Property Name</span></span> | <span data-ttu-id="44bc3-251">資料類型</span><span class="sxs-lookup"><span data-stu-id="44bc3-251">Data Type</span></span> | <span data-ttu-id="44bc3-252">說明</span><span class="sxs-lookup"><span data-stu-id="44bc3-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44bc3-253">headers</span><span class="sxs-lookup"><span data-stu-id="44bc3-253">Headers</span></span> |<span data-ttu-id="44bc3-254">物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-254">object</span></span> |<span data-ttu-id="44bc3-255">Webhook 要求標頭</span><span class="sxs-lookup"><span data-stu-id="44bc3-255">Webhook request headers</span></span> |
| <span data-ttu-id="44bc3-256">body</span><span class="sxs-lookup"><span data-stu-id="44bc3-256">Body</span></span> |<span data-ttu-id="44bc3-257">物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-257">object</span></span> |<span data-ttu-id="44bc3-258">Webhook 要求物件</span><span class="sxs-lookup"><span data-stu-id="44bc3-258">Webhook request object</span></span> |
| <span data-ttu-id="44bc3-259">狀態碼</span><span class="sxs-lookup"><span data-stu-id="44bc3-259">Status Code</span></span> |<span data-ttu-id="44bc3-260">int</span><span class="sxs-lookup"><span data-stu-id="44bc3-260">int</span></span> |<span data-ttu-id="44bc3-261">Webhook 要求狀態碼</span><span class="sxs-lookup"><span data-stu-id="44bc3-261">Webhook request status code</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44bc3-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44bc3-262">Next steps</span></span>

* [<span data-ttu-id="44bc3-263">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="44bc3-263">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="44bc3-264">尋找其他連接器</span><span class="sxs-lookup"><span data-stu-id="44bc3-264">Find other connectors</span></span>](apis-list.md)