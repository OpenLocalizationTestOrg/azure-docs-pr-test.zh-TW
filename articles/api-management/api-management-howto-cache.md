---
title: "快取在 Azure API 管理 tooimprove 效能 aaaAdd |Microsoft 文件"
description: "了解 API 管理服務呼叫載入 tooimprove hello 延遲、 頻寬耗用量，以及 web 服務的方式。"
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
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>在 Azure API 管理中加入快取 tooimprove 效能
可以設定 API 管理中的作業進行回應快取。 對於不常變更的資料，回應快取可大幅降低 API 延遲、頻寬耗用量和 Web 服務負載。

本指南也說明如何 tooadd 回應快取 api 和設定 hello 範例回應 API 作業的原則。 然後，您就可以從 hello 開發人員入口網站 tooverify 快取中的動作呼叫 hello 作業。

> [!NOTE]
> 如需使用原則運算式依索引鍵快取項目的詳細資訊，請參閱 [在 Azure API 管理中自訂快取](api-management-sample-cache-by-key.md)。
> 
> 

## <a name="prerequisites"></a>必要條件
本指南中的下列 hello 步驟之前，您必須具有 API，並設定產品的 API 管理服務執行個體。 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。

## <a name="configure-caching"> </a>設定要快取的作業
在此步驟中，您將檢閱快取設定的 hello hello**取得資源 （快取）** hello 範例回應應用程式開發介面的作業。

> [!NOTE]
> 每個 API 管理服務執行個體是預先設定以回應 API 可與使用的 tooexperiment 和了解 API 管理。 如需詳細資訊，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]。
> 
> 

tooget 啟動，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。 這會帶您 toohello API 管理發行者入口網站。

![發行者入口網站][api-management-management-console]

按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**Echo API**。

![Echo API][api-management-echo-api]

按一下 hello**作業**索引標籤，然後再按一下 hello**取得資源 （快取）**作業 hello**作業**清單。

![Echo API operations][api-management-echo-api-operations]

按一下 hello**快取** 索引標籤 tooview hello 快取設定。 這項作業。

![Caching tab][api-management-caching-tab]

tooenable 快取作業中，選取 hello**啟用**核取方塊。 此範例中已啟用快取。

每個作業的回應做為索引鍵，根據 hello hello 值**區分的查詢字串參數**和**Vary 標頭所**欄位。 如果您想的 toocache 多個回應為基礎的查詢字串參數或標頭，您可以在這兩個欄位中設定它們。

**持續時間**指定快取的 hello 回應 hello 到期間隔。 在此範例中，是 hello 間隔**3600**秒，這是對等 tooone 小時。

使用快取設定，在此範例中的 hello，hello 第一個要求 toohello**取得資源 （快取）**作業傳回的回應 hello 後端服務。 此回應將會快取，做為索引鍵所指定的 hello 標頭和查詢字串參數。 後續呼叫 toohello 作業，並具有相符的參數，會有 hello 快取回應 hello 快取持續時間間隔過期之前傳回。

## <a name="caching-policies"></a>檢閱 hello 快取原則
您可以在此步驟中，檢閱快取設定 hello**取得資源 （快取）** hello 範例回應應用程式開發介面的作業。

當快取設定作業的 hello**快取**索引標籤上，快取原則會加入 hello 作業。 這些原則可以檢視和編輯在 hello 原則編輯器。

按一下**原則**從 hello **API 管理**功能表上，然後再選取 hello **Echo API / 取得資源 （快取）**從 hello**作業**下拉式清單。

![Policy scope operation][api-management-operation-dropdown]

這在 hello 原則編輯器中顯示 hello 原則，這項作業。

![API Management policy editor][api-management-policy-editor]

這項作業的 hello 原則定義包含 hello 原則定義 hello 快取設定，來檢閱使用 hello**快取**hello 上一個步驟中的索引標籤。

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
> 快取原則 hello 原則編輯器 中的所做的變更 toohello 就會反映在 hello**快取** 索引標籤的操作，反之亦然。
> 
> 

## <a name="test-operation"></a>呼叫作業並測試 hello 快取
toosee hello 快取中的動作，我們可以呼叫 hello 作業從 hello 開發人員入口網站。 按一下**開發人員入口網站**hello 右上方功能表中。

![開發人員入口網站][api-management-developer-portal-menu]

按一下**Api**在 hello 上方的功能表，然後選取  **Echo API**。

![Echo API][api-management-apis-echo-api]

> 如果您有只有一個應用程式開發介面設定，或顯示 tooyour 帳戶，然後按一下 應用程式開發介面引導您直接 toohello 作業，該 api。
> 
> 

選取 hello**取得資源 （快取）**作業，然後再按一下**開啟主控台**。

![Open console][api-management-open-console]

hello 主控台可讓您直接從 hello 開發人員入口網站的 tooinvoke 作業。

![主控台][api-management-console]

保留預設值 hello **param1**和**param2**。

選取 hello 所需的索引鍵，從 hello**訂閱金鑰**下拉式清單。 若您的帳戶只有一個訂用帳戶，則系統會自動選取它。

輸入**sampleheader:value1**在 hello**要求標頭**文字方塊。

按一下**HTTP Get**並記下的 hello 回應標頭。

輸入**sampleheader:value2**在 hello**要求標頭**文字方塊，然後再按一下**HTTP Get**。

請注意 hello 該值的**sampleheader**仍然是**value1** hello 回應中。 請嘗試一些不同的值，並請注意，要傳回快取的 hello 回應 hello 第一次呼叫。

輸入**25**到 hello **param2**欄位，，然後按一下**HTTP Get**。

請注意 hello 該值的**sampleheader**在 hello 回應現在是**value2**。 Hello 作業結果會根據查詢字串做為索引鍵，因為未傳回 hello 先前快取回的應。

## <a name="next-steps"> </a>後續步驟
* 如需有關快取原則的詳細資訊，請參閱[快取原則][ Caching policies]在 hello [API 管理原則參考][API Management policy reference]。
* 如需使用原則運算式依索引鍵快取項目的詳細資訊，請參閱 [在 Azure API 管理中自訂快取](api-management-sample-cache-by-key.md)。

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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
