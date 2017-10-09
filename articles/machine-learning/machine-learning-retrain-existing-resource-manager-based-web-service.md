---
title: "aaaRetrain 預測的現有 web 服務 |Microsoft 文件"
description: "了解 tooretrain 模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="b6a40-103">重新定型現有的預測 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b6a40-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="b6a40-104">本文件說明 hello 重新訓練 hello 遵照案例的程序：</span><span class="sxs-lookup"><span data-stu-id="b6a40-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="b6a40-105">您有訓練實驗和預測實驗，您已部署為實際運作的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="b6a40-106">您有新的資料，您希望您預測的 web 服務 toouse tooperform 其計分。</span><span class="sxs-lookup"><span data-stu-id="b6a40-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="b6a40-107">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="b6a40-108">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="b6a40-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="b6a40-109">從您現有的 web 服務和實驗，您需要 toofollow 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b6a40-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="b6a40-110">更新 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-110">Update hello model.</span></span>
   1. <span data-ttu-id="b6a40-111">修改您的 web 服務輸入及輸出的定型實驗 tooallow。</span><span class="sxs-lookup"><span data-stu-id="b6a40-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="b6a40-112">訓練的 web 服務來部署 hello 定型實驗。</span><span class="sxs-lookup"><span data-stu-id="b6a40-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="b6a40-113">使用 hello 定型實驗的批次執行服務 (BES) tooretrain hello 模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="b6a40-114">使用 hello Azure 機器學習 PowerShell cmdlet tooupdate hello 預測實驗。</span><span class="sxs-lookup"><span data-stu-id="b6a40-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="b6a40-115">登入 tooyour Azure 資源管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6a40-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="b6a40-116">收到 hello web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="b6a40-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="b6a40-117">將 hello web 服務定義匯出為 JSON。</span><span class="sxs-lookup"><span data-stu-id="b6a40-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="b6a40-118">更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。</span><span class="sxs-lookup"><span data-stu-id="b6a40-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="b6a40-119">Hello JSON 匯入 web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="b6a40-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="b6a40-120">使用新的 web 服務定義來更新 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="b6a40-121">部署 hello 定型實驗</span><span class="sxs-lookup"><span data-stu-id="b6a40-121">Deploy hello training experiment</span></span>
<span data-ttu-id="b6a40-122">toodeploy hello 訓練試驗訓練的 web 服務，您必須新增 web 服務輸入及輸出 toohello 模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="b6a40-123">藉由連接*Web 服務輸出*模組 toohello 實驗的*[定型模型][ train-model]* 模組，啟用 hello 定型實驗tooproduce 新定型的模型，您可以使用預測實驗中。</span><span class="sxs-lookup"><span data-stu-id="b6a40-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="b6a40-124">如果您有*評估模型*模組，您也可以附加 web 服務輸出 tooget hello 評估的結果做為輸出。</span><span class="sxs-lookup"><span data-stu-id="b6a40-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="b6a40-125">tooupdate 定型實驗：</span><span class="sxs-lookup"><span data-stu-id="b6a40-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="b6a40-126">連接*Web 服務輸入*模組 tooyour 資料輸入 (例如，*清除遺漏資料*模組)。</span><span class="sxs-lookup"><span data-stu-id="b6a40-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="b6a40-127">您通常會想 tooensure 中處理您的輸入的資料相同的 hello 與原始定型資料的方式。</span><span class="sxs-lookup"><span data-stu-id="b6a40-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="b6a40-128">連接*Web 服務輸出*模組 toohello 輸出您*定型模型*模組。</span><span class="sxs-lookup"><span data-stu-id="b6a40-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="b6a40-129">如果您有*評估模型*模組，而且您想要將 toooutput hello 評估結果，連接*Web 服務輸出*模組 toohello 輸出您*評估模型*模組。</span><span class="sxs-lookup"><span data-stu-id="b6a40-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="b6a40-130">執行您的實驗。</span><span class="sxs-lookup"><span data-stu-id="b6a40-130">Run your experiment.</span></span>

