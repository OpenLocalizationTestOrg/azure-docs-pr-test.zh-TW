---
title: "針對重新訓練 Azure Machine Learning Classic Web 服務進行疑難排解 | Microsoft Docs"
description: "找出您在為 Azure Machine Learning Web 服務重新訓練模型時所遇到的常見問題，並加以修正。"
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="e0f81-103">針對 Azure Machine Learning 傳統 Web 服務的重新訓練進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e0f81-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="e0f81-104">重新訓練概觀</span><span class="sxs-lookup"><span data-stu-id="e0f81-104">Retraining overview</span></span>
<span data-ttu-id="e0f81-105">當您將預測性實驗部署為評分 Web 服務時，它會是靜態模型。</span><span class="sxs-lookup"><span data-stu-id="e0f81-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="e0f81-106">當有新資料可用或 API 取用者有自己的資料時，模型就必須重新訓練。</span><span class="sxs-lookup"><span data-stu-id="e0f81-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="e0f81-107">如需傳統 Web 服務重新訓練程序的完整逐步解說，請參閱[以程式設計方式重新訓練 Machine Learning 模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="e0f81-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="e0f81-108">重新訓練程序</span><span class="sxs-lookup"><span data-stu-id="e0f81-108">Retraining process</span></span>
<span data-ttu-id="e0f81-109">當您需要重新訓練 Web 服務時，您必須另外新增某些部分︰</span><span class="sxs-lookup"><span data-stu-id="e0f81-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="e0f81-110">從訓練實驗部署的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="e0f81-111">實驗必須將 **Web 服務輸出**模組附加至**訓練模型**模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="e0f81-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![將 Web 服務的輸出附加至訓練模型。][image1]
* <span data-ttu-id="e0f81-113">新增至評分 Web 服務的新端點。</span><span class="sxs-lookup"><span data-stu-id="e0f81-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="e0f81-114">您可以透過程式設計方式，使用《以程式設計方式重新訓練機器學習服務模型》主題中所參照的範例程式碼加入端點，或是透過 Azure 傳統入口網站來加入。</span><span class="sxs-lookup"><span data-stu-id="e0f81-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="e0f81-115">接著，您可以使用訓練 Web 服務的 API 說明頁面中的範例 C# 程式碼重新訓練模型。</span><span class="sxs-lookup"><span data-stu-id="e0f81-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="e0f81-116">在評估結果後，如果您感到滿意，就可以使用新加入的端點更新已訓練的模型評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="e0f81-117">準備好所有部分之後，為了重新訓練模型所必須採取的主要步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="e0f81-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="e0f81-118">呼叫訓練 Web 服務︰呼叫的對象為批次執行服務 (BES)，而非求回應服務 (RRS)。</span><span class="sxs-lookup"><span data-stu-id="e0f81-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="e0f81-119">您可以使用 API 說明頁面中的範例 C# 程式碼來進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="e0f81-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="e0f81-120">尋找 *BaseLocation*、*RelativeLocation* 和 *SasBlobToken* 的值︰在您呼叫訓練 Web 服務的輸出中會傳回這些值。</span><span class="sxs-lookup"><span data-stu-id="e0f81-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="e0f81-121">![顯示重新訓練範例的輸出和 BaseLocation、RelativeLocation 及 SasBlobToken 的值。][image6]</span><span class="sxs-lookup"><span data-stu-id="e0f81-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="e0f81-122">從評分 Web 服務使用訓練好的新模型更新加入的端點︰使用《以程式設計方式重新訓練機器學習服務模型》所提供的範例程式碼，從評分 Web 服務使用訓練好的新模型更新加入到評分模型的新端點。</span><span class="sxs-lookup"><span data-stu-id="e0f81-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="e0f81-123">常見障礙</span><span class="sxs-lookup"><span data-stu-id="e0f81-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="e0f81-124">檢查是否有正確的 PATCH URL</span><span class="sxs-lookup"><span data-stu-id="e0f81-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="e0f81-125">所使用的 PATCH URL 必須是與新增至評分 Web 服務的新評分端點相關聯的 URL。</span><span class="sxs-lookup"><span data-stu-id="e0f81-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="e0f81-126">有幾個方法可取得 PATCH URL：</span><span class="sxs-lookup"><span data-stu-id="e0f81-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="e0f81-127">**選項 1︰程式設計方式**</span><span class="sxs-lookup"><span data-stu-id="e0f81-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="e0f81-128">若要取得正確的 PATCH URL：</span><span class="sxs-lookup"><span data-stu-id="e0f81-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="e0f81-129">執行 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0f81-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="e0f81-130">從 AddEndpoint 的輸出中找出「HelpLocation」  值並複製 URL。</span><span class="sxs-lookup"><span data-stu-id="e0f81-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![addEndpoint 範例之輸出中的 HelpLocation。][image2]
3. <span data-ttu-id="e0f81-132">將此 URL 貼到瀏覽器中，瀏覽到提供 Web 服務說明連結的頁面。</span><span class="sxs-lookup"><span data-stu-id="e0f81-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="e0f81-133">按一下 [更新資源] 連結以開啟修補說明頁面。</span><span class="sxs-lookup"><span data-stu-id="e0f81-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="e0f81-134">**選項 2：使用 Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="e0f81-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="e0f81-135">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e0f81-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e0f81-136">開啟 [機器學習服務] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e0f81-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="e0f81-137">![機器學習服務索引標籤。][image4]</span><span class="sxs-lookup"><span data-stu-id="e0f81-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="e0f81-138">依序按一下工作區名稱和 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="e0f81-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="e0f81-139">按一下您要使用的評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="e0f81-140">(如果您沒有修改 Web 服務的預設名稱，它的結尾是 [Scoring Exp.]。)</span><span class="sxs-lookup"><span data-stu-id="e0f81-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="e0f81-141">按一下 [新增端點]。</span><span class="sxs-lookup"><span data-stu-id="e0f81-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="e0f81-142">在新增端點之後，按一下其端點名稱。</span><span class="sxs-lookup"><span data-stu-id="e0f81-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="e0f81-143">然後，按一下 [更新資源]  以開啟修補說明頁面。</span><span class="sxs-lookup"><span data-stu-id="e0f81-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f81-144">如果您已將端點新增至訓練 Web 服務，而不是預測性 Web 服務，當您按一下 [更新資源] 連結，就會收到下列錯誤︰很抱歉，但這項功能在此內容中不支援或不可使用。</span><span class="sxs-lookup"><span data-stu-id="e0f81-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="e0f81-145">此 Web 服務有沒有可更新的資源。</span><span class="sxs-lookup"><span data-stu-id="e0f81-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="e0f81-146">造成您的不便我們深感抱歉，並將致力於改善這個工作流程。</span><span class="sxs-lookup"><span data-stu-id="e0f81-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![新端點的儀表板。][image3]

<span data-ttu-id="e0f81-148">PATCH 說明頁面包含必須使用的 PATCH URL，並提供可用來呼叫它的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0f81-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![修補 URL。][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="e0f81-150">檢查正在更新的評分端點是否正確</span><span class="sxs-lookup"><span data-stu-id="e0f81-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="e0f81-151">請勿修補訓練 Web 服務︰修補作業必須是對評分 Web 服務來執行。</span><span class="sxs-lookup"><span data-stu-id="e0f81-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="e0f81-152">請勿修補 Web 服務上的預設端點︰修補作業必須是對您新增的評分 Web 服務端點來執行。</span><span class="sxs-lookup"><span data-stu-id="e0f81-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="e0f81-153">您可以造訪 Azure 傳統入口網站來確認端點位於哪個 Web 服務上。</span><span class="sxs-lookup"><span data-stu-id="e0f81-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0f81-154">請確定您將端點新增至預測性 Web 服務，而不是定型 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="e0f81-155">如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="e0f81-156">預測性 Web 服務應是以 "[predictive exp.]" 結尾。</span><span class="sxs-lookup"><span data-stu-id="e0f81-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="e0f81-157">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e0f81-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e0f81-158">開啟 [機器學習服務] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e0f81-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="e0f81-159">![Machine Learning 工作區 UI。][image4]</span><span class="sxs-lookup"><span data-stu-id="e0f81-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="e0f81-160">選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="e0f81-160">Select your workspace.</span></span>
4. <span data-ttu-id="e0f81-161">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="e0f81-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="e0f81-162">選取您的預測性 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="e0f81-163">確認新的端點已新增至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e0f81-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="e0f81-164">檢查 Web 服務所在的工作區以確保它位於正確區域</span><span class="sxs-lookup"><span data-stu-id="e0f81-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="e0f81-165">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e0f81-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e0f81-166">在功能表中選取 [機器學習服務]。</span><span class="sxs-lookup"><span data-stu-id="e0f81-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="e0f81-167">![Machine Learning 區域 UI。][image4]</span><span class="sxs-lookup"><span data-stu-id="e0f81-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="e0f81-168">確認工作區的所在位置。</span><span class="sxs-lookup"><span data-stu-id="e0f81-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
