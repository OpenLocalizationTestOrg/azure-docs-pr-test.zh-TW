---
title: "在 Log Analytics 中分析資料使用量 | Microsoft Docs"
description: "在 Log Analytics 中使用 [使用量] 儀表板，檢視正在傳送給 Log Analytics 服務的資料量，並分析解決傳送大量資料的原因。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: 9a4709f298131722e9c473a19f7eee0aebf7e1e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a><span data-ttu-id="41b0f-103">在 Log Analytics 中分析資料使用量</span><span class="sxs-lookup"><span data-stu-id="41b0f-103">Analyze data usage in Log Analytics</span></span>
<span data-ttu-id="41b0f-104">Log Analytics 包含下列資訊：收集的資料量、傳送資料的電腦，以及傳送的不同資料類型。</span><span class="sxs-lookup"><span data-stu-id="41b0f-104">Log Analytics includes information on the amount of data collected, which computers sent the data and the different types of data sent.</span></span>  <span data-ttu-id="41b0f-105">使用 [Log Analytics 使用量] 儀表板，查看傳送到 Log Analytics 服務的資料量。</span><span class="sxs-lookup"><span data-stu-id="41b0f-105">Use the **Log Analytics Usage** dashboard to see the amount of data sent to the Log Analytics service.</span></span> <span data-ttu-id="41b0f-106">此儀表板會顯示每個解決方案所收集的資料量，以及您的電腦正在傳送的資料量。</span><span class="sxs-lookup"><span data-stu-id="41b0f-106">The dashboard shows how much data is collected by each solution and how much data your computers are sending.</span></span>

## <a name="understand-the-usage-dashboard"></a><span data-ttu-id="41b0f-107">了解使用量儀表板</span><span class="sxs-lookup"><span data-stu-id="41b0f-107">Understand the Usage dashboard</span></span>
<span data-ttu-id="41b0f-108">[Log Analytics 使用量] 儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="41b0f-108">The **Log Analytics usage** dashboard displays the following information:</span></span>

- <span data-ttu-id="41b0f-109">資料量</span><span class="sxs-lookup"><span data-stu-id="41b0f-109">Data volume</span></span>
    - <span data-ttu-id="41b0f-110">一段時間 (根據您目前的時間範圍) 的資料量</span><span class="sxs-lookup"><span data-stu-id="41b0f-110">Data volume over time (based on your current time scope)</span></span>
    - <span data-ttu-id="41b0f-111">依方案分類的資料量</span><span class="sxs-lookup"><span data-stu-id="41b0f-111">Data volume by solution</span></span>
    - <span data-ttu-id="41b0f-112">與電腦不相關的資料</span><span class="sxs-lookup"><span data-stu-id="41b0f-112">Data not associated with a computer</span></span>
- <span data-ttu-id="41b0f-113">電腦</span><span class="sxs-lookup"><span data-stu-id="41b0f-113">Computers</span></span>
    - <span data-ttu-id="41b0f-114">傳送資料的電腦</span><span class="sxs-lookup"><span data-stu-id="41b0f-114">Computers sending data</span></span>
    - <span data-ttu-id="41b0f-115">過去 24 小時內沒有資料的電腦</span><span class="sxs-lookup"><span data-stu-id="41b0f-115">Computers with no data in last 24 hours</span></span>
- <span data-ttu-id="41b0f-116">供應項目</span><span class="sxs-lookup"><span data-stu-id="41b0f-116">Offerings</span></span>
    - <span data-ttu-id="41b0f-117">深入解析和分析節點</span><span class="sxs-lookup"><span data-stu-id="41b0f-117">Insight and Analytics nodes</span></span>
    - <span data-ttu-id="41b0f-118">自動化和控制節點</span><span class="sxs-lookup"><span data-stu-id="41b0f-118">Automation and Control nodes</span></span>
    - <span data-ttu-id="41b0f-119">安全性節點</span><span class="sxs-lookup"><span data-stu-id="41b0f-119">Security nodes</span></span>
