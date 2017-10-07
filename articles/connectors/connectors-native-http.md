---
title: "透過 HTTP-Azure 邏輯應用程式的任何端點與 aaaCommunicate |Microsoft 文件"
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
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="c03e6-103">開始使用 hello HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="c03e6-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="c03e6-104">以 hello HTTP 動作，您可以擴充工作流程，為您的組織，並透過 HTTP 通訊 tooany 端點。</span><span class="sxs-lookup"><span data-stu-id="c03e6-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="c03e6-105">您可以：</span><span class="sxs-lookup"><span data-stu-id="c03e6-105">You can:</span></span>

* <span data-ttu-id="c03e6-106">建立會在您管理的網站故障時啟動 (觸發程序) 的邏輯應用程式工作流程。</span><span class="sxs-lookup"><span data-stu-id="c03e6-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="c03e6-107">Tooany 與端點通訊透過 HTTP tooextend 您的工作流程至其他服務。</span><span class="sxs-lookup"><span data-stu-id="c03e6-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="c03e6-108">請參閱 < 開始使用邏輯應用程式中的 hello HTTP 動作 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="c03e6-109">使用 hello HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="c03e6-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="c03e6-110">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。</span><span class="sxs-lookup"><span data-stu-id="c03e6-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="c03e6-111">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="c03e6-112">以下是總 hello HTTP tooset 觸發程序在 hello 邏輯應用程式的設計工具中的範例順序。</span><span class="sxs-lookup"><span data-stu-id="c03e6-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="c03e6-113">邏輯應用程式中加入 hello HTTP 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c03e6-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="c03e6-114">填入您想 toopoll hello HTTP 端點的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="c03e6-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="c03e6-115">修改 hello 循環間隔，在它輪詢的頻率。</span><span class="sxs-lookup"><span data-stu-id="c03e6-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="c03e6-116">hello 邏輯應用程式現在就會引發與每個檢查期間，會傳回任何內容。</span><span class="sxs-lookup"><span data-stu-id="c03e6-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP 觸發程序](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="c03e6-118">Hello HTTP 觸發程序的運作方式</span><span class="sxs-lookup"><span data-stu-id="c03e6-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="c03e6-119">hello HTTP 觸發程序會呼叫 tooHTTP 端點傳送以週期性間隔。</span><span class="sxs-lookup"><span data-stu-id="c03e6-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="c03e6-120">根據預設，會低於 300 任何 HTTP 回應碼會導致邏輯應用程式 toorun。</span><span class="sxs-lookup"><span data-stu-id="c03e6-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="c03e6-121">toospecify 是否應該引發 hello 邏輯應用程式，您可以編輯程式碼檢視中的 hello 邏輯應用程式，並加入條件來評估 hello 之後 HTTP 呼叫。</span><span class="sxs-lookup"><span data-stu-id="c03e6-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="c03e6-122">以下是範例 HTTP 觸發程序引發時 hello 傳回狀態碼是否大於或等於太`400`。</span><span class="sxs-lookup"><span data-stu-id="c03e6-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

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

<span data-ttu-id="c03e6-123">關於 hello HTTP 觸發程序參數的完整詳細資料位於[MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="c03e6-124">使用 hello HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="c03e6-124">Use hello HTTP action</span></span>

<span data-ttu-id="c03e6-125">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="c03e6-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="c03e6-126">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="c03e6-127">選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="c03e6-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="c03e6-128">在 hello 動作搜尋方塊中，輸入**http** toolist hello HTTP 動作。</span><span class="sxs-lookup"><span data-stu-id="c03e6-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![選取 hello HTTP 動作](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="c03e6-130">新增 hello HTTP 呼叫的任何必要的參數。</span><span class="sxs-lookup"><span data-stu-id="c03e6-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![完成 hello HTTP 動作](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="c03e6-132">Hello 設計工具工具列上，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="c03e6-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="c03e6-133">儲存並發行位置 （啟用） 在 hello 邏輯應用程式相同的時間。</span><span class="sxs-lookup"><span data-stu-id="c03e6-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="c03e6-134">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="c03e6-134">HTTP trigger</span></span>
<span data-ttu-id="c03e6-135">以下是 hello hello 觸發程序，此連接器支援的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c03e6-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="c03e6-136">hello HTTP 連接器有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c03e6-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="c03e6-137">觸發程序</span><span class="sxs-lookup"><span data-stu-id="c03e6-137">Trigger</span></span> | <span data-ttu-id="c03e6-138">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c03e6-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="c03e6-139">HTTP</span></span> |<span data-ttu-id="c03e6-140">執行 HTTP 呼叫而傳回 hello 回應內容。</span><span class="sxs-lookup"><span data-stu-id="c03e6-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="c03e6-141">HTTP 動作</span><span class="sxs-lookup"><span data-stu-id="c03e6-141">HTTP action</span></span>
<span data-ttu-id="c03e6-142">以下是此連接器支援的 hello 動作的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c03e6-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="c03e6-143">hello HTTP 連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="c03e6-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="c03e6-144">動作</span><span class="sxs-lookup"><span data-stu-id="c03e6-144">Action</span></span> | <span data-ttu-id="c03e6-145">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c03e6-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="c03e6-146">HTTP</span></span> |<span data-ttu-id="c03e6-147">執行 HTTP 呼叫而傳回 hello 回應內容。</span><span class="sxs-lookup"><span data-stu-id="c03e6-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="c03e6-148">HTTP 詳細資料</span><span class="sxs-lookup"><span data-stu-id="c03e6-148">HTTP details</span></span>
<span data-ttu-id="c03e6-149">hello 下列表格說明必要的 hello 與 hello 動作和 hello 對應輸出的詳細資料與使用 hello 動作相關聯的選擇性輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="c03e6-150">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="c03e6-150">HTTP request</span></span>
<span data-ttu-id="c03e6-151">hello 如下 hello 動作，使外送 HTTP 要求的輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="c03e6-152">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="c03e6-153">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-153">Display name</span></span> | <span data-ttu-id="c03e6-154">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-154">Property name</span></span> | <span data-ttu-id="c03e6-155">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c03e6-156">方法 *</span><span class="sxs-lookup"><span data-stu-id="c03e6-156">Method*</span></span> |<span data-ttu-id="c03e6-157">method</span><span class="sxs-lookup"><span data-stu-id="c03e6-157">method</span></span> |<span data-ttu-id="c03e6-158">hello HTTP 指令動詞 toouse</span><span class="sxs-lookup"><span data-stu-id="c03e6-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="c03e6-159">URI*</span><span class="sxs-lookup"><span data-stu-id="c03e6-159">URI*</span></span> |<span data-ttu-id="c03e6-160">uri</span><span class="sxs-lookup"><span data-stu-id="c03e6-160">uri</span></span> |<span data-ttu-id="c03e6-161">hello URI hello HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="c03e6-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="c03e6-162">headers</span><span class="sxs-lookup"><span data-stu-id="c03e6-162">Headers</span></span> |<span data-ttu-id="c03e6-163">headers</span><span class="sxs-lookup"><span data-stu-id="c03e6-163">headers</span></span> |<span data-ttu-id="c03e6-164">HTTP 標頭 tooinclude 的 JSON 物件</span><span class="sxs-lookup"><span data-stu-id="c03e6-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="c03e6-165">內文</span><span class="sxs-lookup"><span data-stu-id="c03e6-165">Body</span></span> |<span data-ttu-id="c03e6-166">body</span><span class="sxs-lookup"><span data-stu-id="c03e6-166">body</span></span> |<span data-ttu-id="c03e6-167">hello HTTP 要求主體</span><span class="sxs-lookup"><span data-stu-id="c03e6-167">hello HTTP request body</span></span> |
| <span data-ttu-id="c03e6-168">驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-168">Authentication</span></span> |<span data-ttu-id="c03e6-169">驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-169">authentication</span></span> |<span data-ttu-id="c03e6-170">詳細資料中 hello[驗證](#authentication)區段</span><span class="sxs-lookup"><span data-stu-id="c03e6-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="c03e6-171">輸出詳細資料</span><span class="sxs-lookup"><span data-stu-id="c03e6-171">Output details</span></span>
<span data-ttu-id="c03e6-172">hello 以下是輸出 hello HTTP 回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c03e6-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="c03e6-173">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-173">Property name</span></span> | <span data-ttu-id="c03e6-174">資料類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-174">Data type</span></span> | <span data-ttu-id="c03e6-175">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c03e6-176">headers</span><span class="sxs-lookup"><span data-stu-id="c03e6-176">Headers</span></span> |<span data-ttu-id="c03e6-177">物件</span><span class="sxs-lookup"><span data-stu-id="c03e6-177">object</span></span> |<span data-ttu-id="c03e6-178">回應標頭</span><span class="sxs-lookup"><span data-stu-id="c03e6-178">Response headers</span></span> |
| <span data-ttu-id="c03e6-179">內文</span><span class="sxs-lookup"><span data-stu-id="c03e6-179">Body</span></span> |<span data-ttu-id="c03e6-180">物件</span><span class="sxs-lookup"><span data-stu-id="c03e6-180">object</span></span> |<span data-ttu-id="c03e6-181">回應物件</span><span class="sxs-lookup"><span data-stu-id="c03e6-181">Response object</span></span> |
| <span data-ttu-id="c03e6-182">Status Code</span><span class="sxs-lookup"><span data-stu-id="c03e6-182">Status Code</span></span> |<span data-ttu-id="c03e6-183">整數</span><span class="sxs-lookup"><span data-stu-id="c03e6-183">int</span></span> |<span data-ttu-id="c03e6-184">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="c03e6-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="c03e6-185">驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-185">Authentication</span></span>
<span data-ttu-id="c03e6-186">hello Logic Apps 功能可讓您 toouse 不同類型的 HTTP 端點的驗證。</span><span class="sxs-lookup"><span data-stu-id="c03e6-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="c03e6-187">您可以使用這項驗證以 hello **HTTP**，  **[HTTP + Swagger](connectors-native-http-swagger.md)**，和 **[HTTP Webhook](connectors-native-webhook.md)** 連接器。</span><span class="sxs-lookup"><span data-stu-id="c03e6-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="c03e6-188">hello 下列類型是驗證的可設定：</span><span class="sxs-lookup"><span data-stu-id="c03e6-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="c03e6-189">基本驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="c03e6-190">用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="c03e6-191">Azure Active Directory (Azure AD) OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="c03e6-192">基本驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-192">Basic authentication</span></span>

<span data-ttu-id="c03e6-193">hello 接驗證物件所需的基本驗證。</span><span class="sxs-lookup"><span data-stu-id="c03e6-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="c03e6-194">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="c03e6-195">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-195">Property name</span></span> | <span data-ttu-id="c03e6-196">資料類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-196">Data type</span></span> | <span data-ttu-id="c03e6-197">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c03e6-198">類型*</span><span class="sxs-lookup"><span data-stu-id="c03e6-198">Type*</span></span> |<span data-ttu-id="c03e6-199">type</span><span class="sxs-lookup"><span data-stu-id="c03e6-199">type</span></span> |<span data-ttu-id="c03e6-200">驗證類型 (若為基本驗證必須是 `Basic` )</span><span class="sxs-lookup"><span data-stu-id="c03e6-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="c03e6-201">使用者名稱*</span><span class="sxs-lookup"><span data-stu-id="c03e6-201">Username*</span></span> |<span data-ttu-id="c03e6-202">username</span><span class="sxs-lookup"><span data-stu-id="c03e6-202">username</span></span> |<span data-ttu-id="c03e6-203">使用者名稱 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="c03e6-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="c03e6-204">密碼*</span><span class="sxs-lookup"><span data-stu-id="c03e6-204">Password*</span></span> |<span data-ttu-id="c03e6-205">password</span><span class="sxs-lookup"><span data-stu-id="c03e6-205">password</span></span> |<span data-ttu-id="c03e6-206">密碼 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="c03e6-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="c03e6-207">如果您想 toouse 無法從 hello 定義擷取密碼時，使用`securestring`參數與 hello `@parameters()`  
> [工作流程定義函式](http://aka.ms/logicappdocs)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="c03e6-208">例如：</span><span class="sxs-lookup"><span data-stu-id="c03e6-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="c03e6-209">用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-209">Client certificate authentication</span></span>

<span data-ttu-id="c03e6-210">hello 下列驗證物件所需的用戶端憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="c03e6-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="c03e6-211">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="c03e6-212">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-212">Property name</span></span> | <span data-ttu-id="c03e6-213">資料類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-213">Data type</span></span> | <span data-ttu-id="c03e6-214">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c03e6-215">類型*</span><span class="sxs-lookup"><span data-stu-id="c03e6-215">Type*</span></span> |<span data-ttu-id="c03e6-216">類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-216">type</span></span> |<span data-ttu-id="c03e6-217">hello 的驗證類型 (必須是`ClientCertificate`進行 SSL 用戶端憑證)</span><span class="sxs-lookup"><span data-stu-id="c03e6-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="c03e6-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="c03e6-218">PFX*</span></span> |<span data-ttu-id="c03e6-219">pfx</span><span class="sxs-lookup"><span data-stu-id="c03e6-219">pfx</span></span> |<span data-ttu-id="c03e6-220">hello hello 個人資訊交換 (PFX) 檔案的 Base64 編碼內容</span><span class="sxs-lookup"><span data-stu-id="c03e6-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="c03e6-221">密碼*</span><span class="sxs-lookup"><span data-stu-id="c03e6-221">Password*</span></span> |<span data-ttu-id="c03e6-222">password</span><span class="sxs-lookup"><span data-stu-id="c03e6-222">password</span></span> |<span data-ttu-id="c03e6-223">hello 密碼 tooaccess hello PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="c03e6-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="c03e6-224">toouse 將不會讀取儲存 hello 邏輯應用程式之後的 hello 定義中的參數，您可以使用`securestring`參數與 hello `@parameters()`  
> [工作流程定義函式](http://aka.ms/logicappdocs)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="c03e6-225">例如：</span><span class="sxs-lookup"><span data-stu-id="c03e6-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="c03e6-226">Azure AD OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="c03e6-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="c03e6-227">hello 接驗證物件所需的 Azure AD 的 OAuth 驗證。</span><span class="sxs-lookup"><span data-stu-id="c03e6-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="c03e6-228">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="c03e6-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="c03e6-229">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c03e6-229">Property name</span></span> | <span data-ttu-id="c03e6-230">資料類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-230">Data type</span></span> | <span data-ttu-id="c03e6-231">說明</span><span class="sxs-lookup"><span data-stu-id="c03e6-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c03e6-232">類型*</span><span class="sxs-lookup"><span data-stu-id="c03e6-232">Type*</span></span> |<span data-ttu-id="c03e6-233">類型</span><span class="sxs-lookup"><span data-stu-id="c03e6-233">type</span></span> |<span data-ttu-id="c03e6-234">hello 的驗證類型 (必須是`ActiveDirectoryOAuth`for Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="c03e6-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="c03e6-235">租用戶*</span><span class="sxs-lookup"><span data-stu-id="c03e6-235">Tenant*</span></span> |<span data-ttu-id="c03e6-236">tenant</span><span class="sxs-lookup"><span data-stu-id="c03e6-236">tenant</span></span> |<span data-ttu-id="c03e6-237">hello hello Azure AD 租用戶的租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="c03e6-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="c03e6-238">對象*</span><span class="sxs-lookup"><span data-stu-id="c03e6-238">Audience*</span></span> |<span data-ttu-id="c03e6-239">audience</span><span class="sxs-lookup"><span data-stu-id="c03e6-239">audience</span></span> |<span data-ttu-id="c03e6-240">您要求授權 toouse hello 資源。</span><span class="sxs-lookup"><span data-stu-id="c03e6-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="c03e6-241">例如：`https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="c03e6-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="c03e6-242">用戶端識別碼*</span><span class="sxs-lookup"><span data-stu-id="c03e6-242">Client ID*</span></span> |<span data-ttu-id="c03e6-243">clientId</span><span class="sxs-lookup"><span data-stu-id="c03e6-243">clientId</span></span> |<span data-ttu-id="c03e6-244">hello hello Azure AD 應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="c03e6-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="c03e6-245">密碼*</span><span class="sxs-lookup"><span data-stu-id="c03e6-245">Secret*</span></span> |<span data-ttu-id="c03e6-246">secret</span><span class="sxs-lookup"><span data-stu-id="c03e6-246">secret</span></span> |<span data-ttu-id="c03e6-247">hello 用戶端要求 hello 語彙基元的 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="c03e6-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="c03e6-248">您可以使用`securestring`參數與 hello `@parameters()` [工作流程定義函式](http://aka.ms/logicappdocs)toouse 將不會在儲存之後 hello 定義可讀取的參數。</span><span class="sxs-lookup"><span data-stu-id="c03e6-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="c03e6-249">例如：</span><span class="sxs-lookup"><span data-stu-id="c03e6-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="c03e6-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c03e6-250">Next steps</span></span>
<span data-ttu-id="c03e6-251">現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="c03e6-252">您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="c03e6-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

