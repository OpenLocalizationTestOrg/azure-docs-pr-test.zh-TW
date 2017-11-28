---
title: "aaaTroubleshooting 與監視的 SAP HANA Azure （大型執行個體） 上 |Microsoft 文件"
description: "針對 SAP HANA on Azure (大型執行個體) 進行疑難排解和監視。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="8ebf6-103">Tootroubleshoot 和監視器的 SAP HANA （大型執行個體），在 Azure 上</span><span class="sxs-lookup"><span data-stu-id="8ebf6-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="8ebf6-104">SAP HANA on Azure (大型執行個體) 中的監視</span><span class="sxs-lookup"><span data-stu-id="8ebf6-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="8ebf6-105">在 Azure （大型執行個體） 上的 SAP HANA 並無不同之任何其他 IaaS 部署中，您需要 toomonitor 什麼 hello OS，hello 應用程式是這麼做，而這些取用 hello 下列資源的方式：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="8ebf6-106">CPU</span><span class="sxs-lookup"><span data-stu-id="8ebf6-106">CPU</span></span>
- <span data-ttu-id="8ebf6-107">記憶體</span><span class="sxs-lookup"><span data-stu-id="8ebf6-107">Memory</span></span>
- <span data-ttu-id="8ebf6-108">網路頻寬</span><span class="sxs-lookup"><span data-stu-id="8ebf6-108">Network bandwidth</span></span>
- <span data-ttu-id="8ebf6-109">磁碟空間</span><span class="sxs-lookup"><span data-stu-id="8ebf6-109">Disk space</span></span>

<span data-ttu-id="8ebf6-110">視需要 toofigure 出 hello 上述指定的資源類別是否足夠，或是否這些取得耗盡與 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="8ebf6-111">以下是更多詳細資料上的每個 hello 不同類別：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="8ebf6-112">**CPU 資源耗用量：** SAP HANA 針對特定工作負載所定義的 hello 比例是強制的 toomake 確定應該使用透過儲存在記憶體中的 hello 資料 toowork 足夠 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="8ebf6-113">不過，可能會其中 HANA 會消耗大量 CPU 執行查詢，因為 toomissing 索引或類似問題的情況。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="8ebf6-114">這表示您應該監視 CPU 的 hello HANA 大型執行個體單位為 hello 特定 HANA 服務所耗用的 CPU 資源的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="8ebf6-115">**記憶體耗用量：**是重要 toomonitor 從 HANA 中,，以及外部 HANA hello 單元上的。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="8ebf6-116">內 HANA，監視 hello 資料配置的記憶體中順序 toostay 內 hello 所需大小的指導方針的 SAP HANA 中的特殊使用。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="8ebf6-117">您也想 toomonitor hello 大型執行個體層級 toomake 確定其他已安裝非-HANA 軟體未不耗用太多的記憶體，因此與 HANA 爭用記憶體的記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="8ebf6-118">**網路頻寬：** hello Azure VNet 閘道的資料移到 hello Azure VNet 的頻寬有限，因此您很有幫助 toomonitor hello 資料所有收到 hello VNet toofigure 出如何關閉您的 hello Azure toohello 限制內的 Azure Vm您選取的 SKU 的閘道。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="8ebf6-119">Hello HANA 大型執行個體的單位，但卻可讓意義 toomonitor 傳入和傳出網路流量及 tookeep 追蹤一段時間所處理的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="8ebf6-120">**磁碟空間：**磁碟空間耗用量通常會隨著時間增加。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="8ebf6-121">其原因有許多，但最重要的包括：資料量增加、執行交易記錄備份、儲存追蹤檔案，以及執行儲存體快照。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="8ebf6-122">因此，它會是重要的 toomonitor 磁碟空間使用量，並管理 hello 與 hello HANA 大型執行個體單元相關聯的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="8ebf6-123">從 HANA 端進行監視和疑難排解</span><span class="sxs-lookup"><span data-stu-id="8ebf6-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="8ebf6-124">在訂單 tooeffectively 分析問題相關的 tooSAP HANA Azure （大型執行個體） 上，有用 toonarrow 向 hello 有問題的根本原因。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="8ebf6-125">SAP 發行大量的文件 toohelp 您。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="8ebf6-126">適用的常見問題集相關的 tooSAP HANA 效能可以在 hello 遵循 SAP 附註：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="8ebf6-127">SAP 附註 #2222200 - 常見問題集：SAP HANA 網路</span><span class="sxs-lookup"><span data-stu-id="8ebf6-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="8ebf6-128">SAP 附註 #2100040 - 常見問題集：SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="8ebf6-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="8ebf6-129">SAP 附註 #199997 - 常見問題集：SAP HANA 記憶體</span><span class="sxs-lookup"><span data-stu-id="8ebf6-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="8ebf6-130">SAP 附註 #200000 - 常見問題集：SAP HANA 效能最佳化</span><span class="sxs-lookup"><span data-stu-id="8ebf6-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="8ebf6-131">SAP 附註 #199930 - 常見問題集：SAP HANA I/O 分析</span><span class="sxs-lookup"><span data-stu-id="8ebf6-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="8ebf6-132">SAP 附註 #2177064 - 常見問題集：SAP HANA 服務重新啟動和當機</span><span class="sxs-lookup"><span data-stu-id="8ebf6-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="8ebf6-133">**SAP HANA 警示**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="8ebf6-134">第一個步驟是檢查 hello 目前 SAP HANA 警示記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="8ebf6-135">在 SAP HANA Studio 中，移太**管理主控台： 警示： 顯示： 所有警示**。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="8ebf6-136">此索引標籤會顯示所有的 SAP HANA 臨界值的範圍之外 hello 設定最小和最大臨界值的特定值 （可用的實體記憶體、 CPU 使用率等）。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="8ebf6-137">根據預設，檢查會每隔 15 分鐘自動重新整理一次。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![在 SAP HANA Studio 中，移 tooAdministration 主控台： 警示： 顯示： 所有警示](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="8ebf6-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-139">**CPU**</span></span>

