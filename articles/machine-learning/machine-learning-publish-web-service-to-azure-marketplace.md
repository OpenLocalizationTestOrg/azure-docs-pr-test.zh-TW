---
title: "(已過時) 將 Machine Learning Web 服務發佈到 Azure Marketplace | Microsoft Docs"
description: "(已過時) 如何將 Azure Machine Learning Web 服務發佈到 Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a>(已過時) 將 Azure Machine Learning Web 服務發佈到 Azure Marketplace

> [!NOTE]
> DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。 因此，這篇文章目前已過時。 
> 
> 替代方案是，您可以將 Machine Learning 實驗發佈到 [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com/)，以利資料科學社群使用。 如需詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。

Azure Marketplace 可讓您發行 Azure Machine Learning Web 服務，作為供外部客戶付費或免費使用的服務。 本文章將提供該程序的概觀，以及入門使用的指引連結。 透過此程序，您將可讓您的 Web 服務成為可供其他開發人員運用在其應用程式中的服務。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a>發行程序概觀
以下是將 Azure Machine Learning Web 服務發行至 Azure Marketplace 的步驟：

1. 建立及發佈機器學習服務要求-回應服務 (RRS)
2. 將服務部署至實際執行環境中，並取得 API 金鑰與 OData 端點資訊。
3. 使用已發行之 Web 服務的 URL，發行至 [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/) 
4. 您的產品在提交之後必須經過審閱和核准，才可供客戶購買。 發行程序可能需要數個工作天。 

## <a name="walk-through"></a>逐步解說
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>步驟 1：建立及發佈機器學習服務要求-回應服務 (RRS)
 如果您尚未這樣做，請查看這個 [逐步解說](machine-learning-walkthrough-5-publish-web-service.md)。

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a>步驟 2：將服務部署至實際執行環境中，並取得 API 金鑰與 OData 端點資訊
1. 從 [Azure 傳統入口網站](http://manage.windowsazure.com)，從左側的導覽列中選取 [機器學習服務] 選項，並選取您的工作區。 
2. 按一下 [ **Web 服務** ] 索引標籤，並選取您想要發佈到 Marketplace 的 Web 服務。
   
    ![Azure Marketplace][workspace]
3. 選取您想要 Marketplace 取用的端點。 如果您尚未建立任何額外的端點，您可以選取 [ **預設** ] 端點。
4. 當您在端點上按一下時，您將能夠看到 **API 金鑰**。 在稍後的步驟 3 中您將需要此資訊，因此建立一個複本。
   
    ![Azure Marketplace][apikey]
5. 按一下 [ **要求/回應** ] 方法，此時我們不支援發佈批次執行服務至 Marketplace。 這將帶您前往進入要求/回應方法的 API 說明頁面。
6. 複製 [ **OData 端點位址**]，在稍後的步驟 3 中您將需要此資訊。
   
    ![Azure Marketplace][odata]

將服務部署到實際執行環境。

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a>步驟 3：使用已發行之 Web 服務的 URL，發行至 Azure Marketplace (資料市場)
1. 瀏覽至 [Azure Marketplace (資料市場)](http://datamarket.azure.com/home) 
2. 按一下頁面頂端的 [ **發佈** ] 連結。 這帶您前往 [Microsoft Azure 發佈入口網站](https://publish.windowsazure.com)
3. 按一下 [ **發行者** ] 區段，以註冊為發行者。
4. 建立新產品時，請選取 [資料服務]，然後按一下 [建立新的資料服務]。 
   
   ![Azure Marketplace][image1]
   
   <br />
5. 在 [ **計劃** ] 下，提供您的產品的相關資訊，包括定價計劃。 決定您要提供免費還是付費服務。 若要收費，請提供付款資訊，例如您的銀行和稅務資訊。
6. 在 [ **行銷** ] 下提供服務的相關資訊，例如您的提供項目的標題和描述。
7. 在 [ **價格** ] 下，您可以設定特定國家/地區的價格，或讓系統為您的提供項目自動定價。
8. 在 [資料服務] 索引標籤中，按一下 [Web 服務] 做為 [資料來源]。
   
    ![Azure Marketplace][image2]
9. 從 Azure 傳統入口網站取得 Web 服務 URL 和 API 金鑰，如以上的步驟 2 所述。
10. 在 [Marketplace 資料服務] 設定對話方塊中，將 OData 端點位址貼入 [ **服務 URL** ] 文字方塊。
11. 在 [驗證] 中，選擇 [標頭] 做為 [驗證配置]。
    
    * 輸入 "Authorization" 作為 [ **標頭名稱**]。
    * 針對 [標頭值]，輸入 "Bearer" (不含引號)，按一下 [空間] 列，然後貼上 API 金鑰。
    * 勾選 [ **這個服務是 OData** ] 核取方塊。
    * 按一下 [ **測試連線** ] 以測試連線。
12. 在 [類別] 下，確保已選取 [機器學習服務]。
13. 完成輸入提供服務所有的中繼資料後，請按一下 [發佈]，然後按一下 [推入到預備環境]。 此時，將通知您必須先修正的任何其餘問題。
14. 確定完成所有未解決的問題後，請按一下 [ **要求核准以推入到實際執行環境**]。 發行程序可能需要數個工作天。 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

