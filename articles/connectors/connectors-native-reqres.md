---
title: "使用要求和回應動作 | Microsoft Docs"
description: "Azure 邏輯應用程式中要求和回應之觸發程序與動作的概觀"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="e7774-103">開始使用要求和回應元件</span><span class="sxs-lookup"><span data-stu-id="e7774-103">Get started with the request and response components</span></span>
<span data-ttu-id="e7774-104">透過邏輯應用程式中的要求和回應元件，您可以即時回應事件。</span><span class="sxs-lookup"><span data-stu-id="e7774-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="e7774-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="e7774-105">For example, you can:</span></span>

* <span data-ttu-id="e7774-106">透過邏輯應用程式使用內部部署資料庫中的資料回應 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="e7774-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="e7774-107">從外部 Webhook 事件觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7774-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="e7774-108">從另一個邏輯應用程式內使用要求和回應動作呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7774-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="e7774-109">若要使用邏輯應用程式中的要求和回應動作來開始作業，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e7774-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="e7774-110">使用 HTTP 要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7774-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="e7774-111">觸發程序是一個事件，可用來啟動邏輯應用程式中定義的工作流程。</span><span class="sxs-lookup"><span data-stu-id="e7774-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="e7774-112">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e7774-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="e7774-113">以下是如何在邏輯應用程式設計工具中設定 HTTP 要求的範例順序。</span><span class="sxs-lookup"><span data-stu-id="e7774-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="e7774-114">將 [要求 - 收到 HTTP 要求時]  觸發程序新增到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7774-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="e7774-115">您可以選擇性地提供 JSON 結構描述 (透過使用 [JSONSchema.net](http://jsonschema.net)之類的工具) 來做為要求本文。</span><span class="sxs-lookup"><span data-stu-id="e7774-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="e7774-116">這可讓設計工具在 HTTP 要求中產生屬性的權杖。</span><span class="sxs-lookup"><span data-stu-id="e7774-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="e7774-117">新增另一個動作以儲存邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7774-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="e7774-118">在儲存邏輯應用程式之後，您可以從要求卡片取得 HTTP 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="e7774-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="e7774-119">針對 URL 的 HTTP POST (您可以使用 [Postman](https://www.getpostman.com/)之類的工具) 會觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7774-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="e7774-120">如果您未定義回應動作，系統會立即將 `202 ACCEPTED` 回應傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="e7774-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="e7774-121">您可以使用回應動作以自訂回應。</span><span class="sxs-lookup"><span data-stu-id="e7774-121">You can use the response action to customize a response.</span></span>
> 
> 

![回應觸發程序](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="e7774-123">使用 HTTP 回應動作</span><span class="sxs-lookup"><span data-stu-id="e7774-123">Use the HTTP Response action</span></span>
<span data-ttu-id="e7774-124">HTTP 回應動作只適用於在 HTTP 要求所觸發的工作流程中使用時。</span><span class="sxs-lookup"><span data-stu-id="e7774-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="e7774-125">如果您未定義回應動作，系統會立即將 `202 ACCEPTED` 回應傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="e7774-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="e7774-126">您可以在工作流程的任何步驟新增回應動作。</span><span class="sxs-lookup"><span data-stu-id="e7774-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="e7774-127">邏輯應用程式只會讓連入要求針對回應開放一分鐘。</span><span class="sxs-lookup"><span data-stu-id="e7774-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="e7774-128">一分鐘後，如果工作流程未傳送任何回應 (且定義中存在回應動作)，則系統會將 `504 GATEWAY TIMEOUT` 傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="e7774-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="e7774-129">以下是新增 HTTP 回應動作的方法︰</span><span class="sxs-lookup"><span data-stu-id="e7774-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="e7774-130">選取 [新增步驟]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e7774-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="e7774-131">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="e7774-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e7774-132">在動作搜尋方塊中，輸入 **回應** 以列出回應動作。</span><span class="sxs-lookup"><span data-stu-id="e7774-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![選取回應動作](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="e7774-134">新增 HTTP 回應訊息所需的任何參數。</span><span class="sxs-lookup"><span data-stu-id="e7774-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![完成回應動作](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="e7774-136">按一下工具列左上角以便儲存，然後邏輯應用程式便會儲存並發佈 (啟動)。</span><span class="sxs-lookup"><span data-stu-id="e7774-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="e7774-137">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7774-137">Request trigger</span></span>
<span data-ttu-id="e7774-138">以下是此連接器所支援觸發程序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7774-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="e7774-139">只有一個要求觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e7774-139">There is a single request trigger.</span></span>

| <span data-ttu-id="e7774-140">觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7774-140">Trigger</span></span> | <span data-ttu-id="e7774-141">說明</span><span class="sxs-lookup"><span data-stu-id="e7774-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7774-142">要求</span><span class="sxs-lookup"><span data-stu-id="e7774-142">Request</span></span> |<span data-ttu-id="e7774-143">收到 HTTP 要求時發生</span><span class="sxs-lookup"><span data-stu-id="e7774-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="e7774-144">回應動作</span><span class="sxs-lookup"><span data-stu-id="e7774-144">Response action</span></span>
<span data-ttu-id="e7774-145">以下是此連接器所支援動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7774-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="e7774-146">只有一個回應動作，此動作只能在伴隨要求觸發程序時使用。</span><span class="sxs-lookup"><span data-stu-id="e7774-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="e7774-147">動作</span><span class="sxs-lookup"><span data-stu-id="e7774-147">Action</span></span> | <span data-ttu-id="e7774-148">說明</span><span class="sxs-lookup"><span data-stu-id="e7774-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7774-149">回應</span><span class="sxs-lookup"><span data-stu-id="e7774-149">Response</span></span> |<span data-ttu-id="e7774-150">傳回相互關聯的 HTTP 要求的回應</span><span class="sxs-lookup"><span data-stu-id="e7774-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="e7774-151">觸發程序和動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="e7774-151">Trigger and action details</span></span>
<span data-ttu-id="e7774-152">下表描述觸發程序和動作的輸入欄位，以及對應的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7774-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="e7774-153">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7774-153">Request trigger</span></span>
<span data-ttu-id="e7774-154">以下是傳入 HTTP 要求之觸發程序的輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="e7774-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="e7774-155">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="e7774-155">Display name</span></span> | <span data-ttu-id="e7774-156">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e7774-156">Property name</span></span> | <span data-ttu-id="e7774-157">說明</span><span class="sxs-lookup"><span data-stu-id="e7774-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7774-158">JSON 結構描述</span><span class="sxs-lookup"><span data-stu-id="e7774-158">JSON Schema</span></span> |<span data-ttu-id="e7774-159">結構描述</span><span class="sxs-lookup"><span data-stu-id="e7774-159">schema</span></span> |<span data-ttu-id="e7774-160">HTTP 要求本文的 JSON 結構描述</span><span class="sxs-lookup"><span data-stu-id="e7774-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="e7774-161">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="e7774-161">**Output details**</span></span>

<span data-ttu-id="e7774-162">以下是要求的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7774-162">The following are output details for the request.</span></span>

| <span data-ttu-id="e7774-163">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e7774-163">Property name</span></span> | <span data-ttu-id="e7774-164">資料類型</span><span class="sxs-lookup"><span data-stu-id="e7774-164">Data type</span></span> | <span data-ttu-id="e7774-165">說明</span><span class="sxs-lookup"><span data-stu-id="e7774-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7774-166">headers</span><span class="sxs-lookup"><span data-stu-id="e7774-166">Headers</span></span> |<span data-ttu-id="e7774-167">物件</span><span class="sxs-lookup"><span data-stu-id="e7774-167">object</span></span> |<span data-ttu-id="e7774-168">要求標頭</span><span class="sxs-lookup"><span data-stu-id="e7774-168">Request headers</span></span> |
| <span data-ttu-id="e7774-169">內文</span><span class="sxs-lookup"><span data-stu-id="e7774-169">Body</span></span> |<span data-ttu-id="e7774-170">物件</span><span class="sxs-lookup"><span data-stu-id="e7774-170">object</span></span> |<span data-ttu-id="e7774-171">要求物件</span><span class="sxs-lookup"><span data-stu-id="e7774-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="e7774-172">回應動作</span><span class="sxs-lookup"><span data-stu-id="e7774-172">Response action</span></span>
<span data-ttu-id="e7774-173">以下是 HTTP 回應動作的輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="e7774-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="e7774-174">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="e7774-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="e7774-175">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="e7774-175">Display name</span></span> | <span data-ttu-id="e7774-176">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e7774-176">Property name</span></span> | <span data-ttu-id="e7774-177">說明</span><span class="sxs-lookup"><span data-stu-id="e7774-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7774-178">狀態碼 *</span><span class="sxs-lookup"><span data-stu-id="e7774-178">Status Code*</span></span> |<span data-ttu-id="e7774-179">StatusCode</span><span class="sxs-lookup"><span data-stu-id="e7774-179">statusCode</span></span> |<span data-ttu-id="e7774-180">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="e7774-180">The HTTP status code</span></span> |
| <span data-ttu-id="e7774-181">標頭</span><span class="sxs-lookup"><span data-stu-id="e7774-181">Headers</span></span> |<span data-ttu-id="e7774-182">標頭</span><span class="sxs-lookup"><span data-stu-id="e7774-182">headers</span></span> |<span data-ttu-id="e7774-183">要包含的任何回應標頭的 JSON 物件</span><span class="sxs-lookup"><span data-stu-id="e7774-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="e7774-184">內文</span><span class="sxs-lookup"><span data-stu-id="e7774-184">Body</span></span> |<span data-ttu-id="e7774-185">內文</span><span class="sxs-lookup"><span data-stu-id="e7774-185">body</span></span> |<span data-ttu-id="e7774-186">回應本文</span><span class="sxs-lookup"><span data-stu-id="e7774-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e7774-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7774-187">Next steps</span></span>
<span data-ttu-id="e7774-188">立即試用平台和 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e7774-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e7774-189">您可以查看我們的 [API 清單](apis-list.md)，以探索邏輯應用程式中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="e7774-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