<span data-ttu-id="8ebf6-140">由於 tooimproper 臨界值 設定觸發警示，解析是 tooreset toohello 預設值或較合理的臨界值。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![重設 toohello 預設值或較合理的臨界值](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="8ebf6-142">hello 下列警示可能表示 CPU 資源的問題：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="8ebf6-143">Host CPU Usage (Alert 5) (主機 CPU 使用率 (警示 5))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="8ebf6-144">Most recent savepoint operation (Alert 28) (最新的儲存點作業 (警示 28))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="8ebf6-145">Savepoint duration (Alert 54) (儲存點持續時間 (警示 54))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="8ebf6-146">從 hello 下列其中一種在 SAP HANA 資料庫上，您可能會發現高 CPU 耗用率：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="8ebf6-147">針對目前和過去的 CPU 使用率，引發了「警示 5」(主機 CPU 使用率)</span><span class="sxs-lookup"><span data-stu-id="8ebf6-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="8ebf6-148">hello hello 概觀畫面上顯示 CPU 使用量</span><span class="sxs-lookup"><span data-stu-id="8ebf6-148">hello displayed CPU usage on hello overview screen</span></span>

![Hello 概觀畫面上顯示 CPU 使用量](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="8ebf6-150">在過去的 hello hello 負載圖形可能會顯示高 CPU 耗用率或高耗用量：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![hello 負載圖形可能會顯示高 CPU 耗用率或高耗用量在過去的 hello](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="8ebf6-152">警示觸發到期 toohigh CPU 使用率可能因多種原因造成，包括但不是限於： 特定交易、 載入資料、 停滯的作業，長時間執行的 SQL 陳述式和不正確的查詢效能 （例如，BW HANA 上執行cube)。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="8ebf6-153">請參閱 toohello [SAP HANA 疑難排解： CPU 相關導致和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false)網站詳細的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="8ebf6-154">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-154">**Operating System**</span></span>

<span data-ttu-id="8ebf6-155">其中一個最重要的 hello 檢查在 Linux 上的 SAP HANA toomake 確定已停用透明龐大的頁面，請參閱[SAP 附註 #2131662 透明龐大頁面 (THP) 在 SAP HANA 伺服器](https://launchpad.support.sap.com/#/notes/2131662)。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="8ebf6-156">您可以檢查透明龐大的頁面是否已啟用透過下列 Linux 命令 hello:**數據機 /sys/kernel/mm/transparent\_hugepage/啟用**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="8ebf6-157">如果_一律_會括在方括號，如下所示，它表示 hello 透明龐大的頁面已啟用: [永遠] madvise 永遠不會; 如果_永遠不會_會括在括號內，如下所示，這表示該 hello 透明龐大的頁面已停用： 一律 madvise [永不]</span><span class="sxs-lookup"><span data-stu-id="8ebf6-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="8ebf6-158">hello 下列 Linux 命令應傳回任何項目： **rpm qa | grep ulimit。**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="8ebf6-159">如果顯示安裝的是 _ulimit_，請立即將它解除安裝。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="8ebf6-160">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-160">**Memory**</span></span>

<span data-ttu-id="8ebf6-161">您可能會注意到 hello 數量的記憶體配置的 hello SAP HANA 資料庫高於預期。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="8ebf6-162">hello 下列警示指出的高記憶體使用量問題：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="8ebf6-163">Host physical memory usage (Alert 1) (主機實體記憶體使用量 (警示 1))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="8ebf6-164">Memory usage of name server (Alert 12) (名稱伺服器的記憶體使用量 (警示 12))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="8ebf6-165">Total memory usage of Column Store tables (Alert 40) (資料行存放區資料表的總記憶體使用量 (警示 40))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="8ebf6-166">Memory usage of services (Alert 43) (服務的記憶體使用量 (警示 43))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="8ebf6-167">Memory usage of main storage of Column Store tables (Alert 45) (資料行存放區資料表的主要儲存體記憶體使用量 (警示 45))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="8ebf6-168">Runtime dump files (Alert 46) (執行階段傾印檔案 (警示 46))</span><span class="sxs-lookup"><span data-stu-id="8ebf6-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="8ebf6-169">請參閱 toohello [SAP HANA 疑難排解： 記憶體問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false)網站詳細的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="8ebf6-170">**網路**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-170">**Network**</span></span>

<span data-ttu-id="8ebf6-171">請參閱太[SAP 附註 #2081065 疑難排解 SAP HANA 網路](https://launchpad.support.sap.com/#/notes/2081065)並執行 hello 網路疑難排解步驟，在此 SAP 附註。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="8ebf6-172">分析伺服器與用戶端之間的來回時間。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="8ebf6-173">A.</span><span class="sxs-lookup"><span data-stu-id="8ebf6-173">A.</span></span> <span data-ttu-id="8ebf6-174">執行 hello SQL 指令碼[ _HANA\_網路\_用戶端_](https://launchpad.support.sap.com/#/notes/1969700)_。_</span><span class="sxs-lookup"><span data-stu-id="8ebf6-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="8ebf6-175">分析節點間的通訊。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-175">Analyze internode communication.</span></span>
  <span data-ttu-id="8ebf6-176">A.</span><span class="sxs-lookup"><span data-stu-id="8ebf6-176">A.</span></span> <span data-ttu-id="8ebf6-177">執行 SQL 指令碼 [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_。_</span><span class="sxs-lookup"><span data-stu-id="8ebf6-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="8ebf6-178">執行 Linux 指令**ifconfig** （hello 輸出會顯示是否發生任何封包遺失）。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="8ebf6-179">執行 Linux 命令 **tcpdump**。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="8ebf6-180">此外，使用開放原始碼 hello [IPERF](https://iperf.fr/)工具 （或類似） toomeasure 實際的應用程式的網路效能。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="8ebf6-181">請參閱 toohello [SAP HANA 疑難排解： 網路效能和連線問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false)網站詳細的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="8ebf6-182">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-182">**Storage**</span></span>

<span data-ttu-id="8ebf6-183">從使用者的觀點而言，應用程式 （或 hello 整體系統） 變得緩慢執行、 沒有回應，或甚至似乎 toohang，如果 I/O 效能的問題。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="8ebf6-184">在 [hello**磁碟區**] 索引標籤在 SAP HANA Studio 中，您可以看到 hello 附加磁碟區，以及每個服務所使用的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![在 hello SAP HANA Studio 中的磁碟區索引標籤，您可以看到 hello 附加磁碟區，以及每個服務所使用的磁碟區](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="8ebf6-186">連接的磁碟區的詳細資料請參閱 < 囉 」 畫面 hello 下半部 hello 磁碟區，例如檔案和 I/O 統計資料。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![連接的磁碟區的詳細資料請參閱 < 囉 」 畫面 hello 下半部 hello 磁碟區，例如檔案和 I/O 統計資料](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="8ebf6-188">請參閱 toohello [SAP HANA 疑難排解： I/O 相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false)和[SAP HANA 疑難排解： 磁碟相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false)網站詳細的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="8ebf6-189">**診斷工具**</span><span class="sxs-lookup"><span data-stu-id="8ebf6-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="8ebf6-190">您可以透過 HANA\_Configuration\_Minichecks 執行「SAP HANA 健康情況檢查」。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="8ebf6-191">此工具會傳回應該已在 SAP HANA Studio 中引發成警示的潛在重大技術問題。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="8ebf6-192">請參閱太[SAP 附註 #1969700 SAP HANA 的 SQL 陳述式集合](https://launchpad.support.sap.com/#/notes/1969700)並下載 hello SQL Statements.zip 檔案附加的 toothat 附註。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="8ebf6-193">此.zip 檔案儲存在 hello 本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="8ebf6-194">在 SAP HANA Studio 中，在 hello**系統資訊**索引標籤上，以滑鼠右鍵按一下 hello**名稱**資料行，然後選取**匯入 SQL 陳述式**。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![在 hello 系統資訊 索引標籤上的 SAP HANA Studio hello 名稱資料行中以滑鼠右鍵按一下並選取匯入 SQL 陳述式](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="8ebf6-196">選取 hello SQL Statements.zip 檔案儲存在本機，並將匯入具有 hello 對應的 SQL 陳述式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="8ebf6-197">此時，hello 可以執行許多不同的診斷檢查，以這些 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="8ebf6-198">Tootest SAP HANA 系統複寫的頻寬需求，例如，滑鼠右鍵按一下 hello**頻寬**陳述式**複寫： 頻寬**選取**開啟**在 SQL 主控台中。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="8ebf6-199">hello 完整的 SQL 陳述式會開啟 允許的輸入的參數 （修改區段） toobe 變更，然後執行。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![hello 完整的 SQL 陳述式會開啟 允許的輸入的參數 （修改區段） toobe 變更，然後執行](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="8ebf6-201">另一個範例是以滑鼠右鍵按一下底下的 hello 陳述式**複寫： 概觀**。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="8ebf6-202">選取**Execute** hello 內容功能表：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-202">Select **Execute** from hello context menu:</span></span>

![另一個範例是以滑鼠右鍵按一下複寫下 hello 陳述式： 概觀。](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="8ebf6-205">這會產生可協助進行疑難排解的資訊：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-205">This results in information that helps with troubleshooting:</span></span>

![這會產生可協助進行疑難排解的資訊](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="8ebf6-207">請勿 hello 相同 hana\_組態\_Minichecks 和任何核取_X_ hello 中的標記_C_ (Critical) 資料行。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="8ebf6-208">範例輸出：</span><span class="sxs-lookup"><span data-stu-id="8ebf6-208">Sample outputs:</span></span>

<span data-ttu-id="8ebf6-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1**：適用於一般 SAP HANA 檢查。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1：適用於一般 SAP HANA 檢查](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="8ebf6-211">**HANA\_Services\_Overview**：適用於 SAP HANA 服務目前執行情況的概觀。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview：適用於 SAP HANA 服務目前執行情況的概觀](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="8ebf6-213">**HANA\_Services\_Statistics**：適用於 SAP HANA 服務資訊 (CPU、記憶體等)。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="8ebf6-214">HANA\_Services\_Statistics：適用於 SAP HANA 服務資訊</span><span class="sxs-lookup"><span data-stu-id="8ebf6-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="8ebf6-215">**HANA\_組態\_概觀\_Rev110 +** hello SAP HANA 執行個體上的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_組態\_概觀\_Rev110 + hello SAP HANA 執行個體上的一般資訊](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="8ebf6-217">**HANA\_組態\_參數\_Rev70 +** toocheck SAP HANA 參數。</span><span class="sxs-lookup"><span data-stu-id="8ebf6-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_組態\_參數\_Rev70 + toocheck SAP HANA 參數](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

