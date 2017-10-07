---
title: "使用 OMS-Azure 邏輯應用程式執行邏輯應用程式的相關 aaaMonitor 和 get insights |Microsoft 文件"
description: "監視記錄分析和 Operations Management Suite (OMS) tooget insights 與更豐富的偵錯詳細資料，進行疑難排解和診斷程式邏輯應用程式執行"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="85ef2-103">透過 Operations Management Suite (OMS) 和 Log Analytics 監視邏輯應用程式執行並取得深入解析</span><span class="sxs-lookup"><span data-stu-id="85ef2-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="85ef2-104">監視和更豐富的偵錯資訊，您可以開啟的記錄分析 hello 在同一時間，當您建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="85ef2-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="85ef2-105">記錄分析會提供診斷記錄和監視應用程式邏輯會透過 hello Operations Management Suite (OMS) 的入口網站來執行。</span><span class="sxs-lookup"><span data-stu-id="85ef2-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="85ef2-106">當您新增 hello 邏輯應用程式管理解決方案 tooOMS 時，您會取得您的邏輯應用程式執行和特定的詳細資訊，例如狀態、 執行時間、 重新送出狀態，以及相互關聯識別碼的彙總的狀態。</span><span class="sxs-lookup"><span data-stu-id="85ef2-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="85ef2-107">本主題說明如何記錄分析或安裝 tooturn hello 在 OMS 中的邏輯應用程式管理解決方案讓您可以檢視執行階段事件，並執行應用程式邏輯的資料。</span><span class="sxs-lookup"><span data-stu-id="85ef2-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="85ef2-108">toomonitor 現有邏輯應用程式，請遵循下列步驟太[開啟診斷記錄，並傳送邏輯應用程式執行階段資料 tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="85ef2-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="85ef2-109">需求</span><span class="sxs-lookup"><span data-stu-id="85ef2-109">Requirements</span></span>

