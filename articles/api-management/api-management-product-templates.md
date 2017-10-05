---
title: "Azure API 管理中的產品範本 | Microsoft Docs"
description: "了解如何在「Azure API 管理」開發人員入口網站中自訂產品頁面的內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="4c30b-103">Azure API 管理中的產品範本</span><span class="sxs-lookup"><span data-stu-id="4c30b-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="4c30b-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="4c30b-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="4c30b-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="4c30b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="4c30b-106">本節的範本可讓您自訂開發人員入口網站中產品頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="4c30b-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="4c30b-107">產品清單</span><span class="sxs-lookup"><span data-stu-id="4c30b-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="4c30b-108">產品</span><span class="sxs-lookup"><span data-stu-id="4c30b-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="4c30b-109">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="4c30b-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="4c30b-110">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="4c30b-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="4c30b-111">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="4c30b-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="4c30b-112"><a name="ProductList"></a>產品清單</span><span class="sxs-lookup"><span data-stu-id="4c30b-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="4c30b-113">**清單**範本可讓您自訂開發人員入口網站中產品清單頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="4c30b-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="4c30b-114">![產品清單](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="4c30b-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4c30b-115">預設範本</span><span class="sxs-lookup"><span data-stu-id="4c30b-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="4c30b-116">控制</span><span class="sxs-lookup"><span data-stu-id="4c30b-116">Controls</span></span>  
 <span data-ttu-id="4c30b-117">`Product list` 範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="4c30b-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="4c30b-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="4c30b-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="4c30b-119">search-control</span><span class="sxs-lookup"><span data-stu-id="4c30b-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="4c30b-120">資料模型</span><span class="sxs-lookup"><span data-stu-id="4c30b-120">Data model</span></span>  
  
|<span data-ttu-id="4c30b-121">屬性</span><span class="sxs-lookup"><span data-stu-id="4c30b-121">Property</span></span>|<span data-ttu-id="4c30b-122">類型</span><span class="sxs-lookup"><span data-stu-id="4c30b-122">Type</span></span>|<span data-ttu-id="4c30b-123">說明</span><span class="sxs-lookup"><span data-stu-id="4c30b-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4c30b-124">分頁</span><span class="sxs-lookup"><span data-stu-id="4c30b-124">Paging</span></span>|<span data-ttu-id="4c30b-125">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="4c30b-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="4c30b-126">產品集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="4c30b-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="4c30b-127">篩選</span><span class="sxs-lookup"><span data-stu-id="4c30b-127">Filtering</span></span>|<span data-ttu-id="4c30b-128">[篩選](api-management-template-data-model-reference.md#Filtering)實體。</span><span class="sxs-lookup"><span data-stu-id="4c30b-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="4c30b-129">產品清單頁面的篩選資訊。</span><span class="sxs-lookup"><span data-stu-id="4c30b-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="4c30b-130">產品</span><span class="sxs-lookup"><span data-stu-id="4c30b-130">Products</span></span>|<span data-ttu-id="4c30b-131">[產品](api-management-template-data-model-reference.md#Product)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="4c30b-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="4c30b-132">目前使用者可看見的產品。</span><span class="sxs-lookup"><span data-stu-id="4c30b-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4c30b-133">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="4c30b-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="4c30b-134"><a name="Product"></a>產品</span><span class="sxs-lookup"><span data-stu-id="4c30b-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="4c30b-135">**產品**範本可讓您自訂開發人員入口網站的產品頁面主體。</span><span class="sxs-lookup"><span data-stu-id="4c30b-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="4c30b-136">![開發人員入口網站的產品頁面](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="4c30b-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4c30b-137">預設範本</span><span class="sxs-lookup"><span data-stu-id="4c30b-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="4c30b-138">控制</span><span class="sxs-lookup"><span data-stu-id="4c30b-138">Controls</span></span>  
 <span data-ttu-id="4c30b-139">`Product list` 範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="4c30b-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="4c30b-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="4c30b-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="4c30b-141">資料模型</span><span class="sxs-lookup"><span data-stu-id="4c30b-141">Data model</span></span>  
  
|<span data-ttu-id="4c30b-142">屬性</span><span class="sxs-lookup"><span data-stu-id="4c30b-142">Property</span></span>|<span data-ttu-id="4c30b-143">類型</span><span class="sxs-lookup"><span data-stu-id="4c30b-143">Type</span></span>|<span data-ttu-id="4c30b-144">說明</span><span class="sxs-lookup"><span data-stu-id="4c30b-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4c30b-145">產品</span><span class="sxs-lookup"><span data-stu-id="4c30b-145">Product</span></span>|[<span data-ttu-id="4c30b-146">產品</span><span class="sxs-lookup"><span data-stu-id="4c30b-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="4c30b-147">指定的產品。</span><span class="sxs-lookup"><span data-stu-id="4c30b-147">The specified product.</span></span>|  
|<span data-ttu-id="4c30b-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="4c30b-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="4c30b-149">布林值</span><span class="sxs-lookup"><span data-stu-id="4c30b-149">boolean</span></span>|<span data-ttu-id="4c30b-150">目前的使用者是否已訂閱此產品。</span><span class="sxs-lookup"><span data-stu-id="4c30b-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="4c30b-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="4c30b-151">SubscriptionState</span></span>|<span data-ttu-id="4c30b-152">number</span><span class="sxs-lookup"><span data-stu-id="4c30b-152">number</span></span>|<span data-ttu-id="4c30b-153">訂用帳戶的狀態。</span><span class="sxs-lookup"><span data-stu-id="4c30b-153">The state of the subscription.</span></span> <span data-ttu-id="4c30b-154">可能的狀態為：</span><span class="sxs-lookup"><span data-stu-id="4c30b-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="4c30b-155">-   `0 - suspended` – 訂用帳戶已遭封鎖，而且訂閱者無法呼叫產品的任何 API。</span><span class="sxs-lookup"><span data-stu-id="4c30b-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="4c30b-156">-   `1 - active` – 訂用帳戶是作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="4c30b-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="4c30b-157">-   `2 - expired` – 訂用帳戶已達到期日，因此已停用。</span><span class="sxs-lookup"><span data-stu-id="4c30b-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="4c30b-158">-   `3 - submitted` – 開發人員已提出訂用帳戶要求，但尚未進行核准或拒絕。</span><span class="sxs-lookup"><span data-stu-id="4c30b-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="4c30b-159">-   `4 - rejected` – 系統管理員已拒絕訂用帳戶要求。</span><span class="sxs-lookup"><span data-stu-id="4c30b-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="4c30b-160">-   `5 - cancelled` – 開發人員或系統管理員已取消訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c30b-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="4c30b-161">限制</span><span class="sxs-lookup"><span data-stu-id="4c30b-161">Limits</span></span>|<span data-ttu-id="4c30b-162">array</span><span class="sxs-lookup"><span data-stu-id="4c30b-162">array</span></span>|<span data-ttu-id="4c30b-163">此屬性已被取代而不應該使用。</span><span class="sxs-lookup"><span data-stu-id="4c30b-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="4c30b-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="4c30b-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="4c30b-165">布林值</span><span class="sxs-lookup"><span data-stu-id="4c30b-165">boolean</span></span>|<span data-ttu-id="4c30b-166">此訂用帳戶是否已啟用[委派](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/)。</span><span class="sxs-lookup"><span data-stu-id="4c30b-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="4c30b-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="4c30b-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="4c30b-168">字串</span><span class="sxs-lookup"><span data-stu-id="4c30b-168">string</span></span>|<span data-ttu-id="4c30b-169">如果已啟用委派，則是所委派的訂用帳戶 URL。</span><span class="sxs-lookup"><span data-stu-id="4c30b-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="4c30b-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="4c30b-170">IsAgreed</span></span>|<span data-ttu-id="4c30b-171">布林值</span><span class="sxs-lookup"><span data-stu-id="4c30b-171">boolean</span></span>|<span data-ttu-id="4c30b-172">如果產品有條款，目前的使用者是否已同意條款。</span><span class="sxs-lookup"><span data-stu-id="4c30b-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="4c30b-173">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4c30b-173">Subscriptions</span></span>|<span data-ttu-id="4c30b-174">[訂用帳戶摘要](api-management-template-data-model-reference.md#SubscriptionSummary)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="4c30b-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="4c30b-175">產品的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c30b-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="4c30b-176">Apis</span><span class="sxs-lookup"><span data-stu-id="4c30b-176">Apis</span></span>|<span data-ttu-id="4c30b-177">[API](api-management-template-data-model-reference.md#API) 實體的集合。</span><span class="sxs-lookup"><span data-stu-id="4c30b-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="4c30b-178">此產品中的 API。</span><span class="sxs-lookup"><span data-stu-id="4c30b-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="4c30b-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="4c30b-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="4c30b-180">布林值</span><span class="sxs-lookup"><span data-stu-id="4c30b-180">boolean</span></span>|<span data-ttu-id="4c30b-181">就訂用帳戶限制而言，目前的使用者是否有資格訂閱此產品。</span><span class="sxs-lookup"><span data-stu-id="4c30b-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="4c30b-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4c30b-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="4c30b-183">布林值</span><span class="sxs-lookup"><span data-stu-id="4c30b-183">boolean</span></span>|<span data-ttu-id="4c30b-184">就是否允許多個訂用帳戶而言，目前的使用者是否有資格訂閱此產品。</span><span class="sxs-lookup"><span data-stu-id="4c30b-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4c30b-185">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="4c30b-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="4c30b-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c30b-186">Next steps</span></span>
<span data-ttu-id="4c30b-187">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="4c30b-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>