---
title: "重新訓練現有的預測 Web 服務 | Microsoft Docs"
description: "了解如何在 Azure Machine Learning 中重新定型模型，以及使用新定型的模型來更新 Web 服務。"
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
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="fcc4f-103">重新定型現有的預測 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fcc4f-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="fcc4f-104">本文件描述下列案例的重新定型程序︰</span><span class="sxs-lookup"><span data-stu-id="fcc4f-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="fcc4f-105">您有訓練實驗和預測實驗，您已部署為實際運作的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="fcc4f-106">您有新的資料想要讓預測 Web 服務用來執行其評分。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="fcc4f-107">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="fcc4f-108">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="fcc4f-109">從您現有的 Web 服務和實驗開始，您必須請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="fcc4f-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="fcc4f-110">更新模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-110">Update the model.</span></span>
   1. <span data-ttu-id="fcc4f-111">修改您的訓練實驗，允許 Web 服務輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="fcc4f-112">將訓練實驗部署為定型 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="fcc4f-113">使用訓練實驗批次執行服務 (BES) 重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="fcc4f-114">使用 Azure Machine Learning PowerShell Cmdlet 來更新預測實驗。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="fcc4f-115">登入您的 Azure Resource Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="fcc4f-116">取得 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="fcc4f-117">將 Web 服務定義匯出為 JSON。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="fcc4f-118">在 JSON 中將參考更新為 ilearner blob。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="fcc4f-119">將 JSON 匯入至 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="fcc4f-120">使用新的 Web 服務定義更新 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="fcc4f-121">部署訓練實驗</span><span class="sxs-lookup"><span data-stu-id="fcc4f-121">Deploy the training experiment</span></span>
<span data-ttu-id="fcc4f-122">若要將訓練實驗部署為重新定型 Web 服務，您必須將 Web 服務輸入和輸出新增至模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="fcc4f-123">藉由將 *Web 服務輸出* 模組連接至實驗的 *[培訓模型][train-model]* 模組，即可讓訓練實驗產生可在預測實驗中使用的定型模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="fcc4f-124">如果您有「評估模型」模組，您也可以附加 Web 服務輸出，以取得評估結果做為輸出。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="fcc4f-125">若要更新您的訓練實驗︰</span><span class="sxs-lookup"><span data-stu-id="fcc4f-125">To update your training experiment:</span></span>

1. <span data-ttu-id="fcc4f-126">將「Web 服務輸入」模組連接至您的資料輸入 (例如，「清除遺漏資料」模組)。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="fcc4f-127">通常，您會想要確保您的輸入資料與原始的訓練資料以相同方式處理。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="fcc4f-128">將 *Web 服務輸出* 模組連接至 *訓練模型* 模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="fcc4f-129">如果您有「評估模型」模組，且您想要輸出評估結果，請將「Web 服務輸出」模組連接至「評估模型」模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="fcc4f-130">執行您的實驗。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-130">Run your experiment.</span></span>

<span data-ttu-id="fcc4f-131">接下來您必須將訓練實驗部署為可產生訓練模型與模型評估結果的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="fcc4f-132">在實驗畫布底端，按一下 [設定 Web 服務]，然後選取 [部署 Web 服務 [新式]]。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="fcc4f-133">Azure Machine Learning Web Services 入口網站會開啟 [部署 Web 服務] 頁面。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="fcc4f-134">輸入您的 Web 服務名稱，選擇付款方案，然後按一下 [部署] 。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="fcc4f-135">您只能使用批次執行方法來建立定型模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="fcc4f-136">使用 BES 以新資料重新定型模型</span><span class="sxs-lookup"><span data-stu-id="fcc4f-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="fcc4f-137">在此範例中，我們使用 C# 建立重新訓練應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="fcc4f-138">您也可以使用 Python 或 R 範例程式碼來完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="fcc4f-139">若要呼叫重新定型 API：</span><span class="sxs-lookup"><span data-stu-id="fcc4f-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="fcc4f-140">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="fcc4f-141">登入 Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="fcc4f-142">按一下您要使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="fcc4f-143">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-143">Click **Consume**.</span></span>
5. <span data-ttu-id="fcc4f-144">在 [取用] 頁面底部的 [範例程式碼] 區段，按一下 [批次]。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="fcc4f-145">複製可用於批次執行的範例 C# 程式碼，然後貼入 Program.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="fcc4f-146">請確定命名空間保持不變。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="fcc4f-147">新增 NuGet 套件 Microsoft.AspNet.WebApi.Client，如註解中所述。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="fcc4f-148">若要新增指向 Microsoft.WindowsAzure.Storage.dll 的參考，您可能需要先安裝 [Azure 儲存體服務的用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="fcc4f-149">下列螢幕擷取畫面顯示 Azure Machine Learning Web 服務入口網站的 [取用]頁面。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![取用頁面][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="fcc4f-151">更新 apikey 宣告</span><span class="sxs-lookup"><span data-stu-id="fcc4f-151">Update the apikey declaration</span></span>
<span data-ttu-id="fcc4f-152">找到 **apikey** 宣告：</span><span class="sxs-lookup"><span data-stu-id="fcc4f-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="fcc4f-153">在 [取用] 頁面的 [基本取用資訊] 區段中，找到主索引鍵，將其複製到 **apiKey** 宣告。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="fcc4f-154">更新 Azure 儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="fcc4f-154">Update the Azure Storage information</span></span>
<span data-ttu-id="fcc4f-155">BES 範例程式碼會將檔案從本機磁碟機 (例如，C:\temp\CensusIpnput.csv) 上傳至 Azure 儲存體、加以處理後，再將結果寫回 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="fcc4f-156">若要更新 Azure 儲存體資訊，您必須從 Azure 傳統入口網站擷取儲存體帳戶名稱、金鑰，以及儲存體帳戶的容器資訊，然後更新對應項目。執行實驗之後，產生的工作流程應該會如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fcc4f-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![執行後產生的工作流程][4]<span data-ttu-id="fcc4f-158">程式碼中的 ng 值。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-158">ng values in the code.</span></span>

