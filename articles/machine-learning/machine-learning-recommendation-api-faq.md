---
title: "向上 aaaSet 並用 hello 機器學習建議 API |Microsoft 文件"
description: "以 Azure Machine Learning 建置之 Microsoft RECOMMENDATIONS API 的常見問題集"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>設定和使用 Machine Learning Recommendations API 的常見問題集
**什麼是 RECOMMENDATIONS？**

> [!NOTE]
> 您應該開始使用 hello 建議 API 認知服務，而不此版本。 hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。 它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。
> 深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)
> 
> 

對於組織和企業倚賴建議 toocross 銷售和向上銷售的產品和服務 tootheir 客戶，Azure Machine Learning 中的建議會提供自助式建議引擎。 它是協同篩選的實作，其使用矩陣分解作為核心演算法。 應用程式開發人員可以使用 REST API 來存取 RECOMMENDATIONS。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**我可以用 RECOMMENDATIONS 來做什麼？**

RECOMMENDATIONS 將一個項目或一組項目作為輸入，並傳回相關建議清單。 例如：線上零售商的客戶會按一下產品。 hello 線上零售店以輸入 tooRECOMMENDATIONS 傳送該產品、 取得一份產品清單，並決定哪些這些產品 toohello 客戶將會顯示。 您可能想 toouse 建議 toooptimize 線上商店或甚至 tooinform 您的內部業務部門或呼叫的中心。

**是否有任何使用量限制？**

建議具有下列使用量限制的 hello:

* 每個訂用帳戶的模型數上限：10
* 一個目錄可保留的項目數上限：100,000
* hello 會保留的使用方式點數目上限是 ~ 5,000,000。 如果要上傳新的或報告，將會刪除最舊的 hello。
* 電子郵件中可以傳送的資料 (例如，匯入目錄資料、匯入使用量資料) 大小上限為 200 MB
* 未作用中之建議項目模型組建的每秒交易數 (TPS) 為 ~2 TPS。 作用中的建議模型組建可以阻擋 too20 TPS。

## <a name="purchase-and-billing"></a>購買和計費
**建議多少 hello 啟動期間成本？**

Recommendations 是一項以訂用帳戶為基礎的服務。 收費是根據每個月的交易量來進行。 您可以檢查 hello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)在 Microsoft Azure Marketplace 以取得價格資訊。

**讓 Recommendations 為我追蹤和儲存使用者活動是否有任何相關聯的成本？**

不在 hello 的時刻。

**Recommendations 是否有免費試用版？**

沒有可用的記錄也就是限制的 too10，000 每月的交易。

**Recommendations 何時會計費？**

付費的訂用帳戶就是任何按月計價的訂用帳戶。 當您購買付費訂用帳戶時，您需立即支付 hello 第一次月的使用。 您需要付費 hello 訂閱頁面 （加上適用稅額） 上的 hello 供應項目相關聯的 hello 數量。 此每月費用是每個月對的 hello 相同行事曆依照原始購買日期，直到您取消 hello 訂用帳戶。 

**如何升級 tooa 較高的層服務？**

您可以購買或更新您的訂用帳戶，從 hello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)Microsoft Azure Marketplace 上的頁面。

當您升級訂用帳戶時：

* 為舊訂用剩餘的交易不會新增 tooyour 新訂用帳戶。 
* 您需支付完整價格 hello 新訂用帳戶，即使您有未使用的交易，在舊訂用帳戶。

處理序 tooupgrade 訂用帳戶：

* Nevigate toohello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)。
* 如果您未登入 toohello Marketplace 中登入。
* Hello 右窗格中，會列出所有的 hello 可用的方案。 按一下您想要 tooupgrade hello 計劃的 hello 選項按鈕。
* 如果您想 tooupgrade，按一下**確定**。 如果您不想 tooupgrade，按一下**取消**。

**重要**仔細閱讀的 hello 對話方塊然後再升級因為計費和使用的含意。

