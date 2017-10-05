---
title: "Azure 串流分析上的 Power BI 儀表板 | Microsoft Docs"
description: "使用即時串流 Power BI 儀表板來收集商業智慧及分析來自串流分析工作的大量資料。"
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
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="01456-104">串流分析及 Power BI：適用於串流資料的即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="01456-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="01456-105">Azure 串流分析可讓您使用其中一個頂尖的商業智慧工具：[Microsoft Power BI](https://powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="01456-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="01456-106">在本文中，您將了解如何使用 Power BI 作為 Azure 串流分析作業的輸出，以建立商業智慧工具。</span><span class="sxs-lookup"><span data-stu-id="01456-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="01456-107">您也將了解如何建立和使用即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="01456-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="01456-108">本文是延續串流分析[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="01456-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="01456-109">本文以該教學課程所建立的工作流程為基礎，並新增 Power BI 輸出，讓您視覺化串流分析作業所偵測到的詐騙電話。</span><span class="sxs-lookup"><span data-stu-id="01456-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="01456-110">您可以觀看此情節的[影片](https://www.youtube.com/watch?v=SGUpT-a99MA)。</span><span class="sxs-lookup"><span data-stu-id="01456-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="01456-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="01456-111">Prerequisites</span></span>

<span data-ttu-id="01456-112">開始之前，請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="01456-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="01456-113">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="01456-113">An Azure account.</span></span>
* <span data-ttu-id="01456-114">Power BI 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="01456-114">An account for Power BI.</span></span> <span data-ttu-id="01456-115">您可以使用公司帳戶或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="01456-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="01456-116">[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程的完整版本。</span><span class="sxs-lookup"><span data-stu-id="01456-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="01456-117">本教學課程包含可產生虛構電話中繼資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01456-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="01456-118">在本教學課程中，您將會建立事件中樞，並將串流通話資料傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="01456-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="01456-119">您將會撰寫查詢來偵測詐騙電話 (相同號碼在同一時間從不同位置的來電)。</span><span class="sxs-lookup"><span data-stu-id="01456-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="01456-120">新增 Power BI 輸出</span><span class="sxs-lookup"><span data-stu-id="01456-120">Add Power BI output</span></span>
<span data-ttu-id="01456-121">在即時詐騙偵測教學課程中，輸出會傳送至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="01456-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="01456-122">在本節中，您會新增輸出將資訊傳送至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="01456-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="01456-123">在 Azure 入口網站中，開啟您稍早建立的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="01456-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="01456-124">如果您使用建議的名稱，則作業的名稱為 `sa_frauddetection_job_demo`。</span><span class="sxs-lookup"><span data-stu-id="01456-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="01456-125">選取作業儀表板中央的 [輸出] 方塊，然後選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="01456-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="01456-126">在 [輸出別名] 中，輸入 `CallStream-PowerBI`。</span><span class="sxs-lookup"><span data-stu-id="01456-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="01456-127">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="01456-127">You can use a different name.</span></span> <span data-ttu-id="01456-128">如果這樣做，請記下來，因為稍後需要用到此名稱。</span><span class="sxs-lookup"><span data-stu-id="01456-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="01456-129">在 [接收] 下，選取 [Power BI]。</span><span class="sxs-lookup"><span data-stu-id="01456-129">Under **Sink**, select **Power BI**.</span></span>

   ![建立 Power BI 的輸出](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="01456-131">按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="01456-131">Click **Authorize**.</span></span>

    <span data-ttu-id="01456-132">隨即會開啟視窗，讓您提供公司或學校帳戶的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="01456-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![輸入用來存取 Power BI 的認證](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="01456-134">輸入認證。</span><span class="sxs-lookup"><span data-stu-id="01456-134">Enter your credentials.</span></span> <span data-ttu-id="01456-135">請注意，當您輸入認證時，也會賦予權限讓串流分析作業存取您的 Power BI 區域。</span><span class="sxs-lookup"><span data-stu-id="01456-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="01456-136">當您返回 [新輸出] 刀鋒視窗時，請輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="01456-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="01456-137">**群組工作區**：在 Power BI 租用戶中，選取您要建立資料集的工作區。</span><span class="sxs-lookup"><span data-stu-id="01456-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="01456-138">**資料集名稱**：輸入 `sa-dataset`。</span><span class="sxs-lookup"><span data-stu-id="01456-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="01456-139">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="01456-139">You can use a different name.</span></span> <span data-ttu-id="01456-140">如果這樣做，請記下來供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="01456-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="01456-141">**資料表名稱**：輸入 `fraudulent-calls`。</span><span class="sxs-lookup"><span data-stu-id="01456-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="01456-142">目前，串流分析作業的 Power BI 輸出在資料集內只能有一個資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI 工作區](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="01456-144">如果 Power BI 的資料集和資料表名稱與您在串流分析作業中所指定的名稱相同，則會覆寫現有的資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="01456-145">我們不建議您在 Power BI 帳戶中明確建立此資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="01456-146">當您啟動串流分析作業，而該作業開始將輸出提取至 Power BI 時，系統會自動建立資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="01456-147">如果作業查詢沒有傳回任何結果，則不會建立資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="01456-148">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="01456-148">Click **Create**.</span></span>

<span data-ttu-id="01456-149">系統會使用下列設定來建立資料集：</span><span class="sxs-lookup"><span data-stu-id="01456-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="01456-150">**defaultRetentionPolicy: BasicFIFO**：資料是 FIFO，最大資料列數 20 萬。</span><span class="sxs-lookup"><span data-stu-id="01456-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="01456-151">**defaultMode: pushStreaming**：資料集同時支援串流磚和傳統報表型視覺效果 </span><span class="sxs-lookup"><span data-stu-id="01456-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="01456-152">(又稱為發送)。</span><span class="sxs-lookup"><span data-stu-id="01456-152">push).</span></span>

<span data-ttu-id="01456-153">您目前無法建立具有其他旗標的資料集。</span><span class="sxs-lookup"><span data-stu-id="01456-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="01456-154">如需 Power BI 資料集的詳細資訊，請參閱 [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) 參考。</span><span class="sxs-lookup"><span data-stu-id="01456-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="01456-155">撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="01456-155">Write the query</span></span>

1. <span data-ttu-id="01456-156">關閉 [輸出] 刀鋒視窗，返回作業刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="01456-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="01456-157">按一下 [查詢] 方塊。</span><span class="sxs-lookup"><span data-stu-id="01456-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="01456-158">輸入下列查詢。</span><span class="sxs-lookup"><span data-stu-id="01456-158">Enter the following query.</span></span> <span data-ttu-id="01456-159">此查詢類似於您在詐騙偵測教學課程中建立的自我聯結查詢。</span><span class="sxs-lookup"><span data-stu-id="01456-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="01456-160">差別在於此查詢會將結果傳送至您所建立的新輸出 (`CallStream-PowerBI`)。</span><span class="sxs-lookup"><span data-stu-id="01456-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="01456-161">如果您在詐騙偵測教學課程中不是將輸入命名為 `CallStream`，請在查詢的 **FROM** 和 **JOIN** 子句中，用您的名稱取代 `CallStream`。</span><span class="sxs-lookup"><span data-stu-id="01456-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="01456-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="01456-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="01456-163">測試查詢</span><span class="sxs-lookup"><span data-stu-id="01456-163">Test the query</span></span>
<span data-ttu-id="01456-164">此為選擇性區段，但建議執行。</span><span class="sxs-lookup"><span data-stu-id="01456-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="01456-165">如果目前沒有執行 TelcoStreaming 應用程式，請依照下列步驟啟動它：</span><span class="sxs-lookup"><span data-stu-id="01456-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="01456-166">開啟命令視窗。</span><span class="sxs-lookup"><span data-stu-id="01456-166">Open a command window.</span></span>
    * <span data-ttu-id="01456-167">移至 telcogenerator.exe 和修改的 telcodatagen.exe.config 檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="01456-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="01456-168">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="01456-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="01456-169">在 [查詢] 刀鋒視窗中，按一下 `CallStream` 輸入旁邊的點，然後選取 [來自輸入的範例資料]。</span><span class="sxs-lookup"><span data-stu-id="01456-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="01456-170">指定您想要取得三分鐘的資料，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="01456-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="01456-171">等待資料已取樣的通知。</span><span class="sxs-lookup"><span data-stu-id="01456-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="01456-172">按一下 [測試]，並確定開始產生結果。</span><span class="sxs-lookup"><span data-stu-id="01456-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="01456-173">執行工作</span><span class="sxs-lookup"><span data-stu-id="01456-173">Run the job</span></span>

1. <span data-ttu-id="01456-174">請確定 TelcoStreaming 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="01456-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="01456-175">關閉 [查詢] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="01456-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="01456-176">在作業刀鋒視窗中，按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="01456-176">In the job blade, click **Start**.</span></span>

    ![啟動串流分析工作](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="01456-178">串流分析作業會開始在傳入資料流中尋找詐騙電話。</span><span class="sxs-lookup"><span data-stu-id="01456-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="01456-179">此作業也會在 Power BI 中建立資料集和資料表，並開始將詐騙電話的相關資料傳送至該資料集和資料表。</span><span class="sxs-lookup"><span data-stu-id="01456-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="01456-180">在 Power BI 中建立儀表板</span><span class="sxs-lookup"><span data-stu-id="01456-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="01456-181">移至 [Powerbi.com](https://powerbi.com)，然後使用公司或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="01456-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="01456-182">如果串流分析作業查詢有輸出結果，您會看到資料集已建立：</span><span class="sxs-lookup"><span data-stu-id="01456-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Power BI 中的串流資料集](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="01456-184">在工作區中，按一下 [+&nbsp;建立]。</span><span class="sxs-lookup"><span data-stu-id="01456-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Power BI 工作區中的 [建立] 按鈕](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="01456-186">建立新的儀表板並命名為 `Fraudulent Calls`。</span><span class="sxs-lookup"><span data-stu-id="01456-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![在 Power BI 工作區中建立並命名儀表板](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="01456-188">在視窗的頂端，按一下 [新增磚]，選取 [自訂串流資料]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="01456-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![自訂串流資料集](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="01456-190">在 [您的資料集] 底下，選取資料集，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="01456-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![您的串流資料集](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="01456-192">在 [視覺效果類型] 底下，選取 [卡]，然後在 [欄位] 清單中，選取 [fraudulentcalls]。</span><span class="sxs-lookup"><span data-stu-id="01456-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![新磚的視覺效果詳細資料](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="01456-194">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="01456-194">Click **Next**.</span></span>

8. <span data-ttu-id="01456-195">填寫磚詳細資料，例如標題和副標題。</span><span class="sxs-lookup"><span data-stu-id="01456-195">Fill in tile details like a title and subtitle.</span></span>

    ![新磚的標題和副標題](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="01456-197">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="01456-197">Click **Apply**.</span></span>

    <span data-ttu-id="01456-198">您現在有一個詐騙計數器了！</span><span class="sxs-lookup"><span data-stu-id="01456-198">Now you have a fraud counter!</span></span>

    ![詐騙計數器](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="01456-200">再次依照步驟來新增磚 (從步驟 4 開始)。</span><span class="sxs-lookup"><span data-stu-id="01456-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="01456-201">這次請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="01456-201">This time, do the following:</span></span>

    * <span data-ttu-id="01456-202">在 [視覺效果類型] 中，選取 [折線圖]。</span><span class="sxs-lookup"><span data-stu-id="01456-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="01456-203">新增軸並選取 [windowend]。</span><span class="sxs-lookup"><span data-stu-id="01456-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="01456-204">新增值並選取 [fraudulentcalls]。</span><span class="sxs-lookup"><span data-stu-id="01456-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="01456-205">在 [要顯示的時間範圍] 中，選取過去 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="01456-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![建立折線圖的磚](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="01456-207">按 [下一步]，新增標題和副標題，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="01456-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="01456-208">Power BI 儀表板現在提供兩個檢視，讓您看到串流資料中偵測到之詐騙電話的相關資料。</span><span class="sxs-lookup"><span data-stu-id="01456-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![完成的 Power BI 儀表板，以兩個磚來顯示詐騙電話](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="01456-210">深入了解 Power BI</span><span class="sxs-lookup"><span data-stu-id="01456-210">Learn more about Power BI</span></span>

<span data-ttu-id="01456-211">本教學課程示範如何為一個資料集只建立幾種視覺效果。</span><span class="sxs-lookup"><span data-stu-id="01456-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="01456-212">Power BI 可協助您為組織建立其他客戶商業智慧型工具。</span><span class="sxs-lookup"><span data-stu-id="01456-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="01456-213">關於其他構想，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="01456-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="01456-214">如需其他 Power BI 儀表板範例，請觀賞 [開始使用 Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) 視訊。</span><span class="sxs-lookup"><span data-stu-id="01456-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="01456-215">如需有關設定串流分析作業輸出至 Power BI 及使用 Power BI 群組的詳細資訊，請檢閱[串流分析輸出](stream-analytics-define-outputs.md)一文的 [Power BI](stream-analytics-define-outputs.md#power-bi) 小節。</span><span class="sxs-lookup"><span data-stu-id="01456-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="01456-216">如需 Power BI 一般用法的相關資訊，請參閱 [Power BI 中的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)。</span><span class="sxs-lookup"><span data-stu-id="01456-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="01456-217">了解限制和最佳作法</span><span class="sxs-lookup"><span data-stu-id="01456-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="01456-218">目前來說，系統大約每秒可呼叫 Power BI 一次。</span><span class="sxs-lookup"><span data-stu-id="01456-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="01456-219">串流視覺效果支援 15 KB 的封包。</span><span class="sxs-lookup"><span data-stu-id="01456-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="01456-220">超過 15 KB，串流視覺效果就會失敗 (但仍會繼續推送)。</span><span class="sxs-lookup"><span data-stu-id="01456-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="01456-221">由於有這些限制，Power BI 最適用的自然是 Azure 串流分析會大量降低資料載入的案例。</span><span class="sxs-lookup"><span data-stu-id="01456-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="01456-222">我們建議使用輪轉視窗或跳動視窗，以確保資料推送最多為每秒推送 1 次，而且您的查詢符合輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="01456-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="01456-223">您可以使用下列方程式，以秒為單位計算要提供給視窗的值：</span><span class="sxs-lookup"><span data-stu-id="01456-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="01456-225">例如：</span><span class="sxs-lookup"><span data-stu-id="01456-225">For example:</span></span>

* <span data-ttu-id="01456-226">您有 1 千個以一秒間隔傳送資料的裝置。</span><span class="sxs-lookup"><span data-stu-id="01456-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="01456-227">您使用的 Power BI Pro SKU 支援每小時 100 萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="01456-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="01456-228">您想要讓每個裝置將平均資料量發佈至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="01456-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="01456-229">因此，方程式會變成︰</span><span class="sxs-lookup"><span data-stu-id="01456-229">As a result, the equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="01456-231">根據此設定，您可以將原始查詢變更如下︰</span><span class="sxs-lookup"><span data-stu-id="01456-231">Given this configuration, you can change the original query to the following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="01456-232">更新授權</span><span class="sxs-lookup"><span data-stu-id="01456-232">Renew authorization</span></span>
<span data-ttu-id="01456-233">如果自從建立作業或上次驗證之後已變更密碼，則您需要重新驗證 Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="01456-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="01456-234">如果您在 Azure Active Directory (Azure AD) 租用戶上設定 Azure Multi-Factor Authentication，則也需要每 2 週更新一次 Power BI 授權。</span><span class="sxs-lookup"><span data-stu-id="01456-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="01456-235">如果未更新，作業記錄中會出現一些徵兆，例如缺乏作業輸出或 `Authenticate user error`。</span><span class="sxs-lookup"><span data-stu-id="01456-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="01456-236">同樣地，如果作業在權杖過期後啟動，則會發生錯誤，作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="01456-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="01456-237">若要解決這個問題，請停止執行作業並移至 Power BI 輸出。</span><span class="sxs-lookup"><span data-stu-id="01456-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="01456-238">若要避免資料遺失，請選取 [更新授權] 連結，然後從 [上次停止時間] 重新啟動作業。</span><span class="sxs-lookup"><span data-stu-id="01456-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="01456-239">Power BI 在重新整理過授權後，授權區域就會出現綠色警示，表示問題已獲得解決。</span><span class="sxs-lookup"><span data-stu-id="01456-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="01456-240">取得說明</span><span class="sxs-lookup"><span data-stu-id="01456-240">Get help</span></span>
<span data-ttu-id="01456-241">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="01456-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01456-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01456-242">Next steps</span></span>
* [<span data-ttu-id="01456-243">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="01456-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="01456-244">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="01456-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="01456-245">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="01456-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="01456-246">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="01456-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="01456-247">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="01456-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
