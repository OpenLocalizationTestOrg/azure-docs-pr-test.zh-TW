---
title: "以程式設計方式重新訓練機器學習服務模型 | Microsoft Docs"
description: "了解如何在 Azure Machine Learning 中以程式設計方式重新定型模型，以及使用新定型的模型來更新 Web 服務。"
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="02a28-103">以程式設計方式重新定型機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="02a28-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="02a28-104">在此逐步解說中，您將學習如何以程式設計方式使用 C# 和 Machine Learning 批次執行服務來重新訓練 Azure Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="02a28-105">重新訓練模型之後，下列逐步解說會說明如何更新預測性 Web 服務中的模型︰</span><span class="sxs-lookup"><span data-stu-id="02a28-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="02a28-106">如果您是在 Machine Learning Web 服務入口網站中部署傳統 Web 服務，請參閱[重新訓練傳統 Web 服務](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="02a28-107">如果您是部署新式 Web 服務，請參閱[使用 Machine Learning Management PowerShell Cmdlet 重新訓練新的 Web 服務](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="02a28-108">如需重新訓練程序的概觀，請參閱[重新訓練 Machine Learning 模型](machine-learning-retrain-machine-learning-model.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="02a28-109">如果您要開始使用現有新的 Azure Resource Manager 型 Web 服務，請參閱 [Retrain an existing Predictive web service (重新訓練現有預測性 Web 服務)](machine-learning-retrain-existing-resource-manager-based-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="02a28-110">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="02a28-110">Create a training experiment</span></span>
<span data-ttu-id="02a28-111">針對這個範例，您將使用Microsoft Azure Machine Learning 範例當中的「範例 5：定型、測試、評估二進位分類：成人資料集」。</span><span class="sxs-lookup"><span data-stu-id="02a28-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="02a28-112">建立實驗：</span><span class="sxs-lookup"><span data-stu-id="02a28-112">To create the experiment:</span></span>

1. <span data-ttu-id="02a28-113">登入 Microsoft Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="02a28-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="02a28-114">按一下儀表板右下角的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="02a28-115">從 Microsoft 範例中，選取 範例 5。</span><span class="sxs-lookup"><span data-stu-id="02a28-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="02a28-116">若要重新命名此實驗，在頂端的實驗畫布上，選取實驗名稱 [範例 5：定型、測試、評估二進位分類：成人資料集]。</span><span class="sxs-lookup"><span data-stu-id="02a28-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="02a28-117">輸入「普查模型」。</span><span class="sxs-lookup"><span data-stu-id="02a28-117">Type Census Model.</span></span>
6. <span data-ttu-id="02a28-118">在實驗畫布底端，按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="02a28-119">按一下 [設定 Web 服務]，然後選取 [重新訓練 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="02a28-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="02a28-120">以下顯示初始實驗。</span><span class="sxs-lookup"><span data-stu-id="02a28-120">The following shows the initial experiment.</span></span>
   
   ![初始實驗。][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="02a28-122">建立預測性實驗並發佈為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="02a28-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="02a28-123">接下來，您要建立預測性實驗。</span><span class="sxs-lookup"><span data-stu-id="02a28-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="02a28-124">在實驗畫布底端，按一下 [設定 Web 服務]，然後選取 [預測性 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="02a28-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="02a28-125">這樣會將模型儲存為訓練模型，並新增 Web 服務輸入與輸出模組。</span><span class="sxs-lookup"><span data-stu-id="02a28-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="02a28-126">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="02a28-126">Click **Run**.</span></span> 
3. <span data-ttu-id="02a28-127">實驗完成執行之後，按一下 [部署 Web 服務 [傳統]] 或 [部署 Web 服務[新式]]。</span><span class="sxs-lookup"><span data-stu-id="02a28-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="02a28-128">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="02a28-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="02a28-129">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="02a28-130">將訓練實驗部署為訓練 Web 服務</span><span class="sxs-lookup"><span data-stu-id="02a28-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="02a28-131">若要重新訓練已訓練的模型，您必須將您建立的訓練實驗部署為重新訓練 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="02a28-132">這個 Web 服務需要將「Web 服務輸出」模組連接到[定型模型][train-model]模組，才能產生新的定型模組。</span><span class="sxs-lookup"><span data-stu-id="02a28-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="02a28-133">若要回到訓練實驗，按一下左窗格中的 [實驗] 圖示，然後按一下名為 [普查模型] 的實驗。</span><span class="sxs-lookup"><span data-stu-id="02a28-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="02a28-134">在 [搜尋實驗項目] 方塊中，輸入「Web 服務」。</span><span class="sxs-lookup"><span data-stu-id="02a28-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="02a28-135">將 [Web 服務輸入] 模組拖曳到實驗畫布，然後將其連接到 [清除遺漏資料] 模組。</span><span class="sxs-lookup"><span data-stu-id="02a28-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="02a28-136">這可確保您的訓練資料與原始的訓練資料以相同方式處理。</span><span class="sxs-lookup"><span data-stu-id="02a28-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="02a28-137">將兩個 [Web 服務輸出] 模組拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="02a28-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="02a28-138">將 [訓練模組] 模組的輸出連接到其中一個，將 [評估模型] 模組的輸出連接到另一個。</span><span class="sxs-lookup"><span data-stu-id="02a28-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="02a28-139">[訓練模型] 的 Web 服務輸出將會提供新的已訓練模型。</span><span class="sxs-lookup"><span data-stu-id="02a28-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="02a28-140">連接到**評估模型**的輸出會傳回該模組的輸出，即執行結果。</span><span class="sxs-lookup"><span data-stu-id="02a28-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="02a28-141">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="02a28-141">Click **Run**.</span></span> 

<span data-ttu-id="02a28-142">接下來您必須將訓練實驗部署為可產生訓練模型與模型評估結果的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="02a28-143">若要這麼做，您的下一組動作取決於您使用傳統 Web 服務或新式 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="02a28-144">**傳統 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="02a28-144">**Classic web service**</span></span>

<span data-ttu-id="02a28-145">在實驗畫布底端，按一下 [設定 Web 服務]，然後選取 [部署 Web 服務 [傳統]]。</span><span class="sxs-lookup"><span data-stu-id="02a28-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="02a28-146">顯示的 Web 服務 [儀表板]  中也包含批次執行的 API 金鑰與 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="02a28-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="02a28-147">只有批次執行方法能夠用來建立定型模型。</span><span class="sxs-lookup"><span data-stu-id="02a28-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="02a28-148">**新式 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="02a28-148">**New web service**</span></span>

<span data-ttu-id="02a28-149">在實驗畫布底端，按一下 [設定 Web 服務]，然後選取 [部署 Web 服務 [新式]]。</span><span class="sxs-lookup"><span data-stu-id="02a28-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="02a28-150">Web 服務的 Azure Machine Learning Web 服務入口網站會開啟 [部署 Web 服務] 頁面。</span><span class="sxs-lookup"><span data-stu-id="02a28-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="02a28-151">輸入您 Web 服務的名稱，選擇付款方案，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="02a28-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="02a28-152">只有批次執行方法能夠用來建立定型模型</span><span class="sxs-lookup"><span data-stu-id="02a28-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="02a28-153">不論傳統或新式，在實驗完成執行後，產生的工作流程應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="02a28-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![執行後產生的工作流程。][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="02a28-155">使用 BES 以新資料重新定型模型</span><span class="sxs-lookup"><span data-stu-id="02a28-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="02a28-156">在此範例中，您使用 C# 建立重新訓練應用程式。</span><span class="sxs-lookup"><span data-stu-id="02a28-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="02a28-157">您也可以使用 Python 或 R 範例程式碼來完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="02a28-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="02a28-158">呼叫重新定型 API：</span><span class="sxs-lookup"><span data-stu-id="02a28-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="02a28-159">在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="02a28-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="02a28-160">登入 Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="02a28-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="02a28-161">如果您使用傳統 Web 服務，按一下 [傳統 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="02a28-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="02a28-162">按一下您要使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="02a28-163">按一下預設端點。</span><span class="sxs-lookup"><span data-stu-id="02a28-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="02a28-164">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="02a28-165">在 [取用] 頁面底部的 [範例程式碼] 區段，按一下 [批次]。</span><span class="sxs-lookup"><span data-stu-id="02a28-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="02a28-166">繼續執行此程序的步驟 5。</span><span class="sxs-lookup"><span data-stu-id="02a28-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="02a28-167">如果您是使用新式 Web 服務，請按一下 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="02a28-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="02a28-168">按一下您要使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02a28-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="02a28-169">按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="02a28-170">在 [取用] 頁面底部的 [範例程式碼] 區段，按一下 [批次]。</span><span class="sxs-lookup"><span data-stu-id="02a28-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="02a28-171">複製可用於批次執行的範例 C# 程式碼，然後貼入 Program.cs 檔案；請確定命名空間保持不變。</span><span class="sxs-lookup"><span data-stu-id="02a28-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="02a28-172">新增 Nuget 套件 Microsoft.AspNet.WebApi.Client，如註解中所述。</span><span class="sxs-lookup"><span data-stu-id="02a28-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="02a28-173">若要新增指向 Microsoft.WindowsAzure.Storage.dll 的參考，您可能需要先安裝 Microsoft Azure 儲存體服務的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="02a28-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="02a28-174">如需詳細資訊，請參閱 [Windows 儲存體服務](https://www.nuget.org/packages/WindowsAzure.Storage)。</span><span class="sxs-lookup"><span data-stu-id="02a28-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="02a28-175">更新 apikey 宣告</span><span class="sxs-lookup"><span data-stu-id="02a28-175">Update the apikey declaration</span></span>
<span data-ttu-id="02a28-176">找到 **apikey** 宣告。</span><span class="sxs-lookup"><span data-stu-id="02a28-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="02a28-177">在 [取用] 頁面的 [基本取用資訊] 區段中，找到主索引鍵，將其複製到 **apiKey** 宣告。</span><span class="sxs-lookup"><span data-stu-id="02a28-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="02a28-178">更新 Azure 儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="02a28-178">Update the Azure Storage information</span></span>
<span data-ttu-id="02a28-179">BES 範例程式碼會將檔案從本機磁碟機 (例如 C:\temp\CensusIpnput.csv) 上傳至 Azure 儲存體、加以處理後，再將結果寫回 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="02a28-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="02a28-180">若要完成此工作，您必須從 Azure 傳統入口網站擷取儲存體帳戶的儲存體帳戶名稱、金鑰和容器資訊，然後更新程式碼裡的對應值。</span><span class="sxs-lookup"><span data-stu-id="02a28-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="02a28-181">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="02a28-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="02a28-182">在左側導覽中，按一下 [儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="02a28-183">在儲存體帳戶的清單中，選取要儲存重新定型模型的帳戶。</span><span class="sxs-lookup"><span data-stu-id="02a28-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="02a28-184">按一下此頁面底部的 [管理存取金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="02a28-185">複製並儲存 **主要存取金鑰** ，然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="02a28-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="02a28-186">按一下頁面頂端的 [容器] 。</span><span class="sxs-lookup"><span data-stu-id="02a28-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="02a28-187">您可以使用現有容器，或建立新的容器並儲存名稱。</span><span class="sxs-lookup"><span data-stu-id="02a28-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="02a28-188">找到 *StorageAccountName*、*StorageAccountKey*、*StorageContainerName* 宣告，更新為您從 Azure 入口網站儲存的值。</span><span class="sxs-lookup"><span data-stu-id="02a28-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="02a28-189">您也必須確保程式碼中指定的位置有輸入檔案。</span><span class="sxs-lookup"><span data-stu-id="02a28-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="02a28-190">指定輸出位置</span><span class="sxs-lookup"><span data-stu-id="02a28-190">Specify the output location</span></span>
<span data-ttu-id="02a28-191">在要求承載中指定輸出位置時，必須將 RelativeLocation  中指定檔案的副檔名指定為 .ilearner。</span><span class="sxs-lookup"><span data-stu-id="02a28-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="02a28-192">請參閱下列範例：</span><span class="sxs-lookup"><span data-stu-id="02a28-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="02a28-193">輸出位置的名稱可能不同於此逐步解說中的名稱，取決於您新增 Web 服務輸出模組的順序。</span><span class="sxs-lookup"><span data-stu-id="02a28-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="02a28-194">因為您設定這個訓練實驗有兩個輸出，結果會包含這兩者的儲存位置資訊。</span><span class="sxs-lookup"><span data-stu-id="02a28-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![重新定型輸出][6]

<span data-ttu-id="02a28-196">圖 4：重新定型輸出。</span><span class="sxs-lookup"><span data-stu-id="02a28-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="02a28-197">評估重新定型結果</span><span class="sxs-lookup"><span data-stu-id="02a28-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="02a28-198">當您執行應用程式時，輸出會包含存取評估結果所需的 URL 和 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="02a28-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="02a28-199">您可以組合 *output2* 輸出結果中的 *BaseLocation*、*RelativeLocation*、*SasBlobToken* (如之前重新訓練輸出的圖中所示)，再將完整 URL 貼入瀏覽器網址列，便能看到重新訓練模型的執行結果。</span><span class="sxs-lookup"><span data-stu-id="02a28-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="02a28-200">查看結果以判斷新的定型模型的執行效能是否良好並足以取代現有模型。</span><span class="sxs-lookup"><span data-stu-id="02a28-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="02a28-201">複製輸出結果中的 *BaseLocation*、*RelativeLocation*、*SasBlobToken*，您在重新訓練程序中將用到它們。</span><span class="sxs-lookup"><span data-stu-id="02a28-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02a28-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02a28-202">Next steps</span></span>
<span data-ttu-id="02a28-203">如果您透過按一下 [部署 Web 服務 [傳統]] 部署預測性 Web 服務，請參閱[重新訓練傳統 Web 服務](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="02a28-204">如果您透過按一下 [部署 Web 服務 [新式]] 部署預測性 Web 服務，請參閱[使用 Machine Learning Management PowerShell Cmdlet 重新訓練新的 Web 服務](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="02a28-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
