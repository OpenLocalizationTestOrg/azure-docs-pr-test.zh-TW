---
title: "對應方案 aaaService 自我進度的示範 |Microsoft 文件"
description: "服務對應是一種解決方案中 Operations Management Suite (OMS)，會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。  這是本身的步調的示範逐步解說使用服務對應 tooidentify 並診斷在 web 應用程式的模擬的問題。"
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
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a><span data-ttu-id="bc873-104">Operations Management Suite (OMS) 自學示範 - 服務對應</span><span class="sxs-lookup"><span data-stu-id="bc873-104">Operations Management Suite (OMS) self paced demo - Service Map</span></span>
<span data-ttu-id="bc873-105">這是引導使用 hello 本身進度的示範[服務對應方案](operations-management-suite-service-map.md)在 Operations Management Suite (OMS) tooidentify 及診斷中的 web 應用程式的模擬的問題。</span><span class="sxs-lookup"><span data-stu-id="bc873-105">This is a self paced demo that walks through using hello [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) tooidentify and diagnose a simulated problem in a web application.</span></span>  <span data-ttu-id="bc873-106">服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-106">Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span>  <span data-ttu-id="bc873-107">它也會合併其他 OMS 服務 tooassist 所收集的資料中分析效能，並識別問題。</span><span class="sxs-lookup"><span data-stu-id="bc873-107">It also consolidates data collected by other OMS services tooassist you in analyzing performance and identifying issues.</span></span>  <span data-ttu-id="bc873-108">您也可以使用[記錄中記錄分析搜尋](../log-analytics/log-analytics-log-searches.md)toodrill 關閉收集中的資料順序 tooidentify hello 根本問題。</span><span class="sxs-lookup"><span data-stu-id="bc873-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) toodrill down on collected data in order tooidentify hello root problem.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="bc873-109">案例描述</span><span class="sxs-lookup"><span data-stu-id="bc873-109">Scenario description</span></span>
<span data-ttu-id="bc873-110">您所收到 hello ACME 客戶入口網站應用程式發生效能問題的通知。</span><span class="sxs-lookup"><span data-stu-id="bc873-110">You've just received a notification that hello ACME Customer Portal application is having performance issues.</span></span>  <span data-ttu-id="bc873-111">您擁有 hello 唯一資訊是這些問題啟動大約 4:00 am PST 今天。</span><span class="sxs-lookup"><span data-stu-id="bc873-111">hello only information that you have is that these issues started about 4:00 am PST today.</span></span>  <span data-ttu-id="bc873-112">您不確定所有 hello 元件該 hello 入口網站，是根據一組 web 伺服器以外。</span><span class="sxs-lookup"><span data-stu-id="bc873-112">You aren't entirely sure of all hello components that hello portal is dependent on other than a set of web servers.</span></span>  

