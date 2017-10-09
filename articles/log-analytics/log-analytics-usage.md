---
title: "記錄分析 aaaAnalyze 資料使用量 |Microsoft 文件"
description: "使用多少資料正在傳送 toohello 記錄分析服務，及進行疑難排解，傳送大量資料的記錄分析 tooview hello 使用量儀表板。"
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
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a><span data-ttu-id="17b90-103">在 Log Analytics 中分析資料使用量</span><span class="sxs-lookup"><span data-stu-id="17b90-103">Analyze data usage in Log Analytics</span></span>
<span data-ttu-id="17b90-104">記錄分析包含 hello 收集的資料量，電腦會傳送 hello 資料和 hello 不同類型的資料傳送的資訊。</span><span class="sxs-lookup"><span data-stu-id="17b90-104">Log Analytics includes information on hello amount of data collected, which computers sent hello data and hello different types of data sent.</span></span>  <span data-ttu-id="17b90-105">使用 hello**記錄分析使用量**儀表板 toosee hello 資料量傳送 toohello 記錄分析服務。</span><span class="sxs-lookup"><span data-stu-id="17b90-105">Use hello **Log Analytics Usage** dashboard toosee hello amount of data sent toohello Log Analytics service.</span></span> <span data-ttu-id="17b90-106">hello 儀表板顯示每個解決方案收集資料量和資料量您的電腦所傳送。</span><span class="sxs-lookup"><span data-stu-id="17b90-106">hello dashboard shows how much data is collected by each solution and how much data your computers are sending.</span></span>

## <a name="understand-hello-usage-dashboard"></a><span data-ttu-id="17b90-107">了解 hello 使用量儀表板</span><span class="sxs-lookup"><span data-stu-id="17b90-107">Understand hello Usage dashboard</span></span>
<span data-ttu-id="17b90-108">hello**記錄分析使用狀況**儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="17b90-108">hello **Log Analytics usage** dashboard displays hello following information:</span></span>

- <span data-ttu-id="17b90-109">資料量</span><span class="sxs-lookup"><span data-stu-id="17b90-109">Data volume</span></span>
    - <span data-ttu-id="17b90-110">一段時間 (根據您目前的時間範圍) 的資料量</span><span class="sxs-lookup"><span data-stu-id="17b90-110">Data volume over time (based on your current time scope)</span></span>
    - <span data-ttu-id="17b90-111">依方案分類的資料量</span><span class="sxs-lookup"><span data-stu-id="17b90-111">Data volume by solution</span></span>
    - <span data-ttu-id="17b90-112">與電腦不相關的資料</span><span class="sxs-lookup"><span data-stu-id="17b90-112">Data not associated with a computer</span></span>
- <span data-ttu-id="17b90-113">電腦</span><span class="sxs-lookup"><span data-stu-id="17b90-113">Computers</span></span>
    - <span data-ttu-id="17b90-114">傳送資料的電腦</span><span class="sxs-lookup"><span data-stu-id="17b90-114">Computers sending data</span></span>
    - <span data-ttu-id="17b90-115">過去 24 小時內沒有資料的電腦</span><span class="sxs-lookup"><span data-stu-id="17b90-115">Computers with no data in last 24 hours</span></span>
- <span data-ttu-id="17b90-116">供應項目</span><span class="sxs-lookup"><span data-stu-id="17b90-116">Offerings</span></span>
    - <span data-ttu-id="17b90-117">深入解析和分析節點</span><span class="sxs-lookup"><span data-stu-id="17b90-117">Insight and Analytics nodes</span></span>
    - <span data-ttu-id="17b90-118">自動化和控制節點</span><span class="sxs-lookup"><span data-stu-id="17b90-118">Automation and Control nodes</span></span>
    - <span data-ttu-id="17b90-119">安全性節點</span><span class="sxs-lookup"><span data-stu-id="17b90-119">Security nodes</span></span>
