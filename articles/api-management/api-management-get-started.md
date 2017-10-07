---
title: "aaaManage 您在 Azure API 管理中的第一個 API |Microsoft 文件"
description: "了解如何 toocreate 應用程式開發介面，加入作業，並開始使用 API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>在 Azure API 管理中管理您的第一個 API
## <a name="overview"> </a>概觀
本指南也說明如何開始使用 Azure API 管理中的 tooquickly，並進行第一次的 API 呼叫。

## <a name="concepts"> </a>什麼是 Azure API 管理？
您可以使用 Azure API 管理 tootake 任何後端，並啟動它為基礎的完整功能 API 程式。

常見案例包括：

* **保護行動基礎結構** 。
* **啟用 ISV 合作夥伴生態系統**藉由提供快速的夥伴上架 hello 開發人員透過入口網站和建立從內部實作應用程式開發介面外觀 toodecouple 不敞開夥伴耗用量。
* **執行內部的 API 程式**藉由提供集中式的位置，如 hello 組織 toocommunicate hello 可用性和最新相關變更 tooAPIs，控制組織的帳戶為基礎的存取為基礎之間的安全通道hello API 閘道和 hello 後端。

hello 系統是由下列元件的 hello 所組成：

* hello **API 閘道**hello 端點的：
  
  * 接受應用程式開發介面呼叫，並將其傳送 tooyour 後端。
  * 驗證 API 金鑰、JWT 權杖、憑證和其他認證。
  * 強制採用使用量配額和頻率限制。
  * 會將您的 API，而不需修改程式碼的 hello 立即轉換。
  * 快取設定的後端回應。
  * 記錄呼叫中繼資料以供分析使用。
* hello**發行者入口網站**hello 系統管理介面設定您應用程式開發介面的程式。 使用方式：
  
  * 定義或匯入 API 結構描述。
  * 將 API 封裝至產品。
  * 設定原則，例如配額或 hello 應用程式開發介面上的轉換。
  * 從分析中取得見解。
  * 管理使用者。
* hello**開發人員入口網站**做 hello 主要 web 存在為開發人員而言，它們可以在其中：
  
  * 閱讀 API 文件。
  * 嘗試透過 hello 互動式主控台應用程式開發介面。
  * 建立帳戶和訂閱 tooget API 金鑰。
  * 存取他們的使用量分析資料。

## <a name="create-service-instance"> </a>建立 API 管理執行個體
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][Azure Free Trial]。
> 
> 

使用 API 管理中的 hello 第一個步驟是 toocreate 服務執行個體。 登入 toohello [Azure 入口網站][ Azure Portal]按一下**新增**， **Web + 行動**， **API 管理**。

![API Management new instance][api-management-create-instance-menu]

如**名稱**，指定唯一的子網域名稱 toouse hello 服務 url。

選擇所需的 hello**訂用帳戶**，**資源群組**和**位置**服務執行個體。

輸入**Contoso Ltd.** hello**組織名稱**，並輸入您的電子郵件地址中 hello**系統管理員電子郵件**欄位。

> [!NOTE]
> 此電子郵件地址用於從 hello API 管理系統的通知。 如需詳細資訊，請參閱[如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理][How tooconfigure notifications and email templates in Azure API Management]。
> 
> 

![New API Management service][api-management-create-instance-step1]

API 管理服務執行個體共有三種層次：開發人員、標準和高階。

> [!NOTE]
> hello 開發人員層適用於開發、 測試及試驗 API 方案，高可用性不是問題。 在 hello Standard 和 Premium 層，您可以調整您的保留的單元計數 toohandle 更多流量。 hello Standard 和 Premium 層提供 API 管理服務以 hello 大部分處理能力和效能。 您可以使用任何階層來完成本教學課程。 如需關於 API 管理層次的詳細資訊，請參閱 [API 管理價格][API Management pricing]。
> 
> 

按一下**建立**toostart 佈建您的服務執行個體。

![New API Management service][api-management-instance-created]

一旦建立 hello 服務執行個體，hello 下一個步驟是 toocreate，或匯入應用程式開發介面。

## <a name="create-api"> </a>匯入 API
API 包含可自用戶端應用程式叫用的一組作業。 應用程式開發介面作業會代理 tooexisting web 服務。

您可以手動建立 API (並可加入作業)，或是匯入這兩者。 在本教學課程中，我們將匯入範例計算機 web 服務由 Microsoft 提供，裝載於 Azure 的 hello 應用程式開發介面。

> [!NOTE]
> 如需建立應用程式開發介面和手動加入作業的指示，請參閱[如何 toocreate Api](api-management-howto-create-apis.md)和[如何 tooadd 作業 tooan API](api-management-howto-add-operations.md)。
> 
> 

應用程式開發介面會在 hello 發行者入口網站設定。 tooreach，按一下 **發行者入口網站**從 hello 服務工具列。

![發行者入口網站][api-management-management-console]

tooimport hello 計算機 API 中，按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。

![匯入 API 按鈕][api-management-import-api]

執行下列步驟 tooconfigure hello [小算盤] 應用程式開發介面的 hello:

1. 按一下**From URL**，輸入**http://calcapi.cloudapp.net/calcapi.json**到 hello**規格文件 URL**文字方塊，然後按一下 hello **Swagger**選項按鈕。
2. 型別**calc**到 hello **Web API URL 尾碼**文字方塊。
3. 按一下 hello**產品 （選擇性）**方塊，然後選擇**入門**。
4. 按一下**儲存**tooimport hello 應用程式開發介面。

