---
title: "Azure IoT 中樞感應器資料的即時資料視覺效果 – Power BI | Microsoft Docs"
description: "使用 Power BI 來視覺化收集自感應器並傳送至 Azure IoT 中樞的溫度和溼度資料。"
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
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="0bcb9-104">使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化</span><span class="sxs-lookup"><span data-stu-id="0bcb9-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="0bcb9-106">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="0bcb9-106">What you learn</span></span>

<span data-ttu-id="0bcb9-107">您可了解如何藉由 Power BI 將 Azure IoT 中樞收到的即時感應器資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="0bcb9-108">如果您想嘗試使用 Web Apps 將 IoT 中樞的資料視覺化，請參閱[使用 Azure Web Apps 將 Azure IoT 中樞的即時感應器資料視覺化](iot-hub-live-data-visualization-in-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0bcb9-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="0bcb9-109">What you do</span></span>

- <span data-ttu-id="0bcb9-110">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="0bcb9-111">建立、設定和執行串流分析作業，以便將資料從 IoT 中樞傳輸至 Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="0bcb9-112">建立及發佈 Power BI 報告，以將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0bcb9-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="0bcb9-113">What you need</span></span>

- <span data-ttu-id="0bcb9-114">完成涵蓋下列需求的[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)教學課程︰</span><span class="sxs-lookup"><span data-stu-id="0bcb9-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="0bcb9-115">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="0bcb9-116">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="0bcb9-117">將訊息傳送到您 Azure IoT 中樞的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="0bcb9-118">Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-118">A Power BI account.</span></span> <span data-ttu-id="0bcb9-119">([免費試用 Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="0bcb9-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="0bcb9-120">設定、設定及執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="0bcb9-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0bcb9-121">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="0bcb9-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="0bcb9-122">在 Azure 入口網站中，按一下 [新增] > [物聯網] > [串流分析作業]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="0bcb9-123">輸入作業的以下資訊。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="0bcb9-124">**作業名稱**：作業名稱。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="0bcb9-125">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-125">The name must be globally unique.</span></span>

   <span data-ttu-id="0bcb9-126">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="0bcb9-127">**位置**︰使用與資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="0bcb9-128">**釘選至儀表板**︰核取此選項可讓您從儀表板輕鬆地存取 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![在 Azure 中建立串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="0bcb9-130">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="0bcb9-131">將輸入新增至串流分析作業</span><span class="sxs-lookup"><span data-stu-id="0bcb9-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="0bcb9-132">開啟串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="0bcb9-133">在 [作業拓撲] 之下，按一下 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="0bcb9-134">在 [輸入] 窗格中，按一下 [新增]，然後輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="0bcb9-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="0bcb9-135">**輸入別名**︰輸入的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="0bcb9-136">**來源**︰選取 [IoT 中樞]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="0bcb9-137">**取用者群組**︰選取您剛建立的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="0bcb9-138">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-138">Click **Create**.</span></span>

   ![在 Azure 中將輸入新增至串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="0bcb9-140">將輸出新增至串流分析作業</span><span class="sxs-lookup"><span data-stu-id="0bcb9-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="0bcb9-141">在 [作業拓撲] 之下，按一下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="0bcb9-142">在 [輸出] 窗格中，按一下 [新增]，然後輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="0bcb9-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="0bcb9-143">**輸出別名**︰輸出的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="0bcb9-144">**接收器**︰選取 [Power BI]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="0bcb9-145">按一下 [授權]，然後登入您的 Power BI 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="0bcb9-146">授權之後，輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="0bcb9-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="0bcb9-147">**群組工作區**︰選取您的目標群組工作區。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="0bcb9-148">**資料集名稱**︰輸入資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="0bcb9-149">**資料表名稱**︰輸入資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="0bcb9-150">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-150">Click **Create**.</span></span>

   ![在 Azure 中將輸出新增至串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="0bcb9-152">設定串流分析作業的查詢</span><span class="sxs-lookup"><span data-stu-id="0bcb9-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="0bcb9-153">在 [作業拓撲] 之下，按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="0bcb9-154">使用作業的輸入別名取代 `[YourInputAlias]`。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="0bcb9-155">使用作業的輸出別名取代 `[YourOutputAlias]`。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="0bcb9-156">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-156">Click **Save**.</span></span>

   ![在 Azure 中將查詢新增至串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="0bcb9-158">執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="0bcb9-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="0bcb9-159">在串流分析作業中，按一下 [啟動] > [立即] > [啟動]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="0bcb9-160">成功啟動作業後，作業狀態會從 [已停止] 變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![在 Azure 中執行串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="0bcb9-162">建立及發佈 Power BI 報告，以將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="0bcb9-163">確保範例應用程式正在您的裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="0bcb9-164">如果沒有，您可以參考[設定您的裝置](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)下的教學課程。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="0bcb9-165">登入您的 [Power BI](https://powerbi.microsoft.com/en-us/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="0bcb9-166">請移至建立串流分析作業輸出時所設定的群組工作區。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="0bcb9-167">按一下 [串流資料集]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="0bcb9-168">您應該會看到在建立串流分析作業輸出時所指定的資料集。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="0bcb9-169">在 [動作] 之下，按一下第一個圖示以建立報告。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![建立 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="0bcb9-171">建立折線圖以顯示一段時間的即時溫度。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="0bcb9-172">在報告建立頁面上，新增折線圖。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="0bcb9-173">在 [欄位] 窗格上，展開您建立串流分析作業輸出時指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="0bcb9-174">將 **EventEnqueuedUtcTime** 拖放至 [視覺效果] 窗格上的 [軸]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="0bcb9-175">將 **temperature** 拖放至 [值]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="0bcb9-176">現已建立折線圖。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-176">Now a line chart is created.</span></span> <span data-ttu-id="0bcb9-177">x 軸會顯示 UTC 時區的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="0bcb9-178">y 軸會顯示感應器的溫度。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-178">The y-axis displays temperature from the sensor.</span></span>

      ![將溫度的折線圖新增至 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="0bcb9-180">建立另一個折線圖以顯示一段時間的即時溼度。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="0bcb9-181">若要這麼做，請遵循上述相同步驟，並將 **EventEnqueuedUtcTime** 放在 x 軸上，將 **humidity** 放在 y 軸上。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![將溼度的折線圖新增至 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="0bcb9-183">按一下 [儲存] 以儲存報告。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="0bcb9-184">按一下 [檔案] > [發佈到網站]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="0bcb9-185">按一下 [建立內嵌程式碼]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="0bcb9-186">您會取得可與任何人共用以供存取報告的報告連結，以及取得程式碼片段以將報告整合到您的部落格或網站。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![發佈 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="0bcb9-188">Microsoft 也會提供 [Power BI 行動應用程式](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/)，以供檢視並與您行動裝置上的 Power BI 儀表板和報告互動。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bcb9-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bcb9-189">Next steps</span></span>

<span data-ttu-id="0bcb9-190">您已成功使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="0bcb9-191">有替代方法可將 Azure IoT 中樞的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="0bcb9-192">請參閱[使用 Azure Web Apps 將來自 Azure IoT 中樞的即時感應器資料視覺化](iot-hub-live-data-visualization-in-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="0bcb9-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
