---
title: "檢查狀態、設定記錄並取得警示 - Azure Logic Apps | Microsoft Docs"
description: "監視邏輯應用程式的狀態和效能、記錄診斷資料，並設定警示"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="98bef-103">監視狀態、設定診斷記錄，以及開啟 Azure Logic Apps 的警示</span><span class="sxs-lookup"><span data-stu-id="98bef-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="98bef-104">在您[建立和執行邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)之後，即可檢查其執行歷程記錄、觸發程式歷程記錄、狀態和效能。</span><span class="sxs-lookup"><span data-stu-id="98bef-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="98bef-105">針對即時事件監視和更豐富的偵錯，設定邏輯應用程式的[診斷記錄](#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="98bef-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="98bef-106">因此，您可以[尋找並檢視事件](#find-events)，例如觸發程序事件、執行事件和動作事件。</span><span class="sxs-lookup"><span data-stu-id="98bef-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="98bef-107">您也可以[搭配使用此診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="98bef-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="98bef-108">若要取得失敗或其他可能問題的通知，請設定[警示](#add-azure-alerts)。</span><span class="sxs-lookup"><span data-stu-id="98bef-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="98bef-109">例如，您可以建立警示來偵測「一小時有五個以上的執行失敗時」。</span><span class="sxs-lookup"><span data-stu-id="98bef-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="98bef-110">您也可以使用 [Azure 診斷事件設定和內容](#diagnostic-event-properties)，透過程式設計方式設定監視、追蹤和記錄。</span><span class="sxs-lookup"><span data-stu-id="98bef-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="98bef-111">檢視邏輯應用程式的執行和觸發程序歷程記錄</span><span class="sxs-lookup"><span data-stu-id="98bef-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="98bef-112">若要在 [Azure 入口網站](https://portal.azure.com)中尋找邏輯應用程式，請在主要 Azure 功能表上選擇 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="98bef-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="98bef-113">在搜尋方塊中，尋找「邏輯應用程式」，然後選擇 [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="98bef-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![尋找邏輯應用程式](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="98bef-115">Azure 入口網站會顯示與 Azure 訂用帳戶相關聯的所有邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="98bef-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="98bef-116">選取邏輯應用程式，然後選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="98bef-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="98bef-117">Azure 入口網站會顯示邏輯應用程式的執行歷程記錄和觸發程序歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="98bef-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="98bef-118">例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-118">For example:</span></span>

   ![邏輯應用程式執行歷程記錄和觸發程序歷程記錄](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="98bef-120">**執行歷程記錄**會顯示邏輯應用程式的所有執行。</span><span class="sxs-lookup"><span data-stu-id="98bef-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="98bef-121">**觸發程序歷程記錄**會顯示邏輯應用程式的所有觸發程序活動。</span><span class="sxs-lookup"><span data-stu-id="98bef-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="98bef-122">如需狀態描述，請參閱[針對邏輯應用程式進行疑難排解](../logic-apps/logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="98bef-123">如果找不到您預期的資料，請在工具列上選擇 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="98bef-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="98bef-124">若要檢視特定執行的步驟，請在 [執行歷程記錄] 下選取該執行。</span><span class="sxs-lookup"><span data-stu-id="98bef-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="98bef-125">監視檢視會顯示該執行中的每個步驟。</span><span class="sxs-lookup"><span data-stu-id="98bef-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="98bef-126">例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-126">For example:</span></span>

   ![特定執行的動作](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="98bef-128">若要取得執行的其他詳細資訊，請選擇 [執行詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="98bef-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="98bef-129">這項資訊摘要說明執行的步驟、狀態、輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="98bef-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![選擇 [執行詳細資料]](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="98bef-131">例如，您可以取得執行的**相互關聯識別碼**，在您使用 [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic) 時可能需要此識別碼。</span><span class="sxs-lookup"><span data-stu-id="98bef-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="98bef-132">若要取得特定步驟的詳細資料，請選擇該步驟。</span><span class="sxs-lookup"><span data-stu-id="98bef-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="98bef-133">您現在可以檢閱詳細資料，例如輸入、輸出以及該步驟所發生的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="98bef-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="98bef-134">例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-134">For example:</span></span>

   ![步驟詳細資料](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="98bef-136">在 Logic Apps 服務內，會加密所有執行階段詳細資料和事件。</span><span class="sxs-lookup"><span data-stu-id="98bef-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="98bef-137">只有在使用者要求檢視該資料時，才對其進行解密。</span><span class="sxs-lookup"><span data-stu-id="98bef-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="98bef-138">您也可以使用 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md) 來控制對這些事件的存取權。</span><span class="sxs-lookup"><span data-stu-id="98bef-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="98bef-139">若要取得特定觸發程序事件的詳細資料，請回到 [概觀] 窗格。</span><span class="sxs-lookup"><span data-stu-id="98bef-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="98bef-140">在 [觸發程序歷程記錄] 下，選取觸發程序事件。</span><span class="sxs-lookup"><span data-stu-id="98bef-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="98bef-141">您現在可以檢閱輸入和輸出這類詳細資料，例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-141">You can now review details like inputs and outputs, for example:</span></span>

   ![觸發程序事件輸出詳細資料](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="98bef-143">開啟邏輯應用程式的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="98bef-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="98bef-144">如需使用執行階段詳細資料和事件進行更豐富的偵錯，您可以使用 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 設定診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="98bef-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="98bef-145">Log Analytics 是 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中的一項服務，可監視您的雲端和內部部署環境，協助您維護其可用性和效能。</span><span class="sxs-lookup"><span data-stu-id="98bef-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="98bef-146">開始之前，您需要有 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="98bef-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="98bef-147">了解[如何建立 OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="98bef-148">在 [Azure 入口網站](https://portal.azure.com)中，尋找並選取邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="98bef-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="98bef-149">在邏輯應用程式刀鋒視窗功能表上，於 [監視] 下選擇 [診斷] > [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="98bef-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![移至 [監視]、[診斷]、[診斷設定]](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="98bef-151">在 [診斷設定] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="98bef-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![開啟診斷記錄](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="98bef-153">現在選取用於記錄的 OMS 工作區和事件類別目錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="98bef-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="98bef-154">選取 [傳送至 Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="98bef-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="98bef-155">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="98bef-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="98bef-156">在 [OMS 工作區] 下，選取要用於記錄的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="98bef-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="98bef-157">在 [記錄] 下，選取 [WorkflowRuntime] 分類。</span><span class="sxs-lookup"><span data-stu-id="98bef-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="98bef-158">選擇計量間隔。</span><span class="sxs-lookup"><span data-stu-id="98bef-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="98bef-159">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="98bef-159">When you're done, choose **Save**.</span></span>

   ![選取用於記錄的 OMS 工作區和資料](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="98bef-161">現在，您可以尋找事件，以及觸發程序事件、執行事件和動作事件的其他資料。</span><span class="sxs-lookup"><span data-stu-id="98bef-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="98bef-162">尋找邏輯應用程式的事件和資料</span><span class="sxs-lookup"><span data-stu-id="98bef-162">Find events and data for your logic app</span></span>

<span data-ttu-id="98bef-163">若要在邏輯應用程式中尋找並檢視觸發程序事件、執行事件和動作事件這類事件，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="98bef-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="98bef-164">在 [Azure 入口網站](https://portal.azure.com)中，選擇 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="98bef-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="98bef-165">搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="98bef-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![選擇 [Log Analytics]](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="98bef-167">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="98bef-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![選取 OMS 工作區](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="98bef-169">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="98bef-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 [OMS 入口網站]](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="98bef-171">在 OMS 首頁上，選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="98bef-171">On your OMS home page, choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="98bef-173">-或-</span><span class="sxs-lookup"><span data-stu-id="98bef-173">-or-</span></span>

   ![在 OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="98bef-175">在搜尋方塊中，指定您想要尋找的欄位，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="98bef-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="98bef-176">當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。</span><span class="sxs-lookup"><span data-stu-id="98bef-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="98bef-177">例如，若要尋找所發生的前 10 個事件，請輸入並選取此搜尋查詢：**Category=WorkflowRuntime |top 10**</span><span class="sxs-lookup"><span data-stu-id="98bef-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![輸入搜尋字串](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="98bef-179">深入了解[如何在 Log Analytics 中尋找資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="98bef-180">在結果頁面上，於左列中選擇您想要檢視的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="98bef-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="98bef-181">若要新增篩選來調整您的查詢，請選擇 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="98bef-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![選擇查詢結果的時間範圍](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="98bef-183">在 [新增篩選] 下，輸入篩選名稱，以找到您想要的篩選。</span><span class="sxs-lookup"><span data-stu-id="98bef-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="98bef-184">選取篩選，然後選擇 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="98bef-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="98bef-185">此範例使用 "status" 這個字，在 **AzureDiagnostics** 下尋找失敗事件。</span><span class="sxs-lookup"><span data-stu-id="98bef-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="98bef-186">在這裡，已選取 **status_s** 的篩選。</span><span class="sxs-lookup"><span data-stu-id="98bef-186">Here the filter for **status_s** is already selected.</span></span>

   ![選取篩選](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="98bef-188">在左列中，選取您想要使用的篩選值，然後選擇 [套用]。</span><span class="sxs-lookup"><span data-stu-id="98bef-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![選取篩選值，然後選擇 [套用]](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="98bef-190">現在，回到您要建置的查詢。</span><span class="sxs-lookup"><span data-stu-id="98bef-190">Now return to the query that you're building.</span></span> <span data-ttu-id="98bef-191">使用您所選取的篩選和值來更新您的查詢。</span><span class="sxs-lookup"><span data-stu-id="98bef-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="98bef-192">現在也會篩選您的先前結果。</span><span class="sxs-lookup"><span data-stu-id="98bef-192">Your previous results are now filtered too.</span></span>

   ![回到具有已篩選結果的查詢](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="98bef-194">若要儲存查詢供日後使用，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="98bef-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="98bef-195">了解[如何儲存查詢](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query)。</span><span class="sxs-lookup"><span data-stu-id="98bef-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="98bef-196">延伸搭配使用診斷資料與其他服務的方式和位置</span><span class="sxs-lookup"><span data-stu-id="98bef-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="98bef-197">使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="98bef-198">在 Azure 儲存體中封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="98bef-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="98bef-199">將 Azure 診斷記錄串流至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="98bef-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="98bef-200">您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="98bef-201">例如：</span><span class="sxs-lookup"><span data-stu-id="98bef-201">For example:</span></span>

* [<span data-ttu-id="98bef-202">將資料從事件中樞串流至串流分析</span><span class="sxs-lookup"><span data-stu-id="98bef-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="98bef-203">使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="98bef-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="98bef-204">根據您要設定的選項，確定您先[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="98bef-205">然後選取您要傳送診斷資料的選項：</span><span class="sxs-lookup"><span data-stu-id="98bef-205">Then select the options for where you want to send diagnostic data:</span></span>

![將資料傳送至 Azure 儲存體帳戶或事件中樞](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="98bef-207">只有在您選擇使用儲存體帳戶時，才會套用保留期間。</span><span class="sxs-lookup"><span data-stu-id="98bef-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="98bef-208">設定邏輯應用程式的警示</span><span class="sxs-lookup"><span data-stu-id="98bef-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="98bef-209">若要監視邏輯應用程式的特定計量或已超過閾值，請設定 [Azure 中的警示](../monitoring-and-diagnostics/monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="98bef-210">了解 [Azure 中的計量](../monitoring-and-diagnostics/monitoring-overview-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="98bef-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="98bef-211">若要在不使用 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 的情況下設定警示，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="98bef-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="98bef-212">如需更進階的警示準則和動作，也請[設定 Log Analytics](#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="98bef-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="98bef-213">在邏輯應用程式刀鋒視窗功能表上，於 [監視] 下選擇 [診斷] > [警示規則] > [新增警示]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="98bef-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![新增邏輯應用程式的警示](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="98bef-215">在 [新增警示規則] 刀鋒視窗上，建立您的警示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="98bef-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="98bef-216">在 [資源] 下，選取尚未選取的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="98bef-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="98bef-217">提供警示的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="98bef-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="98bef-218">選取您想要追蹤的 [計量] 或事件。</span><span class="sxs-lookup"><span data-stu-id="98bef-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="98bef-219">選取 [條件]，並指定計量的 [閾值]，然後選取用於監視此計量的 [期間]。</span><span class="sxs-lookup"><span data-stu-id="98bef-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="98bef-220">選取是否傳送警示的郵件。</span><span class="sxs-lookup"><span data-stu-id="98bef-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="98bef-221">指定用於傳送警示的任何其他電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="98bef-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="98bef-222">您也可以指定要傳送警示的 Webhook URL。</span><span class="sxs-lookup"><span data-stu-id="98bef-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="98bef-223">例如，一小時有五個以上的執行失敗時，此規則會傳送警示：</span><span class="sxs-lookup"><span data-stu-id="98bef-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![建立計量警示規則](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="98bef-225">若要從警示執行邏輯應用程式，您可以在工作流程中包含[要求觸發程序](../connectors/connectors-native-reqres.md)，以讓您執行工作，例如下列範例：</span><span class="sxs-lookup"><span data-stu-id="98bef-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="98bef-226">張貼到 Slack</span><span class="sxs-lookup"><span data-stu-id="98bef-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="98bef-227">傳送文字</span><span class="sxs-lookup"><span data-stu-id="98bef-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="98bef-228">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="98bef-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="98bef-229">Azure 診斷事件設定和詳細資料</span><span class="sxs-lookup"><span data-stu-id="98bef-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="98bef-230">每個診斷事件都會有邏輯應用程式和該事件的詳細資料，例如，狀態、開始時間、結束時間等等。</span><span class="sxs-lookup"><span data-stu-id="98bef-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="98bef-231">若要以程式設計方式設定監視、追蹤和記錄，您可以搭配使用這些詳細資料與 [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) 和 [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows)。</span><span class="sxs-lookup"><span data-stu-id="98bef-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="98bef-232">例如，`ActionCompleted` 事件具有可用於追蹤和監視的 `clientTrackingId` 和 `trackedProperties` 屬性：</span><span class="sxs-lookup"><span data-stu-id="98bef-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="98bef-233">`clientTrackingId`： 如果未提供，Azure 會自動產生這個識別碼，並相互關聯邏輯應用程式執行之間的事件，包括從邏輯應用程式呼叫的任何巢狀工作流程。</span><span class="sxs-lookup"><span data-stu-id="98bef-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="98bef-234">您可以使用觸發程序要求中的自訂識別碼值來傳遞 `x-ms-client-tracking-id` 標頭，以從觸發程序手動指定此識別碼。</span><span class="sxs-lookup"><span data-stu-id="98bef-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="98bef-235">您可以使用要求觸發程序、HTTP 觸發程序或 Webhook 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="98bef-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="98bef-236">`trackedProperties`：若要追蹤診斷資料中的輸入或輸出，您可以將追蹤的屬性新增至邏輯應用程式 JSON 定義中的動作。</span><span class="sxs-lookup"><span data-stu-id="98bef-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="98bef-237">追蹤的屬性只能追蹤單一動作的輸入和輸出，但您可以使用事件的 `correlation` 屬性來跨執行中的動作進行相互關聯。</span><span class="sxs-lookup"><span data-stu-id="98bef-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="98bef-238">若要追蹤一或多個屬性，請將您想要的 `trackedProperties` 區段和屬性新增至動作定義。</span><span class="sxs-lookup"><span data-stu-id="98bef-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="98bef-239">例如，假設您想要追蹤遙測中「訂單識別碼」這類資料：</span><span class="sxs-lookup"><span data-stu-id="98bef-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="98bef-240">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98bef-240">Next steps</span></span>

* [<span data-ttu-id="98bef-241">建立範本以進行邏輯應用程式部署和發行管理</span><span class="sxs-lookup"><span data-stu-id="98bef-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="98bef-242">B2B 案例搭配企業整合套件</span><span class="sxs-lookup"><span data-stu-id="98bef-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="98bef-243">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="98bef-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)