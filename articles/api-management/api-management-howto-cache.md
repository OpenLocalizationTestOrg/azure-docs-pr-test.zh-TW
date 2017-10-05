---
title: "新增快取以改善 Azure API 管理的效能 | Microsoft Docs"
description: "了解如何改善 API 管理服務呼叫的延遲、頻寬耗用量和 Web 服務負載。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="29bc2-103">新增快取以改善 Azure API 管理的效能</span><span class="sxs-lookup"><span data-stu-id="29bc2-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="29bc2-104">可以設定 API 管理中的作業進行回應快取。</span><span class="sxs-lookup"><span data-stu-id="29bc2-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="29bc2-105">對於不常變更的資料，回應快取可大幅降低 API 延遲、頻寬耗用量和 Web 服務負載。</span><span class="sxs-lookup"><span data-stu-id="29bc2-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="29bc2-106">本指南說明如何新增 API 的回應快取，以及設定範例 Echo API 作業的原則。</span><span class="sxs-lookup"><span data-stu-id="29bc2-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="29bc2-107">您之後可以從開發人員入口網站呼叫作業，確認快取作用中。</span><span class="sxs-lookup"><span data-stu-id="29bc2-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="29bc2-108">如需使用原則運算式依索引鍵快取項目的詳細資訊，請參閱 [在 Azure API 管理中自訂快取](api-management-sample-cache-by-key.md)。</span><span class="sxs-lookup"><span data-stu-id="29bc2-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="29bc2-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="29bc2-109">Prerequisites</span></span>
<span data-ttu-id="29bc2-110">遵循本指南中的步驟之前，您必須擁有已設定 API 和產品的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="29bc2-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="29bc2-111">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="29bc2-112"><a name="configure-caching"> </a>設定要快取的作業</span><span class="sxs-lookup"><span data-stu-id="29bc2-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="29bc2-113">在此步驟中，您將檢閱範例 Echo API 的 **取得資源 (快取)** 作業的快取設定。</span><span class="sxs-lookup"><span data-stu-id="29bc2-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="29bc2-114">每個「API 管理」服務執行個體皆隨附預先設定的範例 Echo API，可供您試驗與了解「API 管理」。</span><span class="sxs-lookup"><span data-stu-id="29bc2-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="29bc2-115">如需詳細資訊，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="29bc2-116">若要開始，請在 API 管理服務的 Azure 入口網站中按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="29bc2-117">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="29bc2-117">This takes you to the API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="29bc2-119">從左側 [API 管理] 功能表按一下 [API]，然後按一下 [Echo API]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![Echo API][api-management-echo-api]

<span data-ttu-id="29bc2-121">按一下 [作業] 索引標籤，然後從 [作業] 清單中按一下 [取得資源 (快取)] 作業。</span><span class="sxs-lookup"><span data-stu-id="29bc2-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Echo API operations][api-management-echo-api-operations]

<span data-ttu-id="29bc2-123">按一下 [快取]  索引標籤，以檢視此作業的快取設定。</span><span class="sxs-lookup"><span data-stu-id="29bc2-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Caching tab][api-management-caching-tab]

<span data-ttu-id="29bc2-125">若要對作業啟用快取，請選取 [啟用]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="29bc2-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="29bc2-126">此範例中已啟用快取。</span><span class="sxs-lookup"><span data-stu-id="29bc2-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="29bc2-127">每一個作業回應都是根據 [依查詢字串參數改變] 和 [依標頭改變] 欄位的值來識別。</span><span class="sxs-lookup"><span data-stu-id="29bc2-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="29bc2-128">如果您想要根據查詢字串參數或標頭來快取多個回應，您可以在這兩個欄位中設定。</span><span class="sxs-lookup"><span data-stu-id="29bc2-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="29bc2-129">[持續期間] 指定快取回應的到期間隔。</span><span class="sxs-lookup"><span data-stu-id="29bc2-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="29bc2-130">在此範例中，間隔是 **3600** 秒，相當於一小時。</span><span class="sxs-lookup"><span data-stu-id="29bc2-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="29bc2-131">根據此範例中的快取組態，對 **取得資源 (快取)** 作業的第一個要求是從後端服務傳回回應。</span><span class="sxs-lookup"><span data-stu-id="29bc2-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="29bc2-132">此回應將被快取，並依指定的標頭和查詢字串參數來識別。</span><span class="sxs-lookup"><span data-stu-id="29bc2-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="29bc2-133">後續使用相符的參數呼叫此操作時，將傳回快取的回應，直到快取期間間隔到期為止。</span><span class="sxs-lookup"><span data-stu-id="29bc2-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="29bc2-134"><a name="caching-policies"> </a>檢閱快取原則</span><span class="sxs-lookup"><span data-stu-id="29bc2-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="29bc2-135">在此步驟中，您將檢閱範例 Echo API 的 **取得資源 (快取)** 作業快取設定。</span><span class="sxs-lookup"><span data-stu-id="29bc2-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="29bc2-136">在 [快取]  索引標籤上設定操作的快取設定時，就會加入操作的快取原則。</span><span class="sxs-lookup"><span data-stu-id="29bc2-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="29bc2-137">您可以在原則編輯器中檢閱和編輯這些原則。</span><span class="sxs-lookup"><span data-stu-id="29bc2-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="29bc2-138">從左邊的 [API 管理] 功能表中按一下 [原則]，然後從 [作業] 下拉式清單中選取 [Echo API/取得資源 (快取)]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Policy scope operation][api-management-operation-dropdown]