**何時我的訂用帳戶 tooRecommendations 將結束？**

您的訂用帳戶會在您取消時結束。 如果您想要 toocancel 訂用帳戶，請參閱下列指示的 hello。

**如何取消我的 Recommendations 訂用帳戶？**

您的訂用帳戶中，而使用 hello 遵循步驟 toocancel。 如果您目前的訂用帳戶是付費訂用帳戶，訂用帳戶會作用中持續直到 hello hello 目前計費週期結束為止。 如果您需要立即 hello 取消 toobe 有效，請與我們連絡[Microsoft 支援服務](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)。

**請注意**如果您在計費期間或未使用的交易 hello 結束之前取消計費期間內不提供任何退款。

* 瀏覽 toohello[提供頁面](https://datamarket.azure.com/dataset/amla/recommendations)。
* 如果您未登入 toohello Marketplace 中登入。
* 按一下**取消**toohello hello 資料集名稱和狀態的權限。 您可以使用此訂用帳戶，直到 hello 結尾 hello 目前計費週期或交易限制為止 （何者先發生）。

如果您想要訂用帳戶，因此您可以購買新的訂閱，立即提出票證申請在 toocancel [Microsoft 支援服務](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)。

## <a name="getting-started-with-recommendations"></a>開始使用 Recommendations
**Recommendations 是給我的嗎？** 

Machine Learning 中的建議適用於組織和依賴建議 toocross 銷售和向上銷售的產品或服務 tootheir 客戶的公司。 如果您有面向客戶的網站、銷售團隊、內部銷售團隊或客服中心，而且如果您提供的目錄有好幾十項產品或服務 – 您的盈餘即可受惠於使用 Recommendations。 

實驗順利進行建議是設計的 toobe 相當簡單。 hello 目前 API 架構版本需要基本程式設計技巧。 如果您需要協助，請連絡 hello 廠商開發您的網站。 如果您有內部的 IT 部門或公司內部的開發人員，則應該讓您能夠 tooget 建議 toowork。 

**Hello 設定建議的必要條件為何？**

建議需要您有使用者選項的記錄檔，在關聯 tooyour 類別目錄。 如果您沒有這類記錄檔，而您確實有面向客戶的網站，則 Recommendations 可以為您收集使用者活動。 

Recommendations 也需要您的產品或服務目錄。 如果您沒有 hello 類別目錄，建議使用 hello 實際客戶使用量資料並抽出類別目錄。 隱含目錄不會包含未在使用者交易中回報的項目。

**如何設定建議 hello 第一次？**

之後[訂閱](https://datamarket.azure.com/dataset/amla/recommendations)tooRecommendations，您應該使用 hello API 文件以 hello [Azure 機器學習建議快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)tooset hello 服務。

**哪裡可以找到 API 文件？** 

hello API 文件是[Azure 機器學習建議-快速入門指南](machine-learning-recommendation-api-quick-start-guide.md)。

**選項的作用為何我有 tooupload 類別目錄和使用方式資料 tooRecommendations 嗎？**

您有兩種方式來上傳您的類別目錄和使用量資料： 您可以從您的 CRM 系統或其他記錄檔匯出 hello 資料，並將它上傳 tooRecommendations，或者您可以加入標記 tooyour 網站，將追蹤使用者活動。 如果您使用 hello 第二個方法，hello 資料會儲存在 Azure 中。

## <a name="maintenance-and-support"></a>維護與支援
**我可以有多大的資料集？**

每個資料集可以包含 too100，000 類別目錄項目和註冊 too2048 MB 的使用量資料。
此外，訂閱可以包含設定 too10 資料組 （模型）。

**哪裡可以取得 Recommendations 的技術支援？**

技術支援人員並用於 hello [Microsoft Azure 支援](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning)站台。

**哪裡可以找到 hello 使用條款？**

[Microsoft Azure Machine Learning Recommendations API 服務條款](https://datamarket.azure.com/dataset/amla/recommendations#terms)。