## <a name="components-and-features-used"></a><span data-ttu-id="bc873-113">使用的元件和功能</span><span class="sxs-lookup"><span data-stu-id="bc873-113">Components and features used</span></span>
- [<span data-ttu-id="bc873-114">服務對應解決方案</span><span class="sxs-lookup"><span data-stu-id="bc873-114">Service Map solution</span></span>](operations-management-suite-service-map.md)
- [<span data-ttu-id="bc873-115">Log Analytics 記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="bc873-115">Log Analytics log searches</span></span>](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a><span data-ttu-id="bc873-116">逐步解說</span><span class="sxs-lookup"><span data-stu-id="bc873-116">Walk through</span></span>

### <a name="1-connect-toohello-oms-experience-center"></a><span data-ttu-id="bc873-117">1.連接 toohello OMS 經驗 Center</span><span class="sxs-lookup"><span data-stu-id="bc873-117">1. Connect toohello OMS Experience Center</span></span>
<span data-ttu-id="bc873-118">這個逐步解說會使用 hello [Operations Management Suite 經驗 Center](https://experience.mms.microsoft.com/)以提供完整的 OMS 環境，其中範例資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-118">This walk through uses hello [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span></span> <span data-ttu-id="bc873-119">開始依照此連結，提供您的資訊，然後選取 hello**深入剖析和分析**案例。</span><span class="sxs-lookup"><span data-stu-id="bc873-119">Start by following this link, provide your information and then select hello **Insight and Analytics** scenario.</span></span>


### <a name="2-start-service-map"></a><span data-ttu-id="bc873-120">2.啟動服務對應</span><span class="sxs-lookup"><span data-stu-id="bc873-120">2. Start Service Map</span></span>
<span data-ttu-id="bc873-121">按一下 hello 啟動 hello 服務對應解決方案**服務對應**磚。</span><span class="sxs-lookup"><span data-stu-id="bc873-121">Start hello Service Map solution by clicking on hello **Service Map** tile.</span></span>

![服務對應圖格](media/operations-management-suite-walkthrough-servicemap/tile.png)

<span data-ttu-id="bc873-123">hello 服務對應主控台會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="bc873-123">hello Service Map console is displayed.</span></span>  <span data-ttu-id="bc873-124">Hello 在左的窗格會是您已安裝的 hello 服務對應代理程式的環境中的電腦清單。</span><span class="sxs-lookup"><span data-stu-id="bc873-124">In hello left pane is a list of computers in your environment with hello Service Map agent installed.</span></span>  <span data-ttu-id="bc873-125">您需要選取想要從這個清單 tooview hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="bc873-125">You'll select hello computer that you want tooview from this list.</span></span>

![電腦清單](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a><span data-ttu-id="bc873-127">3.檢視電腦</span><span class="sxs-lookup"><span data-stu-id="bc873-127">3. View computer</span></span>
<span data-ttu-id="bc873-128">我們知道的 hello 網頁伺服器被稱為 AcmeWFE001 和 AcmeWFE002，因此這看起來像是適當起點 toostart。</span><span class="sxs-lookup"><span data-stu-id="bc873-128">We know that hello web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place toostart.</span></span>  <span data-ttu-id="bc873-129">按一下 [AcmeWFE001]。</span><span class="sxs-lookup"><span data-stu-id="bc873-129">Click on **AcmeWFE001**.</span></span>  <span data-ttu-id="bc873-130">這樣會顯示 hello 對應 AcmeWFE001 及其所有相依性。</span><span class="sxs-lookup"><span data-stu-id="bc873-130">This displays hello map for AcmeWFE001 and all of its dependencies.</span></span>  <span data-ttu-id="bc873-131">您可以看到哪些處理程序的執行 hello 所選的電腦上的外部服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-131">You can see which processes are running on hello selected computer and which external services they communicate with.</span></span>

![Web 伺服器](media/operations-management-suite-walkthrough-servicemap/web-server.png)

<span data-ttu-id="bc873-133">我們很在意 hello 效能，我們的 web 應用程式，因此按一下 hello **AcmeAppPool （IIS 應用程式集區）**程序。</span><span class="sxs-lookup"><span data-stu-id="bc873-133">We're concerned about hello performance of our web application so click on hello **AcmeAppPool (IIS App Pool)** process.</span></span>  <span data-ttu-id="bc873-134">這會顯示 hello 這個處理序的詳細資料，並反白顯示相依性。</span><span class="sxs-lookup"><span data-stu-id="bc873-134">This displays hello details for this process and highlights its dependencies.</span></span>  

![應用程式集區](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a><span data-ttu-id="bc873-136">4.變更時間範圍</span><span class="sxs-lookup"><span data-stu-id="bc873-136">4. Change time window</span></span>

<span data-ttu-id="bc873-137">我們聽到看看什麼發生當時的 hello 問題讓我們開始於上午 4:00。</span><span class="sxs-lookup"><span data-stu-id="bc873-137">We heard that hello problem started at 4:00 AM so let's have a look at what was happening at that time.</span></span> <span data-ttu-id="bc873-138">按一下**時間範圍**並變更 hello 時間 too4: 00 AM PST （保留 hello 目前的日期和本地時區調整） 持續時間為 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bc873-138">Click on **Time Range** and change hello time too4:00 AM PST (keep hello current date and adjust for your local time zone) with a duration of 20 minutes.</span></span>

![時間選擇器](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a><span data-ttu-id="bc873-140">5.檢視警示</span><span class="sxs-lookup"><span data-stu-id="bc873-140">5. View alert</span></span>

<span data-ttu-id="bc873-141">我們現在看到該 hello **acmetomcat**相依性都有警示顯示，因此這是我們的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="bc873-141">We now see that hello **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span></span>  <span data-ttu-id="bc873-142">按一下中的 hello 警示圖示**acmetomcat** tooshow hello hello 警示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-142">Click on hello alert icon in **acmetomcat** tooshow hello details for hello alert.</span></span>  <span data-ttu-id="bc873-143">我們可以看到 CPU 使用率有重大警示並可將其展開，以取得更詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-143">We can see that we have critical CPU utilization and can expand it for more detail.</span></span>  <span data-ttu-id="bc873-144">這可能是造成效能變慢的原因。</span><span class="sxs-lookup"><span data-stu-id="bc873-144">This is probably what's causing our slow performance.</span></span> 

![警示](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a><span data-ttu-id="bc873-146">6.檢視效能</span><span class="sxs-lookup"><span data-stu-id="bc873-146">6. View performance</span></span>

<span data-ttu-id="bc873-147">讓我們仔細看看 **acmetomcat**。</span><span class="sxs-lookup"><span data-stu-id="bc873-147">Let's have a closer look at **acmetomcat**.</span></span>  <span data-ttu-id="bc873-148">按一下 hello 中的權限的最上層**acmetomcat**選取**負載 Server 對應**tooshow hello 詳細資料和此機器的相依性。</span><span class="sxs-lookup"><span data-stu-id="bc873-148">Click in hello top right of **acmetomcat** and select **Load Server Map** tooshow hello detail and dependencies for this machine.</span></span> <span data-ttu-id="bc873-149">我們可以再查看稍微這些效能計數器 tooverify 我們停滯。</span><span class="sxs-lookup"><span data-stu-id="bc873-149">We can then look a bit more into those performance counters tooverify our suspicion.</span></span>  <span data-ttu-id="bc873-150">選取 hello**效能** 索引標籤 toodisplay hello[記錄分析所收集的效能計數器](../log-analytics/log-analytics-data-sources-performance-counters.md)hello 時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="bc873-150">Select hello **Performance** tab toodisplay hello [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over hello time range.</span></span>  <span data-ttu-id="bc873-151">我們可以看到，我們收到 hello 處理器和記憶體的週期峰值。</span><span class="sxs-lookup"><span data-stu-id="bc873-151">We can see that we're getting periodic spikes in hello processor and memory.</span></span>

![效能](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a><span data-ttu-id="bc873-153">7.檢視變更追蹤</span><span class="sxs-lookup"><span data-stu-id="bc873-153">7. View change tracking</span></span>
<span data-ttu-id="bc873-154">我們來看看是否可以找出可能造成此高使用率的原因。</span><span class="sxs-lookup"><span data-stu-id="bc873-154">Let's see if we can find out what might have caused this high utilization.</span></span>  <span data-ttu-id="bc873-155">按一下 hello**摘要** 索引標籤。這會提供連線、 重大警示和軟體變更失敗，例如收集 hello 電腦從 OMS 的資訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-155">Click on hello **Summary** tab.  This provides information that OMS has collected from hello computer such as failed connections, critical alerts, and software changes.</span></span>  <span data-ttu-id="bc873-156">具有最近的有趣資訊區段應該已經展開，而且可以展開其他各節 tooinspect 所包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-156">Sections with interesting recent information should already be expanded, and you can expand other sections tooinspect information that they contain.</span></span>


<span data-ttu-id="bc873-157">如果 [變更追蹤] 尚未開啟，則將它展開。</span><span class="sxs-lookup"><span data-stu-id="bc873-157">If **Change Tracking** isn't already open, then expand it.</span></span>  <span data-ttu-id="bc873-158">這會顯示 hello 所收集的資訊[變更追蹤解決方案](../log-analytics/log-analytics-change-tracking.md)。</span><span class="sxs-lookup"><span data-stu-id="bc873-158">This shows information collected by hello [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>  <span data-ttu-id="bc873-159">看起來，已在這段期間範圍內進行軟體變更。</span><span class="sxs-lookup"><span data-stu-id="bc873-159">It looks like there was a software change made during this time window.</span></span>  <span data-ttu-id="bc873-160">按一下**軟體**tooget 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-160">Click on **Software** tooget details.</span></span>  <span data-ttu-id="bc873-161">備份程序是只在上午 4:00 之後加入 toohello 機器，所以這會顯示 hello 正在耗用過多資源的 toobe hello 問題。</span><span class="sxs-lookup"><span data-stu-id="bc873-161">A backup process was added toohello machine just after 4:00 AM, so this appears toobe hello culprit for hello excessive resources being consumed.</span></span>

![變更追蹤](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a><span data-ttu-id="bc873-163">8.在記錄搜尋中檢視詳細資料</span><span class="sxs-lookup"><span data-stu-id="bc873-163">8. View details in Log Search</span></span>
<span data-ttu-id="bc873-164">我們可以進一步驗證，請查看 hello 詳細 hello 記錄分析儲存機制中收集的效能資訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-164">We can further verify this by looking at hello detailed performance information collected in hello Log Analytics repository.</span></span>  <span data-ttu-id="bc873-165">按一下 hello**警示**索引標籤上一次，然後在其中一個 hello**高 CPU**警示。</span><span class="sxs-lookup"><span data-stu-id="bc873-165">Click on hello **Alerts** tab again and then on one of hello **High CPU** alerts.</span></span>  <span data-ttu-id="bc873-166">按一下 [在記錄搜尋中顯示]。</span><span class="sxs-lookup"><span data-stu-id="bc873-166">Click on  **Show in Log Search**.</span></span>  <span data-ttu-id="bc873-167">這會開啟您要執行 hello 記錄搜尋視窗[記錄搜尋](../log-analytics/log-analytics-log-searches.md)針對 hello 儲存機制中儲存的任何資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-167">This opens hello Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in hello repository.</span></span>  <span data-ttu-id="bc873-168">服務對應為我們已經填入 queriy tooretrieve hello 警示我們感興趣。</span><span class="sxs-lookup"><span data-stu-id="bc873-168">Service Map already filled in a queriy for us tooretrieve hello alert we're interested in.</span></span>  

![記錄搜尋](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a><span data-ttu-id="bc873-170">9.開啟已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="bc873-170">9. Open saved search</span></span>
<span data-ttu-id="bc873-171">我們來看看是否我們可以產生此警示的 hello 效能集合中取得更多詳細資料，並確認該備份的程序所造成的問題 hello 我們停滯。</span><span class="sxs-lookup"><span data-stu-id="bc873-171">Let's see if we can get some more detail on hello performance collection that generated this alert and verify our suspicion that hello problems are being caused by that backup process.</span></span>  <span data-ttu-id="bc873-172">變更 hello 時間範圍太**6 小時**。</span><span class="sxs-lookup"><span data-stu-id="bc873-172">Change hello time range too**6 hours**.</span></span>  <span data-ttu-id="bc873-173">然後按一下 **我的最愛**和捲動 toohello 儲存搜尋**服務對應**。</span><span class="sxs-lookup"><span data-stu-id="bc873-173">Then click on **Favorites** and scroll down toohello saved searches for **Service Map**.</span></span>  <span data-ttu-id="bc873-174">這些是我們特別為此分析所建立的查詢。</span><span class="sxs-lookup"><span data-stu-id="bc873-174">These are queries that we created specifically for this analysis.</span></span>  <span data-ttu-id="bc873-175">按一下 [acmetomcat CPU 的前 5 個處理程序]。</span><span class="sxs-lookup"><span data-stu-id="bc873-175">Click on **Top 5 Processes by CPU for acmetomcat**.</span></span>

![儲存的搜尋](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


<span data-ttu-id="bc873-177">此查詢會傳回一份 hello 前 5 個處理序正在耗用處理器上**acmetomcat**。</span><span class="sxs-lookup"><span data-stu-id="bc873-177">This query returns a list of hello top 5 processes consuming processor on **acmetomcat**.</span></span>  <span data-ttu-id="bc873-178">您可以檢查 hello 查詢 tooget 簡介 toohello 查詢語言，用於記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="bc873-178">You can inspect hello query tooget an introduction toohello query language used for log searches.</span></span>  <span data-ttu-id="bc873-179">如果您想要在其他電腦上的 hello 處理序中，您可以修改 hello 查詢 tooretrieve 該資訊。</span><span class="sxs-lookup"><span data-stu-id="bc873-179">If you were interested in hello processes on other computers, you could modify hello query tooretrieve that information.</span></span>

<span data-ttu-id="bc873-180">在此情況下，我們可以看到 hello 備份程序會一致地耗用約 60%的 hello 應用程式伺服器的 CPU。</span><span class="sxs-lookup"><span data-stu-id="bc873-180">In this case, we can see that hello backup process is consistently consuming about 60% of hello app server’s CPU.</span></span>  <span data-ttu-id="bc873-181">這個新程序顯然是效能問題的原因。</span><span class="sxs-lookup"><span data-stu-id="bc873-181">It's pretty obvious that this new process is responsible for our performance problem.</span></span>  <span data-ttu-id="bc873-182">我們的方案會很明顯地 tooremove 這個新備份關閉 hello 應用程式伺服器的軟體。</span><span class="sxs-lookup"><span data-stu-id="bc873-182">Our solution would obviously be tooremove this new backup software off hello application server.</span></span>  <span data-ttu-id="bc873-183">實際上，我們無法利用預期狀態設定 (DSC) 受 Azure 自動化 toodefine 原則，確保絕不會執行這些重要的系統上，此程序。</span><span class="sxs-lookup"><span data-stu-id="bc873-183">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation toodefine policies that ensure this process never runs on these critical systems.</span></span>


## <a name="summary-points"></a><span data-ttu-id="bc873-184">摘要點</span><span class="sxs-lookup"><span data-stu-id="bc873-184">Summary points</span></span>
- <span data-ttu-id="bc873-185">即使您不知道應用程式的所有伺服器和相依性，[服務對應](operations-management-suite-service-map.md)也會提供整個應用程式的檢視。</span><span class="sxs-lookup"><span data-stu-id="bc873-185">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span></span>
- <span data-ttu-id="bc873-186">服務對應介面上的資料收集的其他 OMS 解決方案 toohelp 您識別問題時您的應用程式和其基礎結構。</span><span class="sxs-lookup"><span data-stu-id="bc873-186">Service Map surfaces data collected by other OMS solutions toohelp you identify issues with your application and its underlying infrastructure.</span></span>
- <span data-ttu-id="bc873-187">[記錄搜尋](../log-analytics/log-analytics-log-searches.md)允許您 toodrill 向下到收集 hello 記錄分析儲存機制中的特定資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-187">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you toodrill down into specific data collected in hello Log Analytics repository.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="bc873-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc873-188">Next steps</span></span>
- <span data-ttu-id="bc873-189">深入了解[服務對應](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="bc873-189">Learn more about [Service Map](operations-management-suite-service-map.md).</span></span>
- <span data-ttu-id="bc873-190">[部署和設定](operations-management-suite-service-map-configure.md)服務對應。</span><span class="sxs-lookup"><span data-stu-id="bc873-190">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span></span>
- <span data-ttu-id="bc873-191">了解服務對應所需的 [Log Analytics](../log-analytics/log-analytics-overview.md)，其可儲存代理程式所儲存的作業資料。</span><span class="sxs-lookup"><span data-stu-id="bc873-191">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span></span>