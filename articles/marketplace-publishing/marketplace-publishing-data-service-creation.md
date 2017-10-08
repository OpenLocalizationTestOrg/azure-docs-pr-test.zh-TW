---
title: "aaaGuide toocreating 資料服務的 hello Marketplace |Microsoft 文件"
description: "Toocreate、 認證和部署資料服務的方式的詳細的指示購買 hello Azure Marketplace 上。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Hello Azure Marketplace 的資料服務發行指導
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
> 
> 

完成 hello 步驟 1 之後[帳戶建立及註冊](marketplace-publishing-accounts-creation-registration.md)，我們會引導您執行 hello[一般非技術性](marketplace-publishing-pre-requisites.md)和[技術需求](marketplace-publishing-data-service-creation-prerequisites.md)資料服務提供在 Azure Marketplace。 現在我們將引導您完成 hello 上建立資料服務提供的 hello 步驟[發佈入口網站][ link-pubportal] hello Azure Marketplace。

## <a name="1----login-toohello-publishing-portal"></a>1.  登入 toohello 發佈入口網站。
跳過[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**第一次登入 tooPublishing 入口網站，使用相同的帳戶與您公司的賣方設定檔已註冊於開發人員中心中的 hello。**  （稍後您可以新增任何您公司的員工為共同管理員 hello 發佈入口網站中）。

按一下 hello**發行 Data Services**磚如果這是 hello 第一次登入 hello 發佈入口網站。

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.  選擇**Data Services** hello 上 hello 左側的瀏覽功能表中。
  ![繪圖](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.  建立新的資料服務
為您新的資料服務提供填入 hello 標題，然後按一下上"+"hello 右上。

  ![繪圖](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.  檢閱 hello 子功能表下 hello 新建立 hello 瀏覽功能表中的資料服務。
按一下 hello**逐步解說**索引標籤上，檢閱需要 toopublish 正確 hello 資料服務 hello Azure Marketplace 上的所有必要的步驟。

> [!TIP]
> 您一律可以 hello < 逐步解說 > 頁面中的 hello 連結上按一下，或使用索引標籤左邊為 hello hello 資料服務供應項目的子功能表。
> 
> 

## <a name="5----create-a-new-plan"></a>5.  建立新的方案。
### <a name="offers-plans-transactions"></a>優惠、方案、交易。
每個優惠都可以有多個方案，但至少必須有一 (1) 個方案。 當使用者訂閱 tooyour 提供其訂閱 hello 供應項目的計劃的其中一個。 每個方案會定義使用者如何將會無法 toouse 您的服務。

目前 Azure Marketplace 資料服務的支援只有每月訂用帳戶交易基礎的模型，也就是使用者將支付給根據 toohello 價格他們訂閱 tooand hello 特定計畫的每月費用將會是能 tooconsume 每個月份數hello 計劃所定義的交易。

通常定義為資料服務會傳回的記錄數目每一筆交易傳送 toohello 服務的 hello 查詢為基礎。 hello 預設值為 100。 Tooeach 查詢將會傳回的交易數目的記錄數目除以 100，無條件進位 toohello 最接近的整數。

它是 Azure Marketplace 的服務層責任 toomonitor （公尺） 數字的每個查詢所耗用的交易。

> [!IMPORTANT]
> 達到這個 hello 月 hello 交易限制的使用者將無法繼續 toouse hello 服務其每月訂用帳戶循環結束之前會封鎖。
> 
> hello 計劃，或其中一個 hello 計劃可以 （但不是必須） 包含不限的數目的交易。
> 
> 

### <a name="create-a-plan"></a>建立方案。
1. 按一下**"+"** toohello 下一個 「 加入新的計畫 」。
2. 選擇其中一個 hello 選項： **Unlimited**或**有限**此計劃的使用方式。  如果限制然後提供交易 hello 計劃的 hello 數目將會讓 tooconsume 中一個月。
   
    ![繪圖](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    發佈入口網站將會同時也建議您 「 計劃識別碼 」，將會使用的 toocommunicate toohello 使用者 hello hello UI 中的 hello 計劃的名稱，而且也由 hello 市場服務 tooidentify hello 計劃。 如果您想要您可以變更 hello 「 計劃識別碼 」。
   
   > [!NOTE]
   > hello 「 計劃的識別項 」 必須是唯一的每個優惠 hello 範圍內。 中所使用的許多其他識別碼 hello 發佈入口網站規劃之後 hello 第一個發行 tooproduction 而且您將無法能 toochange 識別碼將會遭到鎖定這個識別項。
   > 
   > 
3. 按一下 tooaccept 您的選擇。
4. 接著，系統將詢問您一些有關您最新建立之方案的其他問題。
   
    ![繪圖](media/marketplace-publishing-data-service-creation/step-5.2.png)

| 問題 | 重要性 |
| --- | --- |
| **這個方案是免費且可供全球使用嗎？** |您可以建立完全免費的方案。 如果它的 hello 僅方案這項優惠 – 這表示，您要發行 「 免費提供 「 hello Marketplace 中。 如果它是只為其中一個 （少） 計劃，它可提供您選項 toooffer 使用者 toolearn 深入了解您的服務，每個月的交易數目相對較小的 hello。  如果 hello 回答 [是]，將會不要求任何進一步的問題。 |

> [!NOTE]
> 使用者可以將升級 toohello 付費計劃。
> 
> 

| 問題 | 重要性 |
| --- | --- |
| **有免費的試用版可用嗎？** |您可以隨時選擇 「 否試用版 」 或提供選項 toouse 「 一個月 」 計劃。 「 發行者 」，例如一個月免費提供此選項 tooprovide 使用者 hello 可能性 toounderstand hello 的優點 hello toouse。 |

> [!IMPORTANT]
> 如果他們已經建立付款方式例如信用卡，enterprise 合約，則使用者就只能無法 toopurchase 免費試用版。
> 
> 之後的 hello 免費試用一個月，Azure Marketplace 會啟動付費客戶 hello hello 訂閱 hello 日當時的價格除非 hello 客戶起始 hello 訂用帳戶取消。 沒有特殊的通知將會提供 toohello 使用者。
> 
> 

| 問題 | 重要性 |
| --- | --- |
| **這個方案需要升級的程式碼 toopurchase 嗎？** |發行者有服務計劃選項 toolimit 存取 tootheir 提供特殊的程式碼，稱為 「 Promocode"toospecific 客戶。 其中將包含此 Promocode 使用者將能夠 toosubscribe toohello 計劃。 如果您選擇 [否]，則表示您同意讓 hello 提供 hello 區域中的每個人都有 (請參閱[Marketplace 行銷內容指南](marketplace-publishing-push-to-staging.md)如需詳細資訊) 將會無法 toosubscribe toothis 計劃。 系統將不會進一步詢問任何問題。 |
| **此外，也會向不具有效促銷方案的人隱藏此方案嗎？** |如果 hello 回應 toohello 前一個問題是"Yes"hello 發行者已經移除此計劃出現在 hello hello Marketplace 的 UI 選項 toocompletely。 這表示，客戶不會看到這個計畫在 hello 供應項目的詳細資料頁面。 使用者將會接收 promocode toopurchase，將會使用這個 promocode 無法 toosubscribe tooit。 |

## <a name="6----create-your-marketplace-marketing-content"></a>6.  建立 Marketplace 行銷內容
Tooprovide 資訊中的所需的**行銷、 定價、 支援和分類**索引標籤，請瀏覽[Marketplace 行銷內容指南](marketplace-publishing-push-to-staging.md)這是發行在 hello 一般 tooall 成品Azure marketplace 所提供。  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.  連接您的優惠 tooyour 服務 （SQL Azure 基礎或 Web 服務為基礎）。
按一下 hello **Data Services**子功能表。

在 hello 上半部的 hello 頁面上將詢問 tooprovide hello 供應項目的**命名空間**。  

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.png)

下列問題的 hello 會定義如何 hello 發行者即將 tooexpose 新建優惠 tooAzure Marketplace。 (如需詳細資訊，請參閱 hello[資料服務技術必要條件指南](marketplace-publishing-data-service-creation-prerequisites.md))。

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.2.png)

**發行 hello 資料庫基礎的服務**

按一下 [資料庫] 。 會出現下列頁面的 hello:

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate hello 資料集的 CSDL 對應基礎 hello SQL Azure 資料庫：

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.4.png)

然後針對每個資料表

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.6.png)