<span data-ttu-id="85ef2-110">開始之前，您會需要 toohave OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="85ef2-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="85ef2-111">深入了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="85ef2-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="85ef2-112">建立 Logic Apps 時開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="85ef2-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="85ef2-113">在 [Azure 入口網站](https://portal.azure.com)中，建立一個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="85ef2-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="85ef2-114">選擇 [新增] > [企業整合] > [邏輯應用程式] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="85ef2-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![建立邏輯應用程式](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="85ef2-116">在 hello**建立邏輯應用程式**頁面上，執行這些工作，如所示：</span><span class="sxs-lookup"><span data-stu-id="85ef2-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="85ef2-117">為您的邏輯應用程式命名並選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="85ef2-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="85ef2-118">建立或選取一個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="85ef2-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="85ef2-119">設定**記錄分析**太**上**。</span><span class="sxs-lookup"><span data-stu-id="85ef2-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="85ef2-120">您想太傳送應用程式邏輯的資料選取 hello OMS 工作區會執行。</span><span class="sxs-lookup"><span data-stu-id="85ef2-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="85ef2-121">當您準備好時，選擇**Pin toodashboard** > **建立**。</span><span class="sxs-lookup"><span data-stu-id="85ef2-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![建立邏輯應用程式](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="85ef2-123">完成此步驟之後，Azure 會建立您的邏輯應用程式，此應用程式現在會與您的 OMS 工作區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="85ef2-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="85ef2-124">此外，這個步驟也會自動會 hello 邏輯應用程式管理解決方案安裝在您的 OMS 工作區中。</span><span class="sxs-lookup"><span data-stu-id="85ef2-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="85ef2-125">在 OMS 中，執行邏輯應用程式的 tooview[繼續執行下列步驟](#view-logic-app-runs-oms)。</span><span class="sxs-lookup"><span data-stu-id="85ef2-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="85ef2-126">安裝在 OMS 中的 hello 邏輯應用程式管理解決方案</span><span class="sxs-lookup"><span data-stu-id="85ef2-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="85ef2-127">如果您在建立邏輯應用程式時已開啟 Log Analytics，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="85ef2-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="85ef2-128">您已經安裝在 OMS 中的 hello 邏輯應用程式管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="85ef2-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="85ef2-129">在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。</span><span class="sxs-lookup"><span data-stu-id="85ef2-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="85ef2-130">搜尋 "log analytics" 作為您的篩選條件，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85ef2-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![選擇 [Log Analytics]](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="85ef2-132">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="85ef2-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![選取 OMS 工作區](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="85ef2-134">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="85ef2-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 [OMS 入口網站]](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="85ef2-136">在您的 OMS 首頁 hello 升級橫幅顯示時，如果選擇 hello 橫幅，讓您先升級您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="85ef2-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="85ef2-137">然後選擇 [方案庫]。</span><span class="sxs-lookup"><span data-stu-id="85ef2-137">Then choose **Solutions Gallery**.</span></span>

   ![選擇 [方案庫]](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="85ef2-139">在下**所有方案**、 尋找並選擇 hello 的 hello 磚**邏輯應用程式管理**方案。</span><span class="sxs-lookup"><span data-stu-id="85ef2-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![選擇 [Logic Apps Management] \(Logic Apps 管理)](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="85ef2-141">在您的 OMS 工作區中的 tooinstall hello 方案選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="85ef2-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![針對 [Logic Apps Management] \(Logic Apps 管理) 選擇 [新增]](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="85ef2-143">在 OMS 工作區中檢視邏輯應用程式執行</span><span class="sxs-lookup"><span data-stu-id="85ef2-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="85ef2-144">tooview hello 計數和邏輯應用程式的狀態將會為您的 OMS 工作區移 toohello [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="85ef2-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="85ef2-145">檢閱上 hello 的 hello 詳細**邏輯應用程式管理**磚。</span><span class="sxs-lookup"><span data-stu-id="85ef2-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![顯示邏輯應用程式執行計數和狀態的概觀磚](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="85ef2-147">如果這個升級橫幅顯示而不是 hello 邏輯應用程式管理圖格，請選擇 hello 橫幅，讓您先升級您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="85ef2-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![升級「OMS 工作區」](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="85ef2-149">關於您邏輯應用程式執行時，更詳細的資料摘要 tooview 選擇 hello**邏輯應用程式管理**磚。</span><span class="sxs-lookup"><span data-stu-id="85ef2-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="85ef2-150">在這裡，您的邏輯應用程式執行會依名稱或執行狀態分組。</span><span class="sxs-lookup"><span data-stu-id="85ef2-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![邏輯應用程式執行的狀態摘要](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="85ef2-152">所有 hello 的 tooview 執行特定邏輯應用程式或狀態、 邏輯應用程式或狀態選取 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="85ef2-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="85ef2-153">以下是範例，顯示特定邏輯應用程式的所有 hello 執行：</span><span class="sxs-lookup"><span data-stu-id="85ef2-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![檢視邏輯應用程式或狀態的執行](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="85ef2-155">hello**重新提交**資料行會顯示 [是] 重新提交執行產生的執行。</span><span class="sxs-lookup"><span data-stu-id="85ef2-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="85ef2-156">toofilter 這些結果，您可以執行用戶端和伺服器端篩選。</span><span class="sxs-lookup"><span data-stu-id="85ef2-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="85ef2-157">用戶端篩選： 針對每個資料行中，選擇您想要的 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="85ef2-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="85ef2-158">這裡有一些範例：</span><span class="sxs-lookup"><span data-stu-id="85ef2-158">Here are some examples:</span></span>

     ![資料行篩選範例](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="85ef2-160">伺服器端篩選： toochoose 的出現，請使用 hello 範圍控制 hello 頁面頂端的 hello 的回合的特定時間視窗或 toolimit hello 數。</span><span class="sxs-lookup"><span data-stu-id="85ef2-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="85ef2-161">根據預設，一次只能出現 1,000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="85ef2-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![變更 hello 時間間隔](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="85ef2-163">所有 tooview 都 hello 動作和特定的執行，選取其詳細資料資料列，這會開啟都 hello 記錄搜尋 頁面。</span><span class="sxs-lookup"><span data-stu-id="85ef2-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="85ef2-164">這項資訊在資料表中，選擇 tooview**資料表**。</span><span class="sxs-lookup"><span data-stu-id="85ef2-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="85ef2-165">toochange hello 查詢中，您可以編輯 hello hello 搜尋列中的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="85ef2-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="85ef2-166">若要獲得更佳的體驗，請選擇 [進階分析]。</span><span class="sxs-lookup"><span data-stu-id="85ef2-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![檢視邏輯應用程式執行的動作和詳細資料](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="85ef2-168">這裡在 hello Azure 記錄分析 頁面上，您可以更新查詢和檢視結果 hello 資料表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="85ef2-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="85ef2-169">此查詢會使用[Kusto 查詢語言](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html)，如果您想 tooview 不同的結果，您可以編輯。</span><span class="sxs-lookup"><span data-stu-id="85ef2-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics - 查詢檢視](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="85ef2-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85ef2-171">Next steps</span></span>

* [<span data-ttu-id="85ef2-172">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="85ef2-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
