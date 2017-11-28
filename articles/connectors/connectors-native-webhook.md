---
title: "Azure 邏輯應用程式的 aaaWebhook 連接器 |Microsoft 文件"
description: "Toouse webhook 動作和觸發程序 tooperform 動作要如何篩選陣列從邏輯應用程式"
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
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a><span data-ttu-id="92da1-103">開始使用 hello webhook 連接器</span><span class="sxs-lookup"><span data-stu-id="92da1-103">Get started with hello webhook connector</span></span>

<span data-ttu-id="92da1-104">Hello webhook 動作以及觸發程序，您可以啟動、 暫停和繼續流程 tooperform 這些工作：</span><span class="sxs-lookup"><span data-stu-id="92da1-104">With hello webhook action and trigger, you can start, pause, and resume flows tooperform these tasks:</span></span>

* <span data-ttu-id="92da1-105">收到項目時，即從 [Azure 事件中樞](https://github.com/logicappsio/EventHubAPI) 觸發</span><span class="sxs-lookup"><span data-stu-id="92da1-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span></span>
* <span data-ttu-id="92da1-106">等待核准再繼續工作流程</span><span class="sxs-lookup"><span data-stu-id="92da1-106">Wait for an approval before continuing a workflow</span></span>

<span data-ttu-id="92da1-107">深入了解[如何 toocreate 自訂應用程式開發介面支援 webhook](../logic-apps/logic-apps-create-api-app.md)。</span><span class="sxs-lookup"><span data-stu-id="92da1-107">Learn more about [how toocreate custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="use-hello-webhook-trigger"></a><span data-ttu-id="92da1-108">使用 hello webhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="92da1-108">Use hello webhook trigger</span></span>

<span data-ttu-id="92da1-109">[觸發程序](connectors-overview.md)是啟動邏輯應用程式工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="92da1-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span></span> <span data-ttu-id="92da1-110">webhook 觸發程序是以事件為基礎，而不是依賴對新項目進行輪詢。</span><span class="sxs-lookup"><span data-stu-id="92da1-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span></span> <span data-ttu-id="92da1-111">像 hello[要求觸發程序](connectors-native-reqres.md)，hello 邏輯應用程式引發 hello 即時事件發生時。</span><span class="sxs-lookup"><span data-stu-id="92da1-111">Like hello [request trigger](connectors-native-reqres.md), hello logic app fires hello instant that an event happens.</span></span> <span data-ttu-id="92da1-112">hello webhook 觸發程序註冊*回呼 URL* tooa 服務，並使用該 URL toofire hello 邏輯應用程式做為所需。</span><span class="sxs-lookup"><span data-stu-id="92da1-112">hello webhook trigger registers a *callback URL* tooa service and uses that URL toofire hello logic app as needed.</span></span>

<span data-ttu-id="92da1-113">以下是示範向上 HTTP tooset 觸發程序在 hello 邏輯應用程式的設計工具中的範例。</span><span class="sxs-lookup"><span data-stu-id="92da1-113">Here's an example that shows how tooset up an HTTP trigger in hello Logic App Designer.</span></span> <span data-ttu-id="92da1-114">hello 步驟假設您已部署或正在存取的 API，遵循 hello [webhook 訂閱及取消訂閱中的 logic apps 模式](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)。</span><span class="sxs-lookup"><span data-stu-id="92da1-114">hello steps assume that you have already deployed or are accessing an API that follows hello [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span></span> <span data-ttu-id="92da1-115">hello 訂閱呼叫每當邏輯應用程式不會儲存具有新的 webhook，或從已停用 tooenabled 切換時建立。</span><span class="sxs-lookup"><span data-stu-id="92da1-115">hello subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled tooenabled.</span></span> <span data-ttu-id="92da1-116">hello 取消訂閱呼叫移除並儲存，或從已啟用 toodisabled 切換邏輯應用程式 webhook 觸發程序時進行。</span><span class="sxs-lookup"><span data-stu-id="92da1-116">hello unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled toodisabled.</span></span>

<span data-ttu-id="92da1-117">**tooadd hello webhook 觸發程序**</span><span class="sxs-lookup"><span data-stu-id="92da1-117">**tooadd hello webhook trigger**</span></span>

1. <span data-ttu-id="92da1-118">新增 hello **HTTP Webhook** hello 邏輯應用程式中的第一個步驟的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="92da1-118">Add hello **HTTP Webhook** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="92da1-119">填寫 hello 參數，如 hello webhook 訂閱及取消訂閱的呼叫。</span><span class="sxs-lookup"><span data-stu-id="92da1-119">Fill in hello parameters for hello webhook subscribe and unsubscribe calls.</span></span>

   <span data-ttu-id="92da1-120">此步驟會遵循相同模式為 hello hello [HTTP 動作](connectors-native-http.md)格式。</span><span class="sxs-lookup"><span data-stu-id="92da1-120">This step follows hello same pattern as hello [HTTP action](connectors-native-http.md) format.</span></span>

     ![HTTP 觸發程序](./media/connectors-native-webhook/using-trigger.png)

3. <span data-ttu-id="92da1-122">加入至少一個動作。</span><span class="sxs-lookup"><span data-stu-id="92da1-122">Add at least one action.</span></span>
4. <span data-ttu-id="92da1-123">按一下**儲存**toopublish hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="92da1-123">Click **Save** toopublish hello logic app.</span></span> <span data-ttu-id="92da1-124">此步驟中呼叫 hello 訂閱 hello 回呼所需的 URL tootrigger 端點此邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="92da1-124">This step calls hello subscribe endpoint with hello callback URL needed tootrigger this logic app.</span></span>
5. <span data-ttu-id="92da1-125">每當 hello 服務會`HTTP POST`toohello 回呼 URL，hello 邏輯應用程式引發，並包含傳入 hello 要求任何資料。</span><span class="sxs-lookup"><span data-stu-id="92da1-125">Whenever hello service makes an `HTTP POST` toohello callback URL, hello logic app fires, and includes any data passed into hello request.</span></span>

## <a name="use-hello-webhook-action"></a><span data-ttu-id="92da1-126">使用 hello webhook 動作</span><span class="sxs-lookup"><span data-stu-id="92da1-126">Use hello webhook action</span></span>

<span data-ttu-id="92da1-127">[*動作*](connectors-overview.md)作業由執行邏輯應用程式中定義的 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="92da1-127">An [*action*](connectors-overview.md) is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="92da1-128">Webhook 動作會註冊*回呼 URL*與服務等候直到 hello URL 會繼續進行之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="92da1-128">A webhook action registers a *callback URL* with a service and waits until hello URL is called before resuming.</span></span> <span data-ttu-id="92da1-129">hello [」 傳送核准電子郵件 」](connectors-create-api-office365-outlook.md)是連接器遵循此模式的範例。</span><span class="sxs-lookup"><span data-stu-id="92da1-129">hello ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span></span> <span data-ttu-id="92da1-130">您可以在任何服務 hello webhook 動作透過擴充此模式。</span><span class="sxs-lookup"><span data-stu-id="92da1-130">You can extend this pattern into any service through hello webhook action.</span></span> 

<span data-ttu-id="92da1-131">以下是示範如何設定中的 webhook 動作 tooset hello 邏輯應用程式的設計工具的範例。</span><span class="sxs-lookup"><span data-stu-id="92da1-131">Here's an example that shows how tooset up a webhook action in hello Logic App Designer.</span></span> <span data-ttu-id="92da1-132">這些步驟假設您已部署或正在存取的 API，遵循 hello [webhook 訂閱及取消訂閱邏輯應用程式中使用的模式](../logic-apps/logic-apps-create-api-app.md#webhook-actions)。</span><span class="sxs-lookup"><span data-stu-id="92da1-132">These steps assume that you have already deployed or are accessing an API that follows hello [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span></span> <span data-ttu-id="92da1-133">hello 訂閱呼叫邏輯應用程式執行 hello webhook 動作時進行。</span><span class="sxs-lookup"><span data-stu-id="92da1-133">hello subscribe call is made when a logic app executes hello webhook action.</span></span> <span data-ttu-id="92da1-134">hello 取消訂閱呼叫時執行取消等待回應，或應用程式逾時之前 hello 邏輯。</span><span class="sxs-lookup"><span data-stu-id="92da1-134">hello unsubscribe call is made when a run is canceled while waiting for a response, or before hello logic app times out.</span></span>

<span data-ttu-id="92da1-135">**tooadd webhook 動作**</span><span class="sxs-lookup"><span data-stu-id="92da1-135">**tooadd a webhook action**</span></span>

1. <span data-ttu-id="92da1-136">選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="92da1-136">Choose **New Step** > **Add an action**.</span></span>

2. <span data-ttu-id="92da1-137">在 [hello] 搜尋方塊中，輸入 「 webhook"toofind hello **HTTP Webhook**動作。</span><span class="sxs-lookup"><span data-stu-id="92da1-137">In hello search box, type "webhook" toofind hello **HTTP Webhook** action.</span></span>

    ![選取查詢動作](./media/connectors-native-webhook/using-action-1.png)

3. <span data-ttu-id="92da1-139">填滿 hello 參數中的 hello webhook 訂閱及取消訂閱呼叫</span><span class="sxs-lookup"><span data-stu-id="92da1-139">Fill in hello parameters for hello webhook subscribe and unsubscribe calls</span></span>

   <span data-ttu-id="92da1-140">此步驟會遵循相同模式為 hello hello [HTTP 動作](connectors-native-http.md)格式。</span><span class="sxs-lookup"><span data-stu-id="92da1-140">This step follows hello same pattern as hello [HTTP action](connectors-native-http.md) format.</span></span>

     ![完整查詢動作](./media/connectors-native-webhook/using-action-2.png)
   
   <span data-ttu-id="92da1-142">在執行階段，hello 邏輯應用程式呼叫 hello 訂閱到達該步驟之後的端點。</span><span class="sxs-lookup"><span data-stu-id="92da1-142">At runtime, hello logic app calls hello subscribe endpoint after reaching that step.</span></span>

4. <span data-ttu-id="92da1-143">按一下**儲存**toopublish hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="92da1-143">Click **Save** toopublish hello logic app.</span></span>

## <a name="technical-details"></a><span data-ttu-id="92da1-144">技術詳細資訊</span><span class="sxs-lookup"><span data-stu-id="92da1-144">Technical details</span></span>

<span data-ttu-id="92da1-145">以下是詳細資料的 webhook 支援 hello 觸發程序及動作相關。</span><span class="sxs-lookup"><span data-stu-id="92da1-145">Here are more details about hello triggers and actions that webhook supports.</span></span>

## <a name="webhook-triggers"></a><span data-ttu-id="92da1-146">WebHook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="92da1-146">Webhook triggers</span></span>

| <span data-ttu-id="92da1-147">動作</span><span class="sxs-lookup"><span data-stu-id="92da1-147">Action</span></span> | <span data-ttu-id="92da1-148">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92da1-149">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="92da1-149">HTTP Webhook</span></span> |<span data-ttu-id="92da1-150">訂閱可以呼叫 hello URL toofire 邏輯應用程式所需的回呼 URL tooa 服務。</span><span class="sxs-lookup"><span data-stu-id="92da1-150">Subscribe a callback URL tooa service that can call hello URL toofire logic app as needed.</span></span> |

### <a name="trigger-details"></a><span data-ttu-id="92da1-151">觸發程序詳細資料</span><span class="sxs-lookup"><span data-stu-id="92da1-151">Trigger details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="92da1-152">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="92da1-152">HTTP Webhook</span></span>

<span data-ttu-id="92da1-153">訂閱可以呼叫 hello URL toofire 邏輯應用程式所需的回呼 URL tooa 服務。</span><span class="sxs-lookup"><span data-stu-id="92da1-153">Subscribe a callback URL tooa service that can call hello URL toofire logic app as needed.</span></span>
<span data-ttu-id="92da1-154">代表必要欄位 * 。</span><span class="sxs-lookup"><span data-stu-id="92da1-154">An * means required field.</span></span>

| <span data-ttu-id="92da1-155">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-155">Display Name</span></span> | <span data-ttu-id="92da1-156">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-156">Property Name</span></span> | <span data-ttu-id="92da1-157">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da1-158">訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="92da1-158">Subscribe Method*</span></span> |<span data-ttu-id="92da1-159">method</span><span class="sxs-lookup"><span data-stu-id="92da1-159">method</span></span> |<span data-ttu-id="92da1-160">訂閱要求的 HTTP 方法 toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-160">HTTP Method toouse for subscribe request</span></span> |
| <span data-ttu-id="92da1-161">訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="92da1-161">Subscribe URI*</span></span> |<span data-ttu-id="92da1-162">uri</span><span class="sxs-lookup"><span data-stu-id="92da1-162">uri</span></span> |<span data-ttu-id="92da1-163">訂閱要求的 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-163">HTTP URI toouse for subscribe request</span></span> |
| <span data-ttu-id="92da1-164">取消訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="92da1-164">Unsubscribe Method*</span></span> |<span data-ttu-id="92da1-165">method</span><span class="sxs-lookup"><span data-stu-id="92da1-165">method</span></span> |<span data-ttu-id="92da1-166">取消訂閱要求的 HTTP 方法 toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-166">HTTP method toouse for unsubscribe request</span></span> |
| <span data-ttu-id="92da1-167">取消訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="92da1-167">Unsubscribe URI*</span></span> |<span data-ttu-id="92da1-168">uri</span><span class="sxs-lookup"><span data-stu-id="92da1-168">uri</span></span> |<span data-ttu-id="92da1-169">取消訂閱要求的 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-169">HTTP URI toouse for unsubscribe request</span></span> |
| <span data-ttu-id="92da1-170">訂閱本文</span><span class="sxs-lookup"><span data-stu-id="92da1-170">Subscribe Body</span></span> |<span data-ttu-id="92da1-171">body</span><span class="sxs-lookup"><span data-stu-id="92da1-171">body</span></span> |<span data-ttu-id="92da1-172">訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="92da1-172">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="92da1-173">訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-173">Subscribe Headers</span></span> |<span data-ttu-id="92da1-174">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-174">headers</span></span> |<span data-ttu-id="92da1-175">訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-175">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="92da1-176">訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-176">Subscribe Authentication</span></span> |<span data-ttu-id="92da1-177">驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-177">authentication</span></span> |<span data-ttu-id="92da1-178">HTTP 驗證 toouse 的訂閱。</span><span class="sxs-lookup"><span data-stu-id="92da1-178">HTTP authentication toouse for subscribe.</span></span> <span data-ttu-id="92da1-179">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="92da1-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="92da1-180">取消訂閱頁面</span><span class="sxs-lookup"><span data-stu-id="92da1-180">Unsubscribe Body</span></span> |<span data-ttu-id="92da1-181">body</span><span class="sxs-lookup"><span data-stu-id="92da1-181">body</span></span> |<span data-ttu-id="92da1-182">取消訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="92da1-182">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="92da1-183">取消訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-183">Unsubscribe Headers</span></span> |<span data-ttu-id="92da1-184">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-184">headers</span></span> |<span data-ttu-id="92da1-185">取消訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-185">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="92da1-186">取消訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-186">Unsubscribe Authentication</span></span> |<span data-ttu-id="92da1-187">驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-187">authentication</span></span> |<span data-ttu-id="92da1-188">HTTP 驗證 toouse 用於取消訂閱。</span><span class="sxs-lookup"><span data-stu-id="92da1-188">HTTP authentication toouse for unsubscribe.</span></span> <span data-ttu-id="92da1-189">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="92da1-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="92da1-190">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="92da1-190">**Output Details**</span></span>

<span data-ttu-id="92da1-191">Webhook 要求</span><span class="sxs-lookup"><span data-stu-id="92da1-191">Webhook request</span></span>

| <span data-ttu-id="92da1-192">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-192">Property Name</span></span> | <span data-ttu-id="92da1-193">資料類型</span><span class="sxs-lookup"><span data-stu-id="92da1-193">Data Type</span></span> | <span data-ttu-id="92da1-194">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da1-195">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-195">Headers</span></span> |<span data-ttu-id="92da1-196">物件</span><span class="sxs-lookup"><span data-stu-id="92da1-196">object</span></span> |<span data-ttu-id="92da1-197">Webhook 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-197">Webhook request headers</span></span> |
| <span data-ttu-id="92da1-198">body</span><span class="sxs-lookup"><span data-stu-id="92da1-198">Body</span></span> |<span data-ttu-id="92da1-199">物件</span><span class="sxs-lookup"><span data-stu-id="92da1-199">object</span></span> |<span data-ttu-id="92da1-200">Webhook 要求物件</span><span class="sxs-lookup"><span data-stu-id="92da1-200">Webhook request object</span></span> |
| <span data-ttu-id="92da1-201">狀態碼</span><span class="sxs-lookup"><span data-stu-id="92da1-201">Status Code</span></span> |<span data-ttu-id="92da1-202">int</span><span class="sxs-lookup"><span data-stu-id="92da1-202">int</span></span> |<span data-ttu-id="92da1-203">Webhook 要求狀態碼</span><span class="sxs-lookup"><span data-stu-id="92da1-203">Webhook request status code</span></span> |

## <a name="webhook-actions"></a><span data-ttu-id="92da1-204">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="92da1-204">Webhook actions</span></span>

| <span data-ttu-id="92da1-205">動作</span><span class="sxs-lookup"><span data-stu-id="92da1-205">Action</span></span> | <span data-ttu-id="92da1-206">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92da1-207">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="92da1-207">HTTP Webhook</span></span> |<span data-ttu-id="92da1-208">訂閱回呼 URL tooa 服務可以呼叫 hello URL tooresume 視工作流程步驟。</span><span class="sxs-lookup"><span data-stu-id="92da1-208">Subscribe a callback URL tooa service that can call hello URL tooresume a workflow step as needed.</span></span> |

### <a name="action-details"></a><span data-ttu-id="92da1-209">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="92da1-209">Action details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="92da1-210">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="92da1-210">HTTP Webhook</span></span>

<span data-ttu-id="92da1-211">訂閱回呼 URL tooa 服務可以呼叫 hello URL tooresume 視工作流程步驟。</span><span class="sxs-lookup"><span data-stu-id="92da1-211">Subscribe a callback URL tooa service that can call hello URL tooresume a workflow step as needed.</span></span>
<span data-ttu-id="92da1-212">代表必要欄位 * 。</span><span class="sxs-lookup"><span data-stu-id="92da1-212">An * means required field.</span></span>

| <span data-ttu-id="92da1-213">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-213">Display Name</span></span> | <span data-ttu-id="92da1-214">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-214">Property Name</span></span> | <span data-ttu-id="92da1-215">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da1-216">訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="92da1-216">Subscribe Method*</span></span> |<span data-ttu-id="92da1-217">method</span><span class="sxs-lookup"><span data-stu-id="92da1-217">method</span></span> |<span data-ttu-id="92da1-218">訂閱要求的 HTTP 方法 toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-218">HTTP Method toouse for subscribe request</span></span> |
| <span data-ttu-id="92da1-219">訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="92da1-219">Subscribe URI*</span></span> |<span data-ttu-id="92da1-220">uri</span><span class="sxs-lookup"><span data-stu-id="92da1-220">uri</span></span> |<span data-ttu-id="92da1-221">訂閱要求的 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-221">HTTP URI toouse for subscribe request</span></span> |
| <span data-ttu-id="92da1-222">取消訂閱方法*</span><span class="sxs-lookup"><span data-stu-id="92da1-222">Unsubscribe Method*</span></span> |<span data-ttu-id="92da1-223">method</span><span class="sxs-lookup"><span data-stu-id="92da1-223">method</span></span> |<span data-ttu-id="92da1-224">取消訂閱要求的 HTTP 方法 toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-224">HTTP method toouse for unsubscribe request</span></span> |
| <span data-ttu-id="92da1-225">取消訂閱 URI*</span><span class="sxs-lookup"><span data-stu-id="92da1-225">Unsubscribe URI*</span></span> |<span data-ttu-id="92da1-226">uri</span><span class="sxs-lookup"><span data-stu-id="92da1-226">uri</span></span> |<span data-ttu-id="92da1-227">取消訂閱要求的 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="92da1-227">HTTP URI toouse for unsubscribe request</span></span> |
| <span data-ttu-id="92da1-228">訂閱本文</span><span class="sxs-lookup"><span data-stu-id="92da1-228">Subscribe Body</span></span> |<span data-ttu-id="92da1-229">body</span><span class="sxs-lookup"><span data-stu-id="92da1-229">body</span></span> |<span data-ttu-id="92da1-230">訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="92da1-230">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="92da1-231">訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-231">Subscribe Headers</span></span> |<span data-ttu-id="92da1-232">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-232">headers</span></span> |<span data-ttu-id="92da1-233">訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-233">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="92da1-234">訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-234">Subscribe Authentication</span></span> |<span data-ttu-id="92da1-235">驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-235">authentication</span></span> |<span data-ttu-id="92da1-236">HTTP 驗證 toouse 的訂閱。</span><span class="sxs-lookup"><span data-stu-id="92da1-236">HTTP authentication toouse for subscribe.</span></span> <span data-ttu-id="92da1-237">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="92da1-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="92da1-238">取消訂閱頁面</span><span class="sxs-lookup"><span data-stu-id="92da1-238">Unsubscribe Body</span></span> |<span data-ttu-id="92da1-239">body</span><span class="sxs-lookup"><span data-stu-id="92da1-239">body</span></span> |<span data-ttu-id="92da1-240">取消訂閱的 HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="92da1-240">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="92da1-241">取消訂閱標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-241">Unsubscribe Headers</span></span> |<span data-ttu-id="92da1-242">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-242">headers</span></span> |<span data-ttu-id="92da1-243">取消訂閱的 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-243">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="92da1-244">取消訂閱驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-244">Unsubscribe Authentication</span></span> |<span data-ttu-id="92da1-245">驗證</span><span class="sxs-lookup"><span data-stu-id="92da1-245">authentication</span></span> |<span data-ttu-id="92da1-246">HTTP 驗證 toouse 用於取消訂閱。</span><span class="sxs-lookup"><span data-stu-id="92da1-246">HTTP authentication toouse for unsubscribe.</span></span> <span data-ttu-id="92da1-247">如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication)</span><span class="sxs-lookup"><span data-stu-id="92da1-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="92da1-248">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="92da1-248">**Output Details**</span></span>

<span data-ttu-id="92da1-249">Webhook 要求</span><span class="sxs-lookup"><span data-stu-id="92da1-249">Webhook request</span></span>

| <span data-ttu-id="92da1-250">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92da1-250">Property Name</span></span> | <span data-ttu-id="92da1-251">資料類型</span><span class="sxs-lookup"><span data-stu-id="92da1-251">Data Type</span></span> | <span data-ttu-id="92da1-252">說明</span><span class="sxs-lookup"><span data-stu-id="92da1-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92da1-253">headers</span><span class="sxs-lookup"><span data-stu-id="92da1-253">Headers</span></span> |<span data-ttu-id="92da1-254">物件</span><span class="sxs-lookup"><span data-stu-id="92da1-254">object</span></span> |<span data-ttu-id="92da1-255">Webhook 要求標頭</span><span class="sxs-lookup"><span data-stu-id="92da1-255">Webhook request headers</span></span> |
| <span data-ttu-id="92da1-256">body</span><span class="sxs-lookup"><span data-stu-id="92da1-256">Body</span></span> |<span data-ttu-id="92da1-257">物件</span><span class="sxs-lookup"><span data-stu-id="92da1-257">object</span></span> |<span data-ttu-id="92da1-258">Webhook 要求物件</span><span class="sxs-lookup"><span data-stu-id="92da1-258">Webhook request object</span></span> |
| <span data-ttu-id="92da1-259">狀態碼</span><span class="sxs-lookup"><span data-stu-id="92da1-259">Status Code</span></span> |<span data-ttu-id="92da1-260">int</span><span class="sxs-lookup"><span data-stu-id="92da1-260">int</span></span> |<span data-ttu-id="92da1-261">Webhook 要求狀態碼</span><span class="sxs-lookup"><span data-stu-id="92da1-261">Webhook request status code</span></span> |

## <a name="next-steps"></a><span data-ttu-id="92da1-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92da1-262">Next steps</span></span>

* [<span data-ttu-id="92da1-263">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="92da1-263">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="92da1-264">尋找其他連接器</span><span class="sxs-lookup"><span data-stu-id="92da1-264">Find other connectors</span></span>](apis-list.md)