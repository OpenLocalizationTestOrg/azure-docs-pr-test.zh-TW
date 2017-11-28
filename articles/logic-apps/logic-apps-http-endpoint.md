---
title: "aaaCall，觸發程序，或巢狀工作流程搭配 HTTP 端點的 Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure 邏輯應用程式設定 HTTP 端點 toocall、 觸發程序或巢狀工作流程"
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
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="6799e-104">在邏輯應用程式中透過 HTTP 端點呼叫、觸發或巢狀處理工作流程</span><span class="sxs-lookup"><span data-stu-id="6799e-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="6799e-105">您可以在邏輯應用程式中利用原生方式公開同步的 HTTP 端點作為觸發程序，以透過 URL 來觸發或呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6799e-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="6799e-106">您也可以使用可呼叫端點的模式，以在邏輯應用程式中巢狀處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="6799e-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="6799e-107">toocreate HTTP 端點，您可以新增這些觸發程序，讓您的 logic apps 可以接收連入要求：</span><span class="sxs-lookup"><span data-stu-id="6799e-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="6799e-108">要求</span><span class="sxs-lookup"><span data-stu-id="6799e-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="6799e-109">API 連線 Webhook</span><span class="sxs-lookup"><span data-stu-id="6799e-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="6799e-110">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="6799e-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="6799e-111">雖然我們的範例使用 hello**要求**觸發程序，您可以使用任何的 hello 列出 HTTP 觸發程序，而且所有適用的原則即會相同 toohello 其他觸發程序類型。</span><span class="sxs-lookup"><span data-stu-id="6799e-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="6799e-112">設定邏輯應用程式的 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="6799e-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="6799e-113">toocreate HTTP 端點，新增觸發程序可以接收傳入要求。</span><span class="sxs-lookup"><span data-stu-id="6799e-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="6799e-114">登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="6799e-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="6799e-115">連線 tooyour 邏輯應用程式，並開啟邏輯應用程式的設計工具。</span><span class="sxs-lookup"><span data-stu-id="6799e-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="6799e-116">新增可讓邏輯應用程式接收傳入要求的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6799e-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="6799e-117">例如，新增 hello**要求**觸發程序 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6799e-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="6799e-118">在下**要求本文 JSON 結構描述**，您可以選擇輸入如您預期 hello 觸發程序 tooreceive hello 裝載 （資料） 的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="6799e-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="6799e-119">hello 設計工具會使用此結構描述來產生 tooconsume、 parse 和傳遞資料，從 hello 觸發程序，透過您的工作流程，可以使用邏輯應用程式的權杖。</span><span class="sxs-lookup"><span data-stu-id="6799e-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="6799e-120">深入了解[從 JSON 結構描述產生的權杖](#generated-tokens)。</span><span class="sxs-lookup"><span data-stu-id="6799e-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="6799e-121">此範例中，輸入 hello hello 設計工具中顯示的結構描述：</span><span class="sxs-lookup"><span data-stu-id="6799e-121">For this example, enter hello schema shown in hello designer:</span></span>

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

    ![加入 hello 要求動作][1]

    > [!TIP]
    > 
    > <span data-ttu-id="6799e-123">您可以從這類工具產生的結構描述的範例 JSON 承載， [jsonschema.net](http://jsonschema.net/)，或在 hello**要求**觸發程序藉由選擇**使用範例內容 toogenerate 結構描述**。</span><span class="sxs-lookup"><span data-stu-id="6799e-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="6799e-124">輸入您的範例承載，然後選擇 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6799e-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="6799e-125">例如，此範例裝載︰</span><span class="sxs-lookup"><span data-stu-id="6799e-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="6799e-126">產生此結構描述︰</span><span class="sxs-lookup"><span data-stu-id="6799e-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="6799e-127">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6799e-127">Save your logic app.</span></span> <span data-ttu-id="6799e-128">在下**HTTP POST toothis URL**，您現在應該會發現產生的回呼 URL，如下列範例：</span><span class="sxs-lookup"><span data-stu-id="6799e-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![為端點產生的回呼 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="6799e-130">此 URL 包含用於驗證的 hello 查詢參數中的共用存取簽章 (SAS) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="6799e-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="6799e-131">您也可以從您的邏輯應用程式概觀 hello Azure 入口網站中取得 hello HTTP 端點 URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="6799e-132">在 [觸發程序記錄] 下方，選取觸發程序：</span><span class="sxs-lookup"><span data-stu-id="6799e-132">Under **Trigger History**, select your trigger:</span></span>

    ![從 Azure 入口網站取得 HTTP 端點 URL][2]

    <span data-ttu-id="6799e-134">或者，您可以取得 hello URL 進行此呼叫：</span><span class="sxs-lookup"><span data-stu-id="6799e-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="6799e-135">變更觸發程序的 hello HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="6799e-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="6799e-136">根據預設，hello**要求**觸發程序需要 HTTP POST 要求，但是您可以使用不同的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6799e-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="6799e-137">您只能指定一種方法類型。</span><span class="sxs-lookup"><span data-stu-id="6799e-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="6799e-138">在 [要求] 觸發程序上，選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="6799e-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="6799e-139">開啟 hello**方法**清單。</span><span class="sxs-lookup"><span data-stu-id="6799e-139">Open hello **Method** list.</span></span> <span data-ttu-id="6799e-140">在此範例中，選取 **GET**，稍後測試 HTTP 端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6799e-141">您可以選取任何其他 HTTP 方法，或指定專屬邏輯應用程式的自訂方法。</span><span class="sxs-lookup"><span data-stu-id="6799e-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![變更 HTTP 方法](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="6799e-143">透過 HTTP 端點 URL 接受參數</span><span class="sxs-lookup"><span data-stu-id="6799e-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="6799e-144">當您想 HTTP 端點 URL tooaccept 參數時，自訂觸發程序的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="6799e-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="6799e-145">在 [要求] 觸發程序上，選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="6799e-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="6799e-146">在下**方法**，指定您想要求 toouse hello HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6799e-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="6799e-147">此範例中，選取 hello**取得**方法，如果您還沒有這麼做，以便您可以測試 HTTP 端點的 URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6799e-148">當您指定觸發程序的相對路徑時，也必須明確地指定觸發程序的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6799e-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="6799e-149">在下**相對路徑**，指定您的 URL 應該接受的比方說，hello 參數的 hello 相對路徑`customers/{customerID}`。</span><span class="sxs-lookup"><span data-stu-id="6799e-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![指定 hello HTTP 方法和參數的相對路徑](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="6799e-151">toouse hello 參數，新增**回應**動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6799e-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="6799e-152">(在觸發程序下方，選擇 [新增步驟] > [新增動作] > [回應])。</span><span class="sxs-lookup"><span data-stu-id="6799e-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="6799e-153">在您的回應**主體**，包括您在觸發程序的相對路徑中指定的 hello 參數 hello token。</span><span class="sxs-lookup"><span data-stu-id="6799e-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="6799e-154">例如，tooreturn `Hello {customerID}`，更新您的回應**主體**與`Hello {customerID token}`。</span><span class="sxs-lookup"><span data-stu-id="6799e-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="6799e-155">hello 動態內容的清單應該會出現並顯示 hello`customerID`權杖以供您 tooselect。</span><span class="sxs-lookup"><span data-stu-id="6799e-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![加入參數 tooresponse 主體](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="6799e-157">您的 [本文] 應該如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6799e-157">Your **Body** should look like this example:</span></span>

    ![含參數的回應本文](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="6799e-159">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6799e-159">Save your logic app.</span></span> 

    <span data-ttu-id="6799e-160">您的 HTTP 端點 URL 現在例如包含 hello 相對路徑：</span><span class="sxs-lookup"><span data-stu-id="6799e-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="6799e-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="6799e-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="6799e-162">您的 HTTP 端點、 複製和貼上至另一個瀏覽器視窗，hello 更新的 URL，但取代的 tootest`{customerID}`與`123456`，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="6799e-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="6799e-163">您的瀏覽器應該顯示下列文字︰</span><span class="sxs-lookup"><span data-stu-id="6799e-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="6799e-164">從 JSON 結構描述產生邏輯應用程式的權杖</span><span class="sxs-lookup"><span data-stu-id="6799e-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="6799e-165">當您提供的 JSON 結構描述中您**要求**觸發程序、 hello 邏輯應用程式的設計工具會產生語彙基元屬性的該結構描述中。</span><span class="sxs-lookup"><span data-stu-id="6799e-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="6799e-166">您接著可以使用這些權杖，透過邏輯應用程式工作流程來傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="6799e-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="6799e-167">例如，如果您新增 hello`title`和`name`屬性 tooyour JSON 結構描述，及其語彙基元現在會於稍後步驟中工作流程的可用 toouse。</span><span class="sxs-lookup"><span data-stu-id="6799e-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="6799e-168">以下是 hello 完整的 JSON 結構描述：</span><span class="sxs-lookup"><span data-stu-id="6799e-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="6799e-169">建立邏輯應用程式的巢狀工作流程</span><span class="sxs-lookup"><span data-stu-id="6799e-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="6799e-170">您可以新增其他可接收要求的邏輯應用程式，以在邏輯應用程式中巢狀處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="6799e-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="6799e-171">tooinclude 這些邏輯應用程式中，新增 hello **Azure 邏輯應用程式-選擇 Logic Apps 工作流程**動作 tooyour 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6799e-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="6799e-172">您接著可以從合格的邏輯應用程式中進行選取。</span><span class="sxs-lookup"><span data-stu-id="6799e-172">You can then select from eligible logic apps.</span></span>

![新增另一個邏輯應用程式](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="6799e-174">透過 HTTP 端點呼叫或觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="6799e-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="6799e-175">建立 HTTP 端點之後，您可以觸發透過應用程式邏輯`POST`方法 toohello 完整的 URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="6799e-176">邏輯應用程式具有直接存取端點的內建支援。</span><span class="sxs-lookup"><span data-stu-id="6799e-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="6799e-177">參考來自傳入要求的內容</span><span class="sxs-lookup"><span data-stu-id="6799e-177">Reference content from an incoming request</span></span>

<span data-ttu-id="6799e-178">如果 hello 內容型別，則為`application/json`，您可以從 hello 連入要求參考屬性。</span><span class="sxs-lookup"><span data-stu-id="6799e-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="6799e-179">否則，內容會被視為單一的二進位單位，您可以將 tooother 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6799e-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="6799e-180">tooreference hello 工作流程內部此內容，您必須轉換該內容。</span><span class="sxs-lookup"><span data-stu-id="6799e-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="6799e-181">例如，如果您傳遞`application/xml`內容，您可以使用  `@xpath()` XPath 擷取，或`@json()`轉換 XML tooJSON。</span><span class="sxs-lookup"><span data-stu-id="6799e-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="6799e-182">深入了解如何[使用內容類型](../logic-apps/logic-apps-content-type.md)。</span><span class="sxs-lookup"><span data-stu-id="6799e-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="6799e-183">tooget hello 輸出從傳入要求，您可以使用 hello`@triggerOutputs()`函式。</span><span class="sxs-lookup"><span data-stu-id="6799e-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="6799e-184">hello 輸出看起來就像此範例中：</span><span class="sxs-lookup"><span data-stu-id="6799e-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="6799e-185">tooaccess hello`body`屬性明確地說，您可以使用 hello`@triggerBody()`捷徑。</span><span class="sxs-lookup"><span data-stu-id="6799e-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="6799e-186">回應 toorequests</span><span class="sxs-lookup"><span data-stu-id="6799e-186">Respond toorequests</span></span>

<span data-ttu-id="6799e-187">您可以藉由傳回內容 toohello 呼叫端啟動邏輯應用程式的 toorespond toocertain 要求。</span><span class="sxs-lookup"><span data-stu-id="6799e-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="6799e-188">tooconstruct hello 狀態碼、 標頭和您的回應主體中，您可以使用 hello**回應**動作。</span><span class="sxs-lookup"><span data-stu-id="6799e-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="6799e-189">這個動作可以出現在邏輯應用程式，不只是在您的工作流程的 hello 結尾的任何位置。</span><span class="sxs-lookup"><span data-stu-id="6799e-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="6799e-190">如果應用程式邏輯不包含**回應**，回應 hello HTTP 端點*立即*與**202 已接受**狀態。</span><span class="sxs-lookup"><span data-stu-id="6799e-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="6799e-191">此外，如 hello 原始要求 tooget hello 回應 hello 回應所需的所有步驟必須內都完成 hello[要求逾時限制](./logic-apps-limits-and-config.md)除非呼叫 hello 做為巢狀的邏輯應用程式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="6799e-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="6799e-192">如果沒有回應的情況發生這項限制內，hello 連入要求會逾時並收到 hello HTTP 回應**408 用戶端逾時**。</span><span class="sxs-lookup"><span data-stu-id="6799e-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="6799e-193">巢狀的 logic apps hello 父邏輯應用程式會繼續 toowait 完成為止，不論則需要多少時間的回應。</span><span class="sxs-lookup"><span data-stu-id="6799e-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="6799e-194">建構 hello 回應</span><span class="sxs-lookup"><span data-stu-id="6799e-194">Construct hello response</span></span>

<span data-ttu-id="6799e-195">您可以在 hello 回應主體中包含一個以上的標頭和任何類型的內容。</span><span class="sxs-lookup"><span data-stu-id="6799e-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="6799e-196">在我們的範例回應 hello 標頭指定 hello 回應的內容類型`application/json`。</span><span class="sxs-lookup"><span data-stu-id="6799e-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="6799e-197">和 hello 主體會包含`title`和`name`根據 hello hello 先前已更新的 JSON 結構描述，**要求**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6799e-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![HTTP 回應動作][3]

<span data-ttu-id="6799e-199">回應具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6799e-199">Responses have these properties:</span></span>

| <span data-ttu-id="6799e-200">屬性</span><span class="sxs-lookup"><span data-stu-id="6799e-200">Property</span></span> | <span data-ttu-id="6799e-201">說明</span><span class="sxs-lookup"><span data-stu-id="6799e-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6799e-202">StatusCode</span><span class="sxs-lookup"><span data-stu-id="6799e-202">statusCode</span></span> |<span data-ttu-id="6799e-203">指定回應 toohello 連入要求的 hello HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6799e-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="6799e-204">此代碼可以是任何以 2xx、4xx 或 5xx 開頭的有效狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6799e-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="6799e-205">但是，不允許 3xx 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6799e-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="6799e-206">headers</span><span class="sxs-lookup"><span data-stu-id="6799e-206">headers</span></span> |<span data-ttu-id="6799e-207">定義任意數目的標頭 tooinclude hello 回應中。</span><span class="sxs-lookup"><span data-stu-id="6799e-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="6799e-208">body</span><span class="sxs-lookup"><span data-stu-id="6799e-208">body</span></span> |<span data-ttu-id="6799e-209">指定本文物件可以是字串、JSON 物件，甚至是上一個步驟中所參考的二進位內容。</span><span class="sxs-lookup"><span data-stu-id="6799e-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="6799e-210">以下是何種 hello JSON 結構描述，看起來像現在 hello**回應**動作：</span><span class="sxs-lookup"><span data-stu-id="6799e-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="6799e-211">tooview hello JSON 個完整定義邏輯上的應用程式，hello 邏輯應用程式的設計工具，選擇**程式碼檢視**。</span><span class="sxs-lookup"><span data-stu-id="6799e-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="6799e-212">問答集</span><span class="sxs-lookup"><span data-stu-id="6799e-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="6799e-213">問︰URL 安全性如何？</span><span class="sxs-lookup"><span data-stu-id="6799e-213">Q: What about URL security?</span></span>

<span data-ttu-id="6799e-214">答：Azure 會使用共用存取簽章 (SAS)，安全地產生邏輯應用程式回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="6799e-215">這個簽章是以查詢參數的形式傳遞，且必須在引發您的邏輯應用程式之前先驗證。</span><span class="sxs-lookup"><span data-stu-id="6799e-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="6799e-216">Azure 會產生 hello 簽章使用的每個邏輯應用程式、 hello 觸發程序名稱和執行的 hello 作業的祕密金鑰的唯一組合。</span><span class="sxs-lookup"><span data-stu-id="6799e-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="6799e-217">因此除非有人存取 toohello 秘密邏輯應用程式金鑰，否則他們無法產生有效的簽章。</span><span class="sxs-lookup"><span data-stu-id="6799e-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6799e-218">生產環境與安全的系統，我們強烈建議針對直接從 hello 瀏覽器呼叫應用程式邏輯，因為：</span><span class="sxs-lookup"><span data-stu-id="6799e-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="6799e-219">hello 共用的存取金鑰會出現在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="6799e-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="6799e-220">您無法管理安全內容的原則，因為 tooshared 網域整個邏輯應用程式的客戶。</span><span class="sxs-lookup"><span data-stu-id="6799e-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="6799e-221">問︰我可以進一步設定 HTTP 端點嗎？</span><span class="sxs-lookup"><span data-stu-id="6799e-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="6799e-222">答︰可以，HTTP 端點透過 [**API 管理**](../api-management/api-management-key-concepts.md)來支援更進階的設定。</span><span class="sxs-lookup"><span data-stu-id="6799e-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="6799e-223">此服務也提供 hello 功能，針對您 tooconsistently 管理您的所有 Api，包括邏輯應用程式、 設定自訂網域名稱、 使用多個驗證方法及詳細資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="6799e-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="6799e-224">變更 hello 要求方法</span><span class="sxs-lookup"><span data-stu-id="6799e-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="6799e-225">變更 hello 的 hello 要求的 URL 區段</span><span class="sxs-lookup"><span data-stu-id="6799e-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="6799e-226">設定您的 API 管理網域中 hello [Azure 入口網站](https://portal.azure.com/ "Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="6799e-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="6799e-227">設定基本驗證的原則 toocheck</span><span class="sxs-lookup"><span data-stu-id="6799e-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="6799e-228">問： 什麼變更時從 hello 2014 年 12 月 1 日預覽移轉 hello 結構描述？</span><span class="sxs-lookup"><span data-stu-id="6799e-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="6799e-229">答︰以下是這些變更的摘要︰</span><span class="sxs-lookup"><span data-stu-id="6799e-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="6799e-230">2014 年 12 月 1 日預覽版</span><span class="sxs-lookup"><span data-stu-id="6799e-230">December 1, 2014 preview</span></span> | <span data-ttu-id="6799e-231">2016 年 6 月 1 日</span><span class="sxs-lookup"><span data-stu-id="6799e-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="6799e-232">按一下 [HTTP 接聽程式] API 應用程式</span><span class="sxs-lookup"><span data-stu-id="6799e-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="6799e-233">按一下 [手動觸發程序] \(不需要 API 應用程式)</span><span class="sxs-lookup"><span data-stu-id="6799e-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="6799e-234">HTTP 接聽程式設定 [自動傳送回應]</span><span class="sxs-lookup"><span data-stu-id="6799e-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="6799e-235">可能包含**回應**動作或不在 hello 工作流程定義</span><span class="sxs-lookup"><span data-stu-id="6799e-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="6799e-236">設定基本或 OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="6799e-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="6799e-237">透過 API 管理</span><span class="sxs-lookup"><span data-stu-id="6799e-237">via API Management</span></span> |
| <span data-ttu-id="6799e-238">設定 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="6799e-238">Configure HTTP method</span></span> |<span data-ttu-id="6799e-239">在 [顯示進階選項] 下方，選擇 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6799e-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="6799e-240">設定相對路徑</span><span class="sxs-lookup"><span data-stu-id="6799e-240">Configure relative path</span></span> |<span data-ttu-id="6799e-241">在 [顯示進階選項] 下方，新增相對路徑。</span><span class="sxs-lookup"><span data-stu-id="6799e-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="6799e-242">透過參考 hello 傳入內容`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="6799e-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="6799e-243">透過 `@triggerOutputs().body` 參考</span><span class="sxs-lookup"><span data-stu-id="6799e-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="6799e-244">**傳送 HTTP 回應**hello HTTP 接聽程式時採取的動作</span><span class="sxs-lookup"><span data-stu-id="6799e-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="6799e-245">按一下**回應 tooHTTP 要求**（沒有 API 應用程式所需）</span><span class="sxs-lookup"><span data-stu-id="6799e-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="6799e-246">取得說明</span><span class="sxs-lookup"><span data-stu-id="6799e-246">Get help</span></span>

<span data-ttu-id="6799e-247">tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="6799e-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="6799e-248">toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="6799e-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6799e-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6799e-249">Next steps</span></span>

* [<span data-ttu-id="6799e-250">撰寫邏輯應用程式定義</span><span class="sxs-lookup"><span data-stu-id="6799e-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="6799e-251">處理錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="6799e-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