- <span data-ttu-id="41b0f-120">效能</span><span class="sxs-lookup"><span data-stu-id="41b0f-120">Performance</span></span>
    - <span data-ttu-id="41b0f-121">收集資料和編制索引所花費的時間</span><span class="sxs-lookup"><span data-stu-id="41b0f-121">Time taken to collect and index data</span></span>
- <span data-ttu-id="41b0f-122">查詢清單</span><span class="sxs-lookup"><span data-stu-id="41b0f-122">List of queries</span></span>

![使用量儀表板](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="to-work-with-usage-data"></a><span data-ttu-id="41b0f-124">處理使用量資料</span><span class="sxs-lookup"><span data-stu-id="41b0f-124">To work with usage data</span></span>
1. <span data-ttu-id="41b0f-125">如果您尚未這麼做，請使用 Azure 訂用帳戶登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="41b0f-125">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com) using your Azure subscription.</span></span>
2. <span data-ttu-id="41b0f-126">在 [中樞] 功能表上按一下 [更多服務]，然後在資源清單中輸入 **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="41b0f-126">On the **Hub** menu, click **More services** and in the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="41b0f-127">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="41b0f-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="41b0f-128">按一下 [Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="41b0f-128">Click **Log Analytics**.</span></span>  
    <span data-ttu-id="41b0f-129">![Azure 中樞](./media/log-analytics-usage/hub.png)</span><span class="sxs-lookup"><span data-stu-id="41b0f-129">![Azure hub](./media/log-analytics-usage/hub.png)</span></span>
3. <span data-ttu-id="41b0f-130">[Log Analytics] 儀表板會顯示您的工作區清單。</span><span class="sxs-lookup"><span data-stu-id="41b0f-130">The **Log Analytics** dashboard shows a list of your workspaces.</span></span> <span data-ttu-id="41b0f-131">選取工作區。</span><span class="sxs-lookup"><span data-stu-id="41b0f-131">Select a workspace.</span></span>
4. <span data-ttu-id="41b0f-132">在 [工作區] 儀表板中，按一下 [Log Analytics 使用量]。</span><span class="sxs-lookup"><span data-stu-id="41b0f-132">In the *workspace* dashboard, click **Log Analytics usage**.</span></span>
5. <span data-ttu-id="41b0f-133">在 [Log Analytics 使用量] 儀表板中，按一下 [時間︰過去 24 小時] 以變更時間間隔。</span><span class="sxs-lookup"><span data-stu-id="41b0f-133">On the **Log Analytics Usage** dashboard, click **Time: Last 24 hours** to change the time interval.</span></span>  
    <span data-ttu-id="41b0f-134">![時間間隔](./media/log-analytics-usage/time.png)</span><span class="sxs-lookup"><span data-stu-id="41b0f-134">![time interval](./media/log-analytics-usage/time.png)</span></span>
6. <span data-ttu-id="41b0f-135">檢視顯示您感興趣之領域的使用量類別刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="41b0f-135">View the usage category blades that show areas you’re interested in.</span></span> <span data-ttu-id="41b0f-136">選擇刀鋒視窗，然後在其中按一下某個項目以在 [記錄檔搜尋](log-analytics-log-searches.md) 中檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-136">Choose a blade and then click an item in it to view more details in [Log Search](log-analytics-log-searches.md).</span></span>  
    <span data-ttu-id="41b0f-137">![範例資料使用量刀鋒視窗](./media/log-analytics-usage/blade.png)</span><span class="sxs-lookup"><span data-stu-id="41b0f-137">![example data usage blade](./media/log-analytics-usage/blade.png)</span></span>
