---
title: "服務對應解決方案自學示範 | Microsoft Docs"
description: "服務對應是 Operations Management Suite (OMS) 中的一個解決方案，可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。  這是一個自學示範，會逐步解說如何使用服務對應來識別及診斷 Web 應用程式中的模擬問題。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: c3548d24c74f8ad865b22d6af3490d0b5cc77a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a><span data-ttu-id="e7579-104">Operations Management Suite (OMS) 自學示範 - 服務對應</span><span class="sxs-lookup"><span data-stu-id="e7579-104">Operations Management Suite (OMS) self paced demo - Service Map</span></span>
<span data-ttu-id="e7579-105">這是一個自學示範，會逐步解說如何使用 Operations Management Suite (OMS) 中的[服務對應解決方案](operations-management-suite-service-map.md)來找出及診斷 Web 應用程式中的模擬問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-105">This is a self paced demo that walks through using the [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) to identify and diagnose a simulated problem in a web application.</span></span>  <span data-ttu-id="e7579-106">服務對應可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="e7579-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span>  <span data-ttu-id="e7579-107">它也會合併其他 OMS 服務所收集的資料，協助您分析效能和找出問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-107">It also consolidates data collected by other OMS services to assist you in analyzing performance and identifying issues.</span></span>  <span data-ttu-id="e7579-108">您也會使用 [Log Analytics 中的記錄搜尋](../log-analytics/log-analytics-log-searches.md)，向下切入收集的資料以便找出根本問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to drill down on collected data in order to identify the root problem.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e7579-109">案例描述</span><span class="sxs-lookup"><span data-stu-id="e7579-109">Scenario description</span></span>
<span data-ttu-id="e7579-110">您剛收到一則通知：ACME 客戶入口網站應用程式發生效能問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-110">You've just received a notification that the ACME Customer Portal application is having performance issues.</span></span>  <span data-ttu-id="e7579-111">您所擁有的唯一資訊就是這些問題大約在今天上午 4:00 (太平洋標準時間) 開始出現。</span><span class="sxs-lookup"><span data-stu-id="e7579-111">The only information that you have is that these issues started about 4:00 am PST today.</span></span>  <span data-ttu-id="e7579-112">除了一組 Web 伺服器以外，您並未完全確定入口網站相依的所有元件。</span><span class="sxs-lookup"><span data-stu-id="e7579-112">You aren't entirely sure of all the components that the portal is dependent on other than a set of web servers.</span></span>  

