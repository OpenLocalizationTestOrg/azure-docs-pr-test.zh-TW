---
title: "aaaRetrain 機器學習模型以程式設計的方式 |Microsoft 文件"
description: "了解 tooprogrammatically 訓練模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中的結果。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="032b9-103">以程式設計方式重新定型機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="032b9-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="032b9-104">在本逐步解說中，您將學習如何 tooprogrammatically 重新定型使用 C# 和機器學習批次執行服務的 hello Azure Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="032b9-105">一旦您已重新定型 hello 模型，hello 遵循逐步解說顯示如何 tooupdate hello 模型在預測 web 服務：</span><span class="sxs-lookup"><span data-stu-id="032b9-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="032b9-106">如果您部署的 hello 機器學習 Web 服務入口網站中的傳統 web 服務，請參閱[傳統 web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="032b9-107">如果您部署新的 web 服務，請參閱[重新定型新的 web 服務使用 hello 機器學習服務管理 cmdlet](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="032b9-108">如需 hello 定型程序的概觀，請參閱[機器學習模型進行重新培訓](machine-learning-retrain-machine-learning-model.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="032b9-109">如果您想 toostart 與現有新的 Azure 資源管理員會根據 web 服務，請參閱[重新定型現有預測 web 服務](machine-learning-retrain-existing-resource-manager-based-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="032b9-110">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="032b9-110">Create a training experiment</span></span>
<span data-ttu-id="032b9-111">針對此範例中，您將使用 「 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 從 hello Microsoft Azure Machine Learning 的範例。</span><span class="sxs-lookup"><span data-stu-id="032b9-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="032b9-112">toocreate hello 實驗：</span><span class="sxs-lookup"><span data-stu-id="032b9-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="032b9-113">登入 tooMicrosoft Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="032b9-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="032b9-114">在 hello 底部 hello 儀表板的右下角，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="032b9-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="032b9-115">從 hello Microsoft 範例中，選取 範例 5。</span><span class="sxs-lookup"><span data-stu-id="032b9-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="032b9-116">toorename hello 實驗中的，在 hello 頂端 hello 實驗畫布範圍，請選取 hello 實驗名稱 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」。</span><span class="sxs-lookup"><span data-stu-id="032b9-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="032b9-117">輸入「普查模型」。</span><span class="sxs-lookup"><span data-stu-id="032b9-117">Type Census Model.</span></span>
6. <span data-ttu-id="032b9-118">在 hello hello 實驗畫布底部，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="032b9-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="032b9-119">按一下 [設定 Web 服務]，然後選取 [重新訓練 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="032b9-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="032b9-120">hello 下列範例示範 hello 初始實驗。</span><span class="sxs-lookup"><span data-stu-id="032b9-120">hello following shows hello initial experiment.</span></span>
   
   ![初始實驗。][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="032b9-122">建立預測性實驗並發佈為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="032b9-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="032b9-123">接下來，您要建立預測性實驗。</span><span class="sxs-lookup"><span data-stu-id="032b9-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="032b9-124">在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**預測 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="032b9-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="032b9-125">這樣會將 hello 模型儲存為定型的模型，並將 web 服務輸入和輸出模組。</span><span class="sxs-lookup"><span data-stu-id="032b9-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="032b9-126">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="032b9-126">Click **Run**.</span></span> 
3. <span data-ttu-id="032b9-127">Hello 實驗執行完成之後，請按一下**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="032b9-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="032b9-128">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="032b9-129">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="032b9-130">部署為定型 web 服務的 hello 定型實驗</span><span class="sxs-lookup"><span data-stu-id="032b9-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="032b9-131">tooretrain hello 定型的模型，您必須部署您建立為 Retraining web 服務的 hello 定型實驗。</span><span class="sxs-lookup"><span data-stu-id="032b9-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="032b9-132">此 web 服務需要*Web 服務輸出*模組連接 toohello *[定型模型][ train-model]* 模組、 新 toobe 無法 tooproduce定型的模型。</span><span class="sxs-lookup"><span data-stu-id="032b9-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="032b9-133">tooreturn toohello 定型實驗中，按一下 hello 左窗格中的 hello 實驗圖示，然後按一下 hello 實驗名為 「 人口普查 」 模型。</span><span class="sxs-lookup"><span data-stu-id="032b9-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="032b9-134">在 hello 搜尋實驗項目搜尋方塊中，輸入 web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="032b9-135">拖曳*Web 服務輸出*模組 hello 到實驗畫布，並連接其輸出 toohello*清除遺漏資料*模組。</span><span class="sxs-lookup"><span data-stu-id="032b9-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="032b9-136">這可確保您訓練的資料會處理相同的 hello 與原始定型資料的方式。</span><span class="sxs-lookup"><span data-stu-id="032b9-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="032b9-137">拖放兩*web 服務輸出*模組 hello 到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="032b9-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="032b9-138">Hello hello 輸出連接*定型模型*模組 tooone 和 hello 輸出 hello*評估模型*模組 toohello 其他。</span><span class="sxs-lookup"><span data-stu-id="032b9-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="032b9-139">hello web 服務輸出**定型模型**為我們提供 hello 新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="032b9-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="032b9-140">hello 輸出太附加**評估模型**傳回該模組的輸出，也就是 hello 效能結果。</span><span class="sxs-lookup"><span data-stu-id="032b9-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="032b9-141">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="032b9-141">Click **Run**.</span></span> 

<span data-ttu-id="032b9-142">接下來您必須部署 hello 定型實驗做會產生定型的模型和模型的評估結果為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="032b9-143">tooaccomplish 您下一步的動作集，這是取決於您使用與傳統 web 服務或新的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="032b9-144">**傳統 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="032b9-144">**Classic web service**</span></span>

<span data-ttu-id="032b9-145">在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**部署 Web 服務 [傳統]**。</span><span class="sxs-lookup"><span data-stu-id="032b9-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="032b9-146">Web 服務的 hello**儀表板**hello API 金鑰與 hello API 說明頁面會顯示批次執行。</span><span class="sxs-lookup"><span data-stu-id="032b9-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="032b9-147">Hello 批次執行方法可用來建立定型模型。</span><span class="sxs-lookup"><span data-stu-id="032b9-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="032b9-148">**新式 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="032b9-148">**New web service**</span></span>

<span data-ttu-id="032b9-149">在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="032b9-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="032b9-150">hello Web 服務 Azure 機器學習 Web 服務入口網站開啟 toohello 部署 web 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="032b9-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="032b9-151">輸入您 Web 服務的名稱，選擇付款方案，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="032b9-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="032b9-152">Hello 批次執行方法可以用來建立定型的模型</span><span class="sxs-lookup"><span data-stu-id="032b9-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="032b9-153">在任一情況下，實驗具有已完成的執行之後 hello 產生工作流程看起來應該如下：</span><span class="sxs-lookup"><span data-stu-id="032b9-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![執行後產生的工作流程。][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="032b9-155">訓練 hello 模型結果與新的資料使用 BES</span><span class="sxs-lookup"><span data-stu-id="032b9-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="032b9-156">例如，您使用重新訓練應用程式的 C# toocreate hello。</span><span class="sxs-lookup"><span data-stu-id="032b9-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="032b9-157">您也可以使用 hello Python 或 R 範例程式碼 tooaccomplish 這項工作。</span><span class="sxs-lookup"><span data-stu-id="032b9-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="032b9-158">toocall hello 重新訓練應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="032b9-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="032b9-159">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="032b9-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="032b9-160">登入 toohello Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="032b9-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="032b9-161">如果您使用傳統 Web 服務，按一下 [傳統 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="032b9-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="032b9-162">按一下您要使用的 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="032b9-163">按一下 hello 預設端點。</span><span class="sxs-lookup"><span data-stu-id="032b9-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="032b9-164">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="032b9-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="032b9-165">在 hello 底部 hello**取用** 頁面的 hello**範例程式碼**區段中，按一下**批次**。</span><span class="sxs-lookup"><span data-stu-id="032b9-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="032b9-166">繼續此程序的 toostep 5。</span><span class="sxs-lookup"><span data-stu-id="032b9-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="032b9-167">如果您是使用新式 Web 服務，請按一下 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="032b9-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="032b9-168">按一下您要使用的 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="032b9-169">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="032b9-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="032b9-170">在 hello 底部 hello 取用的頁面上，於 hello**範例程式碼**區段中，按一下**批次**。</span><span class="sxs-lookup"><span data-stu-id="032b9-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="032b9-171">複製 hello C# 程式碼範例的批次執行，並將它貼到 hello Program.cs 檔案中，確定 hello 命名空間會保持不變。</span><span class="sxs-lookup"><span data-stu-id="032b9-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="032b9-172">新增 hello Nuget 封裝 Microsoft.AspNet.WebApi.Client hello 註解中所指定。</span><span class="sxs-lookup"><span data-stu-id="032b9-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="032b9-173">tooadd hello 參考 tooMicrosoft.WindowsAzure.Storage.dll，您需要 tooinstall hello 用戶端程式庫的 Microsoft Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="032b9-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="032b9-174">如需詳細資訊，請參閱 [Windows 儲存體服務](https://www.nuget.org/packages/WindowsAzure.Storage)。</span><span class="sxs-lookup"><span data-stu-id="032b9-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="032b9-175">更新 hello apikey 宣告</span><span class="sxs-lookup"><span data-stu-id="032b9-175">Update hello apikey declaration</span></span>
<span data-ttu-id="032b9-176">找出 hello **apikey**宣告。</span><span class="sxs-lookup"><span data-stu-id="032b9-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="032b9-177">在 hello**基本耗用量資訊**區段 hello**取用**頁面上，找出 hello 主索引鍵並將它複製 toohello **apikey**宣告。</span><span class="sxs-lookup"><span data-stu-id="032b9-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="032b9-178">更新 hello Azure 儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="032b9-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="032b9-179">hello BES 範例程式碼會將檔案從本機磁碟機 （例如"C:\temp\CensusIpnput.csv 」） tooAzure 儲存體上傳、 加以處理，並將 hello 結果後 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="032b9-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="032b9-180">tooaccomplish 這個工作中，您必須擷取 hello 儲存體帳戶名稱、 金鑰和容器資訊從 hello 傳統 Azure 入口網站和對應值 hello 程式碼中的 hello 更新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="032b9-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="032b9-181">登入 toohello 傳統 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="032b9-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="032b9-182">在 hello 左側瀏覽資料行中，按一下 **儲存體**。</span><span class="sxs-lookup"><span data-stu-id="032b9-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="032b9-183">從儲存體帳戶的 hello 清單中選取一個 toostore hello 重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="032b9-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="032b9-184">在 hello hello 頁面底部，按一下**管理存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="032b9-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="032b9-185">複製並儲存 hello**主要存取金鑰**和 hello 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="032b9-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="032b9-186">在 hello hello 頁面頂端，按一下**容器**。</span><span class="sxs-lookup"><span data-stu-id="032b9-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="032b9-187">選取現有的容器或建立一個新並儲存 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="032b9-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="032b9-188">找出 hello *StorageAccountName*， *StorageAccountKey*，和*StorageContainerName*宣告和更新您從儲存的 hello 值 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="032b9-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="032b9-189">您也必須確定您指定在 hello 程式碼中的 hello 位置位於可用 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="032b9-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="032b9-190">指定 hello 輸出位置</span><span class="sxs-lookup"><span data-stu-id="032b9-190">Specify hello output location</span></span>
<span data-ttu-id="032b9-191">當指定 hello 輸出位置中的 hello 要求內容，hello hello 檔案中指定的副檔名*RelativeLocation*必須指定為 ilearner。</span><span class="sxs-lookup"><span data-stu-id="032b9-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="032b9-192">請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="032b9-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="032b9-193">hello 名稱的輸出位置，可能不同於在本逐步解說是根據您加入 hello web 服務輸出模組中的 hello 順序 hello。</span><span class="sxs-lookup"><span data-stu-id="032b9-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="032b9-194">因為您設定具有兩個輸出此定型實驗，hello 結果會包含儲存體位置的這兩種資訊。</span><span class="sxs-lookup"><span data-stu-id="032b9-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![重新定型輸出][6]

<span data-ttu-id="032b9-196">圖 4：重新定型輸出。</span><span class="sxs-lookup"><span data-stu-id="032b9-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="032b9-197">評估 hello 定型的結果</span><span class="sxs-lookup"><span data-stu-id="032b9-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="032b9-198">當您執行 hello 應用程式時，hello 輸出包含 hello URL 和 SAS 權杖的必要 tooaccess hello 評估結果。</span><span class="sxs-lookup"><span data-stu-id="032b9-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="032b9-199">您可以看到 hello 重新定型模型的 hello 效能結果，藉由結合 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果如*output2* （如 hello 上述重新訓練輸出影像所示） 並貼上 hello 瀏覽器網址列中的 hello 完整 URL。</span><span class="sxs-lookup"><span data-stu-id="032b9-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="032b9-200">請檢查 hello 結果 toodetermine 是否 hello 新定型的模型執行現有的指引也足夠 tooreplace hello。</span><span class="sxs-lookup"><span data-stu-id="032b9-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="032b9-201">複製 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken*從 hello 輸出結果中，您會使用在 hello 定型程序期間。</span><span class="sxs-lookup"><span data-stu-id="032b9-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="032b9-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="032b9-202">Next steps</span></span>
<span data-ttu-id="032b9-203">如果您部署 hello 預測 web 服務，依序按一下**部署 Web 服務 [傳統]**，請參閱[傳統 web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="032b9-204">如果您部署 hello 預測 web 服務，依序按一下**部署 Web 服務 [New]**，請參閱[重新定型新的 web 服務使用 hello 機器學習服務管理 cmdlet](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="032b9-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