7. <span data-ttu-id="41b0f-138">在 [記錄檔搜尋] 儀表板中，檢閱搜尋傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="41b0f-138">On the Log Search dashboard, review the results that are returned from the search.</span></span>  
    ![範例使用量記錄檔搜尋](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a><span data-ttu-id="41b0f-140">當資料收集高於預期時建立警示</span><span class="sxs-lookup"><span data-stu-id="41b0f-140">Create an alert when data collection is higher than expected</span></span>
<span data-ttu-id="41b0f-141">本節說明在下列情況下如何建立警示：</span><span class="sxs-lookup"><span data-stu-id="41b0f-141">This section describes how to create an alert if:</span></span>
- <span data-ttu-id="41b0f-142">資料量超出指定的數量。</span><span class="sxs-lookup"><span data-stu-id="41b0f-142">Data volume exceeds a specified amount.</span></span>
- <span data-ttu-id="41b0f-143">資料量預計會超出指定的數量。</span><span class="sxs-lookup"><span data-stu-id="41b0f-143">Data volume is predicted to exceed a specified amount.</span></span>

<span data-ttu-id="41b0f-144">Log Analytics [警示](log-analytics-alerts-creating.md)會使用搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="41b0f-144">Log Analytics [alerts](log-analytics-alerts-creating.md) use search queries.</span></span> <span data-ttu-id="41b0f-145">在過去 24 小時收集超過 100GB 的資料時，下列查詢的結果：</span><span class="sxs-lookup"><span data-stu-id="41b0f-145">The following query has a result when there is more than 100 GB of data collected in the last 24 hours:</span></span>

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

<span data-ttu-id="41b0f-146">下列查詢會使用簡單的公式來預測在一天中何時會傳送超過 100GB 的資料：</span><span class="sxs-lookup"><span data-stu-id="41b0f-146">The following query uses a simple formula to predict when more than 100 GB of data will be sent in a day:</span></span> 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

<span data-ttu-id="41b0f-147">若要針對不同的資料量顯示警示，請將查詢中的 100 變更為您要顯示警示的 GB 數。</span><span class="sxs-lookup"><span data-stu-id="41b0f-147">To alert on a different data volume, change the 100 in the queries to the number of GB you want to alert on.</span></span>

<span data-ttu-id="41b0f-148">使用[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)中所述的步驟，可在資料收集高於預期時收到通知。</span><span class="sxs-lookup"><span data-stu-id="41b0f-148">Use the steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) to be notified when data collection is higher than expected.</span></span>

<span data-ttu-id="41b0f-149">建立第一個查詢的警示時 - 在 24 小時內有超過 100GB 的資料時，請：</span><span class="sxs-lookup"><span data-stu-id="41b0f-149">When creating the alert for the first query -- when there is more than 100 GB of data in 24 hours, set the:</span></span>
- <span data-ttu-id="41b0f-150">將 [名稱] 設定為「在 24 小時內大於 100GB 的資料量」</span><span class="sxs-lookup"><span data-stu-id="41b0f-150">**Name** to *Data volume greater than 100 GB in 24 hours*</span></span>
- <span data-ttu-id="41b0f-151">將 [嚴重性] 設定為「警告」</span><span class="sxs-lookup"><span data-stu-id="41b0f-151">**Severity** to *Warning*</span></span>
- <span data-ttu-id="41b0f-152">將 [搜尋查詢] 設定為 `Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`</span><span class="sxs-lookup"><span data-stu-id="41b0f-152">**Search query** to `Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`</span></span>
- <span data-ttu-id="41b0f-153">將 [時間範圍] 設定為「24 小時」。</span><span class="sxs-lookup"><span data-stu-id="41b0f-153">**Time window** to *24 Hours*.</span></span>
- <span data-ttu-id="41b0f-154">將 [警示頻率] 設定為一小時，因為使用量資料每小時只會更新一次。</span><span class="sxs-lookup"><span data-stu-id="41b0f-154">**Alert frequency** to be one hour since the usage data only updates once per hour.</span></span>
- <span data-ttu-id="41b0f-155">將 [產生警示的依據] 設定為「結果數目」</span><span class="sxs-lookup"><span data-stu-id="41b0f-155">**Generate alert based on** to be *number of results*</span></span>
- <span data-ttu-id="41b0f-156">將 [結果數目] 設定為「大於 0」</span><span class="sxs-lookup"><span data-stu-id="41b0f-156">**Number of results** to be *Greater than 0*</span></span>

