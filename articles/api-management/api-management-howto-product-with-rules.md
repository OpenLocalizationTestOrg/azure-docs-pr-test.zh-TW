---
title: "aaaProtect 您的 API，使用 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 tooprotect 配額和節流設定 （速率限制） 的原則與您的 API。"
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>使用 Azure API 管理以頻率限制保護 API
本指南也說明是多麼的輕鬆 tooadd 保護您的後端 API 藉由使用 Azure API 管理設定速率限制和配額原則。

在此教學課程中，您將建立可讓開發人員 」 的免費試用 」 應用程式開發介面產品 toomake too10 呼叫每分鐘和向上 tooa 最大值為 200 的呼叫，每週 tooyour API 使用 hello[限制呼叫率，每個訂閱](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[每個訂閱設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)原則。 然後，您將會發行 hello 應用程式開發介面，並測試 hello 速率限制原則。

如需更進階節流使用 hello 案例[速率限制-由-索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey)和[配額的索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey)原則，請參閱[節流使用 Azure API 管理進階的要求](api-management-sample-flexible-throttling.md)。

## <a name="create-product"></a>toocreate 產品
在本步驟中，您將建立不需核准訂用帳戶的免費試用產品。

> [!NOTE]
> 如果您已經有設定的產品，並想 toouse 它在此教學課程，您可以往前跳過[設定呼叫率限制和配額原則][ Configure call rate limit and quota policies]並從該處使用您的產品遵循 hello 教學課程取代 hello 免費試用版的產品。
> 
> 

tooget 啟動，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[管理您在 Azure API 管理中的第一個 API][ Manage your first API in Azure API Management]教學課程。
> 
> 

按一下**產品**在 hello **API 管理**功能表 hello 左的 toodisplay hello**產品**頁面。

![Add product][api-management-add-product]

按一下**新增產品**toodisplay hello**新增新的產品** 對話方塊。

![Add new product][api-management-new-product-window]

在 hello**標題**方塊中，輸入**免費試用版**。

在 [hello**描述**] 方塊中，下列文字的型別 hello: **「 訂閱者 」 將會無法 toorun 10 呼叫/tooa 最大值 200 呼叫/週之後存取遭到拒絕的總分鐘。**

API 管理中的產品可以是受保護或開放的。 受保護的產品，必須是訂閱的 toobefore 可以使用。 開放產品不需要訂用帳戶即可使用。 請確認**需要訂用帳戶**是選取的 toocreate 一個受保護的產品，需要訂用帳戶。 這是 hello 預設設定。

如果您想要系統管理員 tooreview 並接受或拒絕的訂閱嘗試 toothis 產品，選取**需要訂閱核准**。 如果未選取 hello 核取方塊，訂閱嘗試將會自動核准。 在此範例中，訂用帳戶都會自動核准，因此不會選取 hello 方塊。

tooallow 開發人員帳戶 toosubscribe 多次 toohello 新產品，選取 hello**允許多個同時訂閱**核取方塊。 本教學課程不會使用多項同時訂閱，所以維持未核取即可。

輸入的所有值之後，請按一下**儲存**toocreate hello 產品。

![Product added][api-management-product-added]

根據預設，新產品會顯示在 hello toousers**管理員**群組。 我們 tooadd hello**開發人員**群組。 按一下**免費試用版**，然後按一下hello**可視性** 索引標籤。

> 在 API 管理中，群組是產品 toodevelopers 使用的 toomanage hello 可見性。 產品授與的可見性 toogroups 和開發人員可以檢視和訂閱 toohello 產品可見 toohello 所隸屬的群組。 如需詳細資訊，請參閱[toocreate 和使用在 Azure API 管理群組的方式][How toocreate and use groups in Azure API Management]。
> 
> 

![Add developers group][api-management-add-developers-group]

選取 hello**開發人員**核取方塊，然後**儲存**。

## <a name="add-api"></a>tooadd API toohello 產品
在此步驟 hello 教學課程中，我們將加入 hello 回應 API toohello 新免費試用版的產品。

> 每個 API 管理服務執行個體隨附預先設定的一種回應的 API，可以與使用的 tooexperiment 和了解 API 管理。 如需詳細資訊，請參閱[在 Azure API 管理中管理您的第一個 API][Manage your first API in Azure API Management]。
> 
> 

按一下**產品**從 hello **API 管理**hello 左、，然後按一下功能表**免費試用版**tooconfigure hello 產品。

![Configure product][api-management-configure-product]

按一下**新增應用程式開發介面 tooproduct**。

![新增應用程式開發介面 tooproduct][api-management-add-api]

請選取 Echo API，然後按一下儲存。

![Add Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure 呼叫率限制和配額的原則
速率限制和配額會設定在 hello 原則編輯器。 我們將加入本教學課程中的 hello 兩個原則是 hello[限制呼叫率，每個訂閱](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[每個訂閱設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)原則。 在 hello 產品的範圍，就必須套用這些原則。

按一下**原則**下 hello **API 管理**hello 左邊功能表上的。 在 hello**產品**清單中，按一下**免費試用版**。

![Product policy][api-management-product-policy]

按一下**新增原則**tooimport hello 原則範本，並開始建立 hello 速率限制和配額原則。

![Add policy][api-management-add-policy]

速率限制和配額原則是輸入的原則，因此 hello 輸入項目中的位置 hello 資料指標。

![Policy editor][api-management-policy-editor-inbound]

捲動 hello 原則清單且找出 hello**限制呼叫率，每個訂閱**原則項目。

![Policy statements][api-management-limit-policies]

資料指標定位在 hello 之後 hello**輸入**原則項目，按一下旁邊的箭號 hello**限制呼叫率，每個訂閱**tooinsert 其原則範本。

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

您可以看到從 hello 片段，hello 原則允許設定限制 hello 產品的 Api 和操作。 本教學課程中我們將不使用這項功能，因此刪除 hello **api**和**作業**項目從 hello**速率限制**項目，例如只 hello 外部**速率限制**項目維持 hello 下列範例所示。

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

在 hello 免費試用版的產品，hello 最大可允許呼叫率是每分鐘 10 個呼叫，因此請輸入**10**為 hello hello 值**呼叫**屬性，和**60** hello **更新間隔**屬性。

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello**每個訂閱設定使用量配額**原則時，位置緊鄰下 hello 游標新增**速率限制**hello 內的項目**輸入**項目，然後找出並按一下 hello 箭號 toohello 左邊**每個訂閱設定使用量配額**。

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

同樣地 toohello**每個訂閱設定使用量配額**原則，**每個訂閱設定使用量配額**原則允許 hello 產品的 Api 和操作上設定的端點。 本教學課程中我們將不使用這項功能，因此刪除 hello **api**和**作業**項目從 hello**配額**項目，如下列範例中的 hello 中所示。

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

配額可以根據每個間隔、 頻寬或兩者的呼叫 hello 數目。 在本教學課程中，我們不會節流根據的頻寬，請刪除 hello**頻寬**屬性。

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Hello 免費試用版的產品，在 hello 配額會是 200 每週的呼叫。 指定**200**為 hello hello 值**呼叫**屬性，然後再指定**604800**為 hello hello 值**更新間隔**屬性。

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> 原則間隔是依秒來指定。 toocalculate hello 一週的間隔，您可以將 hello 天數 (7) 依 hello 以 hello 分鐘中的每分鐘 (60) 秒的 hello 數小時 (60) 的一天 （24 小時） 的小時數： 7 * 24 * 60 * 60 = 604800。
> 
> 

當您完成設定 hello 原則時，其值必須符合下列範例中的 hello。

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Hello 預期的原則設定之後，請按一下**儲存**。

![Save policy][api-management-policy-save]

## <a name="publish-product"></a> toopublish hello 產品
既然 hello hello 應用程式開發介面，且 hello 原則設定，請使其可以用於開發人員必須發行 hello 產品。 按一下**產品**從 hello **API 管理**hello 左、，然後按一下功能表**免費試用版**tooconfigure hello 產品。

![Configure product][api-management-configure-product]

按一下**發行**，然後按一下 **是，將它發行**tooconfirm。

![Publish product][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe 開發人員帳戶 toohello 產品
現在該 hello 產品發行時，它就是可用訂閱的 toobe tooand 由開發人員使用。

> API 管理執行個體的系統管理員會自動訂閱的 tooevery 產品。 在此教學課程步驟中，我們會訂閱 hello 非系統管理員的開發人員帳戶 toohello 免費試用版產品的其中一個。 如果您的開發人員帳戶屬於 hello 系統管理員角色，然後您可以依照此步驟中，即使您已經訂閱。
> 
> 

按一下**使用者**上 hello **API 管理**hello 功能表左、，然後按一下hello 您的開發人員帳戶名稱。 在此範例中，我們會使用 hello **Clayton Gragg**開發人員帳戶。

![Configure developer][api-management-configure-developer]

按一下 [ **加入訂閱**]。

![加入訂閱][api-management-add-subscription-menu]

選取 免費試用，然後按一下訂閱。

![加入訂閱][api-management-add-subscription]

> [!NOTE]
> 在本教學課程中，不會啟用多個同時訂閱 hello 免費試用版產品。 如果是，您將提示的 tooname hello 訂用帳戶 hello 下列範例所示。
> 
> 

![加入訂閱][api-management-add-subscription-multiple]

按一下後**訂閱**，hello 產品會出現在 hello**訂用帳戶**hello 使用者清單。

![已新增訂用帳戶][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall 作業並測試 hello 速率限制
既然 hello 免費試用版產品設定和發佈，我們可以呼叫某些作業，並測試 hello 速率限制原則。
交換器 toohello 開發人員入口網站，依序按一下**開發人員入口網站**hello 右上方功能表中。

![開發人員入口網站][api-management-developer-portal-menu]

按一下**Api**在 hello 上方的功能表，然後按一下 **Echo API**。

![開發人員入口網站][api-management-developer-portal-api-menu]

按一下 GET 資源，然後按一下嘗試。

![Open console][api-management-open-console]

保留 hello 預設參數值，然後選取 您的訂用帳戶金鑰 hello 免費試用版產品。

![訂用帳戶金鑰][api-management-select-key]

> [!NOTE]
> 如果您有多個訂閱，是確定 tooselect hello 金鑰**免費試用版**，或其他 hello 先前步驟中設定的 hello 原則將不會生效。
> 
> 

按一下**傳送**，然後檢視 hello 回應。 請注意 hello**回應狀態**的**200 確定**。

![Operation results][api-management-http-get-results]

按一下**傳送**的比率大於此數目的 10 每分鐘呼叫 hello 速率限制原則。 當超過 hello 速率限制原則之後，回應狀態**429 太多要求**傳回。

![Operation results][api-management-http-get-429]

hello**回應內容**指出 hello 剩餘間隔之前重試將會成功。

後續呼叫時的每分鐘 10 呼叫 hello 速率限制原則生效時，將會失敗，直到從 hello 經過 60 秒 hello 10 成功呼叫 toohello 產品之前已超過 hello 速率限制的第一個。 在此範例中，hello 剩餘間隔會為 54 秒。

## <a name="next-steps"> </a>後續步驟
* 監看下列影片 hello 設定速率限制和配額的示範。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
