---
title: "資料湖存放區的資料流分析 aaaStream 資料 |Microsoft 文件"
description: "使用 Azure Stream Analytics toostream 資料至 Azure 資料湖存放區"
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
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="bfbd1-103">使用 Azure 串流分析將來自 Azure 儲存體 Blob 的資料串流處理至 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bfbd1-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="bfbd1-104">在本文中，您將學習如何 toouse Azure 資料湖存放區做為 Azure 資料流分析工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="bfbd1-105">本文將示範一個簡單的案例，可從 Azure 儲存體 blob （輸入） 讀取資料並寫入 hello data tooData Lake Store （輸出）。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="bfbd1-106">在這個階段中，建立及設定 Data Lake Store 的輸出資料流分析支援只能在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="bfbd1-107">因此，本教學課程中的某些部分會使用 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="bfbd1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="bfbd1-108">Prerequisites</span></span>
<span data-ttu-id="bfbd1-109">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="bfbd1-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="bfbd1-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-110">**An Azure subscription**.</span></span> <span data-ttu-id="bfbd1-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="bfbd1-112">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-112">**Azure Storage account**.</span></span> <span data-ttu-id="bfbd1-113">您將使用此帳戶 tooinput 資料從 blob 容器的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="bfbd1-114">此教學課程中，假設您有儲存體帳戶呼叫**storageforasa** hello 帳戶內的容器呼叫**storageforasacontainer**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="bfbd1-115">當您建立 hello 容器之後時上, 傳範例資料檔案 tooit。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="bfbd1-116">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="bfbd1-117">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="bfbd1-118">假設您有名為 **asadatalakestore** 的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="bfbd1-119">建立串流分析作業</span><span class="sxs-lookup"><span data-stu-id="bfbd1-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="bfbd1-120">您可以從建立包含輸入來源和輸出目的地的串流分析作業開始。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="bfbd1-121">本教學課程，hello 來源是 Azure blob 容器而且 hello 目的地資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="bfbd1-122">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bfbd1-123">從 hello 左窗格中，按一下 **串流分析工作**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="bfbd1-124">![建立串流分析作業](./media/data-lake-store-stream-analytics/create.job.png "建立串流分析作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="bfbd1-125">請確定您建立可在 hello 作業與 hello 儲存體帳戶，或相同的區域將會產生不同的區域之間移動資料的額外成本。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="bfbd1-126">建立 Blob 輸入 hello 工作</span><span class="sxs-lookup"><span data-stu-id="bfbd1-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="bfbd1-127">開啟 hello 頁面 hello 資料流分析工作，從 hello 左窗格按一下 hello**輸入**索引標籤，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="bfbd1-128">![加入輸入的 tooyour 作業](./media/data-lake-store-stream-analytics/create.input.1.png "加入輸入的 tooyour 作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="bfbd1-129">在 hello**新輸入**刀鋒視窗中，提供下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="bfbd1-130">![加入輸入的 tooyour 作業](./media/data-lake-store-stream-analytics/create.input.2.png "加入輸入的 tooyour 作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="bfbd1-131">如**輸入別名**，輸入 hello 工作輸入唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="bfbd1-132">在 [來源類型] 中，選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="bfbd1-133">在 [來源] 中，選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="bfbd1-134">在 [訂用帳戶] 中，選取 [使用來自目前訂用帳戶的 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="bfbd1-135">如**儲存體帳戶**，選取您所建立的 hello 儲存體帳戶 hello 必要條件的一部分。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="bfbd1-136">如**容器**，選取您在 hello hello 容器選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="bfbd1-137">在 [事件序列化格式] 中，選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="bfbd1-138">在 [分隔符號] 中，選取 [定位鍵]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="bfbd1-139">在 [編碼] 中，選取 [UTF-8]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="bfbd1-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-140">Click **Create**.</span></span> <span data-ttu-id="bfbd1-141">hello 入口網站現在將 hello 輸入並測試 hello 連接 tooit。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="bfbd1-142">建立 Data Lake Store hello 作業輸出</span><span class="sxs-lookup"><span data-stu-id="bfbd1-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="bfbd1-143">開啟 hello 資料流分析工作的 hello 頁面中，按一下 hello**輸出**索引標籤，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="bfbd1-144">![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.1.png "加入輸出 tooyour 作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="bfbd1-145">在 hello**新輸出**刀鋒視窗中，提供下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="bfbd1-146">![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.2.png "加入輸出 tooyour 作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="bfbd1-147">如**輸出別名**，輸入 hello 作業輸出的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="bfbd1-148">這是用於查詢 toodirect hello 查詢輸出 toothis Data Lake Store 的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="bfbd1-149">在 [接收] 中，選取 [Data Lake Store]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="bfbd1-150">您將會提示的 tooauthorize 存取 tooData Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="bfbd1-151">按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="bfbd1-152">在 hello**新輸出**刀鋒視窗中，繼續 tooprovide hello 下列值。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="bfbd1-153">![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.3.png "加入輸出 tooyour 作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="bfbd1-154">如**帳戶名稱**，選取您已建立您想要傳送至 hello 作業輸出 toobe hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="bfbd1-155">如**路徑前置詞模式**，輸入檔案路徑使用 toowrite 內 hello 檔案指定 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="bfbd1-156">如**日期格式**，如果您使用的日期語彙基元 hello 前置詞路徑中，您可以選取組織檔案的 hello 日期格式。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="bfbd1-157">如**時間格式**，如果您使用時間語彙基元 hello 前置詞的路徑中，指定組織檔案的 hello 時間格式。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="bfbd1-158">在 [事件序列化格式] 中，選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="bfbd1-159">在 [分隔符號] 中，選取 [定位鍵]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="bfbd1-160">在 [編碼] 中，選取 [UTF-8]。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="bfbd1-161">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-161">Click **Create**.</span></span> <span data-ttu-id="bfbd1-162">hello 入口網站現在將 hello 輸出，並測試 hello 連接 tooit。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="bfbd1-163">執行 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="bfbd1-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="bfbd1-164">toorun 資料流分析工作，您必須執行的查詢從 hello**查詢** 索引標籤。此教學課程中，您可以執行 hello 範例查詢來取代以 hello hello 預留位置工作輸入和輸出別名，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="bfbd1-165">![執行查詢](./media/data-lake-store-stream-analytics/run.query.png "執行查詢")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="bfbd1-166">按一下**儲存**從 hello 囉 」 畫面頂端，然後從 hello**概觀**索引標籤上，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="bfbd1-167">從 hello 對話方塊中，選取 **自訂時間**，然後設定 hello 目前日期和時間。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="bfbd1-168">![設定作業時間](./media/data-lake-store-stream-analytics/run.query.2.png "設定作業時間")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="bfbd1-169">按一下**啟動**toostart hello 作業。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="bfbd1-170">它可能會佔用 tooa 幾分鐘的時間 toostart hello 作業。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="bfbd1-171">tootrigger hello toopick hello 的工作資料 hello blob 複製的範例資料檔案 toohello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="bfbd1-172">您可以取得範例資料檔從 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="bfbd1-173">本教學課程，讓我們複製 hello 檔案**vehicle1_09142014.csv**。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="bfbd1-174">您可以使用各種用戶端，例如[Azure 儲存體總管](http://storageexplorer.com/)，tooupload 資料 tooa blob 容器。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="bfbd1-175">從 hello**概觀**索引標籤，下方**監視**，請參閱 hello 資料處理的方式。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="bfbd1-176">![監視作業](./media/data-lake-store-stream-analytics/run.query.3.png "監視作業")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="bfbd1-177">最後，您可以確認 hello 工作輸出資料均可在 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="bfbd1-178">![確認輸出](./media/data-lake-store-stream-analytics/run.query.4.png "確認輸出")</span><span class="sxs-lookup"><span data-stu-id="bfbd1-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="bfbd1-179">Hello 資料總管 窗格，請注意該 hello 輸出會寫入的 tooa 資料夾路徑，做為指定在 hello Data Lake Store 輸出設定 (`streamanalytics/job/output/{date}/{time}`)。</span><span class="sxs-lookup"><span data-stu-id="bfbd1-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="bfbd1-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bfbd1-180">See also</span></span>
* [<span data-ttu-id="bfbd1-181">建立 Data Lake Store 的 HDInsight 叢集 toouse</span><span class="sxs-lookup"><span data-stu-id="bfbd1-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