- <span data-ttu-id="17b90-120">效能</span><span class="sxs-lookup"><span data-stu-id="17b90-120">Performance</span></span>
    - <span data-ttu-id="17b90-121">時間 toocollect 和索引的資料</span><span class="sxs-lookup"><span data-stu-id="17b90-121">Time taken toocollect and index data</span></span>
- <span data-ttu-id="17b90-122">查詢清單</span><span class="sxs-lookup"><span data-stu-id="17b90-122">List of queries</span></span>

![使用量儀表板](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a><span data-ttu-id="17b90-124">toowork 與使用量資料</span><span class="sxs-lookup"><span data-stu-id="17b90-124">toowork with usage data</span></span>
1. <span data-ttu-id="17b90-125">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="17b90-125">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com) using your Azure subscription.</span></span>
2. <span data-ttu-id="17b90-126">在 hello**中樞**功能表上，按一下 [**更多服務**hello] 清單中的資源，在輸入**記錄分析**。</span><span class="sxs-lookup"><span data-stu-id="17b90-126">On hello **Hub** menu, click **More services** and in hello list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="17b90-127">當您開始輸入 hello 清單會篩選根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="17b90-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="17b90-128">按一下 [Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="17b90-128">Click **Log Analytics**.</span></span>  
    <span data-ttu-id="17b90-129">![Azure 中樞](./media/log-analytics-usage/hub.png)</span><span class="sxs-lookup"><span data-stu-id="17b90-129">![Azure hub](./media/log-analytics-usage/hub.png)</span></span>
3. <span data-ttu-id="17b90-130">hello**記錄分析**儀表板會顯示您的工作區的清單。</span><span class="sxs-lookup"><span data-stu-id="17b90-130">hello **Log Analytics** dashboard shows a list of your workspaces.</span></span> <span data-ttu-id="17b90-131">選取工作區。</span><span class="sxs-lookup"><span data-stu-id="17b90-131">Select a workspace.</span></span>
4. <span data-ttu-id="17b90-132">在 hello*工作區*儀表板，按一下**記錄分析使用狀況**。</span><span class="sxs-lookup"><span data-stu-id="17b90-132">In hello *workspace* dashboard, click **Log Analytics usage**.</span></span>
5. <span data-ttu-id="17b90-133">在 hello**記錄分析使用量**儀表板，按一下**時間： 過去 24 小時**toochange hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="17b90-133">On hello **Log Analytics Usage** dashboard, click **Time: Last 24 hours** toochange hello time interval.</span></span>  
    <span data-ttu-id="17b90-134">![時間間隔](./media/log-analytics-usage/time.png)</span><span class="sxs-lookup"><span data-stu-id="17b90-134">![time interval](./media/log-analytics-usage/time.png)</span></span>
