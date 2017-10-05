---
title: "Azure API 管理概觀和索引鍵概念 | Microsoft Docs"
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
ms.openlocfilehash: 47358c6c209488d7a12e8afbf7a2d9b3f872f0de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-api-management"></a>什麼是 API 管理？
「API 管理」可協助組織將 API 發佈給外部、合作夥伴及內部開發人員，以發揮其資料與服務的潛力。 各地的公司都想要將其作業延伸為數位平台、建立新的管道、尋找新客戶並對現有客戶促進更深入的參與。 「API 管理」提供的核心專長認證，透過開發人員參與、商務洞察力、分析、安全性和保護，可確保 API 程式獲致成功。

觀看下列影片以取得 Azure API 管理的概觀，並了解如何使用 API 管理，以最少量的工作將許多功能新增至您的 API，包括存取控制、速率限制、監視、事件記錄及回應快取。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

為了使用 API 管理，管理員會建立 API。 每個 API 都包含一或多個作業，而每個 API 則可加入至一或多個產品。 為了使用 API，開發人員會訂閱包含該 API 的產品，而且他們之後可呼叫 API 的作業，但需受限於可能生效的任何使用原則。

本主題說明 API 管理的主要概念。

> [!NOTE]
> 如需詳細資訊，請參閱 [雲端式 API 管理：如何運用 API 的威力](http://j.mp/ms-apim-whitepaper) PDF 白皮書 (英文)。 這份 CITO Research 發表的簡介白皮書涵蓋： 
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
API 是 API 管理服務執行個體的基礎。 每個 API 都代表可供開發人員使用的一組作業。 每個 API 都包含會實作 API 之後端服務的參考，而其作業會與後端服務實作的作業相對應。 API 管理中的作業可設定度相當高，並可控制 URL 對應、查詢和路徑參數、要求和回應內容，以及作業回應快取。 費率限制、配額和 IP 限制原則亦可在 API 或個別作業層級實作。

如需詳細資訊，請參閱[如何建立 API][How to create APIs] 和[如何將作業新增至 API][How to add operations to an API]。

## <a name="products"> </a> 產品
產品是將 API 呈現給開發人員的方式。 在 API 管理中的產品包含一或多個 API，並且設定了標題、說明與使用規定。 產品可以是 [開放] 或 [受保護]。 受保護產品必須先擁有訂用帳戶才能使用，開放產品則可以使用而不需訂用帳戶。 當產品可供開發人員使用時，即可將產品發佈。 發佈產品之後，開發人員即可檢視產品 (以及受保護產品訂閱時)。 訂用帳戶核准是在產品層級設定，可能需要管理員核准，或是可自動核准。

群組的作用是管理產品對於開發人員的可見度。 產品會將可見度授與群組，而開發人員可檢視並訂閱其所屬群組可見的產品。 

如需詳細資訊，請參閱[如何建立和發佈產品][How to create and publish a product]及下列影片。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> 群組
群組的作用是管理產品對於開發人員的可見度。 API 管理具有下列不可變的系統群組。

* **管理員** - Azure 訂用帳戶管理員是此群組的成員。 管理員可管理 API 管理服務執行個體、建立開發人員所使用的 API、作業和產品。
* **開發人員** - 已驗證開發人員入口網站使用者屬於此群組。 開發人員是使用您的 API 建置應用程式的客戶。 開發人員獲授與開發人員入口網站的存取權，並建置呼叫 API 作業的應用程式。
* **來賓** - 未經驗證的開發人員入口網站使用者 (例如，造訪 API 管理執行個體之開發人員入口網站的潛在客戶) 屬於此群組。 他們可獲得特定唯讀存取權限，例如他們可檢視 API 但無法進行呼叫。

除了這些系統群組以外，管理員還可以建立自訂群組，或使用 [使用 Azure Active Directory 相關租用戶中的外部群組](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group)。 自訂群組和外部群組可以與系統群組一起使用，提供開發人員 API 產品的能見度及存取權。 例如，您可以為與特定夥伴組織有關的開發人員建立一個自訂群組，並只允許他們存取來自含相關 API 之產品的 API。 使用者可以是多個群組的成員。

如需詳細資訊，請參閱[如何建立和使用群組][How to create and use groups]。

## <a name="developers"> </a> 開發人員
開發人員代表 API 管理服務執行個體中的使用者帳戶。 開發人員可由管理員建立或邀請加入，也可以透過[開發人員入口網站][Developer portal]註冊。 每個開發人員都是一或多個群組的成員，而且可訂閱對那些群組授與可見度的產品。

當開發人員訂閱產品時，將可獲得產品的主要和次要金鑰。 在對產品的 API 進行呼叫時會使用該金鑰。

如需詳細資訊，請參閱[如何建立或邀請開發人員][How to create or invite developers]和[如何將群組與開發人員建立關聯][How to associate groups with developers]。

## <a name="policies"> </a> 原則
原則是 API 管理的強大功能，可讓發行者透過組態變更 API 的行為。 原則是陳述式的集合，會因 API 的要求或回應循序執行。 常見陳述式包括從 XML 對 JSON 的格式轉換，以及可限制來自開發人員的傳入呼叫數量的呼叫費率限制，而且還有許多原則可供使用。

如果原則不另行指定，則可以在任何 API 管理原則中，使用原則運算式做為屬性值或文字值。 某些原則是以原則運算式為基礎，例如[控制流程](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose)和[設定變數](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable)原則。 如需詳細資訊，請參閱[進階原則](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies)和[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)，並觀看以下影片。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

如需 API 管理原則的完整清單，請參閱[原則參考文件][Policy reference]。 如需使用和設定原則的詳細資訊，請參閱[API 管理原則][API Management policies]。 如需建立產品並加上費率限制和配額原則的教學課程，請參閱[如何建立和設定進階產品設定][How create and configure advanced product settings]。 如需示範，請參閱下列影片。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> 開發人員入口網站
開發人員入口網站是開發人員可了解您的 API、檢視和呼叫作業，以及訂閱產品的地方。 潛在客戶可以造訪開發人員入口網站、檢視 API 和作業，以及註冊。 開發人員入口網站的 URL 位於 Azure 傳統入口網站中 API 管理服務執行個體的儀表板上。

透過加入自訂內容、自訂樣式和加入自己的品牌，即可自訂開發人員入口網站的外觀及操作。

## <a name="api-management-and-the-api-economy"></a>API 管理和 API 經濟效益
若要深入了解 API 管理，請觀看 Microsoft Ignite 2015 會議的以下簡報。

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How to create APIs]: api-management-howto-create-apis.md
[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How to create or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




