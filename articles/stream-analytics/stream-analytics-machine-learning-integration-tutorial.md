---
title: "Azure 串流分析和 Azure Machine Learning 整合 | Microsoft Docs"
description: "如何在串流分析工作中使用使用者定義的函數和機器學習服務"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="48816-103">使用 Azure 串流分析和 Azure Machine Learning 執行情感分析</span><span class="sxs-lookup"><span data-stu-id="48816-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="48816-104">本文說明如何快速設定簡單的 Azure 串流分析工作與 Azure Machine Learning 整合。</span><span class="sxs-lookup"><span data-stu-id="48816-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="48816-105">您要使用 Cortana 智慧資源庫的機器學習服務情感分析模型，來分析串流文字資料並即時判斷情感分數。</span><span class="sxs-lookup"><span data-stu-id="48816-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="48816-106">使用 Cortana Intelligence Suite 可讓您完成這項工作，而不需擔心建立情感分析模型的複雜性。</span><span class="sxs-lookup"><span data-stu-id="48816-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="48816-107">您可以將本文所學套用到以下這類案例：</span><span class="sxs-lookup"><span data-stu-id="48816-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="48816-108">分析串流 Twitter 資料的即時情感。</span><span class="sxs-lookup"><span data-stu-id="48816-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="48816-109">分析客戶與支援人員對談的記錄。</span><span class="sxs-lookup"><span data-stu-id="48816-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="48816-110">評估論壇、部落格和影片的註解。</span><span class="sxs-lookup"><span data-stu-id="48816-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="48816-111">許多其他即時、預測評分的案例。</span><span class="sxs-lookup"><span data-stu-id="48816-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="48816-112">在真實世界的案例中，您會直接從 Twitter 資料流取得資料。</span><span class="sxs-lookup"><span data-stu-id="48816-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="48816-113">為了簡化教學課程，我們已撰寫這個部分，讓串流分析工作從 Azure Blob 儲存體中的 CSV 檔案取得推文。</span><span class="sxs-lookup"><span data-stu-id="48816-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="48816-114">您可以建立您自己的 CSV 檔案，或使用範例 CSV 檔案，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="48816-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![CSV 檔案的範例推文](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="48816-116">您建立的串流分析工作會將情感分析模型做為使用者定義的函數 (UDF) 套用到 Blob 存放區中的範例文字資料。</span><span class="sxs-lookup"><span data-stu-id="48816-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="48816-117">輸出 (情感分析的結果) 會以不同的 CSV 檔案寫入相同的 Blob 存放區。</span><span class="sxs-lookup"><span data-stu-id="48816-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="48816-118">下圖示範這項設定。</span><span class="sxs-lookup"><span data-stu-id="48816-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="48816-119">請注意，如需更真實的案例，可將 Blob 儲存體更換為 Azure 事件中樞輸入內的串流 Twitter 資料。</span><span class="sxs-lookup"><span data-stu-id="48816-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="48816-120">此外，也可針對彙總情緒建置 [Microsoft Power BI](https://powerbi.microsoft.com/) 即時視覺效果。</span><span class="sxs-lookup"><span data-stu-id="48816-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![串流分析機器學習服務整合概觀](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="48816-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="48816-122">Prerequisites</span></span>
<span data-ttu-id="48816-123">開始之前，請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="48816-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="48816-124">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="48816-124">An active Azure subscription.</span></span>
* <span data-ttu-id="48816-125">內附資料的 CSV 檔。</span><span class="sxs-lookup"><span data-stu-id="48816-125">A CSV file with some data in it.</span></span> <span data-ttu-id="48816-126">您可以從 [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv) 下載之前顯示的檔案，或者建立您自己的檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="48816-127">本文中，我們假設您使用 GitHub 的檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="48816-128">總的來說，若要完成本文示範的工作，您要執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="48816-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="48816-129">建立 Azure 儲存體帳戶和 Blob 儲存體容器，並將 CSV 格式的輸入檔案上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="48816-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="48816-130">將 Cortana 智慧資源庫的情感分析模型加入 Azure Machine Learning 工作區，然後在 Machine Learning 工作區中將此模型部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="48816-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="48816-131">建立以函數形式呼叫此 Web 服務的串流分析工作，以判斷所輸入文字的情感。</span><span class="sxs-lookup"><span data-stu-id="48816-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="48816-132">啟動串流分析工作並查看輸出。</span><span class="sxs-lookup"><span data-stu-id="48816-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="48816-133">建立儲存體容器並上傳 CSV 輸入檔</span><span class="sxs-lookup"><span data-stu-id="48816-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="48816-134">在此步驟中，您可以使用任何 CSV 檔案，例如從 GitHub 取得的檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="48816-135">在 Azure 入口網站中，按一下 [新增] &gt; [儲存體] &gt; [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="48816-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![建立新的儲存體帳戶](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="48816-137">提供名稱 (在範例中為 `samldemo`)。</span><span class="sxs-lookup"><span data-stu-id="48816-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="48816-138">名稱只能使用小寫字母和數字，而且在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="48816-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="48816-139">指定現有的資源群組，並指定位置。</span><span class="sxs-lookup"><span data-stu-id="48816-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="48816-140">對於位置，我們建議您在本教學課程中建立的所有資源都使用相同的位置。</span><span class="sxs-lookup"><span data-stu-id="48816-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![提供儲存體帳戶詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="48816-142">在 Azure 入口網站中，選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48816-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="48816-143">在 [儲存體帳戶] 刀鋒視窗中，按一下 [容器]，然後按一下 [+&nbsp;容器] 建立 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="48816-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![建立 Blob 容器](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="48816-145">提供容器的名稱 (在範例中為 `azuresamldemoblob`)，並確認 [存取類型] 設為 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="48816-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="48816-146">完成後，按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="48816-146">When you're done, click **OK**.</span></span>

    ![指定 Blob 容器詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="48816-148">在 [容器] 刀鋒視窗中，選取新的容器，這會開啟該容器的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="48816-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="48816-149">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="48816-149">Click **Upload**.</span></span>

    ![容器的 [上傳] 按鈕](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="48816-151">在 [上傳 Blob] 刀鋒視窗中，指定您在此教學課程想要使用的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="48816-152">對於 [Blob 類型]，選取 [區塊 Blob]，將區塊大小設為 4 MB，這對本教學課程已經足夠。</span><span class="sxs-lookup"><span data-stu-id="48816-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![上傳 Blob 檔案](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="48816-154">按一下刀鋒視窗底部的 [上傳] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48816-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="48816-155">新增 Cortana 智慧資源庫中的情緒分析模型</span><span class="sxs-lookup"><span data-stu-id="48816-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="48816-156">現在，Blob 中已有範例資料，您可以啟用 Cortana 智慧資源庫中的情感分析模型。</span><span class="sxs-lookup"><span data-stu-id="48816-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="48816-157">移至 Cortana 智慧資源庫中的[預測情感分析模型](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) \(英文\) 頁面。</span><span class="sxs-lookup"><span data-stu-id="48816-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="48816-158">按一下 [在 Studio 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="48816-158">Click **Open in Studio**.</span></span>  
   
   ![串流分析機器學習服務, 開啟 Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="48816-160">登入以移至工作區。</span><span class="sxs-lookup"><span data-stu-id="48816-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="48816-161">選取位置。</span><span class="sxs-lookup"><span data-stu-id="48816-161">Select a location.</span></span>

4. <span data-ttu-id="48816-162">按一下頁面底部的 [執行]  。</span><span class="sxs-lookup"><span data-stu-id="48816-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="48816-163">程序會執行大約一分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="48816-163">The process runs, which takes about a minute.</span></span>

   ![在 Machine Learning Studio 中執行實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="48816-165">程序成功執行之後，請選取頁面底部的 [部署 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="48816-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![在 Machine Learning Studio 中將實驗部署為 Web 服務](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="48816-167">若要驗證情感分析模型是否已準備好使用，請按一下 [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48816-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="48816-168">提供文字輸入，例如「我喜歡 Microsoft」。</span><span class="sxs-lookup"><span data-stu-id="48816-168">Provide text input such as "I love Microsoft".</span></span> 

   ![在 Machine Learning Studio 中測試實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="48816-170">如果測試成功，您會看到類似以下範例的結果：</span><span class="sxs-lookup"><span data-stu-id="48816-170">If the test works, you see a result similar to the following example:</span></span>

   ![Machine Learning Studio 中的測試結果](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="48816-172">在 [應用程式] 欄中，按一下 [Excel 2010 或舊版活頁簿] 連結以下載 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="48816-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="48816-173">活頁簿包含您稍後設定串流分析工作所需的 API 金鑰和 URL。</span><span class="sxs-lookup"><span data-stu-id="48816-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![串流分析機器學習服務, 快速概覽](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="48816-175">建立使用機器學習服務模型的串流分析工作</span><span class="sxs-lookup"><span data-stu-id="48816-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="48816-176">您現在可以建立從 Blob 儲存體的 CSV 檔案中讀取範例推文的串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="48816-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="48816-177">建立工作</span><span class="sxs-lookup"><span data-stu-id="48816-177">Create the job</span></span>

1. <span data-ttu-id="48816-178">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="48816-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="48816-179">按一下 [新增] > [物聯網] > [串流分析工作]。</span><span class="sxs-lookup"><span data-stu-id="48816-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![使用新串流分析工作的 Azure 入口網站路徑](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="48816-181">命名工作 `azure-sa-ml-demo`、指定訂用帳戶、指定現有的資源群組或建立一個新的資源群組，並選取工作的位置。</span><span class="sxs-lookup"><span data-stu-id="48816-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![指定新串流分析工作的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="48816-183">設定工作輸入</span><span class="sxs-lookup"><span data-stu-id="48816-183">Configure the job input</span></span>
<span data-ttu-id="48816-184">工作會從您稍早上傳到 Blob 儲存體的 CSV 檔案取得輸入。</span><span class="sxs-lookup"><span data-stu-id="48816-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="48816-185">工作建立之後，請在工作刀鋒視窗的 [工作拓撲] 下，按一下 [輸入] 方塊。</span><span class="sxs-lookup"><span data-stu-id="48816-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![在串流分析工作刀鋒視窗中的 [輸入] 方塊](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="48816-187">在 [輸入] 刀鋒視窗中，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="48816-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![將輸入新增至串流分析工作的 [新增] 按鈕](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="48816-189">使用下列值填寫 [新的輸入] 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="48816-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="48816-190">**輸入別名**：使用名稱 `datainput`。</span><span class="sxs-lookup"><span data-stu-id="48816-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="48816-191">**來源類型**：選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="48816-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="48816-192">**來源**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="48816-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="48816-193">**匯入選項**：選取 [從目前的訂用帳戶使用 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="48816-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="48816-194">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="48816-194">**Storage account**.</span></span> <span data-ttu-id="48816-195">選取您稍早建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48816-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="48816-196">**容器**。</span><span class="sxs-lookup"><span data-stu-id="48816-196">**Container**.</span></span> <span data-ttu-id="48816-197">選取您稍早建立的容器 (`azuresamldemoblob`)。</span><span class="sxs-lookup"><span data-stu-id="48816-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="48816-198">**事件序列化格式**。</span><span class="sxs-lookup"><span data-stu-id="48816-198">**Event serialization format**.</span></span> <span data-ttu-id="48816-199">選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="48816-199">Select **CSV**.</span></span>

    ![新工作輸入的設定](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="48816-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="48816-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="48816-202">設定工作輸出</span><span class="sxs-lookup"><span data-stu-id="48816-202">Configure the job output</span></span>
<span data-ttu-id="48816-203">工作會將結果傳送至取得輸入的相同 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="48816-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="48816-204">在工作刀鋒視窗的 [工作拓撲] 下，按一下 [輸出] 方塊。</span><span class="sxs-lookup"><span data-stu-id="48816-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![建立串流分析作業的新輸出](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="48816-206">在 [輸出] 刀鋒視窗中，按一下 [+ 新增]，然後使用別名 `datamloutput` 新增輸出。</span><span class="sxs-lookup"><span data-stu-id="48816-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="48816-207">對於 [接收器]，選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="48816-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="48816-208">然後使用與您用於 Blob 儲存體之輸入相同的值填入輸出設定的其餘部分：</span><span class="sxs-lookup"><span data-stu-id="48816-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="48816-209">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="48816-209">**Storage account**.</span></span> <span data-ttu-id="48816-210">選取您稍早建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48816-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="48816-211">**容器**。</span><span class="sxs-lookup"><span data-stu-id="48816-211">**Container**.</span></span> <span data-ttu-id="48816-212">選取您稍早建立的容器 (`azuresamldemoblob`)。</span><span class="sxs-lookup"><span data-stu-id="48816-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="48816-213">**事件序列化格式**。</span><span class="sxs-lookup"><span data-stu-id="48816-213">**Event serialization format**.</span></span> <span data-ttu-id="48816-214">選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="48816-214">Select **CSV**.</span></span>

   ![新工作輸出的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="48816-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="48816-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="48816-217">新增機器學習服務函數</span><span class="sxs-lookup"><span data-stu-id="48816-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="48816-218">稍早您將機器學習模型發佈至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="48816-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="48816-219">在我們的案例中，串流分析工作執行時，會將來自輸入的每則範例推文傳送至 Web 服務進行情感分析。</span><span class="sxs-lookup"><span data-stu-id="48816-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="48816-220">Machine Learning Web 服務會傳回情感 (`positive`、`neutral` 或 `negative`)，以及推文屬於正向的機率。</span><span class="sxs-lookup"><span data-stu-id="48816-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="48816-221">在教學課程的本節中，您要在串流分析工作中定義函數。</span><span class="sxs-lookup"><span data-stu-id="48816-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="48816-222">叫用函數，可以將推文傳送至 Web 服務並得到回應。</span><span class="sxs-lookup"><span data-stu-id="48816-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="48816-223">請確定您有稍早下載的 Web 服務 URL 和 API 金鑰 (在 Excel 活頁簿中)。</span><span class="sxs-lookup"><span data-stu-id="48816-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="48816-224">回到工作概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="48816-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="48816-225">在 [設定] 下，選取 [函數]，然後按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="48816-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![將函數新增至串流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="48816-227">輸入 `sentiment` 作為函數別名，並使用下列值填入刀鋒視窗的其餘部分：</span><span class="sxs-lookup"><span data-stu-id="48816-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="48816-228">**函數類型**：選取 [Azure ML]。</span><span class="sxs-lookup"><span data-stu-id="48816-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="48816-229">**匯入選項**：選取 [從不同的訂用帳戶匯入]。</span><span class="sxs-lookup"><span data-stu-id="48816-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="48816-230">這可讓您有機會輸入 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="48816-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="48816-231">**URL**：貼上 Web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="48816-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="48816-232">**金鑰**：貼上 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="48816-232">**Key**: Paste in the API key.</span></span>
  
    ![將機器學習服務函數新增至串流分析工作的設定](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="48816-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="48816-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="48816-235">建立查詢來轉換資料</span><span class="sxs-lookup"><span data-stu-id="48816-235">Create a query to transform the data</span></span>

<span data-ttu-id="48816-236">串流分析使用宣告式、以 SQL 為基礎的查詢來檢查輸入並處理它。</span><span class="sxs-lookup"><span data-stu-id="48816-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="48816-237">在本節中，您要建立從輸入讀取每則推文的查詢，然後叫用機器學習服務函數來執行情感分析。</span><span class="sxs-lookup"><span data-stu-id="48816-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="48816-238">查詢接著會將結果傳送至您定義的輸出 (Blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="48816-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="48816-239">回到工作概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="48816-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="48816-240">在 [工作拓撲] 下，按一下 [查詢] 方塊。</span><span class="sxs-lookup"><span data-stu-id="48816-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="48816-242">輸入下列查詢：</span><span class="sxs-lookup"><span data-stu-id="48816-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="48816-243">查詢會叫用您稍早建立的函數 (`sentiment`) 以便對輸入中的每則推文執行情感分析。</span><span class="sxs-lookup"><span data-stu-id="48816-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="48816-244">按一下 [儲存]  以儲存查詢。</span><span class="sxs-lookup"><span data-stu-id="48816-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="48816-245">啟動串流分析工作並查看輸出</span><span class="sxs-lookup"><span data-stu-id="48816-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="48816-246">您現在可以啟動串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="48816-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="48816-247">啟動工作</span><span class="sxs-lookup"><span data-stu-id="48816-247">Start the job</span></span>
1. <span data-ttu-id="48816-248">回到工作概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="48816-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="48816-249">按一下刀鋒視窗頂端的 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="48816-249">Click **Start** at the top of the blade.</span></span>

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="48816-251">在 [啟動工作] 中，選取 [自訂]，然後選取您將 CSV 檔上傳至 Blob 儲存體的前一天。</span><span class="sxs-lookup"><span data-stu-id="48816-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="48816-252">完成後，按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="48816-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="48816-253">查看輸出</span><span class="sxs-lookup"><span data-stu-id="48816-253">Check the output</span></span>
1. <span data-ttu-id="48816-254">讓工作執行幾分鐘，直到您在 [監視] 方塊中看到活動。</span><span class="sxs-lookup"><span data-stu-id="48816-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="48816-255">如果您有一般用來檢查 Blob 儲存體內容的工具，請使用該工具來檢查 `azuresamldemoblob` 容器。</span><span class="sxs-lookup"><span data-stu-id="48816-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="48816-256">或者，請在 Azure 入口網站中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="48816-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="48816-257">在入口網站中，尋找 `samldemo` 儲存體帳戶，並在該帳戶內，尋找 `azuresamldemoblob` 容器。</span><span class="sxs-lookup"><span data-stu-id="48816-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="48816-258">您會在容器中看到兩個檔案：包含範例推文的檔案，和串流分析工作所產生的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="48816-259">以滑鼠右鍵按一下所產生的檔案，然後選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="48816-259">Right-click the generated file and then select **Download**.</span></span> 

   ![從 Blob 儲存體下載 CSV 工作輸出](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="48816-261">開啟產生的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="48816-261">Open the generated CSV file.</span></span> <span data-ttu-id="48816-262">您會看到類似下列範例的畫面：</span><span class="sxs-lookup"><span data-stu-id="48816-262">You see something like the following example:</span></span>  
   
   ![串流分析機器學習服務, CSV 檢視](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="48816-264">檢視計量</span><span class="sxs-lookup"><span data-stu-id="48816-264">View metrics</span></span>
<span data-ttu-id="48816-265">您也能檢視與 Azure Machine Learning 函數相關的度量。</span><span class="sxs-lookup"><span data-stu-id="48816-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="48816-266">下列與函數相關的計量資訊會顯示在工作刀鋒視窗的 [監視] 方塊中：</span><span class="sxs-lookup"><span data-stu-id="48816-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="48816-267">**函數要求** 指出傳送至 Machine Learning Web 服務的要求數目。</span><span class="sxs-lookup"><span data-stu-id="48816-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="48816-268">**函數事件** 指出要求中的事件數目。</span><span class="sxs-lookup"><span data-stu-id="48816-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="48816-269">根據預設，每個對 Machine Learning Web 服務的要求最多可包含 1,000 個事件。</span><span class="sxs-lookup"><span data-stu-id="48816-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="48816-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48816-270">Next steps</span></span>

* [<span data-ttu-id="48816-271">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="48816-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="48816-272">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="48816-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="48816-273">整合 REST API 與 Machine Learning</span><span class="sxs-lookup"><span data-stu-id="48816-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="48816-274">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="48816-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



