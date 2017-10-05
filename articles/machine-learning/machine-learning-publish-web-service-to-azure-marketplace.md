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
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="be21b-103">(已過時) 將 Azure Machine Learning Web 服務發佈到 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="be21b-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="be21b-104">DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。</span><span class="sxs-lookup"><span data-stu-id="be21b-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="be21b-105">因此，這篇文章目前已過時。</span><span class="sxs-lookup"><span data-stu-id="be21b-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="be21b-106">替代方案是，您可以將 Machine Learning 實驗發佈到 [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com/)，以利資料科學社群使用。</span><span class="sxs-lookup"><span data-stu-id="be21b-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="be21b-107">如需詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。</span><span class="sxs-lookup"><span data-stu-id="be21b-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="be21b-108">Azure Marketplace 可讓您發行 Azure Machine Learning Web 服務，作為供外部客戶付費或免費使用的服務。</span><span class="sxs-lookup"><span data-stu-id="be21b-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="be21b-109">本文章將提供該程序的概觀，以及入門使用的指引連結。</span><span class="sxs-lookup"><span data-stu-id="be21b-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="be21b-110">透過此程序，您將可讓您的 Web 服務成為可供其他開發人員運用在其應用程式中的服務。</span><span class="sxs-lookup"><span data-stu-id="be21b-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="be21b-111">發行程序概觀</span><span class="sxs-lookup"><span data-stu-id="be21b-111">Overview of the publishing process</span></span>
<span data-ttu-id="be21b-112">以下是將 Azure Machine Learning Web 服務發行至 Azure Marketplace 的步驟：</span><span class="sxs-lookup"><span data-stu-id="be21b-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="be21b-113">建立及發佈機器學習服務要求-回應服務 (RRS)</span><span class="sxs-lookup"><span data-stu-id="be21b-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="be21b-114">將服務部署至實際執行環境中，並取得 API 金鑰與 OData 端點資訊。</span><span class="sxs-lookup"><span data-stu-id="be21b-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="be21b-115">使用已發行之 Web 服務的 URL，發行至 [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="be21b-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="be21b-116">您的產品在提交之後必須經過審閱和核准，才可供客戶購買。</span><span class="sxs-lookup"><span data-stu-id="be21b-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="be21b-117">發行程序可能需要數個工作天。</span><span class="sxs-lookup"><span data-stu-id="be21b-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="be21b-118">逐步解說</span><span class="sxs-lookup"><span data-stu-id="be21b-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="be21b-119">步驟 1：建立及發佈機器學習服務要求-回應服務 (RRS)</span><span class="sxs-lookup"><span data-stu-id="be21b-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="be21b-120">如果您尚未這樣做，請查看這個 [逐步解說](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="be21b-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="be21b-121">步驟 2：將服務部署至實際執行環境中，並取得 API 金鑰與 OData 端點資訊</span><span class="sxs-lookup"><span data-stu-id="be21b-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="be21b-122">從 [Azure 傳統入口網站](http://manage.windowsazure.com)，從左側的導覽列中選取 [機器學習服務] 選項，並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="be21b-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="be21b-123">按一下 [ **Web 服務** ] 索引標籤，並選取您想要發佈到 Marketplace 的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="be21b-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="be21b-125">選取您想要 Marketplace 取用的端點。</span><span class="sxs-lookup"><span data-stu-id="be21b-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="be21b-126">如果您尚未建立任何額外的端點，您可以選取 [ **預設** ] 端點。</span><span class="sxs-lookup"><span data-stu-id="be21b-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="be21b-127">當您在端點上按一下時，您將能夠看到 **API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="be21b-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="be21b-128">在稍後的步驟 3 中您將需要此資訊，因此建立一個複本。</span><span class="sxs-lookup"><span data-stu-id="be21b-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="be21b-130">按一下 [ **要求/回應** ] 方法，此時我們不支援發佈批次執行服務至 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="be21b-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="be21b-131">這將帶您前往進入要求/回應方法的 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="be21b-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="be21b-132">複製 [ **OData 端點位址**]，在稍後的步驟 3 中您將需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="be21b-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="be21b-134">將服務部署到實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="be21b-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="be21b-135">步驟 3：使用已發行之 Web 服務的 URL，發行至 Azure Marketplace (資料市場)</span><span class="sxs-lookup"><span data-stu-id="be21b-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="be21b-136">瀏覽至 [Azure Marketplace (資料市場)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="be21b-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="be21b-137">按一下頁面頂端的 [ **發佈** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="be21b-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="be21b-138">這帶您前往 [Microsoft Azure 發佈入口網站](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="be21b-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="be21b-139">按一下 [ **發行者** ] 區段，以註冊為發行者。</span><span class="sxs-lookup"><span data-stu-id="be21b-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="be21b-140">建立新產品時，請選取 [資料服務]，然後按一下 [建立新的資料服務]。</span><span class="sxs-lookup"><span data-stu-id="be21b-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="be21b-142">在 [ **計劃** ] 下，提供您的產品的相關資訊，包括定價計劃。</span><span class="sxs-lookup"><span data-stu-id="be21b-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="be21b-143">決定您要提供免費還是付費服務。</span><span class="sxs-lookup"><span data-stu-id="be21b-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="be21b-144">若要收費，請提供付款資訊，例如您的銀行和稅務資訊。</span><span class="sxs-lookup"><span data-stu-id="be21b-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="be21b-145">在 [ **行銷** ] 下提供服務的相關資訊，例如您的提供項目的標題和描述。</span><span class="sxs-lookup"><span data-stu-id="be21b-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="be21b-146">在 [ **價格** ] 下，您可以設定特定國家/地區的價格，或讓系統為您的提供項目自動定價。</span><span class="sxs-lookup"><span data-stu-id="be21b-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="be21b-147">在 [資料服務] 索引標籤中，按一下 [Web 服務] 做為 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="be21b-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="be21b-149">從 Azure 傳統入口網站取得 Web 服務 URL 和 API 金鑰，如以上的步驟 2 所述。</span><span class="sxs-lookup"><span data-stu-id="be21b-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="be21b-150">在 [Marketplace 資料服務] 設定對話方塊中，將 OData 端點位址貼入 [ **服務 URL** ] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="be21b-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="be21b-151">在 [驗證] 中，選擇 [標頭] 做為 [驗證配置]。</span><span class="sxs-lookup"><span data-stu-id="be21b-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="be21b-152">輸入 "Authorization" 作為 [ **標頭名稱**]。</span><span class="sxs-lookup"><span data-stu-id="be21b-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="be21b-153">針對 [標頭值]，輸入 "Bearer" (不含引號)，按一下 [空間] 列，然後貼上 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="be21b-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="be21b-154">勾選 [ **這個服務是 OData** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="be21b-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="be21b-155">按一下 [ **測試連線** ] 以測試連線。</span><span class="sxs-lookup"><span data-stu-id="be21b-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="be21b-156">在 [類別] 下，確保已選取 [機器學習服務]。</span><span class="sxs-lookup"><span data-stu-id="be21b-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="be21b-157">完成輸入提供服務所有的中繼資料後，請按一下 [發佈]，然後按一下 [推入到預備環境]。</span><span class="sxs-lookup"><span data-stu-id="be21b-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="be21b-158">此時，將通知您必須先修正的任何其餘問題。</span><span class="sxs-lookup"><span data-stu-id="be21b-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="be21b-159">確定完成所有未解決的問題後，請按一下 [ **要求核准以推入到實際執行環境**]。</span><span class="sxs-lookup"><span data-stu-id="be21b-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="be21b-160">發行程序可能需要數個工作天。</span><span class="sxs-lookup"><span data-stu-id="be21b-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

