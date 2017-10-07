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
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="39839-103">（已被取代）發行 Azure Machine Learning Web 服務 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="39839-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="39839-104">DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。</span><span class="sxs-lookup"><span data-stu-id="39839-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="39839-105">因此，這篇文章目前已過時。</span><span class="sxs-lookup"><span data-stu-id="39839-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="39839-106">或者，您可以發佈您的機器學習實驗 toohello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)hello 資料科學社群的 hello 權益。</span><span class="sxs-lookup"><span data-stu-id="39839-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="39839-107">如需詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。</span><span class="sxs-lookup"><span data-stu-id="39839-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="39839-108">hello Azure Marketplace 付費 toopublish Azure Machine Learning web 服務提供 hello 能力或釋出外部客戶所耗用的服務。</span><span class="sxs-lookup"><span data-stu-id="39839-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="39839-109">這篇文章會提供連結 tooguidelines tooget 您啟動與該程序的概觀。</span><span class="sxs-lookup"><span data-stu-id="39839-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="39839-110">使用此程序，您可以在 web 服務可供其他開發人員 tooconsume 其應用程式。</span><span class="sxs-lookup"><span data-stu-id="39839-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="39839-111">Hello 發行程序的概觀</span><span class="sxs-lookup"><span data-stu-id="39839-111">Overview of hello publishing process</span></span>
<span data-ttu-id="39839-112">hello 以下是發佈 Azure Machine Learning web 服務 tooAzure Marketplace hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="39839-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="39839-113">建立及發佈機器學習服務要求-回應服務 (RRS)</span><span class="sxs-lookup"><span data-stu-id="39839-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="39839-114">部署 hello 服務 tooproduction，並取得 API 金鑰和 OData 端點資訊 hello。</span><span class="sxs-lookup"><span data-stu-id="39839-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="39839-115">Hello 的 hello URL 太發佈 web 服務 toopublish[Azure Marketplace （資料市場）](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="39839-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="39839-116">一旦送出，您的優惠檢閱，並需要您的客戶之前核准的 toobe 可以啟動購買它。</span><span class="sxs-lookup"><span data-stu-id="39839-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="39839-117">hello 發佈程序可能需要幾個工作日。</span><span class="sxs-lookup"><span data-stu-id="39839-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="39839-118">逐步解說</span><span class="sxs-lookup"><span data-stu-id="39839-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="39839-119">步驟 1：建立及發佈機器學習服務要求-回應服務 (RRS)</span><span class="sxs-lookup"><span data-stu-id="39839-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="39839-120">如果您尚未這樣做，請查看這個 [逐步解說](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="39839-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="39839-121">步驟 2： 部署 hello 服務 tooproduction，並取得 API 金鑰和 OData 端點資訊 hello</span><span class="sxs-lookup"><span data-stu-id="39839-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="39839-122">從 hello [Azure 傳統入口網站](http://manage.windowsazure.com)，選取 hello **MACHINE LEARNING**選項在 hello 左側的導覽列中，然後選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="39839-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="39839-123">按一下 hello **WEB 服務**索引標籤，而且您想要 toopublish toohello marketplace 選取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="39839-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="39839-125">選取您會像 toohave hello marketplace 消耗 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="39839-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="39839-126">如果您尚未建立任何其他端點，您可以選取 hello**預設**端點。</span><span class="sxs-lookup"><span data-stu-id="39839-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="39839-127">當您按一下 hello 端點上時，您將無法 toosee hello **API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="39839-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="39839-128">在稍後的步驟 3 中您將需要此資訊，因此建立一個複本。</span><span class="sxs-lookup"><span data-stu-id="39839-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="39839-130">按一下 hello**要求/回應**方法，我們不支援發行批次執行，此時服務 toohello marketplace。</span><span class="sxs-lookup"><span data-stu-id="39839-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="39839-131">您可以透過可接受 hello 要求/回應方法 toohello API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="39839-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="39839-132">複製 hello **OData 端點位址**，您將需要此資訊，以便稍後在步驟 3。</span><span class="sxs-lookup"><span data-stu-id="39839-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="39839-134">部署到生產環境的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="39839-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="39839-135">步驟 3: Hello 的 hello URL 發佈 web 服務 toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="39839-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="39839-136">瀏覽過[Azure Marketplace （資料市場）](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="39839-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="39839-137">按一下 hello**發行**hello hello 頁頂端的連結。</span><span class="sxs-lookup"><span data-stu-id="39839-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="39839-138">這會帶您 toohello [Microsoft Azure 發行入口網站](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="39839-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="39839-139">按一下 hello**發行者**區段 tooregister 為發行者。</span><span class="sxs-lookup"><span data-stu-id="39839-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="39839-140">建立新產品時，請選取 資料服務，然後按一下建立新的資料服務。</span><span class="sxs-lookup"><span data-stu-id="39839-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="39839-142">在 [ **計劃** ] 下，提供您的產品的相關資訊，包括定價計劃。</span><span class="sxs-lookup"><span data-stu-id="39839-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="39839-143">決定您要提供免費還是付費服務。</span><span class="sxs-lookup"><span data-stu-id="39839-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="39839-144">tooget 付費，提供付款資訊，例如您的銀行與稅務資訊。</span><span class="sxs-lookup"><span data-stu-id="39839-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="39839-145">在下**行銷**提供您提供服務，例如 hello 標題和描述您的優惠的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="39839-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="39839-146">在下**定價**您可以設定特定國家 （地區），您計劃 hello 價格，或讓 hello 系統 」 autoprice 」 您的優惠。</span><span class="sxs-lookup"><span data-stu-id="39839-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="39839-147">在 hello**資料服務**索引標籤上，按一下  **Web 服務**為 hello**資料來源**。</span><span class="sxs-lookup"><span data-stu-id="39839-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="39839-149">在上述步驟 2 中所述，請從 hello Azure 傳統入口網站，取得 hello web 服務 URL 和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="39839-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="39839-150">在 [hello Marketplace 資料服務設定] 對話方塊中貼上 hello OData 端點位址 hello**服務 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="39839-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="39839-151">如**驗證**，選擇**標頭**為 hello**驗證配置**。</span><span class="sxs-lookup"><span data-stu-id="39839-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="39839-152">輸入 「 授權 」 hello**標頭名稱**。</span><span class="sxs-lookup"><span data-stu-id="39839-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="39839-153">Hello**標頭值**，（不含 hello 引號） 輸入"Bearer"，按一下 hello**空間**列，並再貼上 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="39839-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="39839-154">選取 hello**此服務是 OData**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="39839-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="39839-155">按一下**測試連接**tootest hello 連線。</span><span class="sxs-lookup"><span data-stu-id="39839-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="39839-156">在 [類別] 下，確保已選取 [機器學習服務]。</span><span class="sxs-lookup"><span data-stu-id="39839-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="39839-157">當您完成輸入所有 hello 中繼資料有關您提供服務，按一下**發行**，然後**推送 tooStaging**。</span><span class="sxs-lookup"><span data-stu-id="39839-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="39839-158">此時，系統會通知您的任何其餘的問題，您需要 toofix。</span><span class="sxs-lookup"><span data-stu-id="39839-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="39839-159">您已確保完成所有的 hello 未處理的問題之後，請按一下**要求核准 toopush tooProduction**。</span><span class="sxs-lookup"><span data-stu-id="39839-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="39839-160">hello 發佈程序可能需要幾個工作日。</span><span class="sxs-lookup"><span data-stu-id="39839-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