![Add new API][api-management-import-new-api]

> [!NOTE]
> **API 管理**目前支援匯入 1.2 和 2.0 版本的 Swagger 文件。 即使 [Swagger 2.0 規格](http://swagger.io/specification)表示 `host`、`basePath` 和 `schemes` 是選擇性的屬性，請確定您的 Swagger 2.0 文件**必須**包含這些屬性，否則無法匯入。 
> 
> 

一旦匯入 hello API 時，hello hello api 摘要頁面會顯示 hello 發行者入口網站中。

![API summary][api-management-imported-api-summary]

hello 應用程式開發介面 > 一節中有數個索引標籤。 hello**摘要**索引標籤會顯示有關 hello API 基本度量和資訊。 hello[設定](api-management-howto-create-apis.md#configure-api-settings) 索引標籤是應用程式開發介面的使用的 tooview 和編輯 hello 組態。 hello[作業](api-management-howto-add-operations.md) 索引標籤是使用的 toomanage hello API 的作業。 hello**安全性** 索引標籤可以 hello 後端伺服器的使用的 tooconfigure 閘道驗證使用基本驗證或[相互憑證驗證](api-management-howto-mutual-certificates.md)，和 tooconfigure [使用 OAuth 2.0 的使用者授權](api-management-howto-oauth2.md)。  hello**問題** 索引標籤是使用的 tooview hello 開發人員使用您 Api 所報告的問題。 hello**產品** 索引標籤會包含此應用程式開發介面使用的 tooconfigure hello 產品。

依預設，每個 API 管理執行個體會隨附兩個範例產品：

* **入門**
* **無限制**

在本教學課程中，當 hello 應用程式開發介面已匯入 hello 基本計算機 API 時，已加入 toohello Starter 產品。

在訂單 toomake 呼叫 tooan API 中，開發人員必須先訂閱，他們存取 tooit tooa 產品。 開發人員可以訂閱 tooproducts 在 hello 開發人員入口網站或系統管理員可以訂閱 hello 發行者入口網站中的開發人員 tooproducts。 由於您已建立 hello API 管理執行個體 hello 中先前的步驟在 hello 教學課程中，讓您已訂閱的 tooevery 產品，根據預設，您是系統管理員。

## <a name="call-operation"></a>從 hello 開發人員入口網站呼叫作業
作業可以直接從 hello 開發人員入口網站，可提供便利的方式 tooview 呼叫，並測試應用程式開發介面的 hello 作業。 在此教學課程步驟中，您會呼叫 hello 基本計算機 API**加入兩個整數**作業。 按一下**開發人員入口網站**功能表在 hello hello hello 發行者入口網站的右上方。

![開發人員入口網站][api-management-developer-portal-menu]

按一下**Api**從 hello 最上層功能表，然後再按一下**基本計算機**toosee hello 可用的作業。

![開發人員入口網站][api-management-developer-portal-calc-api]

請注意 hello 範例描述和匯入以及 hello 應用程式開發介面和作業，提供文件以 hello 開發人員會使用這項作業的參數。 手動加入作業時，也可以加入這些說明。

toocall hello**加入兩個整數**作業中，按一下 **試試**。

![試試看][api-management-developer-portal-calc-api-console]

您可以輸入 hello 參數的某些值或保留 hello 的預設值，然後按一下**傳送**。

![HTTP Get][api-management-invoke-get]

叫用作業之後，hello 開發人員入口網站會顯示 hello**回應狀態**，hello**回應標頭**，和任何**回應內容**。

![Response][api-management-invoke-get-response]

## <a name="view-analytics"> </a>檢視分析
基本計算機，藉由選取的參數後 toohello 發行者入口網站的 tooview 分析**管理**功能表在 hello hello hello 開發人員入口網站的右上方。

![管理][api-management-manage-menu]

hello hello 發行者入口網站的預設檢視為 hello**儀表板**，這樣會提供您的 API 管理執行個體的概觀。

![儀表板][api-management-dashboard]

Hello 停留 hello 圖表**基本計算機**toosee hello 特定的衡量標準 hello hello 應用程式開發介面的指定的時段內使用。

> [!NOTE]
> 如果您沒有看到任何線條在圖表上，切換後 toohello 開發人員入口網站和某些 hello API 呼叫、 稍待片刻，並再回來 toohello 儀表板。
> 
> 

按一下**檢視詳細資料**hello 應用程式開發介面，包括放大顯示 hello 度量的 tooview hello 摘要頁面。

![Analytics][api-management-mouse-over]

![摘要][api-management-api-summary-metrics]

對於詳細的計量和報表，按一下 **分析**從 hello **API 管理**hello 左邊功能表上的。

![概觀][api-management-analytics-overview]

hello**分析**區段具有下列四個索引標籤的 hello:

* **一眼**提供整體使用量和健全狀況度量，以及 hello 最上層的開發人員、 最上層的產品、 最上層應用程式開發介面和最上層的作業。
*  提供 API 呼叫和頻寬的深入檢視，包括地理區域的呈現。
* **Health** 著重在狀態碼、快取成功率、回應時間，以及 API 與服務回應時間。
* **活動**提供 hello 的開發人員、 產品、 API 和作業的特定活動的向下鑽研報表。

## <a name="next-steps"> </a>後續步驟
* 了解如何太[保護您的 API 與速率限制](api-management-howto-product-with-rules.md)。

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
