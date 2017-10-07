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
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="fc58f-103">在預備環境中測試您的資料服務產品</span><span class="sxs-lookup"><span data-stu-id="fc58f-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc58f-104">目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。</span><span class="sxs-lookup"><span data-stu-id="fc58f-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="fc58f-105">如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。</span><span class="sxs-lookup"><span data-stu-id="fc58f-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="fc58f-106">如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。</span><span class="sxs-lookup"><span data-stu-id="fc58f-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="fc58f-107">完成 hello 前兩個步驟之後[建立您的 Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)和[發佈入口網站建立您的資料服務提供](marketplace-publishing-data-service-creation.md)已經準備好讓您提供的服務可在 helloAzure marketplace 所提供。</span><span class="sxs-lookup"><span data-stu-id="fc58f-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="fc58f-108">本主題將逐步引導您完成 hello 先、 中繼、 步驟稱為 「 預備 」</span><span class="sxs-lookup"><span data-stu-id="fc58f-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="fc58f-109">預備部署您的優惠，您可以在此測試並驗證其功能之前將它推送 tooproduction 「 沙箱 」 的私用的方法。</span><span class="sxs-lookup"><span data-stu-id="fc58f-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="fc58f-110">hello 供應項目會出現在暫存就像是 tooa 客戶已經部署。</span><span class="sxs-lookup"><span data-stu-id="fc58f-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="fc58f-111">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="fc58f-111">Step 1.</span></span> <span data-ttu-id="fc58f-112">推入的供應項目 toostaging</span><span class="sxs-lookup"><span data-stu-id="fc58f-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="fc58f-113">推入的供應項目 toostaging 可讓您 tootest hello 供應項目之前會變得可用 toofuture 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="fc58f-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="fc58f-114">您可以查看如何您提供的服務將會出現這些訂閱 tooyour 資料的功能。</span><span class="sxs-lookup"><span data-stu-id="fc58f-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="fc58f-116">登入 hello[發佈入口網站](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="fc58f-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="fc58f-117">選取**Data Services** hello 左側瀏覽視窗中</span><span class="sxs-lookup"><span data-stu-id="fc58f-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="fc58f-118">選取您想 toopush toostaging 的優惠。</span><span class="sxs-lookup"><span data-stu-id="fc58f-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="fc58f-119">您會看見 hello 螢幕上。</span><span class="sxs-lookup"><span data-stu-id="fc58f-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="fc58f-120">按一下**推送 tooStaging**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc58f-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="fc58f-121">如果問題與 hello 供應項目所需 toobe 完成先前 toopushing toostaging，您會看到顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="fc58f-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="fc58f-122">Hello 清單中的每個項目上按一下，以更正這些項目。</span><span class="sxs-lookup"><span data-stu-id="fc58f-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="fc58f-123">所有修正，當都按一下**推送 tooStaging**按鈕一次。</span><span class="sxs-lookup"><span data-stu-id="fc58f-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="fc58f-124">如果不沒有提供任何問題，您會看到下列 hello 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="fc58f-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="fc58f-125">如果您不是規劃/未核准 toosurface 您在 Azure 入口網站的優惠 （目前有限容量），然後只關閉 hello 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="fc58f-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="fc58f-126">tootest 資料服務在 Azure 入口網站 （在加法 toohello DataMarket 入口網站），您必須具有 Azure 訂用帳戶 ID tootest。</span><span class="sxs-lookup"><span data-stu-id="fc58f-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="fc58f-127">此訂用帳戶識別碼會識別 hello 帳戶將會允許 tootest 您提供的服務。</span><span class="sxs-lookup"><span data-stu-id="fc58f-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="fc58f-128">剪下並貼上您的訂用帳戶 ID，然後按一下 hello 核取記號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="fc58f-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="fc58f-130">這些的 Azure 訂用帳戶 Id，才需要測試和預備中 hello [Azure 管理入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="fc58f-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="fc58f-131">它們不需要在 Azure Marketplace 中的 tootest。</span><span class="sxs-lookup"><span data-stu-id="fc58f-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="fc58f-132">hello 出現的下一個畫面會顯示，發行正在進行中顯示 「 進行中 」 的 hello 反白顯示的以下圖示。</span><span class="sxs-lookup"><span data-stu-id="fc58f-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="fc58f-133">推送 toostaging 讓 10 too15 分鐘之間。</span><span class="sxs-lookup"><span data-stu-id="fc58f-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="fc58f-134">若時間過長，請先重新整理您的瀏覽器 (在 IE 中請按 F5 鍵)。</span><span class="sxs-lookup"><span data-stu-id="fc58f-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="fc58f-135">在 hello 罕見的情況下，您的優惠仍在發行 toostaging 小時後，按一下 hello 連絡我們連結 toolet 我們知道有問題。</span><span class="sxs-lookup"><span data-stu-id="fc58f-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="fc58f-137">Hello hello 發送 tooStaging 完成進行中 」 圖示將會停止移動，且會更新 hello 狀態太 「 預備 」。</span><span class="sxs-lookup"><span data-stu-id="fc58f-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="fc58f-138">您會 tootest 現在準備好您的優惠。</span><span class="sxs-lookup"><span data-stu-id="fc58f-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="fc58f-139">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="fc58f-139">Step 2.</span></span> <span data-ttu-id="fc58f-140">在 DataMarket 中測試已推送到預備環境中的產品</span><span class="sxs-lookup"><span data-stu-id="fc58f-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="fc58f-141">按一下下列的 hello 文字 hello 連結**」 看到您在提供的服務。.."**</span><span class="sxs-lookup"><span data-stu-id="fc58f-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="fc58f-142">toodisplay 囉 」 畫面 hello 「 訂閱者 」，將會看到您的優惠效能 tooproduction 時，而且會出現在 DataMarket 中。</span><span class="sxs-lookup"><span data-stu-id="fc58f-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="fc58f-144">測試，或確認每個 hello 12 個項目標示 tooensure 上述所有標誌、 價格/交易、 文字、 影像、 文件，而且連結正確且運作正常。</span><span class="sxs-lookup"><span data-stu-id="fc58f-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="fc58f-145">這是您輸入時建立您的優惠的任何測試值已取代為實際值的好時機 tooensure。</span><span class="sxs-lookup"><span data-stu-id="fc58f-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="fc58f-146">產品標誌</span><span class="sxs-lookup"><span data-stu-id="fc58f-146">Offer logo</span></span>
2. <span data-ttu-id="fc58f-147">產品名稱</span><span class="sxs-lookup"><span data-stu-id="fc58f-147">Offer name</span></span>
3. <span data-ttu-id="fc58f-148">發行者名稱/連結 tooyour 公司的網站</span><span class="sxs-lookup"><span data-stu-id="fc58f-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="fc58f-149">您產品的搜尋類別</span><span class="sxs-lookup"><span data-stu-id="fc58f-149">Search categories for your offer</span></span>
5. <span data-ttu-id="fc58f-150">供應項目的支援連結 tooassist 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fc58f-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="fc58f-151">您產品的的內容描述</span><span class="sxs-lookup"><span data-stu-id="fc58f-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="fc58f-152">描述計費詳細資料的產品方案</span><span class="sxs-lookup"><span data-stu-id="fc58f-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="fc58f-153">連結 tooimplementation 程式碼</span><span class="sxs-lookup"><span data-stu-id="fc58f-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="fc58f-154">示範如何使用產品資料的範例影像</span><span class="sxs-lookup"><span data-stu-id="fc58f-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="fc58f-155">輸入/輸出 hello 供應項目內的每個服務的中繼資料</span><span class="sxs-lookup"><span data-stu-id="fc58f-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="fc58f-156">產品的使用規定</span><span class="sxs-lookup"><span data-stu-id="fc58f-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="fc58f-157">Hello 供應項目的資料的預覽</span><span class="sxs-lookup"><span data-stu-id="fc58f-157">Preview of hello offer's data</span></span>

<span data-ttu-id="fc58f-158">最後，檢查 hello 服務運作 hello Datamarket 透過按一下 hello 連結 」 瀏覽此資料集 」。</span><span class="sxs-lookup"><span data-stu-id="fc58f-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="fc58f-159">新視窗會開啟在 hello 工具我們稱 「 服務總管 」 讓您可以預覽 hello 查詢的結果，對您的服務。</span><span class="sxs-lookup"><span data-stu-id="fc58f-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="fc58f-160">在這個視窗中，您可以輸入的 hello 參數所需，並查看 hello 結果顯示您的服務查詢。</span><span class="sxs-lookup"><span data-stu-id="fc58f-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="fc58f-161">此外，是顯示 hello URL 為您的查詢。</span><span class="sxs-lookup"><span data-stu-id="fc58f-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="fc58f-162">為確定 tooreview hello 服務文字描述 hello 顯示在 hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="fc58f-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="fc58f-163">如果您的優惠包含多個服務和呼叫 hello 底部 tooswitch toohello 下一個服務 tooreview hello 索引標籤及測試。</span><span class="sxs-lookup"><span data-stu-id="fc58f-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="fc58f-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc58f-164">Next step</span></span>
<span data-ttu-id="fc58f-165">您如有問題需要協助解決，請連絡 [Azure 發行者支援](http://go.microsoft.com/fwlink/?LinkId=272975)。</span><span class="sxs-lookup"><span data-stu-id="fc58f-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="fc58f-166">如果您滿意並準備好 toopublish 優惠請閱讀 hello[要求核准 tooPush tooProduction](marketplace-publishing-push-to-production.md)文件。</span><span class="sxs-lookup"><span data-stu-id="fc58f-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="fc58f-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fc58f-167">See Also</span></span>
* [<span data-ttu-id="fc58f-168">快速入門： 如何 toopublish 優惠 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="fc58f-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

