---
title: "在 Azure Stream Analytics aaaPower BI 儀表板 |Microsoft 文件"
description: "使用即時串流 Power BI 儀表板 toogather 商業智慧和分析大量資料從資料流分析工作。"
keywords: "分析儀表板, 即時儀表板"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="bd8cd-104">串流分析及 Power BI：適用於串流資料的即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="bd8cd-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="bd8cd-105">Azure 串流分析可讓您的 hello 開頭商業智慧工具，其中一個 tootake 利用[Microsoft Power BI](https://powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="bd8cd-106">在本文中，您將了解如何使用 Power BI 作為 Azure 串流分析作業的輸出，以建立商業智慧工具。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="bd8cd-107">您也學到如何 toocreate 和使用即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="bd8cd-108">本文會繼續從資料流分析 hello[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="bd8cd-109">它建立在該教學課程中的 hello 工作流程為基礎，並新增輸出，讓您可以視覺化資料流分析工作所偵測到的詐騙撥打電話的 Power BI。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="bd8cd-110">您可以觀看此情節的[影片](https://www.youtube.com/watch?v=SGUpT-a99MA)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bd8cd-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="bd8cd-111">Prerequisites</span></span>

<span data-ttu-id="bd8cd-112">開始之前，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="bd8cd-113">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-113">An Azure account.</span></span>
* <span data-ttu-id="bd8cd-114">Power BI 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-114">An account for Power BI.</span></span> <span data-ttu-id="bd8cd-115">您可以使用公司帳戶或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="bd8cd-116">完整的版的 hello[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="bd8cd-117">hello 教學課程包含產生虛構的電話的中繼資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="bd8cd-118">在 hello 教學課程中，您可以建立事件中樞，並傳送 hello 串流通話資料 toohello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="bd8cd-119">您撰寫查詢可偵測詐騙的呼叫 （來自相同數字在 hello hello 呼叫相同的時間在不同的位置）。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="bd8cd-120">新增 Power BI 輸出</span><span class="sxs-lookup"><span data-stu-id="bd8cd-120">Add Power BI output</span></span>
<span data-ttu-id="bd8cd-121">Hello 即時詐騙偵測教學課程中，在 hello 輸出會傳送 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="bd8cd-122">在本節中，您可以將傳送資訊 tooPower BI 輸出。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="bd8cd-123">在 hello Azure 入口網站，開啟您稍早建立的 hello 串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="bd8cd-124">如果您使用 hello 建議的名稱，hello 作業會命名為`sa_frauddetection_job_demo`。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="bd8cd-125">選取 hello**輸出**hello 中間 hello 作業儀表板的方塊，然後選取  **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="bd8cd-126">在 [輸出別名] 中，輸入 `CallStream-PowerBI`。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="bd8cd-127">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-127">You can use a different name.</span></span> <span data-ttu-id="bd8cd-128">如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="bd8cd-129">在 [接收] 下，選取 [Power BI]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-129">Under **Sink**, select **Power BI**.</span></span>

   ![建立 Power BI 的輸出](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="bd8cd-131">按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-131">Click **Authorize**.</span></span>

    <span data-ttu-id="bd8cd-132">隨即會開啟視窗，讓您提供公司或學校帳戶的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![輸入存取 tooPower BI 認證](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="bd8cd-134">輸入認證。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-134">Enter your credentials.</span></span> <span data-ttu-id="bd8cd-135">請注意，則當您輸入認證時，您正在也賦予的權限 toohello 串流分析工作 tooaccess 您 Power BI 的區域。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="bd8cd-136">當您正在傳回 toohello**新輸出**刀鋒視窗中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8cd-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="bd8cd-137">**群組工作區**： 選取您想要 toocreate hello 資料集的 Power BI 租用戶中的工作區。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="bd8cd-138">**資料集名稱**：輸入 `sa-dataset`。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="bd8cd-139">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-139">You can use a different name.</span></span> <span data-ttu-id="bd8cd-140">如果這樣做，請記下來供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="bd8cd-141">**資料表名稱**：輸入 `fraudulent-calls`。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="bd8cd-142">目前，串流分析作業的 Power BI 輸出在資料集內只能有一個資料表。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI 工作區](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="bd8cd-144">如果有 Power BI 資料集，而且資料表中具有 hello hello 相同的名稱是您在 hello 資料流分析作業中指定，會覆寫現有的 hello。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="bd8cd-145">我們不建議您在 Power BI 帳戶中明確建立此資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="bd8cd-146">當您啟動串流分析工作，且 hello 工作開始提取的輸出放入 Power BI 會自動建立。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="bd8cd-147">如果您工作的查詢沒有傳回任何結果，hello 資料集和資料表就不會建立。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="bd8cd-148">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-148">Click **Create**.</span></span>

<span data-ttu-id="bd8cd-149">使用下列設定的 hello 建立 hello 資料集：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="bd8cd-150">**defaultRetentionPolicy: BasicFIFO**：資料是 FIFO，最大資料列數 20 萬。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="bd8cd-151">**defaultMode: pushStreaming**: hello 資料集可支援資料流的圖格和傳統的報表視覺效果 （也稱為</span><span class="sxs-lookup"><span data-stu-id="bd8cd-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="bd8cd-152">(又稱為發送)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-152">push).</span></span>

<span data-ttu-id="bd8cd-153">您目前無法建立具有其他旗標的資料集。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="bd8cd-154">如需有關 Power BI 資料集的詳細資訊，請參閱 hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx)參考。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="bd8cd-155">撰寫 hello 查詢</span><span class="sxs-lookup"><span data-stu-id="bd8cd-155">Write hello query</span></span>

