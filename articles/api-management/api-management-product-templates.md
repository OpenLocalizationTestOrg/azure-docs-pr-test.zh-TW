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
# <a name="product-templates-in-azure-api-management"></a>Azure API 管理中的產品範本
Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。 使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。  
  
 本節中的 hello 範本允許您 toocustomize hello 網頁內容的 hello 產品 hello 開發人員入口網站中。  
  
-   [產品清單](#ProductList)  
  
-   [產品](#Product)  
  
> [!NOTE]
>  預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。 您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。 如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。  
  
##  <a name="ProductList"></a>產品清單  
 hello**產品清單**範本可讓您 toocustomize hello 主體 hello 產品清單頁面 hello 開發人員入口網站中。  
  
 ![產品清單](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>預設範本  
  
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
  
### <a name="controls"></a>控制  
 hello`Product list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>資料模型  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|分頁|[分頁](api-management-template-data-model-reference.md#Paging)實體。|hello hello 產品集合的分頁資訊。|  
|篩選|[篩選](api-management-template-data-model-reference.md#Filtering)實體。|hello 讓 hello 產品清單頁面篩選資訊。|  
|產品|[產品](api-management-template-data-model-reference.md#Product)實體的集合。|hello 產品可見 toohello 目前的使用者。|  
  
### <a name="sample-template-data"></a>範例範本資料  
  
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
  
##  <a name="Product"></a>產品  
 hello**產品**範本可讓您 toocustomize hello hello 產品頁面主體 hello 開發人員入口網站中。  
  
 ![開發人員入口網站的產品頁面](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>預設範本  
  
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
  
### <a name="controls"></a>控制  
 hello`Product list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>資料模型  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|產品|[產品](api-management-template-data-model-reference.md#Product)|hello 指定的產品。|  
|IsDeveloperSubscribed|布林值|Hello 目前使用者是否已訂閱的 toothis 產品。|  
|SubscriptionState|number|hello hello 訂用帳戶狀態。 可能的狀態為：<br /><br /> -   `0 - suspended`– hello 訂用帳戶遭到封鎖，且 hello 訂閱者無法呼叫 hello 產品的任何應用程式開發介面。<br />-   `1 - active`– hello 訂閱在作用中。<br />-   `2 - expired`– hello 訂用帳戶已達到其到期日並且已停用。<br />-   `3 - submitted`– hello 訂用帳戶要求 hello 開發人員已發出但尚未核准或拒絕。<br />-   `4 - rejected`– 系統管理員已拒絕 hello 訂用帳戶要求。<br />-   `5 - cancelled`– hello 開發人員或管理員已取消 hello 訂用帳戶。|  
|限制|array|此屬性已被取代而不應該使用。|  
|DelegatedSubscriptionEnabled|布林值|此訂用帳戶是否已啟用[委派](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/)。|  
|DelegatedSubscriptionUrl|字串|如果已啟用委派，hello 委派訂閱 URL。|  
|IsAgreed|布林值|如果 hello 產品有規定，是否 hello 目前使用者已同意 toohello 條款。|  
|訂用帳戶|[訂用帳戶摘要](api-management-template-data-model-reference.md#SubscriptionSummary)實體的集合。|hello 訂閱 toohello 產品。|  
|Apis|[API](api-management-template-data-model-reference.md#API) 實體的集合。|本產品中的 hello 應用程式開發介面。|  
|CannotAddBecauseSubscriptionNumberLimitReached|布林值|Hello 目前使用者是否有資格 toosubscribe toothis 產品而考慮 toohello 訂用帳戶限制。|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|布林值|Hello 目前使用者是否具有考慮 toomultiple 訂閱被允許或不合格 toosubscribe toothis 產品。|  
  
### <a name="sample-template-data"></a>範例範本資料  
  
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

## <a name="next-steps"></a>後續步驟
如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。
