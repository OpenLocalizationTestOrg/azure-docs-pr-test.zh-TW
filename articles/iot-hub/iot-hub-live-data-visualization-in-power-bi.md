---
title: "aaaReal 時間資料從 Azure IoT 中樞 – Power BI 的感應器資料視覺效果 |Microsoft 文件"
description: "使用 Power BI toovisualize 氣溫和溼度的資料會從 hello 感應器收集並傳送 tooyour Azure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "即時資料視覺效果, 即時資料視覺效果, 感應器資料視覺效果"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="b6eb4-104">使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化</span><span class="sxs-lookup"><span data-stu-id="b6eb4-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="b6eb4-106">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="b6eb4-106">What you learn</span></span>

<span data-ttu-id="b6eb4-107">您了解如何 toovisualize 即時感應器資料的 Azure IoT 中樞接收由 Power BI。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="b6eb4-108">如果您想 tootry 視覺化 hello 資料在您的 IoT 中樞與 Web 應用程式，請參閱[使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b6eb4-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="b6eb4-109">What you do</span></span>

- <span data-ttu-id="b6eb4-110">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="b6eb4-111">建立、 設定及執行資料傳輸的資料流分析作業從您的 IoT 中樞 tooyour Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="b6eb4-112">建立並發行 Power BI 報表 toovisualize hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6eb4-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b6eb4-113">What you need</span></span>

- <span data-ttu-id="b6eb4-114">教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="b6eb4-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b6eb4-115">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="b6eb4-116">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b6eb4-117">用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b6eb4-118">Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-118">A Power BI account.</span></span> <span data-ttu-id="b6eb4-119">([免費試用 Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="b6eb4-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="b6eb4-120">設定、設定及執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="b6eb4-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b6eb4-121">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="b6eb4-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="b6eb4-122">在 hello Azure 入口網站中按一下 新增 > 物聯網 > 串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="b6eb4-123">輸入下列資訊為 hello 工作 hello。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="b6eb4-124">**工作名稱**: hello hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="b6eb4-125">hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="b6eb4-126">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="b6eb4-127">**位置**： 使用 hello 相同資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="b6eb4-128">**Pin toodashboard**： 核取此選項，讓您輕鬆存取 tooyour IoT 中樞，從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![在 Azure 中建立串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="b6eb4-130">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="b6eb4-131">加入輸入的 toohello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="b6eb4-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b6eb4-132">開啟 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b6eb4-133">在 [作業拓撲] 之下，按一下 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="b6eb4-134">在 [hello**輸入**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6eb4-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b6eb4-135">**輸入的別名**: hello hello 輸入唯一別名。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="b6eb4-136">**來源**︰選取 [IoT 中樞]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="b6eb4-137">**取用者群組**: hello 選取您剛才建立的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="b6eb4-138">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-138">Click **Create**.</span></span>

   ![在 Azure 中加入輸入的 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="b6eb4-140">加入輸出 toohello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="b6eb4-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b6eb4-141">在 [作業拓撲] 之下，按一下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="b6eb4-142">在 [hello**輸出**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6eb4-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b6eb4-143">**輸出別名**: hello hello 輸出的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="b6eb4-144">**接收器**︰選取 [Power BI]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="b6eb4-145">按一下 [授權]，然後登入您的 Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="b6eb4-146">授權之後，請輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6eb4-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="b6eb4-147">**群組工作區**︰選取您的目標群組工作區。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="b6eb4-148">**資料集名稱**︰輸入資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="b6eb4-149">**資料表名稱**︰輸入資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="b6eb4-150">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-150">Click **Create**.</span></span>

   ![在 Azure 中加入輸出 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="b6eb4-152">設定 hello hello 資料流分析作業的查詢</span><span class="sxs-lookup"><span data-stu-id="b6eb4-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="b6eb4-153">在 [作業拓撲] 之下，按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="b6eb4-154">取代`[YourInputAlias]`hello 作業的 hello 輸入別名。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="b6eb4-155">取代`[YourOutputAlias]`hello 的 hello 工作的輸出別名。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="b6eb4-156">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-156">Click **Save**.</span></span>

   ![在 Azure 中加入查詢 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="b6eb4-158">執行 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="b6eb4-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="b6eb4-159">在 hello Stream Analytics 工作中，按一下 **啟動** > **現在** > **啟動**。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="b6eb4-160">Hello 工作成功啟動 hello 作業狀態變更從**已停止**太**執行**。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![在 Azure 中執行串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="b6eb4-162">建立及發行 Power BI 報表 toovisualize hello 資料</span><span class="sxs-lookup"><span data-stu-id="b6eb4-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="b6eb4-163">確定 hello 範例應用程式正在執行您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="b6eb4-164">如果沒有，請參閱下的 toohello 教學課程[設定您的裝置](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="b6eb4-165">登入 tooyour [Power BI](https://powerbi.microsoft.com/en-us/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="b6eb4-166">移 toohello 群組工作區中，當您建立 hello hello 資料流分析工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b6eb4-167">按一下 [串流資料集]。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="b6eb4-168">您應該會看到當您建立 hello hello 資料流分析工作的輸出指定的 hello 列出資料集。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b6eb4-169">在下**動作**，按一下第一個圖示 toocreate hello 報表。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![建立 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="b6eb4-171">經過一段時間建立列圖表 tooshow 即時溫度。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="b6eb4-172">在 hello 報表建立頁面上，加入折線圖。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="b6eb4-173">在 [hello**欄位**] 窗格中，展開您指定當您建立 hello hello 之資料流分析工作輸出的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="b6eb4-174">拖曳**EventEnqueuedUtcTime**太**軸**上 hello**視覺效果**窗格。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="b6eb4-175">拖曳**溫度**太**值**。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="b6eb4-176">現已建立折線圖。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-176">Now a line chart is created.</span></span> <span data-ttu-id="b6eb4-177">hello x 軸會顯示以 hello UTC 時區日期和時間。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="b6eb4-178">hello y 軸會顯示從 hello 感應器的溫度。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![加入折線圖的溫度 tooa Microsoft Power BI 報表](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="b6eb4-180">經過一段時間建立另一個行圖表 tooshow 即時溼度。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="b6eb4-181">toodo，遵循的 hello 上述相同步驟，並將**EventEnqueuedUtcTime** hello x 軸上和**溼度**hello y 軸上。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![加入折線圖的溼度 tooa Microsoft Power BI 報表](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="b6eb4-183">按一下**儲存**toosave hello 報表。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="b6eb4-184">按一下**檔案** > **發行 tooweb**。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="b6eb4-185">按一下 建立內嵌程式碼，然後按一下發佈。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="b6eb4-186">您要提供您可以與報表存取的任何人和程式碼片段 toointegrate hello 報告至您部落格或網站共用的 hello 報表連結。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![發佈 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="b6eb4-188">Microsoft 也提供 hello [Power BI 行動應用程式](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/)檢視和與您的 Power BI 儀表板和報表互動行動裝置上。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6eb4-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6eb4-189">Next steps</span></span>

<span data-ttu-id="b6eb4-190">您已成功從您的 Azure IoT 中樞使用 Power BI toovisualize 即時感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="b6eb4-191">沒有從 Azure IoT 中樞的替代方式 toovisualize 資料。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="b6eb4-192">請參閱[使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="b6eb4-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
