---
title: "aaaTroubleshoot 重新訓練 Azure 機器學習傳統 web 服務 |Microsoft 文件"
description: "識別並更正時都重新 hello 模型訓練 Azure 機器學習 Web 服務的一般問題時發生。"
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="521b5-103">疑難排解在 Azure 機器學習傳統 Web 服務的定型 hello</span><span class="sxs-lookup"><span data-stu-id="521b5-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="521b5-104">重新訓練概觀</span><span class="sxs-lookup"><span data-stu-id="521b5-104">Retraining overview</span></span>
<span data-ttu-id="521b5-105">當您將預測性實驗部署為評分 Web 服務時，它會是靜態模型。</span><span class="sxs-lookup"><span data-stu-id="521b5-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="521b5-106">當新的資料可用時，或 hello hello API 取用者擁有自己的資料，hello 模型需要 toobe 重新定型。</span><span class="sxs-lookup"><span data-stu-id="521b5-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="521b5-107">Hello 重新訓練傳統 Web 服務的程序的完整逐步解說，請參閱[重新訓練機器學習模型以程式設計方式](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="521b5-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="521b5-108">重新訓練程序</span><span class="sxs-lookup"><span data-stu-id="521b5-108">Retraining process</span></span>
<span data-ttu-id="521b5-109">當您需要 tooretrain hello Web 服務時，您必須新增某些其他的片段：</span><span class="sxs-lookup"><span data-stu-id="521b5-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="521b5-110">Web 服務，從 hello 訓練試驗部署。</span><span class="sxs-lookup"><span data-stu-id="521b5-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="521b5-111">必須要有 hello 實驗**Web 服務輸出**模組附加的 hello toohello 輸出**定型模型**模組。</span><span class="sxs-lookup"><span data-stu-id="521b5-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![附加 hello web 服務輸出 toohello 定型模型。][image1]
* <span data-ttu-id="521b5-113">新的端點加入 tooyour 計分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="521b5-114">您可以透過程式設計方式加入 hello 端點使用 hello hello 中參考的範例程式碼進行重新培訓機器學習模型以程式設計方式主題或透過 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="521b5-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="521b5-115">然後，您可以使用 hello 範例 C# 程式碼從 hello 訓練 Web 服務的 API 說明頁面 tooretrain 模型。</span><span class="sxs-lookup"><span data-stu-id="521b5-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="521b5-116">評估 hello 結果並感到滿意它們之後，您會更新計分 hello 您加入的新端點的 web 服務的 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="521b5-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="521b5-117">與所有 hello 元件之後，您必須採取 tooretrain hello 模型 hello 主要步驟如下：</span><span class="sxs-lookup"><span data-stu-id="521b5-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="521b5-118">呼叫 hello 訓練 Web 服務： hello 呼叫 toohello 批次執行服務 (BES)，不 hello 要求回應服務 (RR)。</span><span class="sxs-lookup"><span data-stu-id="521b5-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="521b5-119">您可以在 hello API 說明頁面 toomake hello 呼叫使用 hello 範例 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="521b5-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="521b5-120">尋找 hello 的 hello 值*BaseLocation*， *RelativeLocation*，和*SasBlobToken*： 從您呼叫 toohello 訓練 Web hello 輸出中傳回這些值服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="521b5-121">![顯示 hello 輸出的 hello 重新訓練範例與 hello BaseLocation、 RelativeLocation 和 SasBlobToken 的值。][image6]</span><span class="sxs-lookup"><span data-stu-id="521b5-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="521b5-122">更新 hello 加入從 hello 新計分 hello 與 web 服務端點來定型模型： 使用 hello 範例程式碼，提供在 hello 重新訓練機器學習模型以程式設計方式更新 hello 新端點加入新計分模型以 hello toohellohello 訓練 Web 服務從定型的模型。</span><span class="sxs-lookup"><span data-stu-id="521b5-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="521b5-123">常見障礙</span><span class="sxs-lookup"><span data-stu-id="521b5-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="521b5-124">如果您擁有 hello 更正修補程式的 URL，請核取 toosee</span><span class="sxs-lookup"><span data-stu-id="521b5-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="521b5-125">hello 修補程式的 URL，您正在使用必須 hello 與相關聯的 hello 評分端點您新增 toohello 計分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="521b5-126">有數種方式 tooobtain hello 修補程式的 URL:</span><span class="sxs-lookup"><span data-stu-id="521b5-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="521b5-127">**選項 1︰程式設計方式**</span><span class="sxs-lookup"><span data-stu-id="521b5-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="521b5-128">tooget hello 更正修補程式的 URL:</span><span class="sxs-lookup"><span data-stu-id="521b5-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="521b5-129">執行 hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="521b5-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="521b5-130">從 AddEndpoint hello 輸出，找出 hello *HelpLocation*值並複製 hello URL。</span><span class="sxs-lookup"><span data-stu-id="521b5-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation hello hello addEndpoint 範例輸出中。][image2]
3. <span data-ttu-id="521b5-132">Hello URL 貼入瀏覽器 toonavigate tooa 頁面提供 hello Web 服務的說明連結。</span><span class="sxs-lookup"><span data-stu-id="521b5-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="521b5-133">按一下 hello**更新資源**連結 tooopen hello 修補程式說明頁面。</span><span class="sxs-lookup"><span data-stu-id="521b5-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="521b5-134">**選項 2： 使用 hello Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="521b5-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="521b5-135">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="521b5-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="521b5-136">開啟 hello 機器學習服務索引標籤。![機器學習服務索引標籤。][image4]</span><span class="sxs-lookup"><span data-stu-id="521b5-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="521b5-137">依序按一下工作區名稱和 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="521b5-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="521b5-138">按一下 hello 計分您正在使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="521b5-139">（如果您未修改 hello hello web 服務的預設名稱，它會結束 [計分 Exp。] 中。）</span><span class="sxs-lookup"><span data-stu-id="521b5-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="521b5-140">按一下 [新增端點]。</span><span class="sxs-lookup"><span data-stu-id="521b5-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="521b5-141">加入 hello 端點之後，按一下 hello 端點名稱。</span><span class="sxs-lookup"><span data-stu-id="521b5-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="521b5-142">然後按一下 **更新資源**tooopen hello 修補說明頁面。</span><span class="sxs-lookup"><span data-stu-id="521b5-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="521b5-143">如果您已加入而不是 hello 預測 Web 服務的 hello 端點 toohello 訓練 Web 服務，您會收到下列錯誤，當您按一下 hello hello**更新資源**連結： 抱歉，但不是支援這項功能或在此內容中使用。</span><span class="sxs-lookup"><span data-stu-id="521b5-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="521b5-144">此 Web 服務有沒有可更新的資源。</span><span class="sxs-lookup"><span data-stu-id="521b5-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="521b5-145">我們深感抱歉造成您的不便 hello，努力改善此工作流程。</span><span class="sxs-lookup"><span data-stu-id="521b5-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![新端點的儀表板。][image3]

<span data-ttu-id="521b5-147">hello 修補程式說明頁面包含 hello 修補程式的 URL，您必須使用，並提供範例程式碼，您可以使用 toocall 它。</span><span class="sxs-lookup"><span data-stu-id="521b5-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![修補 URL。][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="521b5-149">請檢查您要更新 hello 正確的計分端點 toosee</span><span class="sxs-lookup"><span data-stu-id="521b5-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="521b5-150">無法修補 hello 訓練 Web 服務： hello 修補作業必須 hello 計分 Web 服務上執行。</span><span class="sxs-lookup"><span data-stu-id="521b5-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="521b5-151">無法修補 hello Web 服務上的預設端點： hello 修補作業必須 hello 新計分您加入的 Web 服務端點上執行。</span><span class="sxs-lookup"><span data-stu-id="521b5-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="521b5-152">您可以確認哪一個 Web 服務的 hello 端點是在造訪 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="521b5-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="521b5-153">請確定您要加入 hello 端點 toohello 預測的 Web 服務，hello 訓練 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="521b5-154">如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="521b5-155">hello 預測 Web 服務應該以"[預測 exp 表示。] 結束。</span><span class="sxs-lookup"><span data-stu-id="521b5-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="521b5-156">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="521b5-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="521b5-157">開啟 hello 機器學習服務索引標籤。![Machine Learning 工作區 UI。][image4]</span><span class="sxs-lookup"><span data-stu-id="521b5-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="521b5-158">選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="521b5-158">Select your workspace.</span></span>
4. <span data-ttu-id="521b5-159">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="521b5-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="521b5-160">選取您的預測性 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="521b5-161">確認新的端點已加入 toohello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="521b5-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="521b5-162">檢查您的 web 服務是的 tooensure 處於 hello 正確的地區中的 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="521b5-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="521b5-163">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="521b5-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="521b5-164">選取機器學習 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="521b5-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="521b5-165">![Machine Learning 區域 UI。][image4]</span><span class="sxs-lookup"><span data-stu-id="521b5-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="521b5-166">確認您的工作區的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="521b5-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
