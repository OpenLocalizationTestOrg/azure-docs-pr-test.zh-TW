---
title: "aaaUse 要求和回應動作 |Microsoft 文件"
description: "Hello 要求和回應觸發程序和動作中的 Azure 邏輯應用程式概觀"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="ffaa6-103">開始使用 hello 要求和回應的元件</span><span class="sxs-lookup"><span data-stu-id="ffaa6-103">Get started with hello request and response components</span></span>
<span data-ttu-id="ffaa6-104">Hello 要求和回應中元件的邏輯應用程式，您可以在即時 tooevents 回覆。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="ffaa6-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="ffaa6-105">For example, you can:</span></span>

* <span data-ttu-id="ffaa6-106">從內部部署的資料庫邏輯應用程式透過回應 tooan 含有資料的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="ffaa6-107">從外部 Webhook 事件觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="ffaa6-108">從另一個邏輯應用程式內使用要求和回應動作呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="ffaa6-109">請參閱 < 開始使用邏輯應用程式中的 hello 要求和回應動作的 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="ffaa6-110">使用 hello HTTP 要求的觸發程序</span><span class="sxs-lookup"><span data-stu-id="ffaa6-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="ffaa6-111">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="ffaa6-112">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="ffaa6-113">以下是如何設定 HTTP tooset 要求 hello 邏輯應用程式的設計工具中的範例順序。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="ffaa6-114">加入 hello 觸發程序**要求-當 HTTP 要求**邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="ffaa6-115">您可以選擇性地提供 JSON 結構描述 (使用這類工具[JSONSchema.net](http://jsonschema.net)) hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="ffaa6-116">這可以讓 hello HTTP 要求內容的 hello 設計工具 toogenerate 權杖。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="ffaa6-117">加入另一個動作，讓您可以將儲存 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="ffaa6-118">在儲存之後 hello 邏輯應用程式，您可以從 hello 要求卡取得 hello HTTP 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="ffaa6-119">HTTP POST (您可以使用這類工具[郵差](https://www.getpostman.com/)) toohello URL 觸發程序 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="ffaa6-120">如果您未定義的回應動作， `202 ACCEPTED` toohello 呼叫立即傳回回應。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="ffaa6-121">您可以使用 hello 回應動作 toocustomize 回應。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![回應觸發程序](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="ffaa6-123">使用 hello HTTP 回應動作</span><span class="sxs-lookup"><span data-stu-id="ffaa6-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="ffaa6-124">當您使用的 HTTP 要求所觸發工作流程中才有效 hello HTTP 回應的動作。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="ffaa6-125">如果您未定義的回應動作， `202 ACCEPTED` toohello 呼叫立即傳回回應。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="ffaa6-126">您可以加入回應動作的 hello 工作流程內的任何步驟。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="ffaa6-127">hello 邏輯應用程式只會保留 hello 連入要求開啟之回應的一分鐘。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="ffaa6-128">在一分鐘，如果沒有回應傳送 hello 工作流程 （和回應動作存在 hello 定義中） 後,`504 GATEWAY TIMEOUT`傳回 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="ffaa6-129">以下是如何 tooadd HTTP 回應動作：</span><span class="sxs-lookup"><span data-stu-id="ffaa6-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="ffaa6-130">選取 hello**新步驟** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="ffaa6-131">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ffaa6-132">在 hello 動作搜尋方塊中，輸入**回應**toolist hello 回應動作。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![選取 hello 回應動作](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="ffaa6-134">新增任何所需的 hello HTTP 回應訊息的參數。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![完整的 hello 回應動作](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="ffaa6-136">按一下 hello 左上角 hello 工具列 toosave 和您邏輯應用程式會同時將儲存並發行 （啟動）。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="ffaa6-137">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="ffaa6-137">Request trigger</span></span>
<span data-ttu-id="ffaa6-138">以下是 hello hello 觸發程序，此連接器支援的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="ffaa6-139">只有一個要求觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-139">There is a single request trigger.</span></span>

| <span data-ttu-id="ffaa6-140">觸發程序</span><span class="sxs-lookup"><span data-stu-id="ffaa6-140">Trigger</span></span> | <span data-ttu-id="ffaa6-141">說明</span><span class="sxs-lookup"><span data-stu-id="ffaa6-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffaa6-142">要求</span><span class="sxs-lookup"><span data-stu-id="ffaa6-142">Request</span></span> |<span data-ttu-id="ffaa6-143">收到 HTTP 要求時發生</span><span class="sxs-lookup"><span data-stu-id="ffaa6-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="ffaa6-144">回應動作</span><span class="sxs-lookup"><span data-stu-id="ffaa6-144">Response action</span></span>
<span data-ttu-id="ffaa6-145">以下是此連接器支援的 hello 動作的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="ffaa6-146">只有一個回應動作，此動作只能在伴隨要求觸發程序時使用。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="ffaa6-147">動作</span><span class="sxs-lookup"><span data-stu-id="ffaa6-147">Action</span></span> | <span data-ttu-id="ffaa6-148">說明</span><span class="sxs-lookup"><span data-stu-id="ffaa6-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffaa6-149">Response</span><span class="sxs-lookup"><span data-stu-id="ffaa6-149">Response</span></span> |<span data-ttu-id="ffaa6-150">傳回回應 toohello 相互關聯的 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="ffaa6-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="ffaa6-151">觸發程序和動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="ffaa6-151">Trigger and action details</span></span>
<span data-ttu-id="ffaa6-152">hello 下列資料表描述 hello 輸入的欄位 hello 觸發程序和動作，並 hello 對應的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="ffaa6-153">要求觸發程序</span><span class="sxs-lookup"><span data-stu-id="ffaa6-153">Request trigger</span></span>
<span data-ttu-id="ffaa6-154">hello 以下是 hello 觸發程序，從傳入的 HTTP 要求的輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="ffaa6-155">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="ffaa6-155">Display name</span></span> | <span data-ttu-id="ffaa6-156">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ffaa6-156">Property name</span></span> | <span data-ttu-id="ffaa6-157">說明</span><span class="sxs-lookup"><span data-stu-id="ffaa6-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffaa6-158">JSON 結構描述</span><span class="sxs-lookup"><span data-stu-id="ffaa6-158">JSON Schema</span></span> |<span data-ttu-id="ffaa6-159">結構描述</span><span class="sxs-lookup"><span data-stu-id="ffaa6-159">schema</span></span> |<span data-ttu-id="ffaa6-160">hello hello HTTP 要求主體的 JSON 結構描述</span><span class="sxs-lookup"><span data-stu-id="ffaa6-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="ffaa6-161">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="ffaa6-161">**Output details**</span></span>

<span data-ttu-id="ffaa6-162">hello 如下 hello 要求的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="ffaa6-163">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ffaa6-163">Property name</span></span> | <span data-ttu-id="ffaa6-164">資料類型</span><span class="sxs-lookup"><span data-stu-id="ffaa6-164">Data type</span></span> | <span data-ttu-id="ffaa6-165">說明</span><span class="sxs-lookup"><span data-stu-id="ffaa6-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffaa6-166">headers</span><span class="sxs-lookup"><span data-stu-id="ffaa6-166">Headers</span></span> |<span data-ttu-id="ffaa6-167">物件</span><span class="sxs-lookup"><span data-stu-id="ffaa6-167">object</span></span> |<span data-ttu-id="ffaa6-168">要求標頭</span><span class="sxs-lookup"><span data-stu-id="ffaa6-168">Request headers</span></span> |
| <span data-ttu-id="ffaa6-169">內文</span><span class="sxs-lookup"><span data-stu-id="ffaa6-169">Body</span></span> |<span data-ttu-id="ffaa6-170">物件</span><span class="sxs-lookup"><span data-stu-id="ffaa6-170">object</span></span> |<span data-ttu-id="ffaa6-171">要求物件</span><span class="sxs-lookup"><span data-stu-id="ffaa6-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="ffaa6-172">回應動作</span><span class="sxs-lookup"><span data-stu-id="ffaa6-172">Response action</span></span>
<span data-ttu-id="ffaa6-173">hello 如下 hello HTTP 回應動作的輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="ffaa6-174">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="ffaa6-175">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="ffaa6-175">Display name</span></span> | <span data-ttu-id="ffaa6-176">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ffaa6-176">Property name</span></span> | <span data-ttu-id="ffaa6-177">說明</span><span class="sxs-lookup"><span data-stu-id="ffaa6-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffaa6-178">狀態碼 *</span><span class="sxs-lookup"><span data-stu-id="ffaa6-178">Status Code*</span></span> |<span data-ttu-id="ffaa6-179">StatusCode</span><span class="sxs-lookup"><span data-stu-id="ffaa6-179">statusCode</span></span> |<span data-ttu-id="ffaa6-180">hello HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="ffaa6-180">hello HTTP status code</span></span> |
| <span data-ttu-id="ffaa6-181">headers</span><span class="sxs-lookup"><span data-stu-id="ffaa6-181">Headers</span></span> |<span data-ttu-id="ffaa6-182">headers</span><span class="sxs-lookup"><span data-stu-id="ffaa6-182">headers</span></span> |<span data-ttu-id="ffaa6-183">JSON 物件的任何回應標頭 tooinclude</span><span class="sxs-lookup"><span data-stu-id="ffaa6-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="ffaa6-184">內文</span><span class="sxs-lookup"><span data-stu-id="ffaa6-184">Body</span></span> |<span data-ttu-id="ffaa6-185">body</span><span class="sxs-lookup"><span data-stu-id="ffaa6-185">body</span></span> |<span data-ttu-id="ffaa6-186">hello 回應主體</span><span class="sxs-lookup"><span data-stu-id="ffaa6-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ffaa6-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ffaa6-187">Next steps</span></span>
<span data-ttu-id="ffaa6-188">現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ffaa6-189">您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaa6-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

