---
title: "透過 HTTP 端點呼叫、觸發或巢狀處理工作流程 - Azure Logic Apps | Microsoft Docs"
description: "設定 HTTP 端點來呼叫、觸發或巢狀處理 Azure Logic Apps 的工作流程"
services: logic-apps
keywords: "工作流程, HTTP 端點"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="ec9fd-104">在邏輯應用程式中透過 HTTP 端點呼叫、觸發或巢狀處理工作流程</span><span class="sxs-lookup"><span data-stu-id="ec9fd-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="ec9fd-105">您可以在邏輯應用程式中利用原生方式公開同步的 HTTP 端點作為觸發程序，以透過 URL 來觸發或呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="ec9fd-106">您也可以使用可呼叫端點的模式，以在邏輯應用程式中巢狀處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="ec9fd-107">若要建立 HTTP 端點，您可以新增這些觸發程序，以讓邏輯應用程式接收傳入要求︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="ec9fd-108">要求</span><span class="sxs-lookup"><span data-stu-id="ec9fd-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="ec9fd-109">API 連線 Webhook</span><span class="sxs-lookup"><span data-stu-id="ec9fd-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="ec9fd-110">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="ec9fd-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="ec9fd-111">雖然我們的範例使用 [要求] 觸發程序，但是您可以使用任何列出的 HTTP 觸發程序，而且所有的原則都會同樣地套用到其他觸發程序類型。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="ec9fd-112">設定邏輯應用程式的 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="ec9fd-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="ec9fd-113">若要建立 HTTP 端點，請新增可接收傳入要求的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="ec9fd-114">登入 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="ec9fd-115">移至邏輯應用程式，並開啟邏輯應用程式設計工具。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="ec9fd-116">新增可讓邏輯應用程式接收傳入要求的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="ec9fd-117">例如，將**要求**觸發程序新增至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="ec9fd-118">在 [要求本文 JSON 結構描述] 下方，您可以選擇針對預期要觸發程序收到的承載 (資料) 輸入 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="ec9fd-119">設計工具會使用此結構描述來產生權杖，而邏輯應用程式可以使用權杖以透過工作流程從觸發程序中取用、剖析和傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="ec9fd-120">深入了解[從 JSON 結構描述產生的權杖](#generated-tokens)。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="ec9fd-121">在此範例中，輸入設計工具中所顯示的結構描述︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![新增要求動作][1]

    > [!TIP]
    > 
    > <span data-ttu-id="ec9fd-123">您可以從 [jsonschema.net](http://jsonschema.net/) 這類工具產生範例 JSON 承載的結構描述，或在 [要求] 觸發程序中選擇 [請使用範例承載產生結構描述] 來產生範例 JSON 承載的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="ec9fd-124">輸入您的範例承載，然後選擇 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="ec9fd-125">例如，此範例裝載︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="ec9fd-126">產生此結構描述︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="ec9fd-127">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-127">Save your logic app.</span></span> <span data-ttu-id="ec9fd-128">在 [此 URL 的 HTTP POST] 下方，您現在應該會找到產生的回呼 URL，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![為端點產生的回呼 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="ec9fd-130">此 URL 的查詢參數中包含用於驗證的共用存取簽章 (SAS) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="ec9fd-131">您也可以從 Azure 入口網站的邏輯應用程式概觀中取得 HTTP 端點 URL。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="ec9fd-132">在 [觸發程序記錄] 下方，選取觸發程序：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-132">Under **Trigger History**, select your trigger:</span></span>

    ![從 Azure 入口網站取得 HTTP 端點 URL][2]

    <span data-ttu-id="ec9fd-134">或者，您可以進行這個呼叫來取得 URL：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="ec9fd-135">變更觸發程序的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ec9fd-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="ec9fd-136">根據預設，[要求] 觸發程序會預期 HTTP POST 要求，但您可以使用不同的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec9fd-137">您只能指定一種方法類型。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="ec9fd-138">在 [要求] 觸發程序上，選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="ec9fd-139">開啟 [方法] 清單。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-139">Open the **Method** list.</span></span> <span data-ttu-id="ec9fd-140">在此範例中，選取 **GET**，稍後測試 HTTP 端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec9fd-141">您可以選取任何其他 HTTP 方法，或指定專屬邏輯應用程式的自訂方法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![變更 HTTP 方法](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="ec9fd-143">透過 HTTP 端點 URL 接受參數</span><span class="sxs-lookup"><span data-stu-id="ec9fd-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="ec9fd-144">當您想要 HTTP 端點 URL 接受參數時，請自訂觸發程序的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="ec9fd-145">在 [要求] 觸發程序上，選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="ec9fd-146">在 [方法] 下方，指定您想要要求使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="ec9fd-147">在此範例中，選取 **GET** 方法 (如果還沒有這麼做的話)，以測試 HTTP 端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ec9fd-148">當您指定觸發程序的相對路徑時，也必須明確地指定觸發程序的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="ec9fd-149">在 [相對路徑] 下方，指定您 URL 應該接受之參數的相對路徑，例如，`customers/{customerID}`。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![指定參數的 HTTP 方法和相對路徑](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="ec9fd-151">若要使用參數，請將 [回應] 動作新增至邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ec9fd-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="ec9fd-152">(在觸發程序下方，選擇 [新增步驟] > [新增動作] > [回應])。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="ec9fd-153">在您回應的 [本文] 中，包括觸發程序相對路徑中所指定參數的權杖。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="ec9fd-154">例如，若要傳回 `Hello {customerID}`，請使用 `Hello {customerID token}` 來更新回應的 [本文]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="ec9fd-155">動態內容的清單應該會出現並顯示`customerID`權杖以供您選取。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![將參數新增至回應本文](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="ec9fd-157">您的 [本文] 應該如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-157">Your **Body** should look like this example:</span></span>

    ![含參數的回應本文](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="ec9fd-159">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-159">Save your logic app.</span></span> 

    <span data-ttu-id="ec9fd-160">HTTP 端點 URL 現在包括相對路徑，例如︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="ec9fd-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="ec9fd-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="ec9fd-162">若要測試 HTTP 端點，請複製更新過的 URL，並將其貼入另一個瀏覽器視窗中，但將 `{customerID}` 取代為 `123456`，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="ec9fd-163">您的瀏覽器應該顯示下列文字︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="ec9fd-164">從 JSON 結構描述產生邏輯應用程式的權杖</span><span class="sxs-lookup"><span data-stu-id="ec9fd-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="ec9fd-165">在 [要求] 觸發程序中提供 JSON 結構描述時，邏輯應用程式設計工具會產生該結構描述中屬性的權杖。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="ec9fd-166">您接著可以使用這些權杖，透過邏輯應用程式工作流程來傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="ec9fd-167">在此範例中，如果您將 `title` 和 `name` 屬性新增至 JSON 結構描述，則現在可以將其權杖用於稍後的工作流程步驟。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="ec9fd-168">以下是完整 JSON 結構描述︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="ec9fd-169">建立邏輯應用程式的巢狀工作流程</span><span class="sxs-lookup"><span data-stu-id="ec9fd-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="ec9fd-170">您可以新增其他可接收要求的邏輯應用程式，以在邏輯應用程式中巢狀處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="ec9fd-171">若要包括這些邏輯應用程式，請將 [Azure Logic Apps - 選擇 Logic Apps 工作流程] 動作新增至觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="ec9fd-172">您接著可以從合格的邏輯應用程式中進行選取。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-172">You can then select from eligible logic apps.</span></span>

![新增另一個邏輯應用程式](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="ec9fd-174">透過 HTTP 端點呼叫或觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ec9fd-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="ec9fd-175">建立 HTTP 端點之後，您可以透過完整 URL 的 `POST` 方法來觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="ec9fd-176">邏輯應用程式具有直接存取端點的內建支援。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="ec9fd-177">參考來自傳入要求的內容</span><span class="sxs-lookup"><span data-stu-id="ec9fd-177">Reference content from an incoming request</span></span>

<span data-ttu-id="ec9fd-178">如果內容的類型是 `application/json`，您可以從傳入要求參考屬性。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="ec9fd-179">否則，會將內容視為可傳遞給其他 API 的單一二進位單位。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="ec9fd-180">若要在工作流程內部參考此內容，您必須轉換該內容。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="ec9fd-181">例如，如果您要傳遞 `application/xml` 內容，可以使用 `@xpath()` 進行 XPath 擷取，或使用 `@json()` 來將 XML 轉換成 JSON。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="ec9fd-182">深入了解如何[使用內容類型](../logic-apps/logic-apps-content-type.md)。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="ec9fd-183">若要取得傳入要求的輸出，您可以使用 `@triggerOutputs()` 函式。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="ec9fd-184">輸出可能如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="ec9fd-185">若要特別存取 `body` 屬性，您可以使用 `@triggerBody()` 捷徑。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="ec9fd-186">回應要求</span><span class="sxs-lookup"><span data-stu-id="ec9fd-186">Respond to requests</span></span>

<span data-ttu-id="ec9fd-187">您可能想要將內容傳回給呼叫端，以回應可啟動邏輯應用程式的特定要求。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="ec9fd-188">若要建構回應的狀態碼、標頭和本文，您可以使用 [回應] 動作。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="ec9fd-189">這個動作可以出現在邏輯應用程式的任何位置，而不只是工作流程的結尾。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="ec9fd-190">如果邏輯應用程式未包括 [回應]，則 HTTP 端點會「立即」回應 [202 已接受] 狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="ec9fd-191">而且，為了讓原始要求取得回應，除非您呼叫工作流程作為巢狀邏輯應用程式，否則回應所需的所有步驟都必須在[要求逾時限制](./logic-apps-limits-and-config.md)內完成。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="ec9fd-192">如果未在此限制內產生任何回應，傳入要求就會逾時，並收到 HTTP 回應 [408 用戶端逾時]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="ec9fd-193">針對巢狀邏輯應用程式，無論需要多少時間，父邏輯應用程式都會繼續等候回應，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="ec9fd-194">建構回應</span><span class="sxs-lookup"><span data-stu-id="ec9fd-194">Construct the response</span></span>

<span data-ttu-id="ec9fd-195">您可以在回應本文中包括數個標頭和任何類型的內容。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="ec9fd-196">在範例回應中，標頭指定回應的內容類型為 `application/json`。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="ec9fd-197">而根據先前針對 [要求] 觸發程序所更新的 JSON 結構描述，本文會包含 `title` 和 `name`。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![HTTP 回應動作][3]

<span data-ttu-id="ec9fd-199">回應具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-199">Responses have these properties:</span></span>

| <span data-ttu-id="ec9fd-200">屬性</span><span class="sxs-lookup"><span data-stu-id="ec9fd-200">Property</span></span> | <span data-ttu-id="ec9fd-201">說明</span><span class="sxs-lookup"><span data-stu-id="ec9fd-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec9fd-202">StatusCode</span><span class="sxs-lookup"><span data-stu-id="ec9fd-202">statusCode</span></span> |<span data-ttu-id="ec9fd-203">指定用於回應傳入要求的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="ec9fd-204">此代碼可以是任何以 2xx、4xx 或 5xx 開頭的有效狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="ec9fd-205">但是，不允許 3xx 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="ec9fd-206">headers</span><span class="sxs-lookup"><span data-stu-id="ec9fd-206">headers</span></span> |<span data-ttu-id="ec9fd-207">定義要包含於回應中的標頭，且數目不限。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="ec9fd-208">body</span><span class="sxs-lookup"><span data-stu-id="ec9fd-208">body</span></span> |<span data-ttu-id="ec9fd-209">指定本文物件可以是字串、JSON 物件，甚至是上一個步驟中所參考的二進位內容。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="ec9fd-210">以下是 [回應] 動作之 JSON 結構描述目前的外觀：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="ec9fd-211">若要檢視邏輯應用程式的完整 JSON 定義，請在邏輯應用程式設計工具上選擇 [程式碼檢視]。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="ec9fd-212">問答集</span><span class="sxs-lookup"><span data-stu-id="ec9fd-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="ec9fd-213">問︰URL 安全性如何？</span><span class="sxs-lookup"><span data-stu-id="ec9fd-213">Q: What about URL security?</span></span>

<span data-ttu-id="ec9fd-214">答：Azure 會使用共用存取簽章 (SAS)，安全地產生邏輯應用程式回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="ec9fd-215">這個簽章是以查詢參數的形式傳遞，且必須在引發您的邏輯應用程式之前先驗證。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="ec9fd-216">Azure 會使用每個邏輯應用程式、觸發程序名稱以及要執行作業之秘密金鑰的唯一組合來產生簽章。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="ec9fd-217">因此，除非某人具有邏輯應用程式秘密金鑰的存取權，否則他們無法產生有效的簽章。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ec9fd-218">對於生產和安全系統，強烈建議直接從瀏覽器呼叫邏輯應用程式，因為：</span><span class="sxs-lookup"><span data-stu-id="ec9fd-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="ec9fd-219">URL 中出現共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="ec9fd-220">您由於邏輯應用程式客戶之間共用網域，而無法管理安全內容原則。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="ec9fd-221">問︰我可以進一步設定 HTTP 端點嗎？</span><span class="sxs-lookup"><span data-stu-id="ec9fd-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="ec9fd-222">答︰可以，HTTP 端點透過 [**API 管理**](../api-management/api-management-key-concepts.md)來支援更進階的設定。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="ec9fd-223">此服務也可讓您透過一致的方式管理所有 API，包括邏輯應用程式、設定自訂網域名稱、使用其他驗證方法等等，例如︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="ec9fd-224">變更要求方法</span><span class="sxs-lookup"><span data-stu-id="ec9fd-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="ec9fd-225">變更要求的 URL 區段</span><span class="sxs-lookup"><span data-stu-id="ec9fd-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="ec9fd-226">在 [Azure 入口網站](https://portal.azure.com/ "Azure 入口網站")中設定 API 管理網域</span><span class="sxs-lookup"><span data-stu-id="ec9fd-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="ec9fd-227">設定檢查基本驗證的原則</span><span class="sxs-lookup"><span data-stu-id="ec9fd-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="ec9fd-228">問︰從 2014 年 12 月 1 日預覽版升級結構描述時的變更內容為何？</span><span class="sxs-lookup"><span data-stu-id="ec9fd-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="ec9fd-229">答︰以下是這些變更的摘要︰</span><span class="sxs-lookup"><span data-stu-id="ec9fd-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="ec9fd-230">2014 年 12 月 1 日預覽版</span><span class="sxs-lookup"><span data-stu-id="ec9fd-230">December 1, 2014 preview</span></span> | <span data-ttu-id="ec9fd-231">2016 年 6 月 1 日</span><span class="sxs-lookup"><span data-stu-id="ec9fd-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="ec9fd-232">按一下 [HTTP 接聽程式] API 應用程式</span><span class="sxs-lookup"><span data-stu-id="ec9fd-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="ec9fd-233">按一下 [手動觸發程序] \(不需要 API 應用程式)</span><span class="sxs-lookup"><span data-stu-id="ec9fd-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="ec9fd-234">HTTP 接聽程式設定 [自動傳送回應]</span><span class="sxs-lookup"><span data-stu-id="ec9fd-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="ec9fd-235">包括 [回應] 動作，或不在工作流程定義中</span><span class="sxs-lookup"><span data-stu-id="ec9fd-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="ec9fd-236">設定基本或 OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="ec9fd-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="ec9fd-237">透過 API 管理</span><span class="sxs-lookup"><span data-stu-id="ec9fd-237">via API Management</span></span> |
| <span data-ttu-id="ec9fd-238">設定 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ec9fd-238">Configure HTTP method</span></span> |<span data-ttu-id="ec9fd-239">在 [顯示進階選項] 下方，選擇 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="ec9fd-240">設定相對路徑</span><span class="sxs-lookup"><span data-stu-id="ec9fd-240">Configure relative path</span></span> |<span data-ttu-id="ec9fd-241">在 [顯示進階選項] 下方，新增相對路徑。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="ec9fd-242">透過 `@triggerOutputs().body.Content` 參考傳入本文</span><span class="sxs-lookup"><span data-stu-id="ec9fd-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="ec9fd-243">透過 `@triggerOutputs().body` 參考</span><span class="sxs-lookup"><span data-stu-id="ec9fd-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="ec9fd-244">**傳送 HTTP 回應** 動作</span><span class="sxs-lookup"><span data-stu-id="ec9fd-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="ec9fd-245">按一下 [回應 HTTP 要求] \(不需要 API 應用程式)</span><span class="sxs-lookup"><span data-stu-id="ec9fd-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="ec9fd-246">取得說明</span><span class="sxs-lookup"><span data-stu-id="ec9fd-246">Get help</span></span>

<span data-ttu-id="ec9fd-247">若要提出問題、回答問題以及了解其他 Azure Logic Apps 使用者的做法，請造訪 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ec9fd-248">若要改善 Azure Logic Apps 和連接器，請在 [Azure Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)上票選或提交想法。</span><span class="sxs-lookup"><span data-stu-id="ec9fd-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec9fd-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec9fd-249">Next steps</span></span>

* [<span data-ttu-id="ec9fd-250">撰寫邏輯應用程式定義</span><span class="sxs-lookup"><span data-stu-id="ec9fd-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="ec9fd-251">處理錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="ec9fd-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
