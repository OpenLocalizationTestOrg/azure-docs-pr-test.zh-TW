---
title: "資料服務提供 hello Marketplace aaaTesting |Microsoft 文件"
description: "了解如何 tootest 資料服務提供 hello Azure Marketplace。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>在預備環境中測試您的資料服務產品
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
> 
> 

完成 hello 前兩個步驟之後[建立您的 Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)和[發佈入口網站建立您的資料服務提供](marketplace-publishing-data-service-creation.md)已經準備好讓您提供的服務可在 helloAzure marketplace 所提供。 本主題將逐步引導您完成 hello 先、 中繼、 步驟稱為 「 預備 」

預備部署您的優惠，您可以在此測試並驗證其功能之前將它推送 tooproduction 「 沙箱 」 的私用的方法。 hello 供應項目會出現在暫存就像是 tooa 客戶已經部署。

## <a name="step-1-pushing-your-offer-toostaging"></a>步驟 1. 推入的供應項目 toostaging
推入的供應項目 toostaging 可讓您 tootest hello 供應項目之前會變得可用 toofuture 「 訂閱者 」。  您可以查看如何您提供的服務將會出現這些訂閱 tooyour 資料的功能。  

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. 登入 hello[發佈入口網站](https://publish.windowsazure.com)
2. 選取**Data Services** hello 左側瀏覽視窗中
3. 選取您想 toopush toostaging 的優惠。 您會看見 hello 螢幕上。
4. 按一下**推送 tooStaging**  按鈕。  
5. 如果問題與 hello 供應項目所需 toobe 完成先前 toopushing toostaging，您會看到顯示的清單。  Hello 清單中的每個項目上按一下，以更正這些項目。 所有修正，當都按一下**推送 tooStaging**按鈕一次。

如果不沒有提供任何問題，您會看到下列 hello 快顯視窗。  

如果您不是規劃/未核准 toosurface 您在 Azure 入口網站的優惠 （目前有限容量），然後只關閉 hello 快顯視窗。

tootest 資料服務在 Azure 入口網站 （在加法 toohello DataMarket 入口網站），您必須具有 Azure 訂用帳戶 ID tootest。  此訂用帳戶識別碼會識別 hello 帳戶將會允許 tootest 您提供的服務。  

剪下並貼上您的訂用帳戶 ID，然後按一下 hello 核取記號 toocontinue。

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> 這些的 Azure 訂用帳戶 Id，才需要測試和預備中 hello [Azure 管理入口網站](https://manage.windowsazure.com)。 它們不需要在 Azure Marketplace 中的 tootest。
> 
> 

hello 出現的下一個畫面會顯示，發行正在進行中顯示 「 進行中 」 的 hello 反白顯示的以下圖示。 推送 toostaging 讓 10 too15 分鐘之間。  若時間過長，請先重新整理您的瀏覽器 (在 IE 中請按 F5 鍵)。  在 hello 罕見的情況下，您的優惠仍在發行 toostaging 小時後，按一下 hello 連絡我們連結 toolet 我們知道有問題。

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Hello hello 發送 tooStaging 完成進行中 」 圖示將會停止移動，且會更新 hello 狀態太 「 預備 」。  您會 tootest 現在準備好您的優惠。  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>步驟 2. 在 DataMarket 中測試已推送到預備環境中的產品
按一下下列的 hello 文字 hello 連結**」 看到您在提供的服務。.."** toodisplay 囉 」 畫面 hello 「 訂閱者 」，將會看到您的優惠效能 tooproduction 時，而且會出現在 DataMarket 中。

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

測試，或確認每個 hello 12 個項目標示 tooensure 上述所有標誌、 價格/交易、 文字、 影像、 文件，而且連結正確且運作正常。  這是您輸入時建立您的優惠的任何測試值已取代為實際值的好時機 tooensure。

1. 產品標誌
2. 產品名稱
3. 發行者名稱/連結 tooyour 公司的網站
4. 您產品的搜尋類別
5. 供應項目的支援連結 tooassist 訂閱者
6. 您產品的的內容描述
7. 描述計費詳細資料的產品方案
8. 連結 tooimplementation 程式碼
9. 示範如何使用產品資料的範例影像
10. 輸入/輸出 hello 供應項目內的每個服務的中繼資料
11. 產品的使用規定
12. Hello 供應項目的資料的預覽

最後，檢查 hello 服務運作 hello Datamarket 透過按一下 hello 連結 」 瀏覽此資料集 」。  新視窗會開啟在 hello 工具我們稱 「 服務總管 」 讓您可以預覽 hello 查詢的結果，對您的服務。  在這個視窗中，您可以輸入的 hello 參數所需，並查看 hello 結果顯示您的服務查詢。   此外，是顯示 hello URL 為您的查詢。  

> [!NOTE]
> 為確定 tooreview hello 服務文字描述 hello 顯示在 hello 最上方。  如果您的優惠包含多個服務和呼叫 hello 底部 tooswitch toohello 下一個服務 tooreview hello 索引標籤及測試。
> 
> 

## <a name="next-step"></a>後續步驟
您如有問題需要協助解決，請連絡 [Azure 發行者支援](http://go.microsoft.com/fwlink/?LinkId=272975)。

如果您滿意並準備好 toopublish 優惠請閱讀 hello[要求核准 tooPush tooProduction](marketplace-publishing-push-to-production.md)文件。

## <a name="see-also"></a>另請參閱
* [快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)