1. <span data-ttu-id="bd8cd-156">關閉 hello**輸出**刀鋒視窗，然後傳回 toohello 作業刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="bd8cd-157">按一下 hello**查詢**方塊。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="bd8cd-158">輸入下列查詢的 hello。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-158">Enter hello following query.</span></span> <span data-ttu-id="bd8cd-159">此查詢是類似 toohello 自我聯結的查詢在 hello 詐騙偵測教學課程中建立。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="bd8cd-160">hello 差異在於，此查詢會傳送新的結果 toohello 輸出您所建立 (`CallStream-PowerBI`)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="bd8cd-161">如果您未命名 hello 輸入`CallStream`在 hello 詐騙偵測教學課程中，以取代您的名稱`CallStream`在 hello **FROM**和**聯結**hello 查詢中的子句。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="bd8cd-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="bd8cd-163">測試 hello 查詢</span><span class="sxs-lookup"><span data-stu-id="bd8cd-163">Test hello query</span></span>
<span data-ttu-id="bd8cd-164">此為選擇性區段，但建議執行。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="bd8cd-165">如果目前沒有執行 hello TelcoStreaming 應用程式，則會開始依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="bd8cd-166">開啟命令視窗。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-166">Open a command window.</span></span>
    * <span data-ttu-id="bd8cd-167">移 toohello hello telcogenerator.exe 和修改的 telcodatagen.exe.config 檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="bd8cd-168">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8cd-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="bd8cd-169">在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`CallStream`輸入，然後選取 **範例從輸入資料**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="bd8cd-170">指定您想要取得三分鐘的資料，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="bd8cd-171">請等到您收到 hello 資料取樣。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="bd8cd-172">按一下 [測試]，並確定開始產生結果。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="bd8cd-173">執行 hello 工作</span><span class="sxs-lookup"><span data-stu-id="bd8cd-173">Run hello job</span></span>

