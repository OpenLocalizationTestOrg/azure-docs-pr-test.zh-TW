---
title: "aaaCheck 狀態設定記錄，並取得警示-Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="c276b-103">監視狀態、設定診斷記錄，以及開啟 Azure Logic Apps 的警示</span><span class="sxs-lookup"><span data-stu-id="c276b-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="c276b-104">在您[建立和執行邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)之後，即可檢查其執行歷程記錄、觸發程式歷程記錄、狀態和效能。</span><span class="sxs-lookup"><span data-stu-id="c276b-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="c276b-105">針對即時事件監視和更豐富的偵錯，設定邏輯應用程式的[診斷記錄](#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="c276b-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="c276b-106">因此，您可以[尋找並檢視事件](#find-events)，例如觸發程序事件、執行事件和動作事件。</span><span class="sxs-lookup"><span data-stu-id="c276b-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="c276b-107">您也可以[搭配使用此診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c276b-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="c276b-108">tooget 通知失敗或其他可能的問題，設定[警示](#add-azure-alerts)。</span><span class="sxs-lookup"><span data-stu-id="c276b-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="c276b-109">例如，您可以建立警示來偵測「一小時有五個以上的執行失敗時」。</span><span class="sxs-lookup"><span data-stu-id="c276b-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="c276b-110">您也可以使用 [Azure 診斷事件設定和內容](#diagnostic-event-properties)，透過程式設計方式設定監視、追蹤和記錄。</span><span class="sxs-lookup"><span data-stu-id="c276b-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="c276b-111">檢視邏輯應用程式的執行和觸發程序歷程記錄</span><span class="sxs-lookup"><span data-stu-id="c276b-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="c276b-112">toofind hello 中的應用程式邏輯[Azure 入口網站](https://portal.azure.com)，在 hello Azure 的主功能表，選擇**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="c276b-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="c276b-113">Hello 搜尋方塊中，尋找 「 邏輯應用程式 」，然後選擇**Logic apps**。</span><span class="sxs-lookup"><span data-stu-id="c276b-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![尋找邏輯應用程式](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="c276b-115">hello Azure 入口網站會顯示所有 hello 邏輯應用程式與您 Azure 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="c276b-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="c276b-116">選取邏輯應用程式，然後選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="c276b-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="c276b-117">hello Azure 入口網站會顯示 hello 執行歷程記錄，以及觸發程序邏輯應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="c276b-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="c276b-118">例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-118">For example:</span></span>

   ![邏輯應用程式執行歷程記錄和觸發程序歷程記錄](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="c276b-120">**執行歷程記錄**顯示所有 hello 執行邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c276b-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="c276b-121">**觸發程序記錄**顯示所有 hello 觸發程序活動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c276b-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="c276b-122">如需狀態描述，請參閱[針對邏輯應用程式進行疑難排解](../logic-apps/logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="c276b-123">如果找不到預期 hello 工具列的 hello 資料選擇**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="c276b-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="c276b-124">tooview hello 底下步驟特定執行中，從**執行歷程記錄**，選取執行。</span><span class="sxs-lookup"><span data-stu-id="c276b-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="c276b-125">hello 監視器檢視顯示每個步驟中執行。</span><span class="sxs-lookup"><span data-stu-id="c276b-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="c276b-126">例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-126">For example:</span></span>

   ![特定執行的動作](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="c276b-128">tooget 詳細 hello 執行，請選擇**執行詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="c276b-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="c276b-129">這項資訊摘要說明 hello 步驟、 狀態、 輸入，並執行 hello 的輸出。</span><span class="sxs-lookup"><span data-stu-id="c276b-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![選擇 [執行詳細資料]](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="c276b-131">例如，您可以取得 hello 回合的**相互關聯識別碼**，您可能需要當您使用 hello [Logic apps REST API](https://docs.microsoft.com/rest/api/logic)。</span><span class="sxs-lookup"><span data-stu-id="c276b-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="c276b-132">tooget 詳細特定的步驟中，選擇該步驟。</span><span class="sxs-lookup"><span data-stu-id="c276b-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="c276b-133">您現在可以檢閱詳細資料，例如輸入、輸出以及該步驟所發生的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c276b-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="c276b-134">例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-134">For example:</span></span>

   ![步驟詳細資料](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="c276b-136">Hello Logic Apps 服務內加密的所有執行階段詳細資料與事件。</span><span class="sxs-lookup"><span data-stu-id="c276b-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="c276b-137">只有當使用者要求 tooview 該資料解密。</span><span class="sxs-lookup"><span data-stu-id="c276b-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="c276b-138">您也可以控制與存取 toothese 事件[所有存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="c276b-139">tooget 事件的詳細特定觸發程序，請返回 toohello**概觀**窗格。</span><span class="sxs-lookup"><span data-stu-id="c276b-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="c276b-140">在下**觸發記錄**，選取 hello 觸發程序事件。</span><span class="sxs-lookup"><span data-stu-id="c276b-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="c276b-141">您現在可以檢閱輸入和輸出這類詳細資料，例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-141">You can now review details like inputs and outputs, for example:</span></span>

   ![觸發程序事件輸出詳細資料](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="c276b-143">開啟邏輯應用程式的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="c276b-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="c276b-144">如需使用執行階段詳細資料和事件進行更豐富的偵錯，您可以使用 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 設定診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="c276b-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="c276b-145">記錄分析是中的服務[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)中監視您的雲端和內部部署環境 toohelp 您維護其可用性和效能。</span><span class="sxs-lookup"><span data-stu-id="c276b-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="c276b-146">開始之前，您會需要 toohave OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c276b-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="c276b-147">深入了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="c276b-148">在 hello [Azure 入口網站](https://portal.azure.com)、 尋找並選取邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c276b-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="c276b-149">在 [hello 邏輯應用程式] 刀鋒視窗功能表上底下**監視**，選擇**診斷** > **診斷設定**。</span><span class="sxs-lookup"><span data-stu-id="c276b-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![移 tooMonitoring，診斷，診斷設定](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="c276b-151">在 [診斷設定] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="c276b-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![開啟診斷記錄](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="c276b-153">現在選取 hello OMS 工作區和事件類別目錄的記錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c276b-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="c276b-154">選取**傳送 tooLog 分析**。</span><span class="sxs-lookup"><span data-stu-id="c276b-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="c276b-155">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="c276b-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="c276b-156">在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。</span><span class="sxs-lookup"><span data-stu-id="c276b-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="c276b-157">在下**記錄**，選取 hello **WorkflowRuntime**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="c276b-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="c276b-158">選擇 hello 度量的間隔。</span><span class="sxs-lookup"><span data-stu-id="c276b-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="c276b-159">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c276b-159">When you're done, choose **Save**.</span></span>

   ![選取用於記錄的 OMS 工作區和資料](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="c276b-161">現在，您可以尋找事件，以及觸發程序事件、執行事件和動作事件的其他資料。</span><span class="sxs-lookup"><span data-stu-id="c276b-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="c276b-162">尋找邏輯應用程式的事件和資料</span><span class="sxs-lookup"><span data-stu-id="c276b-162">Find events and data for your logic app</span></span>

<span data-ttu-id="c276b-163">應用程式中的邏輯，例如觸發程序事件，執行事件，以及動作事件，請遵循下列步驟 toofind 並檢視事件。</span><span class="sxs-lookup"><span data-stu-id="c276b-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="c276b-164">在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。</span><span class="sxs-lookup"><span data-stu-id="c276b-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c276b-165">搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c276b-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![選擇 [Log Analytics]](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="c276b-167">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c276b-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![選取 OMS 工作區](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="c276b-169">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="c276b-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 [OMS 入口網站]](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="c276b-171">在 OMS 首頁上，選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="c276b-171">On your OMS home page, choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="c276b-173">-或-</span><span class="sxs-lookup"><span data-stu-id="c276b-173">-or-</span></span>

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="c276b-175">在 hello 搜尋方塊中，指定您想 toofind，欄位按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="c276b-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="c276b-176">當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。</span><span class="sxs-lookup"><span data-stu-id="c276b-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="c276b-177">例如，toofind hello 前 10 個事件發生時，輸入，並選取這個搜尋查詢：**類別 = WorkflowRuntime | 前 10 個**</span><span class="sxs-lookup"><span data-stu-id="c276b-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![輸入搜尋字串](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="c276b-179">深入了解[如何 toofind 記錄分析資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="c276b-180">在 [hello 結果] 頁面上，hello 左工具列，選擇 hello 時間範圍內的 tooview。</span><span class="sxs-lookup"><span data-stu-id="c276b-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="c276b-181">toorefine 所新增的篩選器，查詢選擇**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="c276b-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![選擇查詢結果的時間範圍](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="c276b-183">下**加入篩選**，因此您可以找到您想要的 hello 篩選輸入 hello 篩選器名稱。</span><span class="sxs-lookup"><span data-stu-id="c276b-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="c276b-184">選取 hello 篩選，然後選擇  **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="c276b-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="c276b-185">這個範例會使用 hello word 「 狀態 」 toofind 失敗事件**AzureDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="c276b-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="c276b-186">這裡 hello 篩選**status_s**已選取。</span><span class="sxs-lookup"><span data-stu-id="c276b-186">Here hello filter for **status_s** is already selected.</span></span>

   ![選取篩選](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="c276b-188">在 hello 左列中，選取 hello 篩選值，您想 toouse，並選擇**套用**。</span><span class="sxs-lookup"><span data-stu-id="c276b-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![選取篩選值，然後選擇 [套用]](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="c276b-190">現在會傳回 toohello 您要建置的查詢。</span><span class="sxs-lookup"><span data-stu-id="c276b-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="c276b-191">使用您所選取的篩選和值來更新您的查詢。</span><span class="sxs-lookup"><span data-stu-id="c276b-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="c276b-192">現在也會篩選您的先前結果。</span><span class="sxs-lookup"><span data-stu-id="c276b-192">Your previous results are now filtered too.</span></span>

   ![傳回篩選的結果與 tooyour 查詢](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="c276b-194">toosave 您查詢供未來使用，請選擇 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="c276b-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="c276b-195">深入了解[如何 toosave 查詢](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query)。</span><span class="sxs-lookup"><span data-stu-id="c276b-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="c276b-196">延伸搭配使用診斷資料與其他服務的方式和位置</span><span class="sxs-lookup"><span data-stu-id="c276b-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="c276b-197">使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="c276b-198">在 Azure 儲存體中封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="c276b-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="c276b-199">資料流 Azure 診斷記錄檔 tooAzure 事件中心</span><span class="sxs-lookup"><span data-stu-id="c276b-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="c276b-200">您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="c276b-201">例如：</span><span class="sxs-lookup"><span data-stu-id="c276b-201">For example:</span></span>

* [<span data-ttu-id="c276b-202">從事件中心 tooStream 分析的資料流資料</span><span class="sxs-lookup"><span data-stu-id="c276b-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="c276b-203">使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="c276b-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="c276b-204">根據您想要設定的 hello 選項，請確定您第一次[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="c276b-205">然後選取您想要 toosend 診斷資料的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="c276b-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![傳送資料 tooAzure 儲存體帳戶或事件中心](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="c276b-207">Toouse 您選擇儲存體帳戶時，才會套用保留期限。</span><span class="sxs-lookup"><span data-stu-id="c276b-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="c276b-208">設定邏輯應用程式的警示</span><span class="sxs-lookup"><span data-stu-id="c276b-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="c276b-209">toomonitor 特定的衡量標準或邏輯應用程式中，已超過臨界值設定[在 Azure 中的警示](../monitoring-and-diagnostics/monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="c276b-210">了解 [Azure 中的計量](../monitoring-and-diagnostics/monitoring-overview-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="c276b-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="c276b-211">tooset 向上沒有警示[Azure Log Analytics](../log-analytics/log-analytics-overview.md)，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c276b-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="c276b-212">如需更進階的警示準則和動作，也請[設定 Log Analytics](#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="c276b-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="c276b-213">在 [hello 邏輯應用程式] 刀鋒視窗功能表上底下**監視**，選擇**診斷** > **警示規則** > **新增警示**如下所示：</span><span class="sxs-lookup"><span data-stu-id="c276b-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![新增邏輯應用程式的警示](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="c276b-215">在 hello**加入警示規則**刀鋒視窗中，建立您的警示所示：</span><span class="sxs-lookup"><span data-stu-id="c276b-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="c276b-216">在 [資源] 下，選取尚未選取的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c276b-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="c276b-217">提供警示的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="c276b-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="c276b-218">選取**度量**或想要 tootrack 事件。</span><span class="sxs-lookup"><span data-stu-id="c276b-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="c276b-219">選取**條件**，指定**閾值**hello 度量，以及選取 hello**期間**監視此度量。</span><span class="sxs-lookup"><span data-stu-id="c276b-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="c276b-220">選取是否 toosend 郵件 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="c276b-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="c276b-221">指定用於傳送嗨警示的其他電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="c276b-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="c276b-222">您也可以指定您想要 toosend hello 警示的 webhook URL。</span><span class="sxs-lookup"><span data-stu-id="c276b-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="c276b-223">例如，一小時有五個以上的執行失敗時，此規則會傳送警示：</span><span class="sxs-lookup"><span data-stu-id="c276b-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![建立計量警示規則](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="c276b-225">toorun 邏輯應用程式警示，您可以包含 hello[要求觸發程序](../connectors/connectors-native-reqres.md)在工作流程，可讓您執行工作，如這些範例：</span><span class="sxs-lookup"><span data-stu-id="c276b-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="c276b-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="c276b-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="c276b-227">傳送文字</span><span class="sxs-lookup"><span data-stu-id="c276b-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="c276b-228">新增訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="c276b-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="c276b-229">Azure 診斷事件設定和詳細資料</span><span class="sxs-lookup"><span data-stu-id="c276b-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="c276b-230">每個診斷事件的應用程式邏輯和事件，例如 hello 狀態詳細資料，開始時間、 結束時間等等。</span><span class="sxs-lookup"><span data-stu-id="c276b-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="c276b-231">tooprogrammatically 設定監視、 追蹤和記錄，您可以使用這些詳細資料以 hello [Azure 邏輯應用程式的 REST API](https://docs.microsoft.com/rest/api/logic)和 hello [Azure 診斷的 REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows)。</span><span class="sxs-lookup"><span data-stu-id="c276b-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="c276b-232">比方說，hello`ActionCompleted`事件有 hello`clientTrackingId`和`trackedProperties`屬性，您可以使用追蹤和監視：</span><span class="sxs-lookup"><span data-stu-id="c276b-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="c276b-233">`clientTrackingId`： 如果未提供 Azure 自動產生這個識別碼，並將事件相互關聯之間執行邏輯應用程式，包括任何巢狀工作流程，會從呼叫 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c276b-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="c276b-234">您可以手動指定此識別碼，從觸發程序藉由傳遞`x-ms-client-tracking-id`hello 觸發程序要求在您自訂 ID 值的標頭。</span><span class="sxs-lookup"><span data-stu-id="c276b-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="c276b-235">您可以使用要求觸發程序、HTTP 觸發程序或 Webhook 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c276b-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="c276b-236">`trackedProperties`: tootrack 輸入或輸出中診斷資料，您可以加入追蹤的屬性 tooactions 邏輯應用程式的 JSON 定義中。</span><span class="sxs-lookup"><span data-stu-id="c276b-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="c276b-237">追蹤的屬性可以追蹤僅以單一動作的輸入和輸出，但您可以使用 hello`correlation`事件 toocorrelate 跨中執行的動作的屬性。</span><span class="sxs-lookup"><span data-stu-id="c276b-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="c276b-238">tootrack 一或多個屬性，新增 hello`trackedProperties`區段和 hello 想 toohello 動作定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="c276b-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="c276b-239">例如，假設您要 tootrack 資料，例如 「 訂單識別碼 」 您遙測中：</span><span class="sxs-lookup"><span data-stu-id="c276b-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c276b-240">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c276b-240">Next steps</span></span>

* [<span data-ttu-id="c276b-241">建立範本以進行邏輯應用程式部署和發行管理</span><span class="sxs-lookup"><span data-stu-id="c276b-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="c276b-242">B2B 案例搭配企業整合套件</span><span class="sxs-lookup"><span data-stu-id="c276b-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="c276b-243">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="c276b-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)