<span data-ttu-id="41b0f-157">使用[將動作新增到警示規則](log-analytics-alerts-actions.md)中所述的步驟來設定警示規則的電子郵件、Webhook 或 Runbook 動作。</span><span class="sxs-lookup"><span data-stu-id="41b0f-157">Use the steps described in [add actions to alert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for the alert rule.</span></span>

<span data-ttu-id="41b0f-158">建立第二個查詢的警示時 - 預計在 24 小時內會有超過 100GB 的資料時，請：</span><span class="sxs-lookup"><span data-stu-id="41b0f-158">When creating the alert for the second query -- when it is predicted that there will be more than 100 GB of data in 24 hours, set the:</span></span>
- <span data-ttu-id="41b0f-159">將 [名稱] 設定為「預計在 24 小時內大於 100GB 的資料量」</span><span class="sxs-lookup"><span data-stu-id="41b0f-159">**Name** to *Data volume expected to greater than 100 GB in 24 hours*</span></span>
- <span data-ttu-id="41b0f-160">將 [嚴重性] 設定為「警告」</span><span class="sxs-lookup"><span data-stu-id="41b0f-160">**Severity** to *Warning*</span></span>
- <span data-ttu-id="41b0f-161">將 [搜尋查詢] 設定為 `Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`</span><span class="sxs-lookup"><span data-stu-id="41b0f-161">**Search query** to `Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`</span></span>
- <span data-ttu-id="41b0f-162">將 [時間範圍] 設定為「3 小時」。</span><span class="sxs-lookup"><span data-stu-id="41b0f-162">**Time window** to *3 Hours*.</span></span>
- <span data-ttu-id="41b0f-163">將 [警示頻率] 設定為一小時，因為使用量資料每小時只會更新一次。</span><span class="sxs-lookup"><span data-stu-id="41b0f-163">**Alert frequency** to be one hour since the usage data only updates once per hour.</span></span>
- <span data-ttu-id="41b0f-164">將 [產生警示的依據] 設定為「結果數目」</span><span class="sxs-lookup"><span data-stu-id="41b0f-164">**Generate alert based on** to be *number of results*</span></span>
- <span data-ttu-id="41b0f-165">將 [結果數目] 設定為「大於 0」</span><span class="sxs-lookup"><span data-stu-id="41b0f-165">**Number of results** to be *Greater than 0*</span></span>

<span data-ttu-id="41b0f-166">當您收到警示時，請使用下一節中的步驟，針對使用量高於預期的原因進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="41b0f-166">When you receive an alert, use the steps in the following section to troubleshoot why usage is higher than expected.</span></span>

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a><span data-ttu-id="41b0f-167">針對使用量高於預期的原因進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="41b0f-167">Troubleshooting why usage is higher than expected</span></span>
<span data-ttu-id="41b0f-168">使用量儀表板可協助您找出使用量 (且因而成本) 高於預期的原因。</span><span class="sxs-lookup"><span data-stu-id="41b0f-168">The usage dashboard helps you to identify why usage (and therefore cost) is higher than you are expecting.</span></span>

<span data-ttu-id="41b0f-169">較高的使用量是由下列一個或兩個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="41b0f-169">Higher usage is caused by one, or both of:</span></span>
- <span data-ttu-id="41b0f-170">傳送到 Log Analytics 的資料比預期更多</span><span class="sxs-lookup"><span data-stu-id="41b0f-170">More data than expected being sent to Log Analytics</span></span>
- <span data-ttu-id="41b0f-171">比預期更多的節點將資料傳送到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="41b0f-171">More nodes than expected sending data to Log Analytics</span></span>

### <a name="check-if-there-is-more-data-than-expected"></a><span data-ttu-id="41b0f-172">檢查是否有比預期更多的資料</span><span class="sxs-lookup"><span data-stu-id="41b0f-172">Check if there is more data than expected</span></span> 
<span data-ttu-id="41b0f-173">[使用量] 頁面有兩個重要區段，有助於識別收集最多資料的電腦。</span><span class="sxs-lookup"><span data-stu-id="41b0f-173">There are two key sections of the usage page that help identify what is causing the most data to be collected.</span></span>

<span data-ttu-id="41b0f-174">「一段時間的資料量」圖表會顯示已傳送的資料總量和傳送最多資料的電腦。</span><span class="sxs-lookup"><span data-stu-id="41b0f-174">The *Data volume over time* chart shows the total volume of data sent and the computers sending the most data.</span></span> <span data-ttu-id="41b0f-175">頂端的圖表可讓您查看整體資料使用量為成長中、保持穩定或減少中。</span><span class="sxs-lookup"><span data-stu-id="41b0f-175">The chart at the top allows you to see if your overall data usage is growing, remaining steady or decreasing.</span></span> <span data-ttu-id="41b0f-176">電腦清單會顯示傳送最多資料的 10 部電腦。</span><span class="sxs-lookup"><span data-stu-id="41b0f-176">The list of computers shows the 10 computers sending the most data.</span></span>

<span data-ttu-id="41b0f-177">「依方案分類的資料量」圖表可顯示每個解決方案所傳送的資料量，以及傳送最多資料的解決方案。</span><span class="sxs-lookup"><span data-stu-id="41b0f-177">The *Data volume by solution* chart shows the volume of data that is sent by each solution and the solutions sending the most data.</span></span> <span data-ttu-id="41b0f-178">頂端的圖表會顯示每個解決方案在一段時間內傳送的資料總量。</span><span class="sxs-lookup"><span data-stu-id="41b0f-178">The chart at the top shows the total volume of data that is sent by each solution over time.</span></span> <span data-ttu-id="41b0f-179">此資訊可讓您識別解決方案在一段時間內傳送更多資料、大約相同數量的資料或較少的資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-179">This information allows you to identify whether a solution is sending more data, about the same amount of data, or less data over time.</span></span> <span data-ttu-id="41b0f-180">解決方案清單會顯示 10 個傳送大部分資料的解決方案。</span><span class="sxs-lookup"><span data-stu-id="41b0f-180">The list of solutions shows the 10 solutions sending the most data.</span></span> 

<span data-ttu-id="41b0f-181">這兩個圖表顯示了所有資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-181">These two charts show all data.</span></span> <span data-ttu-id="41b0f-182">某些資料已可計費，其他資料則為免費。</span><span class="sxs-lookup"><span data-stu-id="41b0f-182">Some data is billable, and other data is free.</span></span> <span data-ttu-id="41b0f-183">若要僅顯示可計費的資料，請將搜尋頁面上的查詢修改為包括 `IsBillable=true`。</span><span class="sxs-lookup"><span data-stu-id="41b0f-183">To focus only on data that billable, modify the query on the search page to include `IsBillable=true`.</span></span>  

![資料量圖表](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

<span data-ttu-id="41b0f-185">查看「一段時間的資料量」圖表。</span><span class="sxs-lookup"><span data-stu-id="41b0f-185">Look at the *Data volume over time* chart.</span></span> <span data-ttu-id="41b0f-186">若要查看針對特定電腦傳送最多資料的解決方案和資料類型，請按一下電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="41b0f-186">To see the solutions and data types that are sending the most data for a specific computer, click on the name of the computer.</span></span> <span data-ttu-id="41b0f-187">按一下清單中第一部電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="41b0f-187">Click on the name of the first computer in the list.</span></span>

<span data-ttu-id="41b0f-188">在下列螢幕擷取畫面中，「記錄管理/效能」資料類型針對此電腦傳送最多資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-188">In the following screenshot, the *Log Management / Perf* data type is sending the most data for the computer.</span></span> 

![電腦的資料磁碟區](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

<span data-ttu-id="41b0f-190">接下來，回到「使用量」儀表板並查看「依解決方案的資料磁碟區」圖表。</span><span class="sxs-lookup"><span data-stu-id="41b0f-190">Next, go back to the *Usage* dashboard and look at the *Data volume by solution* chart.</span></span> <span data-ttu-id="41b0f-191">若要查看針對某個解決方案傳送最多資料的電腦，請按一下清單中的解決方案名稱。</span><span class="sxs-lookup"><span data-stu-id="41b0f-191">To see the computers sending the most data for a solution, click on the name of the solution in the list.</span></span> <span data-ttu-id="41b0f-192">按一下清單中第一個解決方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="41b0f-192">Click on the name of the first solution in the list.</span></span> 

<span data-ttu-id="41b0f-193">在下列螢幕擷取畫面中，它會確認 acmetomcat 電腦針對記錄管理解決方案傳送最多資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-193">In the following screenshot, it confirms that the *acmetomcat* computer is sending the most data for the Log Management solution.</span></span>

![解決方案的資料量](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

<span data-ttu-id="41b0f-195">如有需要，請執行其他分析，找出解決方案或資料類型中的大型磁碟區。</span><span class="sxs-lookup"><span data-stu-id="41b0f-195">If needed, perform additional analysis to identify large volumes within a solution or data type.</span></span> <span data-ttu-id="41b0f-196">查詢範例包括：</span><span class="sxs-lookup"><span data-stu-id="41b0f-196">Example queries include:</span></span>

+ <span data-ttu-id="41b0f-197">**安全性**解決方案</span><span class="sxs-lookup"><span data-stu-id="41b0f-197">**Security** solution</span></span>
  - `Type=SecurityEvent | measure count() by EventID`
+ <span data-ttu-id="41b0f-198">**記錄管理**解決方案</span><span class="sxs-lookup"><span data-stu-id="41b0f-198">**Log Management** solution</span></span>
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ <span data-ttu-id="41b0f-199">**Perf** 資料類型</span><span class="sxs-lookup"><span data-stu-id="41b0f-199">**Perf** data type</span></span>
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ <span data-ttu-id="41b0f-200">**Event** 資料類型</span><span class="sxs-lookup"><span data-stu-id="41b0f-200">**Event** data type</span></span>
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ <span data-ttu-id="41b0f-201">**Syslog** 資料類型</span><span class="sxs-lookup"><span data-stu-id="41b0f-201">**Syslog** data type</span></span>
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ <span data-ttu-id="41b0f-202">**AzureDiagnostics** 資料類型</span><span class="sxs-lookup"><span data-stu-id="41b0f-202">**AzureDiagnostics** data type</span></span>
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

<span data-ttu-id="41b0f-203">使用下列步驟來減少所收集的記錄數量：</span><span class="sxs-lookup"><span data-stu-id="41b0f-203">Use the following steps to reduce the volume of logs collected:</span></span>

| <span data-ttu-id="41b0f-204">高資料量的來源</span><span class="sxs-lookup"><span data-stu-id="41b0f-204">Source of high data volume</span></span> | <span data-ttu-id="41b0f-205">如何縮減資料量</span><span class="sxs-lookup"><span data-stu-id="41b0f-205">How to reduce data volume</span></span> |
| -------------------------- | ------------------------- |
| <span data-ttu-id="41b0f-206">安全性事件</span><span class="sxs-lookup"><span data-stu-id="41b0f-206">Security events</span></span>            | <span data-ttu-id="41b0f-207">選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span><span class="sxs-lookup"><span data-stu-id="41b0f-207">Select [common or minimal security events](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span></span> <br> <span data-ttu-id="41b0f-208">變更安全性稽核原則為只收集所需事件。</span><span class="sxs-lookup"><span data-stu-id="41b0f-208">Change the security audit policy to collect only needed events.</span></span> <span data-ttu-id="41b0f-209">特別檢閱下列原則是否需要收集事件：</span><span class="sxs-lookup"><span data-stu-id="41b0f-209">In particular, review the need to collect events for</span></span> <br> <span data-ttu-id="41b0f-210">- [a稽核篩選平台](https://technet.microsoft.com/library/dd772749(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="41b0f-210">- [audit filtering platform](https://technet.microsoft.com/library/dd772749(WS.10).aspx)</span></span> <br> <span data-ttu-id="41b0f-211">- [稽核登錄](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)</span><span class="sxs-lookup"><span data-stu-id="41b0f-211">- [audit registry](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)</span></span><br> <span data-ttu-id="41b0f-212">- [稽核檔案系統](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)</span><span class="sxs-lookup"><span data-stu-id="41b0f-212">- [audit file system](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)</span></span><br> <span data-ttu-id="41b0f-213">- [稽核核心物件](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)</span><span class="sxs-lookup"><span data-stu-id="41b0f-213">- [audit kernel object](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)</span></span><br> <span data-ttu-id="41b0f-214">- [稽核控制代碼操作](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)</span><span class="sxs-lookup"><span data-stu-id="41b0f-214">- [audit handle manipulation](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)</span></span><br> <span data-ttu-id="41b0f-215">- [稽核抽取式存放裝置 ](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage)</span><span class="sxs-lookup"><span data-stu-id="41b0f-215">- [audit removable storage](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage)</span></span> |
| <span data-ttu-id="41b0f-216">效能計數器</span><span class="sxs-lookup"><span data-stu-id="41b0f-216">Performance counters</span></span>       | <span data-ttu-id="41b0f-217">變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)以：</span><span class="sxs-lookup"><span data-stu-id="41b0f-217">Change [performance counter configuration](log-analytics-data-sources-performance-counters.md) to:</span></span> <br> <span data-ttu-id="41b0f-218">- 減少收集頻率</span><span class="sxs-lookup"><span data-stu-id="41b0f-218">- Reduce the frequency of collection</span></span> <br> <span data-ttu-id="41b0f-219">- 減少效能計數器的數目</span><span class="sxs-lookup"><span data-stu-id="41b0f-219">- Reduce number of performance counters</span></span> |
| <span data-ttu-id="41b0f-220">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="41b0f-220">Event logs</span></span>                 | <span data-ttu-id="41b0f-221">變更[事件記錄組態](log-analytics-data-sources-windows-events.md)以：</span><span class="sxs-lookup"><span data-stu-id="41b0f-221">Change [event log configuration](log-analytics-data-sources-windows-events.md) to:</span></span> <br> <span data-ttu-id="41b0f-222">- 減少所收集的事件記錄數目</span><span class="sxs-lookup"><span data-stu-id="41b0f-222">- Reduce the number of event logs collected</span></span> <br> <span data-ttu-id="41b0f-223">- 只收集必要的事件層級。</span><span class="sxs-lookup"><span data-stu-id="41b0f-223">- Collect only required event levels.</span></span> <span data-ttu-id="41b0f-224">例如，不要收集「資訊」層級事件</span><span class="sxs-lookup"><span data-stu-id="41b0f-224">For example, do not collect *Information* level events</span></span> |
| <span data-ttu-id="41b0f-225">syslog</span><span class="sxs-lookup"><span data-stu-id="41b0f-225">Syslog</span></span>                     | <span data-ttu-id="41b0f-226">變更 [Syslog 組態](log-analytics-data-sources-syslog.md)以：</span><span class="sxs-lookup"><span data-stu-id="41b0f-226">Change [syslog configuration](log-analytics-data-sources-syslog.md) to:</span></span> <br> <span data-ttu-id="41b0f-227">- 減少所收集的設施數目</span><span class="sxs-lookup"><span data-stu-id="41b0f-227">- Reduce the number of facilities collected</span></span> <br> <span data-ttu-id="41b0f-228">- 只收集必要的事件層級。</span><span class="sxs-lookup"><span data-stu-id="41b0f-228">- Collect only required event levels.</span></span> <span data-ttu-id="41b0f-229">例如，不要收集「資訊」和「偵錯」層級事件</span><span class="sxs-lookup"><span data-stu-id="41b0f-229">For example, do not collect *Info* and *Debug* level events</span></span> |
| <span data-ttu-id="41b0f-230">AzureDiagnostics</span><span class="sxs-lookup"><span data-stu-id="41b0f-230">AzureDiagnostics</span></span>           | <span data-ttu-id="41b0f-231">變更資源記錄集合：</span><span class="sxs-lookup"><span data-stu-id="41b0f-231">Change resource log collection to:</span></span> <br> <span data-ttu-id="41b0f-232">- 減少會將記錄傳送至 Log Analytics 的資源數目</span><span class="sxs-lookup"><span data-stu-id="41b0f-232">- Reduce the number of resources send logs to Log Analytics</span></span> <br> <span data-ttu-id="41b0f-233">- 只收集必要的記錄</span><span class="sxs-lookup"><span data-stu-id="41b0f-233">- Collect only required logs</span></span> |
| <span data-ttu-id="41b0f-234">電腦中不需要解決方案的方案資料</span><span class="sxs-lookup"><span data-stu-id="41b0f-234">Solution data from computers that don't need the solution</span></span> | <span data-ttu-id="41b0f-235">使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)，只從必要的電腦群組收集資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-235">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) to collect data from only required groups of computers.</span></span> |

### <a name="check-if-there-are-more-nodes-than-expected"></a><span data-ttu-id="41b0f-236">檢查是否有比預期更多的節點</span><span class="sxs-lookup"><span data-stu-id="41b0f-236">Check if there are more nodes than expected</span></span>
<span data-ttu-id="41b0f-237">如果您是在「每節點 (OMS)」定價層上，系統便會根據您使用的節點和解決方案數目來向您收費。</span><span class="sxs-lookup"><span data-stu-id="41b0f-237">If you are on the *per node (OMS)* pricing tier, then you are charged based on the number of nodes and solutions you use.</span></span> <span data-ttu-id="41b0f-238">您可以在使用量儀表板的 [供應項目] 區段中，查看每個供應項目目前使用的節點數。</span><span class="sxs-lookup"><span data-stu-id="41b0f-238">You can see how many nodes of each offer are being used in the *offerings* section of the usage dashboard.</span></span>

![使用量儀表板](./media/log-analytics-usage/log-analytics-usage-offerings.png)

<span data-ttu-id="41b0f-240">按一下 [查看所有...] 以檢視針對所選供應項目傳送資料的完整電腦清單。</span><span class="sxs-lookup"><span data-stu-id="41b0f-240">Click on **See all...** to view the full list of computers sending data for the selected offer.</span></span>

<span data-ttu-id="41b0f-241">使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)，只從必要的電腦群組收集資料。</span><span class="sxs-lookup"><span data-stu-id="41b0f-241">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) to collect data from only required groups of computers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="41b0f-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41b0f-242">Next steps</span></span>
* <span data-ttu-id="41b0f-243">請參閱 [Log Analytics 中的記錄搜尋](log-analytics-log-searches.md)，以了解如何使用搜尋語言。</span><span class="sxs-lookup"><span data-stu-id="41b0f-243">See [Log searches in Log Analytics](log-analytics-log-searches.md) to learn how to use the search language.</span></span> <span data-ttu-id="41b0f-244">您可以使用搜尋查詢，對使用量資料執行額外的分析。</span><span class="sxs-lookup"><span data-stu-id="41b0f-244">You can use search queries to perform additional analysis on the usage data.</span></span>
* <span data-ttu-id="41b0f-245">使用[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)中所述的步驟，可在符合搜尋條件時收到通知</span><span class="sxs-lookup"><span data-stu-id="41b0f-245">Use the steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) to be notified when a search criteria is met</span></span>
* <span data-ttu-id="41b0f-246">使用[解決方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)，只從必要的電腦群組收集資料</span><span class="sxs-lookup"><span data-stu-id="41b0f-246">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) to collect data from only required groups of computers</span></span>
* <span data-ttu-id="41b0f-247">選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span><span class="sxs-lookup"><span data-stu-id="41b0f-247">Select [common or minimal security events](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span></span>
* <span data-ttu-id="41b0f-248">變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)</span><span class="sxs-lookup"><span data-stu-id="41b0f-248">Change [performance counter configuration](log-analytics-data-sources-performance-counters.md)</span></span>
* <span data-ttu-id="41b0f-249">變更[事件記錄組態](log-analytics-data-sources-windows-events.md)</span><span class="sxs-lookup"><span data-stu-id="41b0f-249">Change [event log configuration](log-analytics-data-sources-windows-events.md)</span></span>
* <span data-ttu-id="41b0f-250">變更 [Syslog 組態](log-analytics-data-sources-syslog.md)</span><span class="sxs-lookup"><span data-stu-id="41b0f-250">Change [syslog configuration](log-analytics-data-sources-syslog.md)</span></span>