6. <span data-ttu-id="17b90-135">檢視 hello 使用量類別刀鋒視窗的顯示區域您感興趣。</span><span class="sxs-lookup"><span data-stu-id="17b90-135">View hello usage category blades that show areas you’re interested in.</span></span> <span data-ttu-id="17b90-136">選擇在刀鋒視窗，然後按一下的 tooview 更多詳細資料中的項目[記錄搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="17b90-136">Choose a blade and then click an item in it tooview more details in [Log Search](log-analytics-log-searches.md).</span></span>  
    <span data-ttu-id="17b90-137">![範例資料使用量刀鋒視窗](./media/log-analytics-usage/blade.png)</span><span class="sxs-lookup"><span data-stu-id="17b90-137">![example data usage blade](./media/log-analytics-usage/blade.png)</span></span>
7. <span data-ttu-id="17b90-138">Hello 記錄搜尋儀表板上檢閱 hello 結果所傳回的 hello 搜尋。</span><span class="sxs-lookup"><span data-stu-id="17b90-138">On hello Log Search dashboard, review hello results that are returned from hello search.</span></span>  
    ![範例使用量記錄檔搜尋](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a><span data-ttu-id="17b90-140">當資料收集高於預期時建立警示</span><span class="sxs-lookup"><span data-stu-id="17b90-140">Create an alert when data collection is higher than expected</span></span>
<span data-ttu-id="17b90-141">本章節描述如何 toocreate 警示時：</span><span class="sxs-lookup"><span data-stu-id="17b90-141">This section describes how toocreate an alert if:</span></span>
- <span data-ttu-id="17b90-142">資料量超出指定的數量。</span><span class="sxs-lookup"><span data-stu-id="17b90-142">Data volume exceeds a specified amount.</span></span>
- <span data-ttu-id="17b90-143">資料磁碟區是預測的 tooexceed 指定的數量。</span><span class="sxs-lookup"><span data-stu-id="17b90-143">Data volume is predicted tooexceed a specified amount.</span></span>

<span data-ttu-id="17b90-144">Log Analytics [警示](log-analytics-alerts-creating.md)會使用搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="17b90-144">Log Analytics [alerts](log-analytics-alerts-creating.md) use search queries.</span></span> <span data-ttu-id="17b90-145">hello 下列查詢的結果沒有超過 100 GB hello 過去 24 小時所收集的資料時：</span><span class="sxs-lookup"><span data-stu-id="17b90-145">hello following query has a result when there is more than 100 GB of data collected in hello last 24 hours:</span></span>

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

<span data-ttu-id="17b90-146">hello 下列查詢會使用簡單公式 toopredict 超過 100 GB 的資料會傳送一天中時：</span><span class="sxs-lookup"><span data-stu-id="17b90-146">hello following query uses a simple formula toopredict when more than 100 GB of data will be sent in a day:</span></span> 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

<span data-ttu-id="17b90-147">tooalert 上不同的資料磁碟區，變更 hello 100 hello 查詢 toohello 您想要 tooalert GB 數。</span><span class="sxs-lookup"><span data-stu-id="17b90-147">tooalert on a different data volume, change hello 100 in hello queries toohello number of GB you want tooalert on.</span></span>

<span data-ttu-id="17b90-148">使用中所述的 hello 步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)toobe 超過預期資料收集時收到通知。</span><span class="sxs-lookup"><span data-stu-id="17b90-148">Use hello steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notified when data collection is higher than expected.</span></span>

<span data-ttu-id="17b90-149">在 24 小時內沒有超過 100 GB 的資料時，請建立 hello 警示 hello 第一個查詢，設定:</span><span class="sxs-lookup"><span data-stu-id="17b90-149">When creating hello alert for hello first query -- when there is more than 100 GB of data in 24 hours, set the:</span></span>
- <span data-ttu-id="17b90-150">**名稱**太*大於 24 小時內的 100 GB 資料磁碟區*</span><span class="sxs-lookup"><span data-stu-id="17b90-150">**Name** too*Data volume greater than 100 GB in 24 hours*</span></span>
- <span data-ttu-id="17b90-151">**嚴重性**太*警告*</span><span class="sxs-lookup"><span data-stu-id="17b90-151">**Severity** too*Warning*</span></span>
- <span data-ttu-id="17b90-152">**搜尋查詢**太`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`</span><span class="sxs-lookup"><span data-stu-id="17b90-152">**Search query** too`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`</span></span>
- <span data-ttu-id="17b90-153">**時間間隔**太*24 小時*。</span><span class="sxs-lookup"><span data-stu-id="17b90-153">**Time window** too*24 Hours*.</span></span>
- <span data-ttu-id="17b90-154">**警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。</span><span class="sxs-lookup"><span data-stu-id="17b90-154">**Alert frequency** toobe one hour since hello usage data only updates once per hour.</span></span>
- <span data-ttu-id="17b90-155">**產生警示根據**toobe*的結果數目*</span><span class="sxs-lookup"><span data-stu-id="17b90-155">**Generate alert based on** toobe *number of results*</span></span>
- <span data-ttu-id="17b90-156">**結果數目**toobe*大於 0*</span><span class="sxs-lookup"><span data-stu-id="17b90-156">**Number of results** toobe *Greater than 0*</span></span>

<span data-ttu-id="17b90-157">使用中所述的 hello 步驟[新增動作 tooalert 規則](log-analytics-alerts-actions.md)設定電子郵件、 webhook 或 runbook hello 警示規則的動作。</span><span class="sxs-lookup"><span data-stu-id="17b90-157">Use hello steps described in [add actions tooalert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for hello alert rule.</span></span>

<span data-ttu-id="17b90-158">當 hello 第二個查詢建立 hello 警示時預測 24 小時內，將會超過 100 GB 資料的設定:</span><span class="sxs-lookup"><span data-stu-id="17b90-158">When creating hello alert for hello second query -- when it is predicted that there will be more than 100 GB of data in 24 hours, set the:</span></span>
- <span data-ttu-id="17b90-159">**名稱**太*資料磁碟區中必須要有 100 GB 以上 toogreater 24 小時*</span><span class="sxs-lookup"><span data-stu-id="17b90-159">**Name** too*Data volume expected toogreater than 100 GB in 24 hours*</span></span>
- <span data-ttu-id="17b90-160">**嚴重性**太*警告*</span><span class="sxs-lookup"><span data-stu-id="17b90-160">**Severity** too*Warning*</span></span>
- <span data-ttu-id="17b90-161">**搜尋查詢**太`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`</span><span class="sxs-lookup"><span data-stu-id="17b90-161">**Search query** too`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`</span></span>
- <span data-ttu-id="17b90-162">**時間間隔**太*過去 3 小時內*。</span><span class="sxs-lookup"><span data-stu-id="17b90-162">**Time window** too*3 Hours*.</span></span>
- <span data-ttu-id="17b90-163">**警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。</span><span class="sxs-lookup"><span data-stu-id="17b90-163">**Alert frequency** toobe one hour since hello usage data only updates once per hour.</span></span>
- <span data-ttu-id="17b90-164">**產生警示根據**toobe*的結果數目*</span><span class="sxs-lookup"><span data-stu-id="17b90-164">**Generate alert based on** toobe *number of results*</span></span>
- <span data-ttu-id="17b90-165">**結果數目**toobe*大於 0*</span><span class="sxs-lookup"><span data-stu-id="17b90-165">**Number of results** toobe *Greater than 0*</span></span>

<span data-ttu-id="17b90-166">當您收到警示時，請使用下列區段 tootroubleshoot 為什麼使用量會超過預期的 hello hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="17b90-166">When you receive an alert, use hello steps in hello following section tootroubleshoot why usage is higher than expected.</span></span>

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a><span data-ttu-id="17b90-167">針對使用量高於預期的原因進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="17b90-167">Troubleshooting why usage is higher than expected</span></span>
<span data-ttu-id="17b90-168">hello 使用量儀表板可幫助您 tooidentify 為什麼使用量 （並因此成本） 高於您預期。</span><span class="sxs-lookup"><span data-stu-id="17b90-168">hello usage dashboard helps you tooidentify why usage (and therefore cost) is higher than you are expecting.</span></span>

<span data-ttu-id="17b90-169">較高的使用量是由下列一個或兩個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="17b90-169">Higher usage is caused by one, or both of:</span></span>
- <span data-ttu-id="17b90-170">超過預期傳送 tooLog 分析的資料</span><span class="sxs-lookup"><span data-stu-id="17b90-170">More data than expected being sent tooLog Analytics</span></span>
- <span data-ttu-id="17b90-171">更多的節點比預期傳送資料 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="17b90-171">More nodes than expected sending data tooLog Analytics</span></span>

### <a name="check-if-there-is-more-data-than-expected"></a><span data-ttu-id="17b90-172">檢查是否有比預期更多的資料</span><span class="sxs-lookup"><span data-stu-id="17b90-172">Check if there is more data than expected</span></span> 
<span data-ttu-id="17b90-173">有兩個主要區段 hello 方式 頁面，協助您識別造成大多數資料 toobe 收集的 hello。</span><span class="sxs-lookup"><span data-stu-id="17b90-173">There are two key sections of hello usage page that help identify what is causing hello most data toobe collected.</span></span>

<span data-ttu-id="17b90-174">hello*經過一段時間的資料量*圖表可顯示 hello 總傳送的資料量和 hello 電腦傳送 hello 大部分的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-174">hello *Data volume over time* chart shows hello total volume of data sent and hello computers sending hello most data.</span></span> <span data-ttu-id="17b90-175">hello hello 頂端的圖表可讓您 toosee 如果整體資料使用量成長，剩餘穩定或遞減。</span><span class="sxs-lookup"><span data-stu-id="17b90-175">hello chart at hello top allows you toosee if your overall data usage is growing, remaining steady or decreasing.</span></span> <span data-ttu-id="17b90-176">hello 的電腦清單會顯示 hello 10 電腦傳送嗨大部分的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-176">hello list of computers shows hello 10 computers sending hello most data.</span></span>

<span data-ttu-id="17b90-177">hello*解決方案的資料量*圖表可顯示 hello 磁碟區的每個方案和大部分的資料傳送嗨 hello 解決方案所傳送的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-177">hello *Data volume by solution* chart shows hello volume of data that is sent by each solution and hello solutions sending hello most data.</span></span> <span data-ttu-id="17b90-178">在 hello 最上方的 hello 圖表可顯示 hello 總每個方案所傳送的一段時間的資料量。</span><span class="sxs-lookup"><span data-stu-id="17b90-178">hello chart at hello top shows hello total volume of data that is sent by each solution over time.</span></span> <span data-ttu-id="17b90-179">這項資訊可讓您 tooidentify 是否方案傳送的 hello 相同數量的資料，或小於資料一段時間相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-179">This information allows you tooidentify whether a solution is sending more data, about hello same amount of data, or less data over time.</span></span> <span data-ttu-id="17b90-180">解決方案 hello 清單顯示 hello 10 解決方案傳送嗨大部分的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-180">hello list of solutions shows hello 10 solutions sending hello most data.</span></span> 

<span data-ttu-id="17b90-181">這兩個圖表顯示了所有資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-181">These two charts show all data.</span></span> <span data-ttu-id="17b90-182">某些資料已可計費，其他資料則為免費。</span><span class="sxs-lookup"><span data-stu-id="17b90-182">Some data is billable, and other data is free.</span></span> <span data-ttu-id="17b90-183">只在資料也會列入計費上, toofocus 修改 hello 搜尋頁面 tooinclude hello 查詢`IsBillable=true`。</span><span class="sxs-lookup"><span data-stu-id="17b90-183">toofocus only on data that billable, modify hello query on hello search page tooinclude `IsBillable=true`.</span></span>  

![資料量圖表](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

<span data-ttu-id="17b90-185">查看 hello*經過一段時間的資料量*圖表。</span><span class="sxs-lookup"><span data-stu-id="17b90-185">Look at hello *Data volume over time* chart.</span></span> <span data-ttu-id="17b90-186">toosee hello 方案及傳送 hello 的特定電腦，大部分資料的資料型別按一下 hello hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="17b90-186">toosee hello solutions and data types that are sending hello most data for a specific computer, click on hello name of hello computer.</span></span> <span data-ttu-id="17b90-187">按一下 hello 的 hello hello 清單中的第一部電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="17b90-187">Click on hello name of hello first computer in hello list.</span></span>

<span data-ttu-id="17b90-188">在下列螢幕擷取畫面的 hello，hello*記錄管理 / 效能*資料型別傳送 hello hello 電腦大部分的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-188">In hello following screenshot, hello *Log Management / Perf* data type is sending hello most data for hello computer.</span></span> 

![電腦的資料磁碟區](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

<span data-ttu-id="17b90-190">接下來，請返回 toohello*使用量*儀表板並查看 hello*解決方案的資料量*圖表。</span><span class="sxs-lookup"><span data-stu-id="17b90-190">Next, go back toohello *Usage* dashboard and look at hello *Data volume by solution* chart.</span></span> <span data-ttu-id="17b90-191">hello hello 清單中的 hello 方案名稱按一下 toosee hello 電腦傳送嗨解決方案，大部分的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-191">toosee hello computers sending hello most data for a solution, click on hello name of hello solution in hello list.</span></span> <span data-ttu-id="17b90-192">按一下 hello hello hello 清單中的第一個方案名稱。</span><span class="sxs-lookup"><span data-stu-id="17b90-192">Click on hello name of hello first solution in hello list.</span></span> 

<span data-ttu-id="17b90-193">在下列螢幕擷取畫面的 hello，它會確認該 hello *acmetomcat*電腦傳送嗨 hello 記錄管理解決方案的大部分資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-193">In hello following screenshot, it confirms that hello *acmetomcat* computer is sending hello most data for hello Log Management solution.</span></span>

![解決方案的資料量](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

<span data-ttu-id="17b90-195">如有需要請執行其他分析 tooidentify 大型磁碟區中的方案或資料類型。</span><span class="sxs-lookup"><span data-stu-id="17b90-195">If needed, perform additional analysis tooidentify large volumes within a solution or data type.</span></span> <span data-ttu-id="17b90-196">查詢範例包括：</span><span class="sxs-lookup"><span data-stu-id="17b90-196">Example queries include:</span></span>

+ <span data-ttu-id="17b90-197">**安全性**解決方案</span><span class="sxs-lookup"><span data-stu-id="17b90-197">**Security** solution</span></span>
  - `Type=SecurityEvent | measure count() by EventID`
+ <span data-ttu-id="17b90-198">**記錄管理**解決方案</span><span class="sxs-lookup"><span data-stu-id="17b90-198">**Log Management** solution</span></span>
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ <span data-ttu-id="17b90-199">**Perf** 資料類型</span><span class="sxs-lookup"><span data-stu-id="17b90-199">**Perf** data type</span></span>
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ <span data-ttu-id="17b90-200">**Event** 資料類型</span><span class="sxs-lookup"><span data-stu-id="17b90-200">**Event** data type</span></span>
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ <span data-ttu-id="17b90-201">**Syslog** 資料類型</span><span class="sxs-lookup"><span data-stu-id="17b90-201">**Syslog** data type</span></span>
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ <span data-ttu-id="17b90-202">**AzureDiagnostics** 資料類型</span><span class="sxs-lookup"><span data-stu-id="17b90-202">**AzureDiagnostics** data type</span></span>
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

<span data-ttu-id="17b90-203">使用下列步驟 tooreduce hello 磁碟區的記錄檔收集 hello:</span><span class="sxs-lookup"><span data-stu-id="17b90-203">Use hello following steps tooreduce hello volume of logs collected:</span></span>

| <span data-ttu-id="17b90-204">高資料量的來源</span><span class="sxs-lookup"><span data-stu-id="17b90-204">Source of high data volume</span></span> | <span data-ttu-id="17b90-205">如何 tooreduce 資料磁碟區</span><span class="sxs-lookup"><span data-stu-id="17b90-205">How tooreduce data volume</span></span> |
| -------------------------- | ------------------------- |
| <span data-ttu-id="17b90-206">安全性事件</span><span class="sxs-lookup"><span data-stu-id="17b90-206">Security events</span></span>            | <span data-ttu-id="17b90-207">選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span><span class="sxs-lookup"><span data-stu-id="17b90-207">Select [common or minimal security events](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span></span> <br> <span data-ttu-id="17b90-208">變更 hello 安全性稽核原則只需要 toocollect 事件。</span><span class="sxs-lookup"><span data-stu-id="17b90-208">Change hello security audit policy toocollect only needed events.</span></span> <span data-ttu-id="17b90-209">特別是，檢閱 hello 需要 toocollect 事件</span><span class="sxs-lookup"><span data-stu-id="17b90-209">In particular, review hello need toocollect events for</span></span> <br> <span data-ttu-id="17b90-210">- [a稽核篩選平台](https://technet.microsoft.com/library/dd772749(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="17b90-210">- [audit filtering platform](https://technet.microsoft.com/library/dd772749(WS.10).aspx)</span></span> <br> <span data-ttu-id="17b90-211">- [稽核登錄](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)</span><span class="sxs-lookup"><span data-stu-id="17b90-211">- [audit registry](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)</span></span><br> <span data-ttu-id="17b90-212">- [稽核檔案系統](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)</span><span class="sxs-lookup"><span data-stu-id="17b90-212">- [audit file system](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)</span></span><br> <span data-ttu-id="17b90-213">- [稽核核心物件](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)</span><span class="sxs-lookup"><span data-stu-id="17b90-213">- [audit kernel object](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)</span></span><br> <span data-ttu-id="17b90-214">- [稽核控制代碼操作](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)</span><span class="sxs-lookup"><span data-stu-id="17b90-214">- [audit handle manipulation](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)</span></span><br> <span data-ttu-id="17b90-215">- [稽核抽取式存放裝置 ](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage)</span><span class="sxs-lookup"><span data-stu-id="17b90-215">- [audit removable storage](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage)</span></span> |
| <span data-ttu-id="17b90-216">效能計數器</span><span class="sxs-lookup"><span data-stu-id="17b90-216">Performance counters</span></span>       | <span data-ttu-id="17b90-217">變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)以：</span><span class="sxs-lookup"><span data-stu-id="17b90-217">Change [performance counter configuration](log-analytics-data-sources-performance-counters.md) to:</span></span> <br> <span data-ttu-id="17b90-218">-減少收集頻率 hello</span><span class="sxs-lookup"><span data-stu-id="17b90-218">- Reduce hello frequency of collection</span></span> <br> <span data-ttu-id="17b90-219">- 減少效能計數器的數目</span><span class="sxs-lookup"><span data-stu-id="17b90-219">- Reduce number of performance counters</span></span> |
| <span data-ttu-id="17b90-220">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="17b90-220">Event logs</span></span>                 | <span data-ttu-id="17b90-221">變更[事件記錄組態](log-analytics-data-sources-windows-events.md)以：</span><span class="sxs-lookup"><span data-stu-id="17b90-221">Change [event log configuration](log-analytics-data-sources-windows-events.md) to:</span></span> <br> <span data-ttu-id="17b90-222">-Hello 的減少所收集的事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="17b90-222">- Reduce hello number of event logs collected</span></span> <br> <span data-ttu-id="17b90-223">- 只收集必要的事件層級。</span><span class="sxs-lookup"><span data-stu-id="17b90-223">- Collect only required event levels.</span></span> <span data-ttu-id="17b90-224">例如，不要收集「資訊」層級事件</span><span class="sxs-lookup"><span data-stu-id="17b90-224">For example, do not collect *Information* level events</span></span> |
| <span data-ttu-id="17b90-225">syslog</span><span class="sxs-lookup"><span data-stu-id="17b90-225">Syslog</span></span>                     | <span data-ttu-id="17b90-226">變更 [Syslog 組態](log-analytics-data-sources-syslog.md)以：</span><span class="sxs-lookup"><span data-stu-id="17b90-226">Change [syslog configuration](log-analytics-data-sources-syslog.md) to:</span></span> <br> <span data-ttu-id="17b90-227">-減少收集設備的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="17b90-227">- Reduce hello number of facilities collected</span></span> <br> <span data-ttu-id="17b90-228">- 只收集必要的事件層級。</span><span class="sxs-lookup"><span data-stu-id="17b90-228">- Collect only required event levels.</span></span> <span data-ttu-id="17b90-229">例如，不要收集「資訊」和「偵錯」層級事件</span><span class="sxs-lookup"><span data-stu-id="17b90-229">For example, do not collect *Info* and *Debug* level events</span></span> |
| <span data-ttu-id="17b90-230">AzureDiagnostics</span><span class="sxs-lookup"><span data-stu-id="17b90-230">AzureDiagnostics</span></span>           | <span data-ttu-id="17b90-231">變更資源記錄集合：</span><span class="sxs-lookup"><span data-stu-id="17b90-231">Change resource log collection to:</span></span> <br> <span data-ttu-id="17b90-232">-Hello 的減少資源傳送記錄檔 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="17b90-232">- Reduce hello number of resources send logs tooLog Analytics</span></span> <br> <span data-ttu-id="17b90-233">- 只收集必要的記錄</span><span class="sxs-lookup"><span data-stu-id="17b90-233">- Collect only required logs</span></span> |
| <span data-ttu-id="17b90-234">不需要 hello 解決方案的電腦中的方案資料</span><span class="sxs-lookup"><span data-stu-id="17b90-234">Solution data from computers that don't need hello solution</span></span> | <span data-ttu-id="17b90-235">使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦。</span><span class="sxs-lookup"><span data-stu-id="17b90-235">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect data from only required groups of computers.</span></span> |

### <a name="check-if-there-are-more-nodes-than-expected"></a><span data-ttu-id="17b90-236">檢查是否有比預期更多的節點</span><span class="sxs-lookup"><span data-stu-id="17b90-236">Check if there are more nodes than expected</span></span>
<span data-ttu-id="17b90-237">如果您在 hello*每個節點 (OMS)*定價層，然後向您收費根據 hello 數目節點和您使用的方案。</span><span class="sxs-lookup"><span data-stu-id="17b90-237">If you are on hello *per node (OMS)* pricing tier, then you are charged based on hello number of nodes and solutions you use.</span></span> <span data-ttu-id="17b90-238">您可以看到 hello 中正使用多少個節點的每個優惠*供應項目*hello 使用量儀表板的區段。</span><span class="sxs-lookup"><span data-stu-id="17b90-238">You can see how many nodes of each offer are being used in hello *offerings* section of hello usage dashboard.</span></span>

![使用量儀表板](./media/log-analytics-usage/log-analytics-usage-offerings.png)

<span data-ttu-id="17b90-240">按一下**查看所有...** tooview hello 電腦的完整清單傳送 hello 選供應項目的資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-240">Click on **See all...** tooview hello full list of computers sending data for hello selected offer.</span></span>

<span data-ttu-id="17b90-241">使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦。</span><span class="sxs-lookup"><span data-stu-id="17b90-241">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect data from only required groups of computers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="17b90-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17b90-242">Next steps</span></span>
* <span data-ttu-id="17b90-243">請參閱[記錄中記錄分析搜尋](log-analytics-log-searches.md)toolearn toouse hello 如何搜尋語言。</span><span class="sxs-lookup"><span data-stu-id="17b90-243">See [Log searches in Log Analytics](log-analytics-log-searches.md) toolearn how toouse hello search language.</span></span> <span data-ttu-id="17b90-244">您可以使用 搜尋查詢 tooperform 其他分析 hello 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="17b90-244">You can use search queries tooperform additional analysis on hello usage data.</span></span>
* <span data-ttu-id="17b90-245">使用中所述的 hello 步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)符合搜尋條件時收到通知的 toobe</span><span class="sxs-lookup"><span data-stu-id="17b90-245">Use hello steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notified when a search criteria is met</span></span>
* <span data-ttu-id="17b90-246">使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦</span><span class="sxs-lookup"><span data-stu-id="17b90-246">Use [solution targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect data from only required groups of computers</span></span>
* <span data-ttu-id="17b90-247">選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span><span class="sxs-lookup"><span data-stu-id="17b90-247">Select [common or minimal security events](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)</span></span>
* <span data-ttu-id="17b90-248">變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)</span><span class="sxs-lookup"><span data-stu-id="17b90-248">Change [performance counter configuration](log-analytics-data-sources-performance-counters.md)</span></span>
* <span data-ttu-id="17b90-249">變更[事件記錄組態](log-analytics-data-sources-windows-events.md)</span><span class="sxs-lookup"><span data-stu-id="17b90-249">Change [event log configuration](log-analytics-data-sources-windows-events.md)</span></span>
* <span data-ttu-id="17b90-250">變更 [Syslog 組態](log-analytics-data-sources-syslog.md)</span><span class="sxs-lookup"><span data-stu-id="17b90-250">Change [syslog configuration](log-analytics-data-sources-syslog.md)</span></span>