## <a name="components-and-features-used"></a><span data-ttu-id="e7579-113">使用的元件和功能</span><span class="sxs-lookup"><span data-stu-id="e7579-113">Components and features used</span></span>
- [<span data-ttu-id="e7579-114">服務對應解決方案</span><span class="sxs-lookup"><span data-stu-id="e7579-114">Service Map solution</span></span>](operations-management-suite-service-map.md)
- [<span data-ttu-id="e7579-115">Log Analytics 記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="e7579-115">Log Analytics log searches</span></span>](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a><span data-ttu-id="e7579-116">逐步解說</span><span class="sxs-lookup"><span data-stu-id="e7579-116">Walk through</span></span>

### <a name="1-connect-to-the-oms-experience-center"></a><span data-ttu-id="e7579-117">1.連線至 OMS 體驗中心</span><span class="sxs-lookup"><span data-stu-id="e7579-117">1. Connect to the OMS Experience Center</span></span>
<span data-ttu-id="e7579-118">此逐步解說會使用 [Operations Management Suite 體驗中心](https://experience.mms.microsoft.com/)，提供包含範例資料的完整 OMS 環境。</span><span class="sxs-lookup"><span data-stu-id="e7579-118">This walk through uses the [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span></span> <span data-ttu-id="e7579-119">首先遵循此連結，提供您的資訊，然後選取**深入解析與分析**案例。</span><span class="sxs-lookup"><span data-stu-id="e7579-119">Start by following this link, provide your information and then select the **Insight and Analytics** scenario.</span></span>


### <a name="2-start-service-map"></a><span data-ttu-id="e7579-120">2.啟動服務對應</span><span class="sxs-lookup"><span data-stu-id="e7579-120">2. Start Service Map</span></span>
<span data-ttu-id="e7579-121">按一下 [服務對應] 圖格，以啟動服務對應解決方案。</span><span class="sxs-lookup"><span data-stu-id="e7579-121">Start the Service Map solution by clicking on the **Service Map** tile.</span></span>

![服務對應圖格](media/operations-management-suite-walkthrough-servicemap/tile.png)

<span data-ttu-id="e7579-123">服務對應主控台隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="e7579-123">The Service Map console is displayed.</span></span>  <span data-ttu-id="e7579-124">左窗格中有您的環境中已安裝服務對應代理程式的電腦清單。</span><span class="sxs-lookup"><span data-stu-id="e7579-124">In the left pane is a list of computers in your environment with the Service Map agent installed.</span></span>  <span data-ttu-id="e7579-125">您將從這份清單中選取您想要檢視的電腦。</span><span class="sxs-lookup"><span data-stu-id="e7579-125">You'll select the computer that you want to view from this list.</span></span>

![電腦清單](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a><span data-ttu-id="e7579-127">3.檢視電腦</span><span class="sxs-lookup"><span data-stu-id="e7579-127">3. View computer</span></span>
<span data-ttu-id="e7579-128">我們知道，Web 伺服器稱為 AcmeWFE001 和 AcmeWFE002，所以這似乎是合理的起點。</span><span class="sxs-lookup"><span data-stu-id="e7579-128">We know that the web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place to start.</span></span>  <span data-ttu-id="e7579-129">按一下 [AcmeWFE001]。</span><span class="sxs-lookup"><span data-stu-id="e7579-129">Click on **AcmeWFE001**.</span></span>  <span data-ttu-id="e7579-130">這會顯示 AcmeWFE001 與其所有相依性的對應。</span><span class="sxs-lookup"><span data-stu-id="e7579-130">This displays the map for AcmeWFE001 and all of its dependencies.</span></span>  <span data-ttu-id="e7579-131">您可以查看哪些程序正在選取的電腦上執行，以及與其通訊的外部服務。</span><span class="sxs-lookup"><span data-stu-id="e7579-131">You can see which processes are running on the selected computer and which external services they communicate with.</span></span>

![Web 伺服器](media/operations-management-suite-walkthrough-servicemap/web-server.png)

<span data-ttu-id="e7579-133">我們很擔心 Web 應用程式的效能，所以按一下 [AcmeAppPool (IIS 應用程式集區)] 程序。</span><span class="sxs-lookup"><span data-stu-id="e7579-133">We're concerned about the performance of our web application so click on the **AcmeAppPool (IIS App Pool)** process.</span></span>  <span data-ttu-id="e7579-134">這會顯示此程序的詳細資料，並醒目提示其相依性。</span><span class="sxs-lookup"><span data-stu-id="e7579-134">This displays the details for this process and highlights its dependencies.</span></span>  

![應用程式集區](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a><span data-ttu-id="e7579-136">4.變更時間範圍</span><span class="sxs-lookup"><span data-stu-id="e7579-136">4. Change time window</span></span>

<span data-ttu-id="e7579-137">我們聽到問題是在上午 4:00 開始出現，所以讓我們看看該時間發生什麼狀況。</span><span class="sxs-lookup"><span data-stu-id="e7579-137">We heard that the problem started at 4:00 AM so let's have a look at what was happening at that time.</span></span> <span data-ttu-id="e7579-138">按一下 [時間範圍]，將時間變更為太平洋標準時間上午 4:00 (保留目前的日期並針對當地時區進行調整) 並持續 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e7579-138">Click on **Time Range** and change the time to 4:00 AM PST (keep the current date and adjust for your local time zone) with a duration of 20 minutes.</span></span>

![時間選擇器](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a><span data-ttu-id="e7579-140">5.檢視警示</span><span class="sxs-lookup"><span data-stu-id="e7579-140">5. View alert</span></span>

<span data-ttu-id="e7579-141">我們現在看到 **acmetomcat** 相依性顯示警示，因此這是可能的問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-141">We now see that the **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span></span>  <span data-ttu-id="e7579-142">按一下 **acmetomcat** 中的警示圖示，以顯示警示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7579-142">Click on the alert icon in **acmetomcat** to show the details for the alert.</span></span>  <span data-ttu-id="e7579-143">我們可以看到 CPU 使用率有重大警示並可將其展開，以取得更詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="e7579-143">We can see that we have critical CPU utilization and can expand it for more detail.</span></span>  <span data-ttu-id="e7579-144">這可能是造成效能變慢的原因。</span><span class="sxs-lookup"><span data-stu-id="e7579-144">This is probably what's causing our slow performance.</span></span> 

![警示](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a><span data-ttu-id="e7579-146">6.檢視效能</span><span class="sxs-lookup"><span data-stu-id="e7579-146">6. View performance</span></span>

<span data-ttu-id="e7579-147">讓我們仔細看看 **acmetomcat**。</span><span class="sxs-lookup"><span data-stu-id="e7579-147">Let's have a closer look at **acmetomcat**.</span></span>  <span data-ttu-id="e7579-148">按一下右上方的 **acmetomcat**，然後選取 [載入伺服器對應] 以顯示這台電腦的詳細資料和相依性。</span><span class="sxs-lookup"><span data-stu-id="e7579-148">Click in the top right of **acmetomcat** and select **Load Server Map** to show the detail and dependencies for this machine.</span></span> <span data-ttu-id="e7579-149">然後我們可以進一步查看這些效能計數器，以確認我們的懷疑。</span><span class="sxs-lookup"><span data-stu-id="e7579-149">We can then look a bit more into those performance counters to verify our suspicion.</span></span>  <span data-ttu-id="e7579-150">選取 [效能] 索引標籤，以顯示 [Log Analytics 在時間範圍內所收集的效能計數器](../log-analytics/log-analytics-data-sources-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="e7579-150">Select the **Performance** tab to display the [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over the time range.</span></span>  <span data-ttu-id="e7579-151">我們可以看到，我們的處理器和記憶體出現週期性尖峰。</span><span class="sxs-lookup"><span data-stu-id="e7579-151">We can see that we're getting periodic spikes in the processor and memory.</span></span>

![效能](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a><span data-ttu-id="e7579-153">7.檢視變更追蹤</span><span class="sxs-lookup"><span data-stu-id="e7579-153">7. View change tracking</span></span>
<span data-ttu-id="e7579-154">我們來看看是否可以找出可能造成此高使用率的原因。</span><span class="sxs-lookup"><span data-stu-id="e7579-154">Let's see if we can find out what might have caused this high utilization.</span></span>  <span data-ttu-id="e7579-155">按一下 [摘要] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e7579-155">Click on the **Summary** tab.</span></span>  <span data-ttu-id="e7579-156">這會提供 OMS 從電腦收集到的資訊，例如失敗的連線、重大警示，以及軟體變更。</span><span class="sxs-lookup"><span data-stu-id="e7579-156">This provides information that OMS has collected from the computer such as failed connections, critical alerts, and software changes.</span></span>  <span data-ttu-id="e7579-157">具有最新有趣資訊的區段應該已經展開，而您可以展開其他區段來檢查其中包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="e7579-157">Sections with interesting recent information should already be expanded, and you can expand other sections to inspect information that they contain.</span></span>


<span data-ttu-id="e7579-158">如果 [變更追蹤] 尚未開啟，則將它展開。</span><span class="sxs-lookup"><span data-stu-id="e7579-158">If **Change Tracking** isn't already open, then expand it.</span></span>  <span data-ttu-id="e7579-159">這會顯示[變更追蹤解決方案](../log-analytics/log-analytics-change-tracking.md)所收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="e7579-159">This shows information collected by the [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>  <span data-ttu-id="e7579-160">看起來，已在這段期間範圍內進行軟體變更。</span><span class="sxs-lookup"><span data-stu-id="e7579-160">It looks like there was a software change made during this time window.</span></span>  <span data-ttu-id="e7579-161">按一下 [軟體] 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7579-161">Click on **Software** to get details.</span></span>  <span data-ttu-id="e7579-162">備份程序已在上午 4:00 後新增至電腦，因此這似乎耗用過多資源的罪魁禍首。</span><span class="sxs-lookup"><span data-stu-id="e7579-162">A backup process was added to the machine just after 4:00 AM, so this appears to be the culprit for the excessive resources being consumed.</span></span>

![變更追蹤](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a><span data-ttu-id="e7579-164">8.在記錄搜尋中檢視詳細資料</span><span class="sxs-lookup"><span data-stu-id="e7579-164">8. View details in Log Search</span></span>
<span data-ttu-id="e7579-165">我們可以查看在 Log Analytics 存放庫中收集的詳細效能資訊，進一步確認這點。</span><span class="sxs-lookup"><span data-stu-id="e7579-165">We can further verify this by looking at the detailed performance information collected in the Log Analytics repository.</span></span>  <span data-ttu-id="e7579-166">再次按一下 [警示] 索引標籤，然後按一下其中一個 [高 CPU] 警示。</span><span class="sxs-lookup"><span data-stu-id="e7579-166">Click on the **Alerts** tab again and then on one of the **High CPU** alerts.</span></span>  <span data-ttu-id="e7579-167">按一下 [在記錄搜尋中顯示]。</span><span class="sxs-lookup"><span data-stu-id="e7579-167">Click on  **Show in Log Search**.</span></span>  <span data-ttu-id="e7579-168">這會開啟 [記錄搜尋] 視窗，您可以在該視窗中對存放庫中儲存的任何資料執行[記錄搜尋](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="e7579-168">This opens the Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in the repository.</span></span>  <span data-ttu-id="e7579-169">服務對應已填入查詢中，以供我們擷取感興趣的警示。</span><span class="sxs-lookup"><span data-stu-id="e7579-169">Service Map already filled in a queriy for us to retrieve the alert we're interested in.</span></span>  

![記錄搜尋](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a><span data-ttu-id="e7579-171">9.開啟已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="e7579-171">9. Open saved search</span></span>
<span data-ttu-id="e7579-172">我們看看是否可以取得更多有關產生此警示之效能集合的詳細資料，並確認我們懷疑的問題是由該備份程序所造成。</span><span class="sxs-lookup"><span data-stu-id="e7579-172">Let's see if we can get some more detail on the performance collection that generated this alert and verify our suspicion that the problems are being caused by that backup process.</span></span>  <span data-ttu-id="e7579-173">將時間範圍變更為 [6 小時]。</span><span class="sxs-lookup"><span data-stu-id="e7579-173">Change the time range to **6 hours**.</span></span>  <span data-ttu-id="e7579-174">然後按一下 [我的最愛] 並向下捲動至針對 [服務對應] 儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="e7579-174">Then click on **Favorites** and scroll down to the saved searches for **Service Map**.</span></span>  <span data-ttu-id="e7579-175">這些是我們特別為此分析所建立的查詢。</span><span class="sxs-lookup"><span data-stu-id="e7579-175">These are queries that we created specifically for this analysis.</span></span>  <span data-ttu-id="e7579-176">按一下 [acmetomcat CPU 的前 5 個處理程序]。</span><span class="sxs-lookup"><span data-stu-id="e7579-176">Click on **Top 5 Processes by CPU for acmetomcat**.</span></span>

![儲存的搜尋](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


<span data-ttu-id="e7579-178">此查詢會傳回在 **acmetomcat** 上耗用處理器的前 5 個處理程序。</span><span class="sxs-lookup"><span data-stu-id="e7579-178">This query returns a list of the top 5 processes consuming processor on **acmetomcat**.</span></span>  <span data-ttu-id="e7579-179">您可以檢查此查詢，以取得用於記錄搜尋的查詢語言簡介。</span><span class="sxs-lookup"><span data-stu-id="e7579-179">You can inspect the query to get an introduction to the query language used for log searches.</span></span>  <span data-ttu-id="e7579-180">如果您對其他電腦上的處理程序感興趣，您可以修改查詢來擷取該資訊。</span><span class="sxs-lookup"><span data-stu-id="e7579-180">If you were interested in the processes on other computers, you could modify the query to retrieve that information.</span></span>

<span data-ttu-id="e7579-181">在此情況下，我們可以看到備份程序始終耗用大約 60% 的應用程式伺服器 CPU。</span><span class="sxs-lookup"><span data-stu-id="e7579-181">In this case, we can see that the backup process is consistently consuming about 60% of the app server’s CPU.</span></span>  <span data-ttu-id="e7579-182">這個新程序顯然是效能問題的原因。</span><span class="sxs-lookup"><span data-stu-id="e7579-182">It's pretty obvious that this new process is responsible for our performance problem.</span></span>  <span data-ttu-id="e7579-183">我們的解決方法顯然會是移除應用程式伺服器中的這個新備份軟體。</span><span class="sxs-lookup"><span data-stu-id="e7579-183">Our solution would obviously be to remove this new backup software off the application server.</span></span>  <span data-ttu-id="e7579-184">我們實際可以運用 Azure 自動化所管理的期望狀態組態 (DSC) 來定義原則，以確保此程序永遠不會在這些重要系統上執行。</span><span class="sxs-lookup"><span data-stu-id="e7579-184">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation to define policies that ensure this process never runs on these critical systems.</span></span>


## <a name="summary-points"></a><span data-ttu-id="e7579-185">摘要點</span><span class="sxs-lookup"><span data-stu-id="e7579-185">Summary points</span></span>
- <span data-ttu-id="e7579-186">即使您不知道應用程式的所有伺服器和相依性，[服務對應](operations-management-suite-service-map.md)也會提供整個應用程式的檢視。</span><span class="sxs-lookup"><span data-stu-id="e7579-186">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span></span>
- <span data-ttu-id="e7579-187">服務對應會呈現其他 OMS 解決方案所收集的資料，協助您找出您的應用程式與其基礎結構的問題。</span><span class="sxs-lookup"><span data-stu-id="e7579-187">Service Map surfaces data collected by other OMS solutions to help you identify issues with your application and its underlying infrastructure.</span></span>
- <span data-ttu-id="e7579-188">[記錄搜尋](../log-analytics/log-analytics-log-searches.md)可讓您向下切入 Log Analytics 存放庫中收集的特定資料。</span><span class="sxs-lookup"><span data-stu-id="e7579-188">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you to drill down into specific data collected in the Log Analytics repository.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="e7579-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7579-189">Next steps</span></span>
- <span data-ttu-id="e7579-190">深入了解[服務對應](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="e7579-190">Learn more about [Service Map](operations-management-suite-service-map.md).</span></span>
- <span data-ttu-id="e7579-191">[部署和設定](operations-management-suite-service-map-configure.md)服務對應。</span><span class="sxs-lookup"><span data-stu-id="e7579-191">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span></span>
- <span data-ttu-id="e7579-192">了解服務對應所需的 [Log Analytics](../log-analytics/log-analytics-overview.md)，其可儲存代理程式所儲存的作業資料。</span><span class="sxs-lookup"><span data-stu-id="e7579-192">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span></span>