1. <span data-ttu-id="bd8cd-174">請確定該 hello TelcoStreaming 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="bd8cd-175">關閉 hello**查詢**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="bd8cd-176">在 hello 作業刀鋒視窗中，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-176">In hello job blade, click **Start**.</span></span>

    ![啟動 hello 資料流分析工作](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="bd8cd-178">串流分析工作會開始尋找 hello 內送資料流中的詐騙呼叫。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="bd8cd-179">hello 作業也會建立 hello 資料集和資料表在 Power BI 中，並啟動傳送 hello 詐騙呼叫 toothem 相關資料。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="bd8cd-180">在 Power BI 中建立 hello 儀表板</span><span class="sxs-lookup"><span data-stu-id="bd8cd-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="bd8cd-181">跳過[Powerbi.com](https://powerbi.com)並以您的工作或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="bd8cd-182">如果 hello 資料流分析工作查詢結果的輸出，您會看到已建立的資料集：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Power BI 中的串流資料集](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="bd8cd-184">在工作區中，按一下 [+&nbsp;建立]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![在 Power BI 工作區中的 hello 建立按鈕](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="bd8cd-186">建立新的儀表板並命名為 `Fraudulent Calls`。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![在 Power BI 工作區中建立並命名儀表板](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="bd8cd-188">在 hello hello 視窗頂端，按一下 **新增磚**，選取**自訂串流資料**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![自訂串流資料集](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="bd8cd-190">在 [您的資料集] 底下，選取資料集，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![您的串流資料集](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="bd8cd-192">在下**視覺效果類型**，選取**卡**，然後在 hello**欄位**清單中，選取**fraudulentcalls**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![新磚的視覺效果詳細資料](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="bd8cd-194">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-194">Click **Next**.</span></span>

8. <span data-ttu-id="bd8cd-195">填寫磚詳細資料，例如標題和副標題。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-195">Fill in tile details like a title and subtitle.</span></span>

    ![新磚的標題和副標題](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="bd8cd-197">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-197">Click **Apply**.</span></span>

    <span data-ttu-id="bd8cd-198">您現在有一個詐騙計數器了！</span><span class="sxs-lookup"><span data-stu-id="bd8cd-198">Now you have a fraud counter!</span></span>

    ![詐騙計數器](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="bd8cd-200">後續 hello 步驟再次 tooadd 磚 （以步驟 4 開始）。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="bd8cd-201">這次不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-201">This time, do hello following:</span></span>

    * <span data-ttu-id="bd8cd-202">當您收到太**視覺效果類型**，選取**折線圖**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="bd8cd-203">新增軸並選取 [windowend]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="bd8cd-204">新增值並選取 [fraudulentcalls]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="bd8cd-205">如**時間視窗 toodisplay**，選取 hello 過去 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![建立折線圖的磚](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="bd8cd-207">按 [下一步]，新增標題和副標題，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="bd8cd-208">hello Power BI 儀表板現在可以讓您有關詐騙呼叫兩個資料檢視偵測到在 hello 串流資料。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![完成的 Power BI 儀表板，以兩個磚來顯示詐騙電話](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="bd8cd-210">深入了解 Power BI</span><span class="sxs-lookup"><span data-stu-id="bd8cd-210">Learn more about Power BI</span></span>

<span data-ttu-id="bd8cd-211">本教學課程示範如何 toocreate 只有幾種不同的資料集的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="bd8cd-212">Power BI 可協助您為組織建立其他客戶商業智慧型工具。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="bd8cd-213">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8cd-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="bd8cd-214">在 Power BI 儀表板的另一個範例，監看的 hello[開始使用 Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s)視訊。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="bd8cd-215">如需有關設定資料流分析工作輸出 tooPower BI，並使用 Power BI 群組，請檢閱 hello [Power BI](stream-analytics-define-outputs.md#power-bi)區段 hello[輸出資料流分析](stream-analytics-define-outputs.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="bd8cd-216">如需 Power BI 一般用法的相關資訊，請參閱 [Power BI 中的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="bd8cd-217">了解限制和最佳作法</span><span class="sxs-lookup"><span data-stu-id="bd8cd-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="bd8cd-218">目前來說，系統大約每秒可呼叫 Power BI 一次。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="bd8cd-219">串流視覺效果支援 15 KB 的封包。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="bd8cd-220">此外，資料流的視覺效果失敗 （但發送繼續 toowork）。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="bd8cd-221">由於這些限制，Power BI 本身最自然 toocases Azure Stream Analytics 並大幅減少資料載入的位置。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="bd8cd-222">我們建議使用輪轉視窗或 Hopping 視窗 tooensure 資料推入已最多每秒一個推入，而且查詢落在 hello 輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="bd8cd-223">您可以使用下列方程式 toocompute hello 值 toogive hello 您的視窗，以秒為單位：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="bd8cd-225">例如：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-225">For example:</span></span>

* <span data-ttu-id="bd8cd-226">您有 1 千個以一秒間隔傳送資料的裝置。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="bd8cd-227">您正在使用 hello Power BI Pro SKU 支援每小時 1,000,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="bd8cd-228">您想 toopublish hello 數量平均每個裝置 tooPower BI 的資料。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="bd8cd-229">如此一來，hello 方程式會變成：</span><span class="sxs-lookup"><span data-stu-id="bd8cd-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="bd8cd-231">指定這個設定，您可以變更原始查詢 toohello 下列 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8cd-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="bd8cd-232">更新授權</span><span class="sxs-lookup"><span data-stu-id="bd8cd-232">Renew authorization</span></span>
<span data-ttu-id="bd8cd-233">如果 hello 密碼已變更您的工作已建立或上次經過驗證之後，您需要 tooreauthenticate Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="bd8cd-234">如果您的 Azure Active Directory (Azure AD) 租用戶上設定了 Azure Multi-factor Authentication，您也需要 toorenew 每隔兩週的 Power BI 授權。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="bd8cd-235">如果您未更新，您可以查看徵兆，例如工作輸出缺少或`Authenticate user error`hello 作業記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="bd8cd-236">同樣地，如果 hello 語彙基元過期之後，就會啟動一個工作，就會發生錯誤，並 hello 作業失敗時。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="bd8cd-237">tooresolve 這個問題，請停止正在執行的 hello 工作，並移的 tooyour Power BI 輸出。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="bd8cd-238">tooavoid 資料遺失，選取 hello**更新授權**連結，然後再重新啟動您的工作，從 hello**上次停止時間**。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="bd8cd-239">已使用 Power BI 重新整理 hello 授權之後，綠色的警示會出現在 hello 授權區域 tooreflect hello 問題已解決。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="bd8cd-240">取得說明</span><span class="sxs-lookup"><span data-stu-id="bd8cd-240">Get help</span></span>
<span data-ttu-id="bd8cd-241">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="bd8cd-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd8cd-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd8cd-242">Next steps</span></span>
* [<span data-ttu-id="bd8cd-243">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="bd8cd-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bd8cd-244">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bd8cd-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bd8cd-245">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="bd8cd-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bd8cd-246">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="bd8cd-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bd8cd-247">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="bd8cd-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