如果 Web 服務

  ![繪圖](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> 讀取[對應的現有 web 服務 tooOData 透過 CSDL](marketplace-publishing-data-service-creation-odata-mapping.md)詳細的指示和範例建立 CSDL 的 Web 服務。
> 
> 

## <a name="next-steps"></a>後續步驟
既然您已建立您的資料服務優惠，請確定您完成在 hello hello 指示[Marketplace 行銷內容指南](marketplace-publishing-push-to-staging.md)您向前移動太之前[暫存中測試您的資料服務](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>另請參閱
* [快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* 如果您有興趣了解 hello 整體 OData 對應程序及目的閱讀此文章[資料服務 OData 對應](marketplace-publishing-data-service-creation-odata-mapping.md)tooreview 定義、 結構和指示。
* 如果您有興趣在學習並了解 hello 特定節點和它們的參數，請閱讀此文章[資料服務 OData 對應節點](marketplace-publishing-data-service-creation-odata-mapping-nodes.md)的定義和說明、 範例和案例使用的內容。
* 如果您有興趣檢視範例，請閱讀這篇文章[資料服務 OData 對應範例](marketplace-publishing-data-service-creation-odata-mapping-examples.md)toosee 範例程式碼，並了解程式碼語法和內容。

[link-pubportal]:https://publish.windowsazure.com
