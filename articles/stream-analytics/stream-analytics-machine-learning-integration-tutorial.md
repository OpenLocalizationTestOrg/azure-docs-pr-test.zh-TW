---
title: "aaaAzure 資料流分析和機器學習的整合 |Microsoft 文件"
description: "如何 toouse 使用者定義函數和機器學習中資料流分析工作"
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
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="d43f9-103">使用 Azure 串流分析和 Azure Machine Learning 執行情感分析</span><span class="sxs-lookup"><span data-stu-id="d43f9-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="d43f9-104">本文說明如何 tooquickly 設定整合 Azure Machine Learning 的簡單 Azure Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="d43f9-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="d43f9-105">您使用的機器學習情緒分析模型與 hello Cortana 智慧組件庫 tooanalyze 資料流處理的文字資料，並判斷即時 hello 人氣分數。</span><span class="sxs-lookup"><span data-stu-id="d43f9-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="d43f9-106">使用 hello Cortana 智慧套件，可讓您完成這項工作，而不需擔心 hello 複雜的建置情緒分析模型。</span><span class="sxs-lookup"><span data-stu-id="d43f9-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="d43f9-107">您可以套用您從這類的發行項 tooscenarios 了解：</span><span class="sxs-lookup"><span data-stu-id="d43f9-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="d43f9-108">分析串流 Twitter 資料的即時情感。</span><span class="sxs-lookup"><span data-stu-id="d43f9-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="d43f9-109">分析客戶與支援人員對談的記錄。</span><span class="sxs-lookup"><span data-stu-id="d43f9-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="d43f9-110">評估論壇、部落格和影片的註解。</span><span class="sxs-lookup"><span data-stu-id="d43f9-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="d43f9-111">許多其他即時、預測評分的案例。</span><span class="sxs-lookup"><span data-stu-id="d43f9-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="d43f9-112">在真實世界案例中，您會取得 hello 資料直接從 Twitter 資料流。</span><span class="sxs-lookup"><span data-stu-id="d43f9-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="d43f9-113">toosimplify hello 教學課程中，我們已寫入它，如此 hello 串流分析工作取得推文從 Azure Blob 儲存體中的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="d43f9-114">您可以建立您自己的 CSV 檔案，或 hello 下列影像所示，您可以使用範例 CSV 檔案：</span><span class="sxs-lookup"><span data-stu-id="d43f9-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![CSV 檔案的範例推文](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="d43f9-116">您所建立的 hello 串流分析工作套用 hello 情緒分析模型做為使用者定義函數 (UDF) 的 hello 範例文字資料的 hello blob 存放區。</span><span class="sxs-lookup"><span data-stu-id="d43f9-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="d43f9-117">hello 輸出 （hello 情緒分析中的 hello 結果） 都會寫入 toohello 不同的 CSV 檔案中的同一個 blob 存放區。</span><span class="sxs-lookup"><span data-stu-id="d43f9-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="d43f9-118">hello 下圖示範這項設定。</span><span class="sxs-lookup"><span data-stu-id="d43f9-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="d43f9-119">請注意，如需更真實的案例，可將 Blob 儲存體更換為 Azure 事件中樞輸入內的串流 Twitter 資料。</span><span class="sxs-lookup"><span data-stu-id="d43f9-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="d43f9-120">此外，您可以建置[Microsoft Power BI](https://powerbi.microsoft.com/)即時的視覺效果的 hello 彙總的人氣。</span><span class="sxs-lookup"><span data-stu-id="d43f9-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![串流分析機器學習服務整合概觀](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="d43f9-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="d43f9-122">Prerequisites</span></span>
<span data-ttu-id="d43f9-123">開始之前，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d43f9-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="d43f9-124">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43f9-124">An active Azure subscription.</span></span>
* <span data-ttu-id="d43f9-125">內附資料的 CSV 檔。</span><span class="sxs-lookup"><span data-stu-id="d43f9-125">A CSV file with some data in it.</span></span> <span data-ttu-id="d43f9-126">您可以下載從稍早所示的 hello 檔案[GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv)，或者您可以建立您自己的檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="d43f9-127">本文中，我們假設您使用從 GitHub hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="d43f9-128">在高層級，在本文中示範 toocomplete hello 工作您不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="d43f9-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="d43f9-129">建立 Azure 儲存體帳戶和 blob 儲存體容器，並上傳 CSV 格式的輸入的檔案 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="d43f9-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="d43f9-130">從 hello Cortana 智慧組件庫 tooyour Azure Machine Learning 工作區加入情緒分析模型並將部署此模型為 hello Machine Learning 工作區中的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="d43f9-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="d43f9-131">建立順序 toodetermine 人氣中的函式會呼叫此 web 服務的 hello 文字輸入資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="d43f9-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="d43f9-132">啟動 hello 資料流分析工作，並檢查 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="d43f9-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="d43f9-133">建立儲存體容器及上傳 hello CSV 輸入的檔</span><span class="sxs-lookup"><span data-stu-id="d43f9-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="d43f9-134">此步驟中，您可以使用任何 CSV 檔案，例如其中一個可從 GitHub hello。</span><span class="sxs-lookup"><span data-stu-id="d43f9-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="d43f9-135">在 hello Azure 入口網站，按一下 **新增** &gt; **儲存體** &gt; **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![建立新的儲存體帳戶](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="d43f9-137">提供的名稱 (`samldemo` hello 範例中)。</span><span class="sxs-lookup"><span data-stu-id="d43f9-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="d43f9-138">hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。</span><span class="sxs-lookup"><span data-stu-id="d43f9-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="d43f9-139">指定現有的資源群組，並指定位置。</span><span class="sxs-lookup"><span data-stu-id="d43f9-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="d43f9-140">我們建議您針對位置，建立在此教學課程使用的所有都 hello 資源都 hello 相同位置。</span><span class="sxs-lookup"><span data-stu-id="d43f9-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![提供儲存體帳戶詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="d43f9-142">在 hello Azure 入口網站，選取 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43f9-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="d43f9-143">在 hello 儲存體帳戶刀鋒視窗中，按一下 **容器**，然後按一下  **+&nbsp;容器**toocreate blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d43f9-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![建立 Blob 容器](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="d43f9-145">提供 hello 容器的名稱 (`azuresamldemoblob` hello 範例中)，並確認**存取類型**設定得**Blob**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="d43f9-146">完成後，按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-146">When you're done, click **OK**.</span></span>

    ![指定 Blob 容器詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="d43f9-148">在 hello**容器**刀鋒視窗中，選取 hello 新的容器，這會開啟該容器的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d43f9-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="d43f9-149">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="d43f9-149">Click **Upload**.</span></span>

    ![容器的 [上傳] 按鈕](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="d43f9-151">在 hello**上傳 blob**刀鋒視窗中，指定您想 toouse，本教學課程中的 hello CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="d43f9-152">如**Blob 類型**，選取**區塊 blob**和 set hello 區塊大小 too4 MB，足以讓本教學課程。</span><span class="sxs-lookup"><span data-stu-id="d43f9-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![上傳 Blob 檔案](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="d43f9-154">按一下 hello**上傳**在 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d43f9-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="d43f9-155">從 hello Cortana 智慧組件庫加入 hello 情緒分析模型</span><span class="sxs-lookup"><span data-stu-id="d43f9-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="d43f9-156">Hello 範例資料是 blob，您可以啟用 Cortana 智慧組件庫中的 hello 情緒分析模型。</span><span class="sxs-lookup"><span data-stu-id="d43f9-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="d43f9-157">移 toohello[預測情緒分析模型](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1)hello Cortana 智慧組件庫中的頁面。</span><span class="sxs-lookup"><span data-stu-id="d43f9-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="d43f9-158">按一下 [在 Studio 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-158">Click **Open in Studio**.</span></span>  
   
   ![串流分析機器學習服務, 開啟 Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="d43f9-160">登入 toogo toohello 工作區。</span><span class="sxs-lookup"><span data-stu-id="d43f9-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="d43f9-161">選取位置。</span><span class="sxs-lookup"><span data-stu-id="d43f9-161">Select a location.</span></span>

4. <span data-ttu-id="d43f9-162">按一下**執行**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="d43f9-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="d43f9-163">hello 程序會執行，其約一分鐘。</span><span class="sxs-lookup"><span data-stu-id="d43f9-163">hello process runs, which takes about a minute.</span></span>

   ![在 Machine Learning Studio 中執行實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="d43f9-165">Hello 程序已順利執行之後，請選取**部署 Web 服務**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="d43f9-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![在 Machine Learning Studio 中將實驗部署為 Web 服務](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="d43f9-167">hello 情緒分析模型是準備 toouse 的 toovalidate 按一下 hello**測試** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d43f9-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="d43f9-168">提供文字輸入，例如「我喜歡 Microsoft」。</span><span class="sxs-lookup"><span data-stu-id="d43f9-168">Provide text input such as "I love Microsoft".</span></span> 

   ![在 Machine Learning Studio 中測試實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="d43f9-170">如果 hello 測試正常運作，您會看到結果類似 toohello，下列範例：</span><span class="sxs-lookup"><span data-stu-id="d43f9-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![Machine Learning Studio 中的測試結果](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="d43f9-172">在 hello**應用程式**資料行中，按一下 hello **Excel 2010 或舊版的活頁簿**連結 toodownload Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="d43f9-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="d43f9-173">hello 活頁簿包含 hello API 金鑰和 hello URL，您需要稍後 tooset 向上 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="d43f9-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![串流分析機器學習服務, 快速概覽](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="d43f9-175">建立 hello 機器學習模型會使用資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="d43f9-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="d43f9-176">您現在可以建立從 blob 儲存體中的 hello CSV 檔案中讀取 hello 範例推文資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="d43f9-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="d43f9-177">建立 hello 作業</span><span class="sxs-lookup"><span data-stu-id="d43f9-177">Create hello job</span></span>

1. <span data-ttu-id="d43f9-178">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d43f9-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="d43f9-179">按一下 [新增] > [物聯網] > [串流分析工作]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Azure 入口網站的路徑，以取得 tooa 新的資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="d43f9-181">名稱 hello 工作`azure-sa-ml-demo`、 指定訂用帳戶、 指定現有的資源群組或建立一個新和選取 hello hello 作業的位置。</span><span class="sxs-lookup"><span data-stu-id="d43f9-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![指定新串流分析工作的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="d43f9-183">設定 hello 作業輸入</span><span class="sxs-lookup"><span data-stu-id="d43f9-183">Configure hello job input</span></span>
<span data-ttu-id="d43f9-184">hello 作業從您上傳先前 tooblob 儲存體的 hello CSV 檔案取得其輸入。</span><span class="sxs-lookup"><span data-stu-id="d43f9-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="d43f9-185">Hello 工作建立之後下, 之後**作業拓撲**在 hello 作業刀鋒視窗中，按一下 hello**輸入**方塊。</span><span class="sxs-lookup"><span data-stu-id="d43f9-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![在串流分析工作刀鋒視窗中的 [輸入] 方塊](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="d43f9-187">在 hello**輸入**刀鋒視窗中，按一下  **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![[新增] 按鈕，新增輸入的 toohello 資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="d43f9-189">填寫 hello**新輸入**刀鋒視窗包含下列值：</span><span class="sxs-lookup"><span data-stu-id="d43f9-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="d43f9-190">**輸入的別名**： 使用 hello 名稱`datainput`。</span><span class="sxs-lookup"><span data-stu-id="d43f9-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="d43f9-191">**來源類型**：選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="d43f9-192">**來源**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="d43f9-193">**匯入選項**：選取 [從目前的訂用帳戶使用 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="d43f9-194">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-194">**Storage account**.</span></span> <span data-ttu-id="d43f9-195">選取您稍早建立的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43f9-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="d43f9-196">**容器**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-196">**Container**.</span></span> <span data-ttu-id="d43f9-197">選取 hello 您稍早建立的容器 (`azuresamldemoblob`)。</span><span class="sxs-lookup"><span data-stu-id="d43f9-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="d43f9-198">**事件序列化格式**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-198">**Event serialization format**.</span></span> <span data-ttu-id="d43f9-199">選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-199">Select **CSV**.</span></span>

    ![新工作輸入的設定](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="d43f9-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d43f9-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="d43f9-202">設定 hello 作業輸出</span><span class="sxs-lookup"><span data-stu-id="d43f9-202">Configure hello job output</span></span>
<span data-ttu-id="d43f9-203">相同 blob 儲存體它取得在此對話方塊輸入 hello 作業傳送結果 toohello。</span><span class="sxs-lookup"><span data-stu-id="d43f9-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="d43f9-204">在下**作業拓撲**在 hello 作業刀鋒視窗中，按一下 hello**輸出**方塊。</span><span class="sxs-lookup"><span data-stu-id="d43f9-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![建立串流分析作業的新輸出](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="d43f9-206">在 hello**輸出**刀鋒視窗中，按一下**+ 加**，並將輸出結果與 hello 別名`datamloutput`。</span><span class="sxs-lookup"><span data-stu-id="d43f9-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="d43f9-207">對於 [接收器]，選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="d43f9-208">然後在 hello hello 其餘部分的填滿輸出使用的設定 hello 相同的值與您用於輸入 hello blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="d43f9-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="d43f9-209">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-209">**Storage account**.</span></span> <span data-ttu-id="d43f9-210">選取您稍早建立的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d43f9-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="d43f9-211">**容器**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-211">**Container**.</span></span> <span data-ttu-id="d43f9-212">選取 hello 您稍早建立的容器 (`azuresamldemoblob`)。</span><span class="sxs-lookup"><span data-stu-id="d43f9-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="d43f9-213">**事件序列化格式**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-213">**Event serialization format**.</span></span> <span data-ttu-id="d43f9-214">選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-214">Select **CSV**.</span></span>

   ![新工作輸出的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="d43f9-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d43f9-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="d43f9-217">新增 hello 機器學習服務函數</span><span class="sxs-lookup"><span data-stu-id="d43f9-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="d43f9-218">先前您發行的機器學習模型 tooa web 服務。</span><span class="sxs-lookup"><span data-stu-id="d43f9-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="d43f9-219">在我們的案例中，當執行 hello 資料流分析作業時，會傳送每個範例推文情緒分析 hello 輸入的 toohello web 服務。</span><span class="sxs-lookup"><span data-stu-id="d43f9-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="d43f9-220">hello 機器學習 web 服務傳回的人氣 (`positive`， `neutral`，或`negative`) 與 hello 推文中的正面的機率。</span><span class="sxs-lookup"><span data-stu-id="d43f9-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="d43f9-221">在本節中的 hello 教學課程，您可以定義 hello 資料流分析作業中的函式。</span><span class="sxs-lookup"><span data-stu-id="d43f9-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="d43f9-222">hello 函式可以是叫用的 toosend 推文 toohello web 服務，並回到 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d43f9-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="d43f9-223">請確定您擁有 hello web 服務 URL 和 API 金鑰您稍早在 hello Excel 活頁簿中下載。</span><span class="sxs-lookup"><span data-stu-id="d43f9-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="d43f9-224">傳回 toohello 作業概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d43f9-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="d43f9-225">在 設定 下，選取 函數，然後按一下+ 新增。</span><span class="sxs-lookup"><span data-stu-id="d43f9-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![新增函式 toohello 資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="d43f9-227">輸入`sentiment`為 hello 函式別名，並填寫 hello 其餘 hello 刀鋒視窗中使用這些值：</span><span class="sxs-lookup"><span data-stu-id="d43f9-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="d43f9-228">**函數類型**：選取 [Azure ML]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="d43f9-229">**匯入選項**：選取 [從不同的訂用帳戶匯入]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="d43f9-230">這可讓您有機會 tooenter hello URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="d43f9-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="d43f9-231">**URL**: hello web 服務 URL 中的貼。</span><span class="sxs-lookup"><span data-stu-id="d43f9-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="d43f9-232">**索引鍵**: hello API 機碼中的貼。</span><span class="sxs-lookup"><span data-stu-id="d43f9-232">**Key**: Paste in hello API key.</span></span>
  
    ![新增機器學習服務函數 toohello 資料流分析工作設定](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="d43f9-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d43f9-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="d43f9-235">建立查詢 tootransform hello 資料</span><span class="sxs-lookup"><span data-stu-id="d43f9-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="d43f9-236">資料流分析會使用宣告式、 以 SQL 為基礎的查詢 tooexamine hello 輸入，並加以處理。</span><span class="sxs-lookup"><span data-stu-id="d43f9-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="d43f9-237">在本節中，您可以建立從輸入讀取每個推文，然後再叫用 hello 機器學習服務函數 tooperform 情緒分析的查詢。</span><span class="sxs-lookup"><span data-stu-id="d43f9-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="d43f9-238">hello 查詢接著會傳送 hello 結果 toohello 輸出，您會定義 （blob 儲存）。</span><span class="sxs-lookup"><span data-stu-id="d43f9-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="d43f9-239">傳回 toohello 作業概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d43f9-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="d43f9-240">在下**作業拓撲**，按一下 hello**查詢**方塊。</span><span class="sxs-lookup"><span data-stu-id="d43f9-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="d43f9-242">輸入下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="d43f9-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="d43f9-243">hello 查詢叫用您稍早建立的 hello 函式 (`sentiment`) 順序 tooperform 情緒分析 」 在 hello 輸入中的每個推文中。</span><span class="sxs-lookup"><span data-stu-id="d43f9-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="d43f9-244">按一下**儲存**toosave hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="d43f9-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="d43f9-245">啟動 hello 資料流分析工作，並檢查 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="d43f9-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="d43f9-246">您現在可以啟動 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="d43f9-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="d43f9-247">啟動 hello 工作</span><span class="sxs-lookup"><span data-stu-id="d43f9-247">Start hello job</span></span>
1. <span data-ttu-id="d43f9-248">傳回 toohello 作業概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d43f9-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="d43f9-249">按一下**啟動**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="d43f9-249">Click **Start** at hello top of hello blade.</span></span>

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="d43f9-251">在 hello**開始工作**，選取**自訂**，然後選取一天前 toowhen 您上傳 CSV 檔案 tooblob 存放裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="d43f9-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="d43f9-252">完成後，按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="d43f9-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="d43f9-253">核取 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="d43f9-253">Check hello output</span></span>
1. <span data-ttu-id="d43f9-254">讓的 hello 工作執行直到您看到 hello 中的活動的幾分鐘**監視**方塊。</span><span class="sxs-lookup"><span data-stu-id="d43f9-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="d43f9-255">如果您通常使用 blob 儲存體 tooexamine hello 內容的工具，請使用該工具 tooexamine hello`azuresamldemoblob`容器。</span><span class="sxs-lookup"><span data-stu-id="d43f9-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="d43f9-256">或者，不要 hello hello Azure 入口網站中所述步驟：</span><span class="sxs-lookup"><span data-stu-id="d43f9-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="d43f9-257">在 hello 入口網站中，尋找 hello`samldemo`儲存體帳戶，而且 hello 帳戶內找出 hello`azuresamldemoblob`容器。</span><span class="sxs-lookup"><span data-stu-id="d43f9-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="d43f9-258">您看到 hello 容器中的兩個檔案： hello 檔案，其中包含 hello 範例推文和 hello 資料流分析工作所產生的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="d43f9-259">產生的 hello 檔案上按一下滑鼠右鍵，然後選取**下載**。</span><span class="sxs-lookup"><span data-stu-id="d43f9-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![從 Blob 儲存體下載 CSV 工作輸出](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="d43f9-261">開啟 hello 產生 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="d43f9-261">Open hello generated CSV file.</span></span> <span data-ttu-id="d43f9-262">您會看到類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d43f9-262">You see something like hello following example:</span></span>  
   
   ![串流分析機器學習服務, CSV 檢視](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="d43f9-264">檢視計量</span><span class="sxs-lookup"><span data-stu-id="d43f9-264">View metrics</span></span>
<span data-ttu-id="d43f9-265">您也能檢視與 Azure Machine Learning 函數相關的度量。</span><span class="sxs-lookup"><span data-stu-id="d43f9-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="d43f9-266">hello 下列函式相關的度量資訊會顯示在 hello**監視**方塊 hello 作業刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="d43f9-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="d43f9-267">**函式要求**指出傳送要求 tooa 機器學習 web 服務的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="d43f9-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="d43f9-268">**函式事件**指出 hello hello 要求中的事件數目。</span><span class="sxs-lookup"><span data-stu-id="d43f9-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="d43f9-269">根據預設，每個要求 tooa 機器學習 web 服務包含 too1，000 事件。</span><span class="sxs-lookup"><span data-stu-id="d43f9-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d43f9-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d43f9-270">Next steps</span></span>

* [<span data-ttu-id="d43f9-271">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="d43f9-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d43f9-272">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="d43f9-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d43f9-273">整合 REST API 與 Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d43f9-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="d43f9-274">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="d43f9-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