<span data-ttu-id="b6a40-131">接下來，您必須部署 hello 定型實驗做會產生定型的模型和模型的評估結果為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="b6a40-132">在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**，然後選取**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="b6a40-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="b6a40-133">hello Azure 機器學習 Web 服務入口網站開啟 toohello**部署 Web 服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="b6a40-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="b6a40-134">輸入您的 Web 服務名稱，選擇付款方案，然後按一下部署 。</span><span class="sxs-lookup"><span data-stu-id="b6a40-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="b6a40-135">您只能使用 hello 批次執行方法來建立定型的模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="b6a40-136">使用 BES 進行重新培訓 hello 模型使用新的資料</span><span class="sxs-lookup"><span data-stu-id="b6a40-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="b6a40-137">此範例中，我們會使用重新訓練應用程式的 C# toocreate hello。</span><span class="sxs-lookup"><span data-stu-id="b6a40-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="b6a40-138">您也可以使用 Python 或 R 的範例程式碼 tooaccomplish 這項工作。</span><span class="sxs-lookup"><span data-stu-id="b6a40-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="b6a40-139">重新訓練應用程式開發介面 toocall hello:</span><span class="sxs-lookup"><span data-stu-id="b6a40-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="b6a40-140">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="b6a40-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="b6a40-141">登入 toohello 機器學習 Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6a40-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="b6a40-142">按一下您正在使用的 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="b6a40-143">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="b6a40-143">Click **Consume**.</span></span>
5. <span data-ttu-id="b6a40-144">在 hello 底部 hello**取用** 頁面的 hello**範例程式碼**區段中，按一下**批次**。</span><span class="sxs-lookup"><span data-stu-id="b6a40-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="b6a40-145">複製 hello C# 程式碼範例的批次執行，並將它貼到 hello Program.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6a40-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="b6a40-146">請確定該 hello 命名空間會保持不變。</span><span class="sxs-lookup"><span data-stu-id="b6a40-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="b6a40-147">新增 hello NuGet 封裝 Microsoft.AspNet.WebApi.Client，hello 註解中所指定。</span><span class="sxs-lookup"><span data-stu-id="b6a40-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="b6a40-148">tooadd hello 參考 tooMicrosoft.WindowsAzure.Storage.dll，您可能必須先 tooinstall hello [Azure 儲存體服務的用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)。</span><span class="sxs-lookup"><span data-stu-id="b6a40-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="b6a40-149">hello 下列螢幕擷取畫面顯示 hello**取用**hello Azure 機器學習 Web 服務入口網站頁面中的。</span><span class="sxs-lookup"><span data-stu-id="b6a40-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![取用頁面][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="b6a40-151">更新 hello apikey 宣告</span><span class="sxs-lookup"><span data-stu-id="b6a40-151">Update hello apikey declaration</span></span>
<span data-ttu-id="b6a40-152">找出 hello **apikey**宣告：</span><span class="sxs-lookup"><span data-stu-id="b6a40-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="b6a40-153">在 hello**基本耗用量資訊**區段 hello**取用**頁面上，找出 hello 主索引鍵並將它複製 toohello **apikey**宣告。</span><span class="sxs-lookup"><span data-stu-id="b6a40-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="b6a40-154">更新 hello Azure 儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="b6a40-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="b6a40-155">hello BES 範例程式碼會將檔案從本機磁碟機 (例如，"C:\temp\CensusIpnput.csv 」) tooAzure 儲存體上傳、 加以處理，並將 hello 結果後 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b6a40-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="b6a40-156">tooupdate hello Azure 儲存體資訊，您必須擷取 hello hello Azure 傳統入口網站，從儲存體帳戶的名稱、 金鑰和容器資訊，然後執行實驗之後, 更新 hello correspondi hello 所產生的儲存體帳戶工作流程應該類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b6a40-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![執行後產生的工作流程][4]<span data-ttu-id="b6a40-158">ng hello 程式碼中的值。</span><span class="sxs-lookup"><span data-stu-id="b6a40-158">ng values in hello code.</span></span>

