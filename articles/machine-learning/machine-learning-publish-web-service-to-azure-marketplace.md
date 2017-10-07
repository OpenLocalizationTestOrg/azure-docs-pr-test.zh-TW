---
title: "aaa(deprecated) 發行機器學習 web 服務 tooAzure Marketplace |Microsoft 文件"
description: "（已被取代）如何 toopublish 您 Azure Machine Learning Web 服務 toohello Azure Marketplace"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>（已被取代）發行 Azure Machine Learning Web 服務 toohello Azure Marketplace

> [!NOTE]
> DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。 因此，這篇文章目前已過時。 
> 
> 或者，您可以發佈您的機器學習實驗 toohello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)hello 資料科學社群的 hello 權益。 如需詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。

hello Azure Marketplace 付費 toopublish Azure Machine Learning web 服務提供 hello 能力或釋出外部客戶所耗用的服務。 這篇文章會提供連結 tooguidelines tooget 您啟動與該程序的概觀。 使用此程序，您可以在 web 服務可供其他開發人員 tooconsume 其應用程式。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Hello 發行程序的概觀
hello 以下是發佈 Azure Machine Learning web 服務 tooAzure Marketplace hello 步驟：

1. 建立及發佈機器學習服務要求-回應服務 (RRS)
2. 部署 hello 服務 tooproduction，並取得 API 金鑰和 OData 端點資訊 hello。
3. Hello 的 hello URL 太發佈 web 服務 toopublish[Azure Marketplace （資料市場）](https://publish.windowsazure.com/workspace/) 
4. 一旦送出，您的優惠檢閱，並需要您的客戶之前核准的 toobe 可以啟動購買它。 hello 發佈程序可能需要幾個工作日。 

## <a name="walk-through"></a>逐步解說
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>步驟 1：建立及發佈機器學習服務要求-回應服務 (RRS)
 如果您尚未這樣做，請查看這個 [逐步解說](machine-learning-walkthrough-5-publish-web-service.md)。

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>步驟 2： 部署 hello 服務 tooproduction，並取得 API 金鑰和 OData 端點資訊 hello
1. 從 hello [Azure 傳統入口網站](http://manage.windowsazure.com)，選取 hello **MACHINE LEARNING**選項在 hello 左側的導覽列中，然後選取您的工作區。 
2. 按一下 hello **WEB 服務**索引標籤，而且您想要 toopublish toohello marketplace 選取 hello web 服務。
   
    ![Azure Marketplace][workspace]
3. 選取您會像 toohave hello marketplace 消耗 hello 端點。 如果您尚未建立任何其他端點，您可以選取 hello**預設**端點。
4. 當您按一下 hello 端點上時，您將無法 toosee hello **API 金鑰**。 在稍後的步驟 3 中您將需要此資訊，因此建立一個複本。
   
    ![Azure Marketplace][apikey]
5. 按一下 hello**要求/回應**方法，我們不支援發行批次執行，此時服務 toohello marketplace。 您可以透過可接受 hello 要求/回應方法 toohello API 說明頁面。
6. 複製 hello **OData 端點位址**，您將需要此資訊，以便稍後在步驟 3。
   
    ![Azure Marketplace][odata]

部署到生產環境的 hello 服務。

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>步驟 3: Hello 的 hello URL 發佈 web 服務 toopublish tooAzure Marketplace (DataMarket)
1. 瀏覽過[Azure Marketplace （資料市場）](http://datamarket.azure.com/home) 
2. 按一下 hello**發行**hello hello 頁頂端的連結。 這會帶您 toohello [Microsoft Azure 發行入口網站](https://publish.windowsazure.com)
3. 按一下 hello**發行者**區段 tooregister 為發行者。
4. 建立新產品時，請選取 資料服務，然後按一下建立新的資料服務。 
   
   ![Azure Marketplace][image1]
   
   <br />
5. 在 [ **計劃** ] 下，提供您的產品的相關資訊，包括定價計劃。 決定您要提供免費還是付費服務。 tooget 付費，提供付款資訊，例如您的銀行與稅務資訊。
6. 在下**行銷**提供您提供服務，例如 hello 標題和描述您的優惠的相關資訊。
7. 在下**定價**您可以設定特定國家 （地區），您計劃 hello 價格，或讓 hello 系統 」 autoprice 」 您的優惠。
8. 在 hello**資料服務**索引標籤上，按一下  **Web 服務**為 hello**資料來源**。
   
    ![Azure Marketplace][image2]
9. 在上述步驟 2 中所述，請從 hello Azure 傳統入口網站，取得 hello web 服務 URL 和 API 金鑰。
10. 在 [hello Marketplace 資料服務設定] 對話方塊中貼上 hello OData 端點位址 hello**服務 URL**文字方塊。
11. 如**驗證**，選擇**標頭**為 hello**驗證配置**。
    
    * 輸入 「 授權 」 hello**標頭名稱**。
    * Hello**標頭值**，（不含 hello 引號） 輸入"Bearer"，按一下 hello**空間**列，並再貼上 hello API 金鑰。
    * 選取 hello**此服務是 OData**核取方塊。
    * 按一下**測試連接**tootest hello 連線。
12. 在 [類別] 下，確保已選取 [機器學習服務]。
13. 當您完成輸入所有 hello 中繼資料有關您提供服務，按一下**發行**，然後**推送 tooStaging**。 此時，系統會通知您的任何其餘的問題，您需要 toofix。
14. 您已確保完成所有的 hello 未處理的問題之後，請按一下**要求核准 toopush tooProduction**。 hello 發佈程序可能需要幾個工作日。 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

