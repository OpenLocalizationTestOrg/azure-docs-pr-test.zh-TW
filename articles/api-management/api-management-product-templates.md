---
title: "在 Azure API 管理 aaaProduct 範本 |Microsoft 文件"
description: "了解 hello Azure API 管理開發人員入口網站中的 hello 產品 toocustomize hello 內容頁面的方式。"
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
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="f433a-103">Azure API 管理中的產品範本</span><span class="sxs-lookup"><span data-stu-id="f433a-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="f433a-104">Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。</span><span class="sxs-lookup"><span data-stu-id="f433a-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="f433a-105">使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="f433a-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="f433a-106">本節中的 hello 範本允許您 toocustomize hello 網頁內容的 hello 產品 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f433a-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="f433a-107">產品清單</span><span class="sxs-lookup"><span data-stu-id="f433a-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="f433a-108">產品</span><span class="sxs-lookup"><span data-stu-id="f433a-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="f433a-109">預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。</span><span class="sxs-lookup"><span data-stu-id="f433a-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="f433a-110">您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。</span><span class="sxs-lookup"><span data-stu-id="f433a-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="f433a-111">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="f433a-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="f433a-112"><a name="ProductList"></a>產品清單</span><span class="sxs-lookup"><span data-stu-id="f433a-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="f433a-113">hello**產品清單**範本可讓您 toocustomize hello 主體 hello 產品清單頁面 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f433a-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f433a-114">![產品清單](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="f433a-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="f433a-115">預設範本</span><span class="sxs-lookup"><span data-stu-id="f433a-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="f433a-116">控制</span><span class="sxs-lookup"><span data-stu-id="f433a-116">Controls</span></span>  
 <span data-ttu-id="f433a-117">hello`Product list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="f433a-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="f433a-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="f433a-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="f433a-119">search-control</span><span class="sxs-lookup"><span data-stu-id="f433a-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="f433a-120">資料模型</span><span class="sxs-lookup"><span data-stu-id="f433a-120">Data model</span></span>  
  
|<span data-ttu-id="f433a-121">屬性</span><span class="sxs-lookup"><span data-stu-id="f433a-121">Property</span></span>|<span data-ttu-id="f433a-122">類型</span><span class="sxs-lookup"><span data-stu-id="f433a-122">Type</span></span>|<span data-ttu-id="f433a-123">說明</span><span class="sxs-lookup"><span data-stu-id="f433a-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="f433a-124">分頁</span><span class="sxs-lookup"><span data-stu-id="f433a-124">Paging</span></span>|<span data-ttu-id="f433a-125">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="f433a-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="f433a-126">hello hello 產品集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="f433a-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="f433a-127">篩選</span><span class="sxs-lookup"><span data-stu-id="f433a-127">Filtering</span></span>|<span data-ttu-id="f433a-128">[篩選](api-management-template-data-model-reference.md#Filtering)實體。</span><span class="sxs-lookup"><span data-stu-id="f433a-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="f433a-129">hello 讓 hello 產品清單頁面篩選資訊。</span><span class="sxs-lookup"><span data-stu-id="f433a-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="f433a-130">產品</span><span class="sxs-lookup"><span data-stu-id="f433a-130">Products</span></span>|<span data-ttu-id="f433a-131">[產品](api-management-template-data-model-reference.md#Product)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="f433a-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="f433a-132">hello 產品可見 toohello 目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="f433a-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="f433a-133">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="f433a-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="f433a-134"><a name="Product"></a>產品</span><span class="sxs-lookup"><span data-stu-id="f433a-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="f433a-135">hello**產品**範本可讓您 toocustomize hello hello 產品頁面主體 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f433a-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f433a-136">![開發人員入口網站的產品頁面](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="f433a-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="f433a-137">預設範本</span><span class="sxs-lookup"><span data-stu-id="f433a-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="f433a-138">控制</span><span class="sxs-lookup"><span data-stu-id="f433a-138">Controls</span></span>  
 <span data-ttu-id="f433a-139">hello`Product list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="f433a-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="f433a-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="f433a-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="f433a-141">資料模型</span><span class="sxs-lookup"><span data-stu-id="f433a-141">Data model</span></span>  
  
|<span data-ttu-id="f433a-142">屬性</span><span class="sxs-lookup"><span data-stu-id="f433a-142">Property</span></span>|<span data-ttu-id="f433a-143">類型</span><span class="sxs-lookup"><span data-stu-id="f433a-143">Type</span></span>|<span data-ttu-id="f433a-144">說明</span><span class="sxs-lookup"><span data-stu-id="f433a-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="f433a-145">產品</span><span class="sxs-lookup"><span data-stu-id="f433a-145">Product</span></span>|[<span data-ttu-id="f433a-146">產品</span><span class="sxs-lookup"><span data-stu-id="f433a-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="f433a-147">hello 指定的產品。</span><span class="sxs-lookup"><span data-stu-id="f433a-147">hello specified product.</span></span>|  
|<span data-ttu-id="f433a-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="f433a-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="f433a-149">布林值</span><span class="sxs-lookup"><span data-stu-id="f433a-149">boolean</span></span>|<span data-ttu-id="f433a-150">Hello 目前使用者是否已訂閱的 toothis 產品。</span><span class="sxs-lookup"><span data-stu-id="f433a-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="f433a-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="f433a-151">SubscriptionState</span></span>|<span data-ttu-id="f433a-152">number</span><span class="sxs-lookup"><span data-stu-id="f433a-152">number</span></span>|<span data-ttu-id="f433a-153">hello hello 訂用帳戶狀態。</span><span class="sxs-lookup"><span data-stu-id="f433a-153">hello state of hello subscription.</span></span> <span data-ttu-id="f433a-154">可能的狀態為：</span><span class="sxs-lookup"><span data-stu-id="f433a-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="f433a-155">-   `0 - suspended`– hello 訂用帳戶遭到封鎖，且 hello 訂閱者無法呼叫 hello 產品的任何應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f433a-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="f433a-156">-   `1 - active`– hello 訂閱在作用中。</span><span class="sxs-lookup"><span data-stu-id="f433a-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="f433a-157">-   `2 - expired`– hello 訂用帳戶已達到其到期日並且已停用。</span><span class="sxs-lookup"><span data-stu-id="f433a-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="f433a-158">-   `3 - submitted`– hello 訂用帳戶要求 hello 開發人員已發出但尚未核准或拒絕。</span><span class="sxs-lookup"><span data-stu-id="f433a-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="f433a-159">-   `4 - rejected`– 系統管理員已拒絕 hello 訂用帳戶要求。</span><span class="sxs-lookup"><span data-stu-id="f433a-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="f433a-160">-   `5 - cancelled`– hello 開發人員或管理員已取消 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f433a-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="f433a-161">限制</span><span class="sxs-lookup"><span data-stu-id="f433a-161">Limits</span></span>|<span data-ttu-id="f433a-162">array</span><span class="sxs-lookup"><span data-stu-id="f433a-162">array</span></span>|<span data-ttu-id="f433a-163">此屬性已被取代而不應該使用。</span><span class="sxs-lookup"><span data-stu-id="f433a-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="f433a-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="f433a-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="f433a-165">布林值</span><span class="sxs-lookup"><span data-stu-id="f433a-165">boolean</span></span>|<span data-ttu-id="f433a-166">此訂用帳戶是否已啟用[委派](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/)。</span><span class="sxs-lookup"><span data-stu-id="f433a-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="f433a-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="f433a-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="f433a-168">字串</span><span class="sxs-lookup"><span data-stu-id="f433a-168">string</span></span>|<span data-ttu-id="f433a-169">如果已啟用委派，hello 委派訂閱 URL。</span><span class="sxs-lookup"><span data-stu-id="f433a-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="f433a-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="f433a-170">IsAgreed</span></span>|<span data-ttu-id="f433a-171">布林值</span><span class="sxs-lookup"><span data-stu-id="f433a-171">boolean</span></span>|<span data-ttu-id="f433a-172">如果 hello 產品有規定，是否 hello 目前使用者已同意 toohello 條款。</span><span class="sxs-lookup"><span data-stu-id="f433a-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="f433a-173">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f433a-173">Subscriptions</span></span>|<span data-ttu-id="f433a-174">[訂用帳戶摘要](api-management-template-data-model-reference.md#SubscriptionSummary)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="f433a-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="f433a-175">hello 訂閱 toohello 產品。</span><span class="sxs-lookup"><span data-stu-id="f433a-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="f433a-176">Apis</span><span class="sxs-lookup"><span data-stu-id="f433a-176">Apis</span></span>|<span data-ttu-id="f433a-177">[API](api-management-template-data-model-reference.md#API) 實體的集合。</span><span class="sxs-lookup"><span data-stu-id="f433a-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="f433a-178">本產品中的 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f433a-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="f433a-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="f433a-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="f433a-180">布林值</span><span class="sxs-lookup"><span data-stu-id="f433a-180">boolean</span></span>|<span data-ttu-id="f433a-181">Hello 目前使用者是否有資格 toosubscribe toothis 產品而考慮 toohello 訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="f433a-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="f433a-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="f433a-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="f433a-183">布林值</span><span class="sxs-lookup"><span data-stu-id="f433a-183">boolean</span></span>|<span data-ttu-id="f433a-184">Hello 目前使用者是否具有考慮 toomultiple 訂閱被允許或不合格 toosubscribe toothis 產品。</span><span class="sxs-lookup"><span data-stu-id="f433a-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="f433a-185">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="f433a-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="f433a-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f433a-186">Next steps</span></span>
<span data-ttu-id="f433a-187">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f433a-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
