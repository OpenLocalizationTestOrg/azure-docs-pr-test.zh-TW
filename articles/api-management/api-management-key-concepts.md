---
title: "aaaAzure API 管理的概觀和索引鍵概念 |Microsoft 文件"
description: "了解 API、產品、角色、群組及其他 API 管理的主要概念。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>什麼是 API 管理？
API 管理可協助組織發行應用程式開發介面 tooexternal、 合作夥伴和內部開發人員 toounlock hello 可能會其資料和服務。 企業 everywhere 會尋找 tooextend 其作業由數位平台、 建立新通路、 尋找新客戶和深化與現有的。 API 管理提供 hello 核心能力 tooensure 成功的 API 程式，透過開發人員的努力、 企業洞察力、 分析、 安全性和保護。

監看 hello 下列影片以取得 Azure API 管理的概觀，以及了解如何 toouse API 管理 tooadd 許多功能 tooyour 應用程式開發介面，包括存取控制限制、 監視、 事件記錄和評分快取回應，與您的組件上的最少工作。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse API 管理，系統管理員建立應用程式開發介面。 每個應用程式開發介面包含一或多個作業，並可以新增每個 API，tooone 或多個產品。 toouse 應用程式開發介面，開發人員必須訂閱 tooa 產品，其中包含應用程式開發介面，並呼叫作用中的主體 tooany 使用量原則 hello API 的作業。

本主題說明 API 管理的主要概念。

> [!NOTE]
> 如需詳細資訊，請參閱 hello[雲端為基礎的 API 管理： 另外 hello 應用程式開發介面電源](http://j.mp/ms-apim-whitepaper)PDF （英文） 白皮書。 這份 CITO Research 發表的簡介白皮書涵蓋： 
> 
> * 常見的 API 需求與挑戰
> * 解構 API 並呈現其外貌
> * 讓開發人員快速上手
> * 保護存取
> * 分析與度量
> * 藉由 API 管理平台獲得控制權和深層資訊
> * 比較使用雲端與內部部署解決方案
> * Azure API 管理
> 
> 

## <a name="apis"> </a>API 和作業
應用程式開發介面是 hello foundation API 管理服務執行個體。 每個應用程式開發介面代表一組作業可用 toodevelopers。 每個應用程式開發介面包含參考 toohello 後端服務實作 hello API 和其作業對應 toohello 作業 hello 後端服務實作。 API 管理中的作業可設定度相當高，並可控制 URL 對應、查詢和路徑參數、要求和回應內容，以及作業回應快取。 速率限制、 配額和 IP 限制原則也可以在 hello 應用程式開發介面或個別作業層級實作。

如需詳細資訊，請參閱[如何 toocreate Api] [ How toocreate APIs]和[如何 tooadd 作業 tooan API][How tooadd operations tooan API]。

## <a name="products"> </a> 產品
應用程式開發介面的方式呈現的 toodevelopers 的產品。 在 API 管理中的產品包含一或多個 API，並且設定了標題、說明與使用規定。 產品可以是 [開放] 或 [受保護]。 受保護的產品必須是它們可以用於，開啟時的訂閱的 toobefore 不用在訂用帳戶可以使用產品。 當產品可供開發人員使用時，即可將產品發佈。 一旦發佈，，就可以檢視 （和大小寫的受保護的產品訂閱 hello 中） 的開發人員。 訂用帳戶核准在 hello 產品層級和可以需要系統管理員核准，或要自動核准。

群組是產品 toodevelopers 使用的 toomanage hello 可見性。 產品授與的可見性 toogroups 和開發人員可以檢視和訂閱 toohello 產品可見 toohello 所隸屬的群組。 

如需詳細資訊，請參閱[如何 toocreate 及發佈產品][ How toocreate and publish a product]和下列視訊 hello。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> 群組
群組是產品 toodevelopers 使用的 toomanage hello 可見性。 API 管理有下列不可變群組 hello。

* **管理員** - Azure 訂用帳戶管理員是此群組的成員。 系統管理員管理 API 管理服務執行個體，建立 hello Api、 操作及開發人員所使用的產品。
* **開發人員** - 已驗證開發人員入口網站使用者屬於此群組。 開發人員會使用您的應用程式開發介面建置應用程式的 hello 客戶。 開發人員會授與存取 toohello 開發人員入口網站，並建置呼叫 hello 作業的應用程式開發介面的應用程式。
* **來賓**-未經驗證的開發人員入口網站的使用者，例如造訪 hello 開發人員入口網站的 API 管理執行個體都會歸類到此群組的潛在客戶。 它們可以被授與特定的唯讀存取，例如 hello 能力 tooview 應用程式開發介面，但不是呼叫它們。

在加法 toothese 系統群組中，系統管理員可以建立自訂群組或[運用在相關聯的 Azure Active Directory 租用戶中的外部群組](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group)。 自訂和外部群組可一起提供開發人員的可見性的系統群組，以及存取 tooAPI 產品。 例如，您可以建立一個自訂群組具有特定關係的開發人員夥伴組織，並允許它們存取 toohello Api 從產品，其中包含相關的 Api。 使用者可以是多個群組的成員。

如需詳細資訊，請參閱[如何 toocreate 和使用群組][How toocreate and use groups]。

## <a name="developers"> </a> 開發人員
開發人員代表 hello API 管理服務執行個體中的使用者帳戶。 或開發人員可以建立或受邀 toojoin 由系統管理員，他們可以註冊從 hello[開發人員入口網站][Developer portal]。 每位開發人員一或多個群組的成員，而且可以訂閱 toohello 產品可見性 toothose 群組授與。

當開發人員必須訂閱 tooa 產品則會授與 hello 產品的 hello 主要和次要金鑰。 建立 hello 產品的 Api 呼叫時，會使用此金鑰。

如需詳細資訊，請參閱[如何 toocreate 或邀請開發人員][ How toocreate or invite developers]和[tooassociate 與開發人員的群組方式][How tooassociate groups with developers]。

## <a name="policies"> </a> 原則
原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 API 管理的強大功能。 原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。 受歡迎的陳述式包含格式轉換，從 XML tooJSON 並呼叫速率限制為開發人員，從連入呼叫 toorestrict hello 數量和許多其他原則可供使用。

除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。 某些原則，例如 hello[控制流程](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose)和[設定變數](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable)原則為基礎的原則運算式。 如需詳細資訊，請參閱[進階原則](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies)，[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)，並監看式 hello 遵循視訊。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

如需 API 管理原則的完整清單，請參閱[原則參考文件][Policy reference]。 如需使用和設定原則的詳細資訊，請參閱[API 管理原則][API Management policies]。 如需建立產品並加上費率限制和配額原則的教學課程，請參閱[如何建立和設定進階產品設定][How create and configure advanced product settings]。 示範，請參閱下列視訊 hello。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> 開發人員入口網站
開發人員可以深入了解您應用程式開發介面、 檢視和呼叫的作業，而訂閱 tooproducts hello 開發人員入口網站。 潛在客戶可以瀏覽 hello 開發人員入口網站，檢視應用程式開發介面和作業，並註冊。 您的開發人員入口網站的 hello URL 位於 hello Azure 傳統入口網站，您的 API 管理服務執行個體中的 hello 儀表板。

您可以自訂 hello 的外觀與您的開發人員入口網站新增自訂內容、 自訂樣式，以及新增您的品牌。

## <a name="api-management-and-hello-api-economy"></a>API 管理和 hello API 經濟
toolearn 深入了解 API 管理，監看式 hello hello Microsoft Ignite 2015 會議中的下列簡報。

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