1. <span data-ttu-id="b6a40-159">登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6a40-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="b6a40-160">在 hello 左側瀏覽資料行中，按一下 **儲存體**。</span><span class="sxs-lookup"><span data-stu-id="b6a40-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="b6a40-161">從儲存體帳戶的 hello 清單中選取一個 toostore hello 重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="b6a40-162">在 hello hello 頁面底部，按一下**管理存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b6a40-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="b6a40-163">複製並儲存 hello**主要存取金鑰**和 hello 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b6a40-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="b6a40-164">在 hello hello 頁面頂端，按一下**容器**。</span><span class="sxs-lookup"><span data-stu-id="b6a40-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="b6a40-165">選取現有的容器，或建立一個新並儲存 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6a40-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="b6a40-166">找出 hello *StorageAccountName*， *StorageAccountKey*，和*StorageContainerName*宣告和更新您儲存從 hello 傳統入口網站的 hello 值.</span><span class="sxs-lookup"><span data-stu-id="b6a40-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="b6a40-167">您也必須確定該 hello 輸入的檔可在您指定在 hello 程式碼中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="b6a40-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="b6a40-168">指定 hello 輸出位置</span><span class="sxs-lookup"><span data-stu-id="b6a40-168">Specify hello output location</span></span>
<span data-ttu-id="b6a40-169">當您在 hello 要求裝載中指定 hello 輸出位置時，hello hello 檔案中指定的副檔名*RelativeLocation*必須指定為`ilearner`。</span><span class="sxs-lookup"><span data-stu-id="b6a40-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="b6a40-170">請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a40-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="b6a40-171">hello 以下是範例的輸出重新訓練：![重新訓練輸出][6]</span><span class="sxs-lookup"><span data-stu-id="b6a40-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="b6a40-172">評估 hello 定型的結果</span><span class="sxs-lookup"><span data-stu-id="b6a40-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="b6a40-173">當您執行 hello 應用程式時，hello 輸出會包括 hello URL 和必要 tooaccess hello 評估結果的共用的存取簽章 token。</span><span class="sxs-lookup"><span data-stu-id="b6a40-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="b6a40-174">您可以看到 hello 重新定型模型的 hello 效能結果，藉由結合 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果如*output2* （如 hello 上述重新訓練輸出影像所示） 並貼入 hello 瀏覽器網址列中的 hello 完整 URL。</span><span class="sxs-lookup"><span data-stu-id="b6a40-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="b6a40-175">請檢查 hello 結果 toodetermine 是否 hello 新定型的模型執行現有的指引也足夠 tooreplace hello。</span><span class="sxs-lookup"><span data-stu-id="b6a40-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="b6a40-176">複製 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果。</span><span class="sxs-lookup"><span data-stu-id="b6a40-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="b6a40-177">進行重新培訓 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="b6a40-177">Retrain hello web service</span></span>
<span data-ttu-id="b6a40-178">當您重新訓練新的 web 服務時，您會更新 hello 預測 web 服務定義 tooreference hello 新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="b6a40-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="b6a40-179">hello web 服務定義是 hello 定型模型的 hello web 服務的內部表示法，而且不是直接修改。</span><span class="sxs-lookup"><span data-stu-id="b6a40-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="b6a40-180">請確定您會預測實驗和未定型實驗擷取 hello web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="b6a40-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="b6a40-181">登入 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="b6a40-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="b6a40-182">您必須先登入 tooyour 從 hello PowerShell 環境中的 Azure 帳戶，使用 hello[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b6a40-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="b6a40-183">取得 hello Web 服務定義物件</span><span class="sxs-lookup"><span data-stu-id="b6a40-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="b6a40-184">接下來，呼叫 hello 取得 hello Web 服務定義物件[Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b6a40-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="b6a40-185">toodetermine hello 資源群組名稱的現有 web 服務，在您訂用帳戶中執行不含任何參數 toodisplay hello web 服務的 hello Get AzureRmMlWebService cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b6a40-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="b6a40-186">找出 hello web 服務，然後查看 其 web 服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6a40-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="b6a40-187">hello hello 資源群組名稱是 hello 識別碼 hello 第四個元素後方 hello *resourceGroups*項目。</span><span class="sxs-lookup"><span data-stu-id="b6a40-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="b6a40-188">在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="b6a40-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="b6a40-189">或者，toodetermine hello 資源群組名稱的現有 web 服務，請登入 toohello Azure 機器學習 Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="b6a40-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="b6a40-190">選取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6a40-190">Select hello web service.</span></span> <span data-ttu-id="b6a40-191">hello 資源群組名稱是 hello hello web 服務，URL hello 第五個項目後方 hello *resourceGroups*項目。</span><span class="sxs-lookup"><span data-stu-id="b6a40-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="b6a40-192">在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="b6a40-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="b6a40-193">匯出為 JSON 的 hello Web 服務定義物件</span><span class="sxs-lookup"><span data-stu-id="b6a40-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="b6a40-194">hello 定型的模型 toouse hello toomodify hello 定義新定型模型，您必須先使用 hello[匯出 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 它 tooa JSON 格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="b6a40-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="b6a40-195">更新 hello 參考 toohello ilearner 做為 blob</span><span class="sxs-lookup"><span data-stu-id="b6a40-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="b6a40-196">在 [hello 資產，找出 hello [定型的模型]，更新 hello *uri* hello 中的值*locationInfo*節點以 hello hello ilearner 做為 blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="b6a40-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="b6a40-197">hello URI 由產生結合 hello *BaseLocation*和 hello *RelativeLocation* hello BES 訓練呼叫 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="b6a40-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="b6a40-198">Hello JSON 匯入 Web 服務定義物件</span><span class="sxs-lookup"><span data-stu-id="b6a40-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="b6a40-199">您必須使用 hello[匯入 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello 修改回您可以使用 tooupdate hello predicative 實驗的 Web 服務定義物件的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6a40-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="b6a40-200">更新 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="b6a40-200">Update hello web service</span></span>
<span data-ttu-id="b6a40-201">最後，使用 hello[更新 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 預測實驗。</span><span class="sxs-lookup"><span data-stu-id="b6a40-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
