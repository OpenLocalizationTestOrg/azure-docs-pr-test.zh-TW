---
title: "將來自串流分析的資料串流處理至 Data Lake Store | Microsoft Docs"
description: "使用 Azure 串流分析將資料串流處理至 Azure Data Lake Store"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="a3235-103">使用 Azure 串流分析將來自 Azure 儲存體 Blob 的資料串流處理至 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a3235-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="a3235-104">在這篇文章中，您將了解如何使用 Azure Data Lake Store 做為 Azure 串流分析作業的輸出。</span><span class="sxs-lookup"><span data-stu-id="a3235-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="a3235-105">這篇文章示範從 Azure 儲存體 Blob (輸入) 讀取資料以及將資料寫入至 Data Lake Store (輸出) 的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="a3235-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="a3235-106">目前只有在 [Azure 傳統入口網站](https://manage.windowsazure.com)支援建立及設定串流分析的 Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="a3235-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a3235-107">因此，此教學課程的部份內容會使用 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="a3235-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a3235-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a3235-108">Prerequisites</span></span>
<span data-ttu-id="a3235-109">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="a3235-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="a3235-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a3235-110">**An Azure subscription**.</span></span> <span data-ttu-id="a3235-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a3235-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a3235-112">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a3235-112">**Azure Storage account**.</span></span> <span data-ttu-id="a3235-113">您將使用來自此帳戶的 Blob 容器來輸入串流分析作業的資料。</span><span class="sxs-lookup"><span data-stu-id="a3235-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="a3235-114">本教學課程中，假設您有名為 **storageforasa** 的儲存體帳戶，並在該帳戶中建立名為 **storageforasacontainer** 的容器。</span><span class="sxs-lookup"><span data-stu-id="a3235-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="a3235-115">一旦您已建立容器，請將範例資料檔案上傳給容器。</span><span class="sxs-lookup"><span data-stu-id="a3235-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="a3235-116">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a3235-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="a3235-117">遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="a3235-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="a3235-118">假設您有名為 **asadatalakestore** 的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3235-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="a3235-119">建立串流分析作業</span><span class="sxs-lookup"><span data-stu-id="a3235-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="a3235-120">您可以從建立包含輸入來源和輸出目的地的串流分析作業開始。</span><span class="sxs-lookup"><span data-stu-id="a3235-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="a3235-121">本教學課程中，來源是 Azure Blob 容器，而目的地則是 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="a3235-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="a3235-122">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a3235-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a3235-123">從左窗格中，按一下 [串流分析作業]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a3235-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="a3235-124">![建立串流分析作業](./media/data-lake-store-stream-analytics/create.job.png "建立串流分析作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="a3235-125">請確定您所建立的作業位於和儲存體帳戶相同的區域，否則在區域之間移動資料，您會需要支付額外費用。</span><span class="sxs-lookup"><span data-stu-id="a3235-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="a3235-126">建立作業的 Blob 輸入</span><span class="sxs-lookup"><span data-stu-id="a3235-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="a3235-127">開啟「串流分析作業」頁面，在左窗格中按一下 [輸入] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a3235-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="a3235-128">![將輸入新增至您的作業](./media/data-lake-store-stream-analytics/create.input.1.png "將輸入新增至您的作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="a3235-129">在 [新增輸入] 刀鋒視窗中，提供下列值。</span><span class="sxs-lookup"><span data-stu-id="a3235-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="a3235-130">![將輸入新增至您的作業](./media/data-lake-store-stream-analytics/create.input.2.png "將輸入新增至您的作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="a3235-131">在 [輸入別名] 中輸入作業輸入的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="a3235-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="a3235-132">在 [來源類型] 中，選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="a3235-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="a3235-133">在 [來源] 中，選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="a3235-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="a3235-134">在 [訂用帳戶] 中，選取 [使用來自目前訂用帳戶的 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="a3235-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="a3235-135">在 [儲存體帳戶] 中，選取您在必要條件中所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3235-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="a3235-136">在 [容器] 中，選取您在選取的儲存體帳戶中建立的容器。</span><span class="sxs-lookup"><span data-stu-id="a3235-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="a3235-137">在 [事件序列化格式] 中，選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="a3235-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="a3235-138">在 [分隔符號] 中，選取 [定位鍵]。</span><span class="sxs-lookup"><span data-stu-id="a3235-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="a3235-139">在 [編碼] 中，選取 [UTF-8]。</span><span class="sxs-lookup"><span data-stu-id="a3235-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="a3235-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a3235-140">Click **Create**.</span></span> <span data-ttu-id="a3235-141">入口網站現在會新增輸入並測試其連線。</span><span class="sxs-lookup"><span data-stu-id="a3235-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="a3235-142">建立作業的 Data Lake Store 輸出</span><span class="sxs-lookup"><span data-stu-id="a3235-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="a3235-143">開啟「串流分析作業」頁面，按一下 [輸出] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a3235-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="a3235-144">![將輸出新增至您的作業](./media/data-lake-store-stream-analytics/create.output.1.png "將輸出新增至您的作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="a3235-145">在 [新增輸出] 刀鋒視窗中，提供下列值。</span><span class="sxs-lookup"><span data-stu-id="a3235-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="a3235-146">![將輸出新增至您的作業](./media/data-lake-store-stream-analytics/create.output.2.png "將輸出新增至您的作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="a3235-147">在 [輸出別名] 中輸入作業輸出的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="a3235-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="a3235-148">此為易記名稱，用於在查詢中將查詢輸出指向這個 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="a3235-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="a3235-149">在 [接收] 中，選取 [Data Lake Store]。</span><span class="sxs-lookup"><span data-stu-id="a3235-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="a3235-150">系統會提示您授權 Data Lake Store 帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="a3235-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="a3235-151">按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="a3235-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="a3235-152">在 [新增輸出] 刀鋒視窗中，繼續來提供下列值。</span><span class="sxs-lookup"><span data-stu-id="a3235-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="a3235-153">![將輸出新增至您的作業](./media/data-lake-store-stream-analytics/create.output.3.png "將輸出新增至您的作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="a3235-154">在 [帳戶名稱] 中，選取您已建立並且要在其中傳入作業輸出的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3235-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="a3235-155">在 [路徑前置詞模式] 中，輸入用來在指定的 Data Lake Store 帳戶中寫入檔案的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="a3235-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="a3235-156">在 [日期格式] 中，如果您在前置詞路徑中使用日期權杖，您可以選取組織檔案要用的日期格式。</span><span class="sxs-lookup"><span data-stu-id="a3235-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="a3235-157">在 [時間格式] 中，如果您在前置詞路徑中使用時間權杖，請指定組織檔案時要使用的時間格式。</span><span class="sxs-lookup"><span data-stu-id="a3235-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="a3235-158">在 [事件序列化格式] 中，選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="a3235-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="a3235-159">在 [分隔符號] 中，選取 [定位鍵]。</span><span class="sxs-lookup"><span data-stu-id="a3235-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="a3235-160">在 [編碼] 中，選取 [UTF-8]。</span><span class="sxs-lookup"><span data-stu-id="a3235-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="a3235-161">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="a3235-161">Click **Create**.</span></span> <span data-ttu-id="a3235-162">入口網站現在會新增輸出並測試其連線。</span><span class="sxs-lookup"><span data-stu-id="a3235-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="a3235-163">執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="a3235-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="a3235-164">若要執行串流分析作業，您必須從 [查詢] 索引標籤來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="a3235-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="a3235-165">本教學課程中，您可以藉由以作業輸入和輸出別名取代預留位置的方式執行範例查詢，如下方螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="a3235-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="a3235-166">![執行查詢](./media/data-lake-store-stream-analytics/run.query.png "執行查詢")</span><span class="sxs-lookup"><span data-stu-id="a3235-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="a3235-167">在畫面頂端按一下 [儲存]，然後在 [概觀] 索引標籤上按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="a3235-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="a3235-168">在對話方塊中，選取 [自訂時間]，然後設定目前的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="a3235-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="a3235-169">![設定作業時間](./media/data-lake-store-stream-analytics/run.query.2.png "設定作業時間")</span><span class="sxs-lookup"><span data-stu-id="a3235-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="a3235-170">按一下 [啟動] 以啟動作業。</span><span class="sxs-lookup"><span data-stu-id="a3235-170">Click **Start** to start the job.</span></span> <span data-ttu-id="a3235-171">啟動作業會需要費時幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="a3235-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="a3235-172">若要觸發作業以從 Blob 挑選資料，請將範例資料檔案複製到 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="a3235-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="a3235-173">您可以從 [Azure Data Lake Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)取得範例資料檔案。</span><span class="sxs-lookup"><span data-stu-id="a3235-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="a3235-174">在本教學課程中，我們要複製檔案 **vehicle1_09142014.csv**。</span><span class="sxs-lookup"><span data-stu-id="a3235-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="a3235-175">您可以使用各種用戶端，例如： [Azure 儲存體總管](http://storageexplorer.com/)，將資料上傳至 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="a3235-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="a3235-176">在 [概觀] 索引標籤的 [監視] 底下，查看資料的處理情形。</span><span class="sxs-lookup"><span data-stu-id="a3235-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="a3235-177">![監視作業](./media/data-lake-store-stream-analytics/run.query.3.png "監視作業")</span><span class="sxs-lookup"><span data-stu-id="a3235-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="a3235-178">最後，您可以確認作業輸出資料已可在 Data Lake Store 帳戶中使用。</span><span class="sxs-lookup"><span data-stu-id="a3235-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="a3235-179">![確認輸出](./media/data-lake-store-stream-analytics/run.query.4.png "確認輸出")</span><span class="sxs-lookup"><span data-stu-id="a3235-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="a3235-180">請注意，在 [資料總管] 窗格中，輸出會寫入至 Data Lake Store 輸出設定中所指定的資料夾路徑 (`streamanalytics/job/output/{date}/{time}`)。</span><span class="sxs-lookup"><span data-stu-id="a3235-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="a3235-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a3235-181">See also</span></span>
* [<span data-ttu-id="a3235-182">建立 HDInsight 叢集以使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a3235-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
