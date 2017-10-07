---
title: "aaaHow tooadd 作業 tooan API 在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何在 Azure API 管理 tooadd 作業 tooan 應用程式開發介面。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="6dc6c-103">如何在 Azure API 管理 tooadd 作業 tooan 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="6dc6c-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="6dc6c-104">您必須先加入作業，才能夠使用 API 管理中的 API。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="6dc6c-105">本指南適顯示如何 tooadd 及 API 管理中設定不同類型的作業 tooan 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="6dc6c-106"><a name="add-operation"> </a>新增作業</span><span class="sxs-lookup"><span data-stu-id="6dc6c-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="6dc6c-107">作業可加入與 hello 發行者入口網站中設定 tooan API。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="6dc6c-108">tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="6dc6c-110">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="6dc6c-111">Hello 發行者入口網站，然後選取 hello 中選取 hello 所需的應用程式開發介面**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![作業][api-management-operations]

<span data-ttu-id="6dc6c-113">按一下**Add 作業**tooadd 新作業。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="6dc6c-114">hello**新作業**將會顯示與 hello**簽章**預設會選取索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Add operation][api-management-add-operation]

<span data-ttu-id="6dc6c-116">指定 hello **HTTP 指令動詞**hello 下拉式清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![HTTP method][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="6dc6c-118">URL 片段包含一或多個 URL 路徑區段和零個或多個查詢字串參數中輸入，藉以定義 hello URL 範本。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="6dc6c-119">hello URL 範本，附加的 toohello hello 應用程式開發介面，基底 URL 會識別單一 HTTP 作業。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="6dc6c-120">可能包含一或多個以大括弧識別的具名變數部分。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="6dc6c-121">這些變數的組件稱為範本參數，而且會動態指派時正在處理 hello API 管理平台 hello 要求從 hello 要求 URL 中擷取的值。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="6dc6c-122">hello URL 範本可以包含萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="6dc6c-123">例如，指定`/*`會向前復原所有要求的 HTTP 方法 toohello 回都結束服務。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="6dc6c-125">如有需要，指定 hello**重寫 URL 範本**。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="6dc6c-126">這可讓您 toouse hello 標準 URL 範本為處理傳入要求 hello 前端上的，同時呼叫 hello 後端透過根據 toohello 轉換 URL 重寫範本。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="6dc6c-127">來自 hello URL 範本的範本參數應該用於 hello 重寫成範本。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="6dc6c-128">hello 下列範例顯示如何在內容編碼方式 hello hello 上一個範例的 web 服務中的路徑區段可供做為查詢參數，在 hello 發行 hello 透過 API 管理平台使用 hello URL 範本的應用程式開發介面的型別。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![URL template rewrite][api-management-url-template-rewrite]

<span data-ttu-id="6dc6c-130">呼叫端 toohello 作業將會使用 hello 格式`/customers?customerid=ALFKI`，這將會太對應`/Customers('ALFKI')`hello 後端服務會叫用。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="6dc6c-131">**顯示**名稱和**描述**提供 hello 作業的描述，而且使用的 tooprovide 文件 toohello hello 開發人員入口網站中使用此 API 的開發人員。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![說明][api-management-description]

<span data-ttu-id="6dc6c-133">hello 作業描述中可以指定做為純文字或 HTML hello**描述**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="6dc6c-134"><a name="operation-caching"> </a>作業快取</span><span class="sxs-lookup"><span data-stu-id="6dc6c-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="6dc6c-135">回應快取可減少 hello API 取用者，降低頻寬耗用量看得見的延遲，並減少 hello 負載 hello HTTP web 服務實作 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="6dc6c-136">tooeasily 和快速啟用快取 hello 作業中，選取 hello**快取**索引標籤上，並檢查 hello**啟用**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![快取][api-management-caching-tab]

<span data-ttu-id="6dc6c-138">**持續時間**指定 hello 時哪些 hello 作業回應會保留在 hello 快取的時間週期。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="6dc6c-139">hello 預設值為 3600 秒或 1 小時。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="6dc6c-140">快取索引鍵是使用的 toodifferentiate 各次回應之間，如此 hello 回應對應 tooeach 不同的快取索引鍵，會在它自己個別快取的值。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="6dc6c-141">（選擇性） 輸入 特定的查詢字串參數及/或計算快取索引鍵值在 hello 時使用的 HTTP 標頭 toobe**區分的查詢字串參數**和**Vary 標頭所**文字方塊分別。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="6dc6c-142">當不會指定的完整要求 URL，而且下列 HTTP 標頭值的 hello 用於快取金鑰的產生：**接受**和**Accept-charset**。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="6dc6c-143">如需有關快取和快取原則的詳細資訊，請參閱[toocache 作業會在 Azure API 管理如何產生][How toocache operation results in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="6dc6c-144"><a name="request-parameters"> </a>要求參數</span><span class="sxs-lookup"><span data-stu-id="6dc6c-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="6dc6c-145">作業參數是在 hello 參數 索引標籤上管理。指定在 hello 參數**URL 範本**上 hello**簽章** 索引標籤會自動新增，而且可以變更只是藉由編輯 hello URL 範本。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="6dc6c-146">可手動輸入其他參數。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="6dc6c-147">按一下新的查詢參數，tooadd**加入查詢參數**並輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="6dc6c-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="6dc6c-148">**名稱** - 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="6dc6c-149">**描述**-（選擇性） hello 參數的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="6dc6c-150">**型別**-hello 下拉式清單中選取的參數類型。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="6dc6c-151">**值**-可以指派 toothis 參數的值。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="6dc6c-152">其中一個 hello 值可標示為預設值 （選擇性）。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="6dc6c-153">**需要**-藉由檢查 hello 核取方塊，讓 hello 參數成為強制。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![要求參數][api-management-request-parameters]

## <span data-ttu-id="6dc6c-155"><a name="request-body"> </a>要求本文</span><span class="sxs-lookup"><span data-stu-id="6dc6c-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="6dc6c-156">如果允許 hello 作業 （例如 PUT、 POST） 和要求主體，您可能會提供一個範例，它在所有 hello 支援表示格式 (例如 json、 XML)。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="6dc6c-157">hello 要求主體使用僅供文件，但不會驗證。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="6dc6c-158">要求本文，tooenter 切換 toohello**主體** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="6dc6c-159">按一下**新增表示**，開始輸入所需的內容類型名稱 (例如應用程式/json)，則會在 [hello] 下拉式清單中選取它，並貼上 hello 預期 hello 文字方塊中的 hello 選格式的要求主體範例。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Request body][api-management-request-body]

<span data-ttu-id="6dc6c-161">在其他 toorepresentations，也可以指定選擇性的文字中描述 hello**描述**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="6dc6c-162"><a name="responses"> </a>回應</span><span class="sxs-lookup"><span data-stu-id="6dc6c-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="6dc6c-163">是很好的作法 tooprovide 範例的所有狀態碼，可能會產生 hello 作業的回應。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="6dc6c-164">每個狀態碼可能有一個以上的回應主體範例，各供一個 hello 支援的內容類型。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="6dc6c-165">tooadd 回應時，按一下**新增**並開始輸入 hello 所需狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="6dc6c-166">在此範例 hello 狀態程式碼是**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="6dc6c-167">一旦 hello 程式碼顯示在 [hello] 下拉式清單中，選取它，而且 hello 回應程式碼建立和加入 tooyour 作業。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Response code][api-management-response-code]

<span data-ttu-id="6dc6c-169">按一下**新增表示**，開始輸入 hello 所需的內容類型名稱 (例如應用程式/json)，然後選取在 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Body content type][api-management-response-body-content-type]

<span data-ttu-id="6dc6c-171">Hello 選取格式貼入 hello 文字方塊 hello 回應主體範例。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Response body][api-management-response-body]

<span data-ttu-id="6dc6c-173">如有需要，新增選用的描述成 hello**描述**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="6dc6c-174">一旦設定 hello 作業之後，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="6dc6c-175"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="6dc6c-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="6dc6c-176">一旦 hello 作業加入 tooan API，hello 下一個步驟為 tooassociate hello API 與產品，並將它發行，可讓開發人員可以呼叫其作業。</span><span class="sxs-lookup"><span data-stu-id="6dc6c-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="6dc6c-177">[如何 toocreate 及發佈產品][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="6dc6c-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
