---
title: "透過 HTTP - Azure Logic Apps 與任何端點通訊 | Microsoft Docs"
description: "建立可以透過 HTTP 與任何端點通訊的邏輯應用程式"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="51616-103">開始使用 HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="51616-103">Get started with the HTTP action</span></span>

<span data-ttu-id="51616-104">您可以利用 HTTP 動作來延伸組織的工作流程，並透過 HTTP 與任何端點通訊。</span><span class="sxs-lookup"><span data-stu-id="51616-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="51616-105">您可以：</span><span class="sxs-lookup"><span data-stu-id="51616-105">You can:</span></span>

* <span data-ttu-id="51616-106">建立會在您管理的網站故障時啟動 (觸發程序) 的邏輯應用程式工作流程。</span><span class="sxs-lookup"><span data-stu-id="51616-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="51616-107">透過 HTTP 與任何端點通訊，將工作流程延伸至其他服務。</span><span class="sxs-lookup"><span data-stu-id="51616-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="51616-108">若要使用邏輯應用程式中的 HTTP 動作來開始作業，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="51616-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="51616-109">使用 HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="51616-109">Use the HTTP trigger</span></span>
<span data-ttu-id="51616-110">觸發程序是一個事件，可用來啟動邏輯應用程式中定義的工作流程。</span><span class="sxs-lookup"><span data-stu-id="51616-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="51616-111">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51616-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="51616-112">以下是如何在邏輯應用程式設計工具中設定 HTTP 觸發程序的範例順序。</span><span class="sxs-lookup"><span data-stu-id="51616-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="51616-113">在邏輯應用程式中新增 HTTP 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="51616-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="51616-114">為想要輪詢的 HTTP 端點填入參數。</span><span class="sxs-lookup"><span data-stu-id="51616-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="51616-115">修改其輪詢頻率的循環間隔。</span><span class="sxs-lookup"><span data-stu-id="51616-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="51616-116">邏輯應用程式現在會在每個檢查期間傳回任何內容時引發。</span><span class="sxs-lookup"><span data-stu-id="51616-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP 觸發程序](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="51616-118">HTTP 觸發程序的運作方式</span><span class="sxs-lookup"><span data-stu-id="51616-118">How the HTTP trigger works</span></span>

<span data-ttu-id="51616-119">HTTP 觸發程序會以循環間隔呼叫 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="51616-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="51616-120">依預設，任何低於 300 的 HTTP 回應碼都會執行邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="51616-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="51616-121">若要指定是否應該觸發邏輯應用程式，您可以在程式碼檢視中編輯邏輯應用程式，並新增條件以在 HTTP 呼叫之後進行評估。</span><span class="sxs-lookup"><span data-stu-id="51616-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="51616-122">以下是 HTTP 觸發程序的範例，它會在每次傳回的狀態碼大於或等於 `400` 時觸發。</span><span class="sxs-lookup"><span data-stu-id="51616-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="51616-123">如需關於 HTTP 觸發程序參數的詳細資料，可在 [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)取得。</span><span class="sxs-lookup"><span data-stu-id="51616-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="51616-124">使用 HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="51616-124">Use the HTTP action</span></span>

<span data-ttu-id="51616-125">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="51616-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="51616-126">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51616-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="51616-127">選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="51616-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="51616-128">在動作搜尋方塊中，輸入 **http** 以列出 HTTP 動作。</span><span class="sxs-lookup"><span data-stu-id="51616-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![選取 HTTP 動作](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="51616-130">新增任何必要參數以呼叫 HTTP。</span><span class="sxs-lookup"><span data-stu-id="51616-130">Add any required parameters for the HTTP call.</span></span>
   
    ![完成 HTTP 動作](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="51616-132">在程式設計工具的工具列上，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="51616-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="51616-133">系統已儲存您的邏輯應用程式並在同一時間發佈 (啟動)。</span><span class="sxs-lookup"><span data-stu-id="51616-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="51616-134">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="51616-134">HTTP trigger</span></span>
<span data-ttu-id="51616-135">以下是此連接器所支援觸發程序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51616-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="51616-136">HTTP 連接器有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="51616-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="51616-137">觸發程序</span><span class="sxs-lookup"><span data-stu-id="51616-137">Trigger</span></span> | <span data-ttu-id="51616-138">說明</span><span class="sxs-lookup"><span data-stu-id="51616-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51616-139">http</span><span class="sxs-lookup"><span data-stu-id="51616-139">HTTP</span></span> |<span data-ttu-id="51616-140">進行 HTTP 呼叫並傳回回應內容。</span><span class="sxs-lookup"><span data-stu-id="51616-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="51616-141">HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="51616-141">HTTP action</span></span>
<span data-ttu-id="51616-142">以下是此連接器所支援動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51616-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="51616-143">HTTP 連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="51616-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="51616-144">動作</span><span class="sxs-lookup"><span data-stu-id="51616-144">Action</span></span> | <span data-ttu-id="51616-145">說明</span><span class="sxs-lookup"><span data-stu-id="51616-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51616-146">http</span><span class="sxs-lookup"><span data-stu-id="51616-146">HTTP</span></span> |<span data-ttu-id="51616-147">進行 HTTP 呼叫並傳回回應內容。</span><span class="sxs-lookup"><span data-stu-id="51616-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="51616-148">HTTP 詳細資料</span><span class="sxs-lookup"><span data-stu-id="51616-148">HTTP details</span></span>
<span data-ttu-id="51616-149">下表說明動作的必要與選擇性輸入欄位，以及與使用動作相關聯的對應輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51616-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="51616-150">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="51616-150">HTTP request</span></span>
<span data-ttu-id="51616-151">以下是動作的輸入欄位，可進行 HTTP 輸出要求。</span><span class="sxs-lookup"><span data-stu-id="51616-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="51616-152">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="51616-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="51616-153">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="51616-153">Display name</span></span> | <span data-ttu-id="51616-154">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="51616-154">Property name</span></span> | <span data-ttu-id="51616-155">說明</span><span class="sxs-lookup"><span data-stu-id="51616-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51616-156">方法 *</span><span class="sxs-lookup"><span data-stu-id="51616-156">Method*</span></span> |<span data-ttu-id="51616-157">method</span><span class="sxs-lookup"><span data-stu-id="51616-157">method</span></span> |<span data-ttu-id="51616-158">要使用的 HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="51616-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="51616-159">URI*</span><span class="sxs-lookup"><span data-stu-id="51616-159">URI*</span></span> |<span data-ttu-id="51616-160">uri</span><span class="sxs-lookup"><span data-stu-id="51616-160">uri</span></span> |<span data-ttu-id="51616-161">HTTP 要求的 URI</span><span class="sxs-lookup"><span data-stu-id="51616-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="51616-162">標頭</span><span class="sxs-lookup"><span data-stu-id="51616-162">Headers</span></span> |<span data-ttu-id="51616-163">標頭</span><span class="sxs-lookup"><span data-stu-id="51616-163">headers</span></span> |<span data-ttu-id="51616-164">要包含的 HTTP 標頭的 JSON 物件</span><span class="sxs-lookup"><span data-stu-id="51616-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="51616-165">內文</span><span class="sxs-lookup"><span data-stu-id="51616-165">Body</span></span> |<span data-ttu-id="51616-166">內文</span><span class="sxs-lookup"><span data-stu-id="51616-166">body</span></span> |<span data-ttu-id="51616-167">HTTP 要求本文</span><span class="sxs-lookup"><span data-stu-id="51616-167">The HTTP request body</span></span> |
| <span data-ttu-id="51616-168">驗證</span><span class="sxs-lookup"><span data-stu-id="51616-168">Authentication</span></span> |<span data-ttu-id="51616-169">驗證</span><span class="sxs-lookup"><span data-stu-id="51616-169">authentication</span></span> |<span data-ttu-id="51616-170">詳細資料在 [驗證](#authentication) 一節中</span><span class="sxs-lookup"><span data-stu-id="51616-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="51616-171">輸出詳細資料</span><span class="sxs-lookup"><span data-stu-id="51616-171">Output details</span></span>
<span data-ttu-id="51616-172">以下是 HTTP 回應的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51616-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="51616-173">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="51616-173">Property name</span></span> | <span data-ttu-id="51616-174">資料類型</span><span class="sxs-lookup"><span data-stu-id="51616-174">Data type</span></span> | <span data-ttu-id="51616-175">說明</span><span class="sxs-lookup"><span data-stu-id="51616-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51616-176">headers</span><span class="sxs-lookup"><span data-stu-id="51616-176">Headers</span></span> |<span data-ttu-id="51616-177">物件</span><span class="sxs-lookup"><span data-stu-id="51616-177">object</span></span> |<span data-ttu-id="51616-178">回應標頭</span><span class="sxs-lookup"><span data-stu-id="51616-178">Response headers</span></span> |
| <span data-ttu-id="51616-179">內文</span><span class="sxs-lookup"><span data-stu-id="51616-179">Body</span></span> |<span data-ttu-id="51616-180">物件</span><span class="sxs-lookup"><span data-stu-id="51616-180">object</span></span> |<span data-ttu-id="51616-181">回應物件</span><span class="sxs-lookup"><span data-stu-id="51616-181">Response object</span></span> |
| <span data-ttu-id="51616-182">Status Code</span><span class="sxs-lookup"><span data-stu-id="51616-182">Status Code</span></span> |<span data-ttu-id="51616-183">整數</span><span class="sxs-lookup"><span data-stu-id="51616-183">int</span></span> |<span data-ttu-id="51616-184">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="51616-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="51616-185">驗證</span><span class="sxs-lookup"><span data-stu-id="51616-185">Authentication</span></span>
<span data-ttu-id="51616-186">Logic Apps 功能可讓您針對 HTTP 端點使用不同類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="51616-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="51616-187">您可以將此驗證搭配 **HTTP**、**[HTTP + Swagger](connectors-native-http-swagger.md)** 及 **[HTTP Webhook](connectors-native-webhook.md)** 連接器使用。</span><span class="sxs-lookup"><span data-stu-id="51616-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="51616-188">下列是可設定的驗證類型︰</span><span class="sxs-lookup"><span data-stu-id="51616-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="51616-189">基本驗證</span><span class="sxs-lookup"><span data-stu-id="51616-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="51616-190">用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="51616-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="51616-191">Azure Active Directory (Azure AD) OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="51616-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="51616-192">基本驗證</span><span class="sxs-lookup"><span data-stu-id="51616-192">Basic authentication</span></span>

<span data-ttu-id="51616-193">以下是基本驗證所需的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="51616-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="51616-194">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="51616-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="51616-195">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="51616-195">Property name</span></span> | <span data-ttu-id="51616-196">資料類型</span><span class="sxs-lookup"><span data-stu-id="51616-196">Data type</span></span> | <span data-ttu-id="51616-197">說明</span><span class="sxs-lookup"><span data-stu-id="51616-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51616-198">類型*</span><span class="sxs-lookup"><span data-stu-id="51616-198">Type*</span></span> |<span data-ttu-id="51616-199">type</span><span class="sxs-lookup"><span data-stu-id="51616-199">type</span></span> |<span data-ttu-id="51616-200">驗證類型 (若為基本驗證必須是 `Basic` )</span><span class="sxs-lookup"><span data-stu-id="51616-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="51616-201">使用者名稱*</span><span class="sxs-lookup"><span data-stu-id="51616-201">Username*</span></span> |<span data-ttu-id="51616-202">username</span><span class="sxs-lookup"><span data-stu-id="51616-202">username</span></span> |<span data-ttu-id="51616-203">要驗證的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="51616-203">User name to authenticate</span></span> |
| <span data-ttu-id="51616-204">密碼*</span><span class="sxs-lookup"><span data-stu-id="51616-204">Password*</span></span> |<span data-ttu-id="51616-205">password</span><span class="sxs-lookup"><span data-stu-id="51616-205">password</span></span> |<span data-ttu-id="51616-206">要驗證的密碼</span><span class="sxs-lookup"><span data-stu-id="51616-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="51616-207">如果您要使用無法從定義中擷取的密碼，請使用 `securestring` 參數和 `@parameters()` 
> [工作流程定義函式](http://aka.ms/logicappdocs)。</span><span class="sxs-lookup"><span data-stu-id="51616-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="51616-208">例如：</span><span class="sxs-lookup"><span data-stu-id="51616-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="51616-209">用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="51616-209">Client certificate authentication</span></span>

<span data-ttu-id="51616-210">以下是用戶端憑證驗證需要的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="51616-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="51616-211">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="51616-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="51616-212">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="51616-212">Property name</span></span> | <span data-ttu-id="51616-213">資料類型</span><span class="sxs-lookup"><span data-stu-id="51616-213">Data type</span></span> | <span data-ttu-id="51616-214">說明</span><span class="sxs-lookup"><span data-stu-id="51616-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51616-215">類型*</span><span class="sxs-lookup"><span data-stu-id="51616-215">Type*</span></span> |<span data-ttu-id="51616-216">type</span><span class="sxs-lookup"><span data-stu-id="51616-216">type</span></span> |<span data-ttu-id="51616-217">驗證類型 (若為 SSL 用戶端憑證，必須是 `ClientCertificate` )</span><span class="sxs-lookup"><span data-stu-id="51616-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="51616-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="51616-218">PFX*</span></span> |<span data-ttu-id="51616-219">pfx</span><span class="sxs-lookup"><span data-stu-id="51616-219">pfx</span></span> |<span data-ttu-id="51616-220">Base 64 編碼的個人資訊交換 (PFX) 檔案內容</span><span class="sxs-lookup"><span data-stu-id="51616-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="51616-221">密碼*</span><span class="sxs-lookup"><span data-stu-id="51616-221">Password*</span></span> |<span data-ttu-id="51616-222">password</span><span class="sxs-lookup"><span data-stu-id="51616-222">password</span></span> |<span data-ttu-id="51616-223">存取 PFX 檔案的密碼</span><span class="sxs-lookup"><span data-stu-id="51616-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="51616-224">若要在儲存邏輯應用程式後，使用無法在定義中讀取的參數，您可以使用 `securestring` 參數和 `@parameters()`  
> [工作流程定義函式](http://aka.ms/logicappdocs)。</span><span class="sxs-lookup"><span data-stu-id="51616-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="51616-225">例如：</span><span class="sxs-lookup"><span data-stu-id="51616-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="51616-226">Azure AD OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="51616-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="51616-227">以下是 Azure AD OAuth 驗證所需的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="51616-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="51616-228">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="51616-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="51616-229">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="51616-229">Property name</span></span> | <span data-ttu-id="51616-230">資料類型</span><span class="sxs-lookup"><span data-stu-id="51616-230">Data type</span></span> | <span data-ttu-id="51616-231">說明</span><span class="sxs-lookup"><span data-stu-id="51616-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51616-232">類型*</span><span class="sxs-lookup"><span data-stu-id="51616-232">Type*</span></span> |<span data-ttu-id="51616-233">type</span><span class="sxs-lookup"><span data-stu-id="51616-233">type</span></span> |<span data-ttu-id="51616-234">驗證類型 (若為 Azure AD OAuth 必須是 `ActiveDirectoryOAuth` )</span><span class="sxs-lookup"><span data-stu-id="51616-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="51616-235">租用戶*</span><span class="sxs-lookup"><span data-stu-id="51616-235">Tenant*</span></span> |<span data-ttu-id="51616-236">tenant</span><span class="sxs-lookup"><span data-stu-id="51616-236">tenant</span></span> |<span data-ttu-id="51616-237">Azure AD 租用戶的租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="51616-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="51616-238">對象*</span><span class="sxs-lookup"><span data-stu-id="51616-238">Audience*</span></span> |<span data-ttu-id="51616-239">audience</span><span class="sxs-lookup"><span data-stu-id="51616-239">audience</span></span> |<span data-ttu-id="51616-240">您要求授權使用的資源。</span><span class="sxs-lookup"><span data-stu-id="51616-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="51616-241">例如：`https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="51616-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="51616-242">用戶端識別碼*</span><span class="sxs-lookup"><span data-stu-id="51616-242">Client ID*</span></span> |<span data-ttu-id="51616-243">clientId</span><span class="sxs-lookup"><span data-stu-id="51616-243">clientId</span></span> |<span data-ttu-id="51616-244">Azure AD 應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="51616-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="51616-245">密碼*</span><span class="sxs-lookup"><span data-stu-id="51616-245">Secret*</span></span> |<span data-ttu-id="51616-246">secret</span><span class="sxs-lookup"><span data-stu-id="51616-246">secret</span></span> |<span data-ttu-id="51616-247">要求權杖之用戶端的密碼</span><span class="sxs-lookup"><span data-stu-id="51616-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="51616-248">使用 `securestring` 參數和 `@parameters()` [工作流程定義函式](http://aka.ms/logicappdocs)，您就能在儲存後使用無法在定義中讀取的參數。</span><span class="sxs-lookup"><span data-stu-id="51616-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="51616-249">例如：</span><span class="sxs-lookup"><span data-stu-id="51616-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="51616-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51616-250">Next steps</span></span>
<span data-ttu-id="51616-251">立即試用平台和 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="51616-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="51616-252">您可以查看我們的 [API 清單](apis-list.md)，以探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="51616-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

