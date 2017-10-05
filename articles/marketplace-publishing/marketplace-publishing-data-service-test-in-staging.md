---
title: "測試要發行到 Marketplace 的資料服務 | Microsoft Docs"
description: "了解如何測試要發行到 Azure Marketplace 的資料服務。"
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
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="dc040-103">在預備環境中測試您的資料服務產品</span><span class="sxs-lookup"><span data-stu-id="dc040-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dc040-104">目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。</span><span class="sxs-lookup"><span data-stu-id="dc040-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="dc040-105">如果您有想要在 AppSource 上發佈的 SaaS 商務應用程式，您可以在[這裡](https://appsource.microsoft.com/partners)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dc040-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="dc040-106">如果您有想要在 Azure Marketplace 發佈的 IaaS 應用程式或開發人員服務，您可以在[這裡](https://azure.microsoft.com/marketplace/programs/certified/)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dc040-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="dc040-107">完成[建立 Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)及[在發佈入口網站中建立您的資料服務產品](marketplace-publishing-data-service-creation.md)這兩個步驟之後，您就可以開始準備在 Azure Marketplace 中銷售您的產品。</span><span class="sxs-lookup"><span data-stu-id="dc040-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="dc040-108">本主題將逐步引導您執行第一個中繼步驟，稱為「預備環境」</span><span class="sxs-lookup"><span data-stu-id="dc040-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="dc040-109">預備環境代表將您的供應項目部署在私人的「沙箱」中，您可以在推送到生產環境之前在沙箱中測試與驗證其功能。</span><span class="sxs-lookup"><span data-stu-id="dc040-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="dc040-110">供應項目會出現在預備環境中，就如同客戶已部署該項目一樣。</span><span class="sxs-lookup"><span data-stu-id="dc040-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="dc040-111">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="dc040-111">Step 1.</span></span> <span data-ttu-id="dc040-112">將您的產品發送到預備環境</span><span class="sxs-lookup"><span data-stu-id="dc040-112">Pushing your offer to staging</span></span>
<span data-ttu-id="dc040-113">將產品發送到預備環境可讓您先測試您的產品，然後再將其提供給日後的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="dc040-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="dc040-114">您可以從資料訂閱者的角度來看您的產品，並了解其功能的運作狀況。</span><span class="sxs-lookup"><span data-stu-id="dc040-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="dc040-116">登入 [發行入口網站](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="dc040-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="dc040-117">選取左導覽視窗中的 [資料服務]  。</span><span class="sxs-lookup"><span data-stu-id="dc040-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="dc040-118">選取要推送到預備環境的產品。</span><span class="sxs-lookup"><span data-stu-id="dc040-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="dc040-119">您將會看到上列畫面。</span><span class="sxs-lookup"><span data-stu-id="dc040-119">You will see the above screen.</span></span>
4. <span data-ttu-id="dc040-120">按一下 [推送至預備環境]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc040-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="dc040-121">您的產品如有任何問題必須在推送到預備環境之前解決，將顯示問題清單。</span><span class="sxs-lookup"><span data-stu-id="dc040-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="dc040-122">按一下清單中每個項目，以更正這些項目。</span><span class="sxs-lookup"><span data-stu-id="dc040-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="dc040-123">當所有的更正作業完成之後，請再按一下 [推送至預備環境]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc040-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="dc040-124">您的產品若無任何問題，將會顯示下列快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="dc040-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="dc040-125">若您不打算在 Azure 入口網站 (目前容量有限) 中提供您的產品，或此舉未獲核准，只需關閉快顯視窗即可。</span><span class="sxs-lookup"><span data-stu-id="dc040-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="dc040-126">除了 DataMarket 入口網站之外，若還要在 Azure 入口網站中測試您的資料服務，您必須要有可供測試的 Azure 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="dc040-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="dc040-127">此訂用帳戶 ID 將會識別能夠測試您產品的帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc040-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="dc040-128">剪下並貼上您的訂用帳戶 ID，然後按一下核取記號以繼續。</span><span class="sxs-lookup"><span data-stu-id="dc040-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="dc040-130">只有在 [Azure 管理入口網站](https://manage.windowsazure.com)的測試及預備環境中，才需要這些 Azure 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="dc040-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="dc040-131">在 Azure Marketplace 測試不需要這些 ID。</span><span class="sxs-lookup"><span data-stu-id="dc040-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="dc040-132">接下來的畫面會顯示進行中圖示，以指出發行正在進行中，如下圖中的黃色強調顯示所示。</span><span class="sxs-lookup"><span data-stu-id="dc040-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="dc040-133">推送到預備環境約需 10 到 15 分鐘的時間完成。</span><span class="sxs-lookup"><span data-stu-id="dc040-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="dc040-134">若時間過長，請先重新整理您的瀏覽器 (在 IE 中請按 F5 鍵)。</span><span class="sxs-lookup"><span data-stu-id="dc040-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="dc040-135">在極少數的情況下，您的產品可以持續推送了一小時以上的時間還在推送，此時，請按一下 [與我們連絡] 連結，通知我們發生此問題。</span><span class="sxs-lookup"><span data-stu-id="dc040-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="dc040-137">當推送到預備環境作業完成時，進行中圖示會停止移動，且狀態會更新成 [已推送到預備環境]。</span><span class="sxs-lookup"><span data-stu-id="dc040-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="dc040-138">您現在已可開始測試您的產品。</span><span class="sxs-lookup"><span data-stu-id="dc040-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="dc040-139">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="dc040-139">Step 2.</span></span> <span data-ttu-id="dc040-140">在 DataMarket 中測試已推送到預備環境中的產品</span><span class="sxs-lookup"><span data-stu-id="dc040-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="dc040-141">按一下在 **在...中檢視您的服務產品**</span><span class="sxs-lookup"><span data-stu-id="dc040-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="dc040-142">之後顯示的連結，可顯示您的產品在生產環境及 DataMarket 中時，訂閱者會見到的畫面。</span><span class="sxs-lookup"><span data-stu-id="dc040-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="dc040-144">測試或驗證上列標記的 12 個項目，確認所有標誌、價格/交易、文字、影像、文件及連結均正確，並能正常運作。</span><span class="sxs-lookup"><span data-stu-id="dc040-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="dc040-145">此時也很適合確認您在建立產品時所輸入的測試值，也全由實際值所代。</span><span class="sxs-lookup"><span data-stu-id="dc040-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="dc040-146">產品標誌</span><span class="sxs-lookup"><span data-stu-id="dc040-146">Offer logo</span></span>
2. <span data-ttu-id="dc040-147">產品名稱</span><span class="sxs-lookup"><span data-stu-id="dc040-147">Offer name</span></span>
3. <span data-ttu-id="dc040-148">發行者名稱/您公司網站的連結</span><span class="sxs-lookup"><span data-stu-id="dc040-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="dc040-149">您產品的搜尋類別</span><span class="sxs-lookup"><span data-stu-id="dc040-149">Search categories for your offer</span></span>
5. <span data-ttu-id="dc040-150">您產品的支援連結 (用於協助訂閱者)</span><span class="sxs-lookup"><span data-stu-id="dc040-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="dc040-151">您產品的的內容描述</span><span class="sxs-lookup"><span data-stu-id="dc040-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="dc040-152">描述計費詳細資料的產品方案</span><span class="sxs-lookup"><span data-stu-id="dc040-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="dc040-153">實作程式碼的連結</span><span class="sxs-lookup"><span data-stu-id="dc040-153">Link to implementation code</span></span>
9. <span data-ttu-id="dc040-154">示範如何使用產品資料的範例影像</span><span class="sxs-lookup"><span data-stu-id="dc040-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="dc040-155">產品中每項服務的輸入/輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="dc040-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="dc040-156">產品的使用規定</span><span class="sxs-lookup"><span data-stu-id="dc040-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="dc040-157">產品資料預覽</span><span class="sxs-lookup"><span data-stu-id="dc040-157">Preview of the offer's data</span></span>

<span data-ttu-id="dc040-158">最後，請按一下 [探索此資料集]，確認服務在 Datamarket 中能夠正常運作。</span><span class="sxs-lookup"><span data-stu-id="dc040-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="dc040-159">新視窗會隨即在工具 (稱為「服務總管」) 中開啟，讓您可以預覽對服務的執行的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="dc040-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="dc040-160">您可以在此視窗中輸入所需的參數，然後檢視您對服務執行查詢所得的結果。</span><span class="sxs-lookup"><span data-stu-id="dc040-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="dc040-161">此外，顯示的內容會是查詢的 URL。</span><span class="sxs-lookup"><span data-stu-id="dc040-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="dc040-162">請務必檢閱視窗最上方所顯示的服務文字描述。</span><span class="sxs-lookup"><span data-stu-id="dc040-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="dc040-163">您的產品若由多個服務呼叫組成，請按一下視窗底部的各個索引標籤記切換到下一項服務，以進行檢閱及測試。</span><span class="sxs-lookup"><span data-stu-id="dc040-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="dc040-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc040-164">Next step</span></span>
<span data-ttu-id="dc040-165">您如有問題需要協助解決，請連絡 [Azure 發行者支援](http://go.microsoft.com/fwlink/?LinkId=272975)。</span><span class="sxs-lookup"><span data-stu-id="dc040-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="dc040-166">若您對一切結果感到滿意，並準備好發行您的產品，請閱讀 [申請核准發行到生產環境](marketplace-publishing-push-to-production.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="dc040-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="dc040-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dc040-167">See Also</span></span>
* [<span data-ttu-id="dc040-168">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="dc040-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