1. <span data-ttu-id="fcc4f-159">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="fcc4f-160">在左側導覽中，按一下 [儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="fcc4f-161">在儲存體帳戶的清單中，選取要儲存重新定型模型的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="fcc4f-162">按一下此頁面底部的 [管理存取金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="fcc4f-163">複製並儲存 **主要存取金鑰** ，然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="fcc4f-164">按一下頁面頂端的 [容器] 。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="fcc4f-165">您可以使用現有容器，或建立新的容器並儲存名稱。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="fcc4f-166">找到 StorageAccountName、StorageAccountKey、StorageContainerName 宣告，更新為您從傳統入口網站儲存的值。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="fcc4f-167">您也必須確保程式碼中指定的位置有輸入檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="fcc4f-168">指定輸出位置</span><span class="sxs-lookup"><span data-stu-id="fcc4f-168">Specify the output location</span></span>
<span data-ttu-id="fcc4f-169">在要求承載中指定輸出位置時，必須將 RelativeLocation  中指定檔案的副檔名指定為 `ilearner`。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="fcc4f-170">請參閱下列範例：</span><span class="sxs-lookup"><span data-stu-id="fcc4f-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="fcc4f-171">以下是重新定型輸出的範例︰![重新定型輸出][6]</span><span class="sxs-lookup"><span data-stu-id="fcc4f-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="fcc4f-172">評估重新定型結果</span><span class="sxs-lookup"><span data-stu-id="fcc4f-172">Evaluate the retraining results</span></span>
<span data-ttu-id="fcc4f-173">當您執行應用程式時，輸出會包含存取評估結果所需的 URL 和共用存取簽章權杖。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="fcc4f-174">您可以組合 output2 輸出結果中的 BaseLocation、RelativeLocation、SasBlobToken (如之前重新訓練輸出的圖中所示)，再將完整 URL 貼入瀏覽器網址列，便能看到重新訓練模型的執行結果。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="fcc4f-175">查看結果以判斷新的定型模型的執行效能是否良好並足以取代現有模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="fcc4f-176">複製輸出結果中的 BaseLocation、RelativeLocation、SasBlobToken。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="fcc4f-177">重新定型 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fcc4f-177">Retrain the web service</span></span>
<span data-ttu-id="fcc4f-178">當您重新定型新的 Web 服務時，可以更新預測性 Web 服務定義以參考新的定型模型。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="fcc4f-179">Web 服務定義是 Web 服務定型模型的內部表示法，且不可直接修改。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="fcc4f-180">請確定您要擷取的是預測性實驗而非訓練實驗的 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="fcc4f-181">登入 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fcc4f-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="fcc4f-182">您必須先在 PowerShell 環境中，使用 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) Cmdlet 登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="fcc4f-183">取得 Web 服務定義物件</span><span class="sxs-lookup"><span data-stu-id="fcc4f-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="fcc4f-184">接下來，呼叫 [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) Cmdlet 取得 Web 服務定義物件。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="fcc4f-185">若要判斷現有 Web 服務的資源群組名稱，執行不含任何參數的 Get-AzureRmMlWebService cmdlet 來顯示您訂用帳戶中的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="fcc4f-186">找出 Web 服務，再查看其 Web 服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="fcc4f-187">資源群組的名稱是識別碼中的第四個元素，緊接在 resourceGroups  元素之後。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="fcc4f-188">在下列範例中，資源群組名稱是 Default-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="fcc4f-189">或者，若要判斷現有 Web 服務的資源群組名稱，登入 Azure Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="fcc4f-190">選取 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-190">Select the web service.</span></span> <span data-ttu-id="fcc4f-191">資源群組名稱是 Web 服務 URL 的第五個元素，緊接在 resourceGroups  元素之後。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="fcc4f-192">在下列範例中，資源群組名稱是 Default-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="fcc4f-193">將 Web 服務定義物件匯出為 JSON</span><span class="sxs-lookup"><span data-stu-id="fcc4f-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="fcc4f-194">若要將定義修改為定型模型以使用新定型的模型，您必須先使用 [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) Cmdlet 將其匯出為 JSON 格式檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="fcc4f-195">將參考更新為 ilearner blob</span><span class="sxs-lookup"><span data-stu-id="fcc4f-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="fcc4f-196">在資產中，找出 [定型模型]，使用 ilearner blob 的 URI 更新 locationInfo 節點中的 uri 值。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="fcc4f-197">URI 的產生方式為結合來自 BES 重新定型呼叫輸出的 BaseLocation 和 RelativeLocation。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="fcc4f-198">將 JSON 匯入至 Web 服務定義物件</span><span class="sxs-lookup"><span data-stu-id="fcc4f-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="fcc4f-199">您必須使用 [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) Cmdlet 將修改過的 JSON 檔案轉換回可用來更新預測性實驗的 Web 服務定義物件。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="fcc4f-200">更新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fcc4f-200">Update the web service</span></span>
<span data-ttu-id="fcc4f-201">最後，使用 [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) Cmdlet 來更新預測性實驗。</span><span class="sxs-lookup"><span data-stu-id="fcc4f-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