<span data-ttu-id="29bc2-140">這樣會在原則編輯器中顯示此操作的原則。</span><span class="sxs-lookup"><span data-stu-id="29bc2-140">This displays the policies for this operation in the policy editor.</span></span>

![API Management policy editor][api-management-policy-editor]

<span data-ttu-id="29bc2-142">此操作的原則定義中包含一些原則，定義上一個步驟中使用 [快取]  索引標籤所檢閱的快取組態。</span><span class="sxs-lookup"><span data-stu-id="29bc2-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="29bc2-143">在原則編輯器中對快取原則所做的變更，將反映在作業的 [快取] 索引標籤中，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="29bc2-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="29bc2-144"><a name="test-operation"> </a>呼叫作業和測試快取</span><span class="sxs-lookup"><span data-stu-id="29bc2-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="29bc2-145">為了瞭解快取的運作方式，我們可以從開發人員入口網站呼叫操作。</span><span class="sxs-lookup"><span data-stu-id="29bc2-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="29bc2-146">在右上角的功能表中按一下 [開發人員入口網站]  。</span><span class="sxs-lookup"><span data-stu-id="29bc2-146">Click **Developer portal** in the top right menu.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="29bc2-148">在頂端功能表中按一下 [API]，然後選取 [Echo API]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> <span data-ttu-id="29bc2-150">如果您的帳戶只設定或只看見一個 API，按一下 API 將帶您直接前往該 API 的作業。</span><span class="sxs-lookup"><span data-stu-id="29bc2-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="29bc2-151">選取 [取得資源 (快取)] 作業，然後按一下 [開啟主控台]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="29bc2-153">主控台可讓您直接從開發人員入口網站叫用操作。</span><span class="sxs-lookup"><span data-stu-id="29bc2-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![主控台][api-management-console]

<span data-ttu-id="29bc2-155">保留 **param1** 和 **param2** 的預設值。</span><span class="sxs-lookup"><span data-stu-id="29bc2-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="29bc2-156">從 [subscription-key]  下拉式清單中選取所需的金鑰。</span><span class="sxs-lookup"><span data-stu-id="29bc2-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="29bc2-157">若您的帳戶只有一個訂用帳戶，則系統會自動選取它。</span><span class="sxs-lookup"><span data-stu-id="29bc2-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="29bc2-158">在 [要求標頭] 文字方塊中輸入 **sampleheader:value1**。</span><span class="sxs-lookup"><span data-stu-id="29bc2-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="29bc2-159">按一下 [HTTP Get]  ，並記下回應標頭。</span><span class="sxs-lookup"><span data-stu-id="29bc2-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="29bc2-160">在 [要求標頭] 文字方塊中輸入 **sampleheader:value2**，然後按一下 [HTTP Get]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="29bc2-161">請注意，在回應中，**sampleheader** 的值仍然是 **value1**。</span><span class="sxs-lookup"><span data-stu-id="29bc2-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="29bc2-162">請試驗一些不同的值，可發現傳回第一次呼叫的快取回應。</span><span class="sxs-lookup"><span data-stu-id="29bc2-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="29bc2-163">在 [param2] 欄位中輸入 **25**，然後按一下 [HTTP Get]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="29bc2-164">請注意，回應中的 **sampleheader** 值現在是 **value2**。</span><span class="sxs-lookup"><span data-stu-id="29bc2-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="29bc2-165">因為操作結果是依查詢字串來識別，所以不會傳回前一個快取回應。</span><span class="sxs-lookup"><span data-stu-id="29bc2-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="29bc2-166"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="29bc2-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="29bc2-167">如需快取原則的詳細資訊，請參閱 [API 管理原則參考文件][API Management policy reference]中的[快取原則][Caching policies]。</span><span class="sxs-lookup"><span data-stu-id="29bc2-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="29bc2-168">如需使用原則運算式依索引鍵快取項目的詳細資訊，請參閱 [在 Azure API 管理中自訂快取](api-management-sample-cache-by-key.md)。</span><span class="sxs-lookup"><span data-stu-id="29bc2-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
